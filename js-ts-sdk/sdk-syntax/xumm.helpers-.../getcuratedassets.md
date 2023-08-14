# getCuratedAssets()

The `getCuratedAssets` method allows you to get the list of trusted issuers and IOU's. This is the same list used to populate the "Add Asset" button at the XUMM home screan.

```typescript
const curatedAssets = await Sdk.getCuratedAssets();
```

Returns [`<CuratedAssetsResponse>`](https://github.com/XRPL-Labs/XUMM-SDK/blob/master/src/types/Meta/CuratedAssetsResponse.ts):

```javascript
{
  curatedAssets: {
    issuers: [ 'Bitstamp', 'GateHub' ],
    currencies: [ 'USD', 'BTC', 'EUR', 'ETH' ],
    details: {
      Bitstamp: [Object],
      GateHub: [Object]
    }
  }
}
```
