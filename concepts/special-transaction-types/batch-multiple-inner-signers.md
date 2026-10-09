---
description: >-
  The Batch feature allows multiple transactions to be packaged together and
  executed as a single atomic transaction. Create and submit a batch of up to 8
  transactions that succeed or fail atomically.
icon: layer-group
---

# Batch (multiple inner signers)

The `Batch` transaction type can be submitted through the Xaman API as any regular Sign Request (payload). It requires:

* `TransactionType` "Batch"
* `Flags` as integer, with one of the processing methods allowed for a Batch transaction:
  * ALLORNOTHING (tfAllOrNothing), Flag integer value: **65536**
  * ONLYONE (tfOnlyOne), Flag integer value: **131072**
  * UNTILFAILURE (tfUntilFailure), Flag integer value: **262144**
  * INDEPENDENT (tfIndependent), Flag integer value: **524288**
* `RawTransactions` containing the inner transactions of the batch. Note that **every single inner transaction** needs to:
  * Have `Fee` at a string containing the value "0"
  * Have `SigningPubkey` as empty string ""
  * Have the `Flags` field contain the flag indicating it is an inner Batch transaction: `1073741824`

## Multiple 'inner' signers

One of the amazing features of Batch is the ability to atomically have multiple parties interact. Combined with ALLORNOTHING on the upper Batch, this allows for fully atomic transactions between multiple parties, where either every participant gets what they agreed to, or none of them do.

To use this feature, every individual party involved in the inner 'RawTransactions' needs to provide a signature for the entire batch, then to be combined in the parent Batch. The parent Batch is then signed and submitted by the **Batch Account** (the `Account` of the Batch transaction). This can be one of the participants, or another account (e.g. an account paying the fee).

{% hint style="warning" %}
**The Batch Account and its `Sequence` must be known before anyone signs.** Since the BatchV1_1 amendment, every inner signature also signs the Batch `Account` and `Sequence` (or `TicketSequence`). Changing them afterwards makes the inner signatures invalid, and only that Batch Account can sign and submit the Batch. Only the `Fee` can still change.

Xaman 5.4.0 and newer sign inner Batch signatures for BatchV1_1. Inner signatures from older Xaman versions are rejected by networks with BatchV1_1 enabled.
{% endhint %}

Normally, the Batch transaction would require a formatted object with signers and signatures to be added to the Batch transaction in the `BatchSigners` field, [as per XRPL's Batch specification](https://xls.xrpl.org/xls/XLS-0056-batch.html).

**To make it easier to deal with multiple inner signers, when using the Xaman SDK / API you can gather individual signer's transactions and then combine using only the Payload UUID's (or signed transaction blobs), at which point Xaman will 'unfurl' the information to craft a valid Batch transaction with multiple signers.**

The workflow woud be as follows:

### 1. Multiple participants in \`RawTransactions\`

Craft the Batch transaction with the `RawTransactions` containing all transactions to be approved (signed) by different participants. **At this stage the r-addresses for the individual transactions must already be known** (see: [signin.md](signin.md "mention"))**.** The overall Batch may look like below.

The upper Batch transaction **must** contain the `Account` (the Batch Account) and its `Sequence`. For a Batch using a Ticket, set `Sequence` to `0` and add the `TicketSequence`. In the example below, the Batch Account is one of the participants: it uses `Sequence` 36968 for the Batch, and 36969 for its own inner transaction.

<pre class="language-json"><code class="lang-json">{
<strong>    "TransactionType": "Batch",
</strong><strong>    "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
</strong><strong>    "Sequence": 36968,
</strong>    "Flags": 65536,
    "Fee": "1337",
    "RawTransactions": [
      {
        "RawTransaction": {
          "TransactionType": "Payment",
<strong>          "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
</strong>          "Destination": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
          "Amount": "100",
          "Sequence": 36969,
          "Fee": "0",
          "Flags": 1073741824,
          "SigningPubKey": ""
        }
      },
      {
        "RawTransaction": {
          "TransactionType": "CredentialCreate",
          "Expiration": 889004799,
<strong>          "Account": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
</strong>          "Subject": "rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ",
          "URI": "CAFEBABE",
          "CredentialType": "4B5943CAFEBABE",
          "Sequence": 36971,
          "Flags": 1073741824,
          "Fee": "0",
          "SigningPubKey": ""
        }
      }
    ]
}
</code></pre>

### 2. Gather individual inner transaction signatures

As can be seen in the proposed JSON transaction above, two accounts have an inner transaction:&#x20;

* `rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ`, the Batch Account: it signs the Batch itself in step 3
* `r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4`, an inner signer: it signs in this step

Every account with an inner transaction, except the Batch Account, is an inner signer. Each inner signer can now be presented with the Batch to be approved, where the signer is pre-filled, and thus enforced. The payload will have to be created with `submit: false` as we don't want to try to submit, we just want to get a signature from the Batch participant. Send the exact same Batch (`Account`, `Sequence`, `Flags` and `RawTransactions`) to every inner signer.

{% hint style="warning" %}
This means if someone with Xaman installed without the specific account present with signing permissions, Xaman will reject the sign request.
{% endhint %}

#### Payload (sign request):

<pre class="language-json"><code class="lang-json">{
  "options": {
    "submit": false,
<strong>    "signer": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4"
</strong>  },
  "txjson": {
    "TransactionType": "Batch",
    "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
    "Sequence": 36968,
    "Flags": 65536,
    "Fee": "1337",
    "RawTransactions": [
      {
        "RawTransaction": {
          "TransactionType": "Payment",
<strong>          "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
</strong>          "Destination": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
          "Amount": "100",
          "Sequence": 36969,
          "Fee": "0",
          "Flags": 1073741824,
          "SigningPubKey": ""
        }
      },
      {
        "RawTransaction": {
          "TransactionType": "CredentialCreate",
          "Expiration": 889004799,
          "Account": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
          "Subject": "rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ",
          "URI": "CAFEBABE",
          "CredentialType": "4B5943CAFEBABE",
          "Sequence": 36971,
          "Flags": 1073741824,
          "Fee": "0",
          "SigningPubKey": ""
        }
      }
    ]
  }
}
</code></pre>

The same routine has then to be walked through for other inner signers.

### 3. Combine the inner transaction signatures and submit the Batch

Every Sign Request in the previous steps (per signer) is assigned an `uuid`. Gather those who are signed successfully by the inner signers, to be combined (bundled) in the Batch transaction. This last Sign Request is signed by the Batch Account (set it as the `signer`), and `submit` can be `true`. Xaman adds the inner signatures and sorts them by account, as the network requires.

{% hint style="success" %}
Note! While the official Batch spec requires a full signer object to be present in the `BatchSigners` field, Xaman accepts three different notations:

1. Conform native XRPL implementation: `BatchSigners` formatted object, containing an STArray with multiple signer pubkeys + their signature
2. **Xaman specific (**_**more**_**&#x20;convenient)**: the signed TX blob (as string) - this works for TX blobs signed by Xaman, or by any other XRPL signing implementation.
3. **Xaman specific (most convenient)**: the signed Payload UUID - this works only if all signers are Xaman users, and the payloads were created by the same Xaman API application.
{% endhint %}

<pre class="language-json"><code class="lang-json">{
  "options": {
<strong>    "submit": true,
</strong><strong>    "signer": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ"
</strong>  },
  "txjson": {
    "TransactionType": "Batch",
    "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
    "Sequence": 36968,
    "Flags": 65536,
    "Fee": "1337",
<strong>    "BatchSigners": [
</strong><strong>      "82a46463-c8e7-4f5f-9a9e-4cc8a5b332b9"
</strong><strong>    ],
</strong>    "RawTransactions": [
      {
        "RawTransaction": {
          "TransactionType": "Payment",
          "Account": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ",
          "Destination": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
          "Amount": "100",
          "Sequence": 36969,
          "Fee": "0",
          "Flags": 1073741824,
          "SigningPubKey": ""
        }
      },
      {
        "RawTransaction": {
          "TransactionType": "CredentialCreate",
          "Expiration": 889004799,
          "Account": "r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4",
          "Subject": "rwietsevLFg8XSmG3bEZzFein1g8RBqWDZ",
          "URI": "CAFEBABE",
          "CredentialType": "4B5943CAFEBABE",
          "Sequence": 36971,
          "Flags": 1073741824,
          "Fee": "0",
          "SigningPubKey": ""
        }
      }
    ]
  }
}
</code></pre>
