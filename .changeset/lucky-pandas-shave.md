---
'@shopify/hydrogen': patch
---

Stop the analytics and consent bootstrap from breaking hydration.

- `Analytics.Provider` now applies its post-hydration state updates (the deferred shop and cart resolutions, and consent changes reported by the Customer Privacy API) inside `startTransition`. Previously these urgent updates could land while a streamed Suspense boundary below the provider was still dehydrated, which made React discard that boundary's server HTML and client-render it (recoverable error #421).
- `useCustomerPrivacy` no longer crashes the page when a browser extension or another script has locked `window.Shopify` so it cannot be extended. It now logs a warning and skips loading the Customer Privacy API instead.
