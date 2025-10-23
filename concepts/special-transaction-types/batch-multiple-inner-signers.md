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

To use this feature, every individual party involved in the inner 'RawTransactions' need to provide a signature for the entire batch, then to be combined in the parent Batch. At this point any account (even one not participating in the inner Batch transactions) can bundle and submit, as the combined inner batch participant's transactions will satisfy the signing requirements.&#x20;

Normally, the Batch transaction would require a formatted object with signers and signatures to be added to the Batch transaction in the `BatchSigners` field, [as per XRPL's Batch specification](https://xls.xrpl.org/xls/XLS-0056-batch.html).

**To make it easier to deal with multiple inner signers, when using the Xaman SDK / API you can gather individual signer's transactions and then combine using only the Payload UUID's (or signed transaction blobs), at which point Xaman will 'unfurl' the information to craft a valid Batch transaction with multiple signers.**

The workflow woud be as follows:

### 1. Multiple participants in \`RawTransactions\`

Craft the Batch transaction with the `RawTransactions` containing all transactions to be approved (signed) by different participants. **At this stage the r-addresses for the individual transactions must already be known.** The overall Batch may look like below.

{% hint style="success" %}
At this stage the upper Batch Transaction can have the `Sequence`/`Ticket` , `Fee`, and `Account` fields omitted. They don't have to be known yet, as they can be added later when the inner transactions are signed and any account can submit the bundle.
{% endhint %}

<pre class="language-json"><code class="lang-json">{
<strong>    "TransactionType": "Batch",
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

### 2. Gather individual inner transaction sigatures

As can be seen in the proposed JSON transaction above, two signers will need to approve the transaction:&#x20;

* `rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ`&#x20;
* `r38xHAWRdc5enrYsHKQxUzHf6javKrV3i4`

Each participant can now be presented with the Batch to be approved, where the signer is pre-filled, and thus enforced. The payload will have to be created with `submit: false` as we don't want to try to submit, we just want to get a signature from the Batch participant.

{% hint style="warning" %}
This means if someone with Xaman installed without the specific account present with signing permissions, Xaman will reject the sign request.
{% endhint %}

#### Payload (sign request):

<pre class="language-json"><code class="lang-json">{
  "options": {
    "submit": false,
<strong>    "signer": "rnMsCBhSWeK3ngU7JWkejHsYZs3UVWqNoQ"
</strong>  },
  "txjson": {
    "TransactionType": "Batch",
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

The same routine has then to be walked through for other signers.

### 3. Combine the inner transaction signatures and submit the Batch

Every Sign Request in the previous steps (per signer) is assigned an `uuid`. Gather those who are signed succesfully by the inner Batch transactions participants, to be combined (bundled) later to submit the Batch transaction. Now a specific signer is **not required** and `submit` can be `true` :

<pre class="language-json"><code class="lang-json">{
  "options": {
<strong>    "submit": true
</strong>  },
  "txjson": {
    "TransactionType": "Batch",
    "Flags": 65536,
    "Fee": "1337",
<strong>    "BatchSigners": [
</strong><strong>      "82a46463-c8e7-4f5f-9a9e-4cc8a5b332b9",
</strong><strong>      "15dce664-a040-40ca-8de7-fdf3cc337055"
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
