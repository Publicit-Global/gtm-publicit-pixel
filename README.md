# Publicit Pixel · Google Tag Manager template

Official Google Tag Manager tag template for the [Publicit](https://publicit.com) pixel.
It builds retargeting audiences for Connected TV campaigns on Publicit and measures
purchases, without editing your site's code.

## Setup

1. In Google Tag Manager, open **Templates → Search Gallery** and add **Publicit Pixel**.
2. Create a tag of type **Publicit Pixel**:
   - **Pixel key**: your `pk_live_…` key, from **Audiences** in the
     [Publicit dashboard](https://app.publicit.com).
   - **Event**: *Page view*.
   - **Trigger**: *All Pages*.
3. To measure purchases, add a second tag of type **Publicit Pixel**:
   - **Event**: *Purchase*.
   - **Order value, currency and order ID**: map them from your data layer, for example
     `ecommerce.value`, `ecommerce.currency` and `ecommerce.transaction_id`.
   - **Trigger**: your `purchase` event.
4. Choose how consent is obtained (see below) and publish the container.

You can also send custom events, such as `lead` or `sign_up`, with **Event → Custom event**.

## Consent

The pixel never sends an event without advertising consent. Pick where that consent
comes from:

| Option | Behaviour |
|---|---|
| **Google Consent Mode** (default) | Fires once `ad_storage` and `ad_user_data` are granted, including when they are granted later in the visit. |
| **Detected by the pixel** | The pixel reads a TCF v2 CMP (`__tcfapi`) or the Publicit CMP. |
| **My trigger already fires only with consent** | Use this when the tag's trigger or consent settings already gate it. |

The pixel also respects Global Privacy Control and Do Not Track.

## Data sent

- The tag loads `https://px.publicit.com/p.js`. Like any web request, this exposes the
  visitor's IP address and user agent to Publicit.
- After consent, the pixel sends to `px.publicit.com`:
  - a page visit;
  - for purchases, the order value, currency and order ID.
- Publicit derives a household identifier from a salted hash of the IP address and
  discards the IP. No cookies are set except the opt-out cookie
  (`https://px.publicit.com/optout`).

- [Terms of use](https://publicit.com/terms-of-use)
- [Privacy policy](https://publicit.com/privacy-policy)

## Support

Write to engineering@publicit.es or open an issue in this repository.
