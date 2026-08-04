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

## review

Use this metaobject for the customer reviews rail.

Fields:
- `quote` - Multi-line text
- `author` - Single line text
- `rating` - Number (integer or decimal, 1–5)
- `photo` - File/image (optional)
- `product` - Product reference (optional)

In Shopify admin, go to **Content → Metaobjects → Add definition**, name it `Review`, add the fields above using the shown keys, then create entries. In the Reviews rail section, select the entries in **Reviews** and set **Maximum reviews** to control how many appear. The rail safely shows its editor empty state until at least one entry is selected.
