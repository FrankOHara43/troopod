# Purelane homepage build notes

The original prototype was a static, div-heavy HTML demo: product silhouettes and copy were embedded in markup, bundle savings were hardcoded, repeated review cards simulated movement, and its IDs/scripts were not safe for Shopify’s section editor. It also lacked useful empty states and real image handling.

## What changed

- **Hero:** kept the existing visual treatment, but made its rotator lifecycle-safe for section reloads, added focus visibility, meaningful image-alt fallbacks, and responsive image candidates.
- **Shop grid:** uses real Shopify products through the existing reusable card snippet, including responsive, lazy-loaded product media and a safe empty state. Placeholder SVG IDs are now section-specific.
- **Best-selling combos:** preserves the prototype’s scroll-snap rail while allowing combo metaobjects and fallback blocks. Its keyboard rail listener now initializes and cleans up in the theme editor.
- **Bundles:** models the prototype’s pick-any tier offers as editable manual product-list blocks. The comparison total and saving are calculated from selected product variants; semantic card/list markup replaced the prototype’s generic wrappers.
- **Reviews:** adds a merchant-selected `review` metaobject rail with CSS-only marquee behavior, hover/focus pause, reduced-motion fallback, optional reviewer photo/product, and labelled star ratings.

## Deferred work

The prototype implies a real bundle-picker/cart flow, but it does not specify the required bundle app, line-item properties, inventory rules, or discount implementation. The current CTA remains a configurable link. With more time, I would connect it to the chosen bundle solution, add visual regression tests against the prototype at key breakpoints, and validate final contrast with the store’s installed theme tokens and real imagery.
