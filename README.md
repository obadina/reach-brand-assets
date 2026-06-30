# Reach Brand Assets

Public CDN for Reach brand assets — logos, icons, and exportables for all brands in the Navigator Design System.

**Base URL:** `https://obadina.github.io/reach-brand-assets`

---

## Usage

### Direct URL

```
https://obadina.github.io/reach-brand-assets/brands/{brand-cue}/logo.png
```

Example:
```
https://obadina.github.io/reach-brand-assets/brands/aberdeenlive/logo.png
```

### Manifest JSON

Fetch the manifest at build time to get all brands and their asset URLs:

```
GET https://obadina.github.io/reach-brand-assets/manifest.json
```

```json
{
  "version": "1.0.0",
  "baseUrl": "https://obadina.github.io/reach-brand-assets",
  "brands": {
    "aberdeenlive": {
      "name": "Aberdeen Live",
      "assets": {
        "logo": "brands/aberdeenlive/logo.png"
      }
    }
  }
}
```

Full asset URL = `baseUrl + "/" + assets.logo`

---

## Asset structure

```
brands/
  {brand-cue}/
    logo.png              ← default logo
    logo-christmas.png    ← seasonal variant (when applicable)
    icon.svg              ← app icon / favicon (when applicable)
manifest.json             ← index of all brands + asset paths
```

---

## Seasonal and variant assets

Variant assets sit alongside the default in the same brand folder and are listed under the brand's `variants` key in the manifest:

```json
{
  "aberdeenlive": {
    "name": "Aberdeen Live",
    "assets": {
      "logo": "brands/aberdeenlive/logo.png"
    },
    "variants": {
      "christmas": "brands/aberdeenlive/logo-christmas.png"
    }
  }
}
```

Devs resolve the active asset using a feature flag:

```js
const variant = featureFlags.get("logo-variant") // e.g. "christmas" or null
const assetPath = manifest.brands[cue].variants?.[variant] ?? manifest.brands[cue].assets.logo
const url = manifest.baseUrl + "/" + assetPath
```

---

## For designers: adding or updating assets

1. Export the asset from Figma (use the Exportables panel on the brand's frame).
2. Place it in `brands/{brand-cue}/` using the naming convention above.
3. Update `manifest.json` — add the new asset path under the brand's `assets` or `variants` key.
4. Open a pull request. Once merged, the asset is live within minutes.

No code changes or dev deploys needed for asset updates.

---

## Brands without logos

14 brands currently have no logo asset. Contributions welcome — export from the NavigatorDS Assets Figma file and follow the steps above.

---

## Related

- [Token Documentation Site](https://github.com/obadina/reach-design-hub) — per-brand colour and typography docs
- [NavigatorDS Assets (Figma)](https://www.figma.com/design/ktnOQyf13cJP65WNxWWU35/NavigatorDS-Assets)
