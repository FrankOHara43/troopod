# Metaobjects

## combo

Use this metaobject for the best-selling combos rail.

Fields:
- `title` - Single line text
- `description` - Rich text
- `products` - Product list
- `image` - File/image
- `badge_text` - Single line text

Notes:
- `title`, `description`, `products`, `image`, and `badge_text` are the source of truth for combo content.
- The section still includes fallback block settings so it can render safely before the metaobject entries are connected.
- Per-combo pricing, save labels, CTA text, and stack captions are section block fields because the prototype treats them as layout-specific merchandising, not product catalog data.
