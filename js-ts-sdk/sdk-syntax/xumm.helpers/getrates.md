---
description: Get aggregated exchange rates vs. XRP for most fiat & crypto assets.
---

# getRates( … )

The `getRates` method allows you to get the exchange rates for an `XRP` <> requested pair. The source information is aggregated from several data providers.

```typescript
const rate = await Sdk.getRates('BTC');
```

#### Example response

```json
{
	"USD": 1,
	"XRP": 0.52069,
	"__meta": {
		"currency": {
			"en": "US Dollar",
			"code": "USD",
			"symbol": "$",
			"isoDecimals": 4
		}
	}
}
```
