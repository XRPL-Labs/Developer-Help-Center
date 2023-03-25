---
description: >-
  When building xApps, it makes a lot of sense to stick to the design (colour
  palette, font, etc.) as used by Xumm to offer the best user experience to xApp
  users.
---

# Style guide

#### Font family

The main application uses the font-family: `proxima-nova, sans-serif`. **Only** when using this font for your (web) xApp to be embedded in XUMM, use this stylesheet:

```
<link rel="stylesheet" href="https://use.typekit.net/vtt7ckl.css">
```

When offering your application anywhere else than as embedded (web) xApp, check your licensing needs and requirements for the use of Proxima Nova.

#### Colours

Starting XUMM version 1.1 four colour palettes are available. The colour the app is running in will be passed to the xApp in the `style` parameter, see the [xapp/ott/:token](https://xumm.readme.io/reference/xappotttoken) documentation (applies to the SDK as well).

Used colour palette codes:

* LIGHT
* DARK
* MOONLIGHT
* ROYAL

{% hint style="info" %}
Your xApp launch URL will receive a GET parameter (query param) named `xAppStyle` containing the colour palette name as active on the client device. If your xApp URL is eg.:

```
https://my.app.local/some/app
```

... the URL opened will be:

```
https://my.app.local/some/app?xAppStyle={THEME}
```
{% endhint %}

#### Standard CSS stylesheets

The four available themes are shipped as Bootstrap (version 4.5) rolled stylesheets, ready to use. You can include a Bootstrap 4.5 stylesheet by pointing to:

```
https://xumm.app/assets/themes/xapp/xumm-{theme}/bootstrap.min.css
```

The `{theme}` element should be replaced by the theme name in **lower case** notation.

#### SPA / Front-end app only

To load the right stylesheet dynamically in an environment without a backend, consider using this script in your `<head>`:

```html
<script>
  var theme = ((new URLSearchParams(document.location.href))
               .get('xAppStyle') || 'light').toLowerCase()
  var link = document.createElement('link')
  link.href = 'https://xumm.app/assets/themes/xapp/xumm-'
    + theme + '/bootstrap.min.css'
  link.type = 'text/css'
  link.rel = 'stylesheet'
  document.getElementsByTagName('head')[0].appendChild(link)
</script>
```

#### Colours

<figure><img src="../../.gitbook/assets/xApp Color palette.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/xApp Color Palette Scheme.png" alt=""><figcaption></figcaption></figure>
