# getKycStatus( ... )

The `getKycStatus` return the KYC status of a user based on a user\_token, issued after the user signed a Sign Request (from your app) before (see Payloads - Intro).

If a user token specified is invalid, revoked, expired, etc. the method will always return `NONE`, just like when a user didn't go through KYC. You cannot distinct a non-KYC'd user from an invalid token.

Alternatively, KYC status can be retrieved for an XPRL account address: the address selected in XUMM when the session KYC was initiated by.

```typescript
const kycStatus = await Sdk.getKycStatus(
  "00000000-0000-0000-0000-000000000000"
);
```

... or using an account address:

```typescript
const kycStatus = await Sdk.getKycStatus("rwu1dgaUq8DCj3ZLFXzRbc1Aco5xLykMMQ");
```

Returns [`<keyof PossibleKycStatuses>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/KycStatusResponse.ts#L1).

**Notes on KYC information**

* Once an account has successfully completed the XUMM KYC flow, the KYC flag will be applied to the account even if the identity document used to KYC expired. The flag shows that the account was **once** KYC'd by a real person with a real identity document.
* Please note that the KYC flag provided by XUMM can't be seen as a "all good, let's go ahead" flag: it should be used as **one of the data points** to determine if an account can be trusted. There are situations where the KYC flag is still `true`, but an account can no longer be trusted. Eg. when account keys are compromised and the account is now controlled by a 3rd party. While unlikely, depending on the level of trust required for your application you may want to mitigate against these kinds of fraud.
