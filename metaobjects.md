# Metaobjects

## combo

Use this metaobject for the Best selling combos rail.

| Field key | Admin field type | Required | Purpose |
| --- | --- | --- | --- |
| `title` | Single line text | Yes | Combo name |
| `description` | Rich text | No | Card description |
| `products` | List of products | No | Products shown in the compact product stack |
| `image` | File/image | No | Fallback image when no products are selected |
| `badge_text` | Single line text | No | Merchandising badge |

### Admin setup

1. In Shopify admin, open **Content → Metaobjects → Add definition** and name it `Combo` (type `combo`).
2. Add the fields above with the exact keys and save.
3. Create combo entries in **Content → Metaobjects → Combo**.
4. In **Online Store → Themes → Customize**, open Best selling combos. Add a Combo card block, select its combo entry, then set its layout-specific price, savings, CTA, flag, and stack captions. Those are section-block fields because the prototype treats them as merchandising presentation rather than reusable catalog content.

The section retains fallback block fields so it remains usable before any entries are connected.

## review

Use this metaobject for the customer reviews rail.

Fields:
- `quote` - Multi-line text
- `author` - Single line text
- `rating` - Number (integer or decimal, 1–5)
- `photo` - File/image (optional)
- `product` - Product reference (optional)

### Admin setup

1. In Shopify admin, open **Content → Metaobjects → Add definition** and name it `Review` (type `review`).
2. Add the fields above with the exact keys and save. For `rating`, constrain values to 1–5 in the definition when available.
3. Create entries in **Content → Metaobjects → Review**.
4. In the Reviews rail section, select entries in **Reviews** and set **Maximum reviews**. The rail safely shows its editor empty state until at least one entry is selected.
