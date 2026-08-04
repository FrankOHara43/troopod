# Purelane Homepage Audit

Scope: only `section.hero`, `#shop`, `#combos`, `#bundles`, and `#reviews`.

## 1) Hero (`section.hero`)

### Hardcoded merchant-facing content
- Headline: `Clean That Lasts`
- Accent word: `Lasts`
- Lede: `Homecare that works on the toughest grime, made from plants. Kind to your home, your family and the world outside it.`
- Primary CTA: `Shop now`
- Secondary CTA: `How it works`
- Side promise badges: `Plant powered`, `Safe for kids & pets`, `Zero harsh chemicals`
- Mobile badge strip repeats the same three promises as `Plant powered`, `Kids & pet safe`, `Zero harsh chem`
- Slide 1 copy: `Single bottle`, `₹200`, `₹299`, `33% off`
- Slide 1 product label / alt text: `Purelane foaming kitchen cleaner spray bottle`
- Slide 2 copy: `Any 2 products`, `₹349`, `₹598`, `Save ₹249`
- Slide 2 product labels / alt text: `Purelane tap cleaner and limescale remover spray bottle`, `Purelane foaming kitchen cleaner spray bottle`
- Slide 3 copy: `Any 3 products`, `₹499`, `₹897`, `Save ₹398`
- Slide 3 product labels / alt text: `Purelane tap cleaner and limescale remover spray bottle`, `Purelane copper, bronze and brass cleaner pump bottle`, `Purelane foaming kitchen cleaner spray bottle`
- Slide dot labels: `Show 1 product`, `Show 2 products`, `Show 3 products`

### Repeated card/tile patterns and variants
- Three-slide hero product rotator.
- Same bottle art appears across slides, with `p-kbtl` reused in slide 1 and slide 2.
- Variant pattern is product count, not a different template: 1-product, 2-product, 3-product.
- Price tag block (`ptag`) repeats on every slide with different labels, prices, and savings.

### CSS that is risky at 375px–768px
- `@media(max-width:900px) .hero-prod` switches from absolute positioning to a centered block. On small screens this pushes the product stage under the copy and can make the first viewport very tall.
- `@media(max-width:900px) .hero::before` changes to a much darker overlay; if the background scene changes, text readability becomes very dependent on the exact fade.
- `@media(max-width:900px) .hstage` is still `clamp(300px,44svh,430px)`, which is large for 375px widths and can crowd the fold.
- `@media(max-width:900px) .ptag { max-width:58% }` leaves little room for longer merchant copy, so the price/savings block can wrap or feel cramped.
- `@media(max-width:420px) .hero-prod { width:min(92vw,360px) }` is close to full width and can dominate the viewport on phones.

### Animation / transition logic
- Scroll-driven scene crossfade changes the fixed background scene as the user scrolls.
- Scroll-driven parallax moves the water layers and the hero product stage via `requestAnimationFrame` in the `scroll` handler.
- Mouse-move parallax applies only on `min-width:1024px`.
- The hero product stage auto-rotates through 3 slides every 3.8s via `setInterval` after `IntersectionObserver` says the stage is visible.
- Hovering the hero stage stops the autoplay; leaving it restarts it.
- The hero product container also gets an infinite `animate()` drift loop on load when motion is not reduced.

### Accessibility issues
- The hero is motion-heavy by default; reduced-motion fallback exists, but the default experience still relies on continuous animation and scroll-linked motion.
- The hero has no explicit pause button for the auto-rotating slide show; only hover stops it.
- The product visuals use `role="img"` and `aria-label`, which is good, but the slide content is still mostly conveyed through visual composition and pricing badges.
- `btn-ghost` and the hero overlay rely on contrast from the background scene; readability is scene-dependent.

### Performance issues
- Very large inline SVG background layers plus turbulence/displacement filters in the water scene.
- Multiple infinite animations: water drift, bubble rise, scene fade, product drift, hero autoplay.
- Scroll and mousemove both trigger JS-driven transforms.
- The hero is visually rich but expensive to paint and composite, especially on mobile GPUs.

## 2) Shop (`#shop`)

### Hardcoded merchant-facing content
- Section kicker: `Bestsellers`
- Heading: `Loved by 30,000 homes`
- Card 1 badge: `Best seller`
- Card 1 title: `Tap cleaner & limescale remover`
- Card 1 rating text: `★ 4.8 · 237 reviews`
- Card 1 price: `₹200` / `₹299` / `33% off`
- Card 1 alt text: `Tap cleaner and limescale remover spray with carton`
- Card 1 CTA: `Add to cart`
- Card 2 badge: `Best seller`
- Card 2 title: `Kitchen cleaner, foaming`
- Card 2 rating text: `★ 4.8 · 254 reviews`
- Card 2 price: `₹200` / `₹299` / `33% off`
- Card 2 alt text: `Foaming kitchen cleaner spray with carton`
- Card 2 CTA: `Add to cart`
- Card 3 badge: `Top rated`
- Card 3 title: `Copper, bronze & brass cleaner`
- Card 3 rating text: `★ 4.8 · 231 reviews`
- Card 3 price: `₹200` / `₹299` / `33% off`
- Card 3 alt text: `Copper, bronze and brass cleaner pump bottle with carton`
- Card 3 CTA: `Add to cart`
- Card 4 badge: `New`
- Card 4 title: `Washing machine cleaner & descaler`
- Card 4 rating text: `★ 4.8 · 183 reviews`
- Card 4 price: `₹200` / `₹299` / `33% off`
- Card 4 alt text: `Washing machine cleaner and descaler tablets carton`
- Card 4 CTA: `Add to cart`
- Card 5 repeats the tap cleaner product with a hardcoded inline SVG pack illustration.
- Card 5 title repeats: `Tap cleaner & limescale remover`
- Card 5 rating text repeats: `★ 4.8 · 237 reviews`
- Card 5 price repeats: `₹200` / `₹299` / `33% off`
- Card 5 SVG carton text: `PURELANE`, `TAP CLEANER`, `LIMESCALE`, `500 ML`
- Card 6 repeats the kitchen cleaner product with inline SVG carton art.
- Card 6 title repeats: `Kitchen cleaner, foaming`
- Card 6 rating text repeats: `★ 4.8 · 254 reviews`
- Card 6 SVG carton text: `PURELANE`, `KITCHEN`, `CLEANER`, `500 ML`
- Card 7 repeats the copper/brass cleaner product with inline SVG carton art.
- Card 7 title repeats: `Copper, bronze & brass cleaner`
- Card 7 rating text repeats: `★ 4.8 · 231 reviews`
- Card 7 SVG carton text: `PURELANE`, `COPPER BRASS`, `& BRONZE`, `300 ML`
- Card 8 repeats the washing machine cleaner product with inline SVG carton art.
- Card 8 title repeats: `Washing machine cleaner & descaler`
- Card 8 rating text repeats: `★ 4.8 · 183 reviews`
- Card 8 SVG carton text: `PURELANE`, `WASHING MC`, `DESCALER`, `8 TABLETS`

### Repeated card/tile patterns and variants
- Eight cards total, but they are four products shown twice.
- Two visual variants per product: one uses `.pimg` background art, the other uses a hardcoded inline SVG package illustration.
- No sold-out state is present.
- No no-image state is present in `#shop`; every card has visual artwork.
- The repeated product set is not a separate assortment; it is a duplicated presentation of the same four SKUs.

### CSS that is risky at 375px–768px
- `.shelf` stays a 2-column grid until `min-width:860px`, so 375px–768px is always two-up and therefore tight for uppercase product titles, prices, and buttons.
- `@media(max-width:760px) .card .shot { height:126px }` shrinks the art area, but the grid still remains two columns, so the copy area becomes the first thing to crowd.
- The long product names, especially `Copper, bronze & brass cleaner` and `Washing machine cleaner & descaler`, are likely to wrap to two lines in narrow columns.
- The SVG-backed cards contain hardcoded text inside the artwork, so the art itself does not reflow with the card width.

### Animation / transition logic
- Cards hover-lift with `transform: translateY(-5px)` and a `.4s` transition.
- No JS behavior is attached to the shop grid itself.

### Accessibility issues
- The first four cards use `role="img"` and `aria-label` on the product art, which is good.
- The SVG-backed duplicate cards do not have explicit `aria-hidden="true"`, so assistive tech may encounter noisy decorative SVG content.
- The shop duplicates the same four products twice in the DOM, which can be confusing for screen reader users and keyboard users trying to orient themselves.
- The card buttons are unlabeled beyond `Add to cart`, so the product context must come from surrounding text.
- Secondary text such as review counts and discount labels is visually de-emphasized and may be borderline on contrast when rendered on the light glass background.

### Performance issues
- Eight product cards are rendered, with four of them duplicated content.
- The duplicated cards carry large inline SVG art directly in the HTML, increasing DOM weight and parse cost.
- All product artwork is inlined or CSS-backed, so there is no opportunity for native image lazy-loading here.

## 3) Best-selling Combos (`#combos`)

### Hardcoded merchant-facing content
- Section kicker: `Pre-built to save you money`
- Heading: `Best selling combos`
- Intro copy: `Swipe through the boxes people order most. Each one is already priced below buying the same products on their own.`
- Combo 1 label: `You save ₹398`
- Combo 1 flag: `Most popular`
- Combo 1 title: `Kitchen essentials`
- Combo 1 count: `3 products`
- Combo 1 includes: `Foaming Kitchen Cleaner, Dishwash Gel & Tap Cleaner`
- Combo 1 supporting copy: `Everything for a sparkling kitchen, no need to pick separately.`
- Combo 1 price: `₹499` / `₹897` / `Save ₹398`
- Combo 1 fine print: `Inclusive of all taxes · COD available`
- Combo 1 button: `Shop bundle`
- Combo 1 stack labels: `Cuts grease instantly`, `Squeaky clean dishes`, `Melts hard water stains`
- Combo 2 label: `You save ₹448`
- Combo 2 title: `Laundry care bundle`
- Combo 2 count: `3 products`
- Combo 2 includes: `Laundry Detergent, Fabric Conditioner & Machine Cleaner Powder`
- Combo 2 supporting copy: `Softer, fresher wash, all in one box.`
- Combo 2 price: `₹499` / `₹947` / `Save ₹448`
- Combo 2 fine print: `Inclusive of all taxes · COD available`
- Combo 2 button: `Shop bundle`
- Combo 2 stack labels: `Removes tough stains & odour`, `Softens & freshens every wash`, `Deep-cleans your machine`
- Combo 2 uses a no-image tile placeholder in the stack for the middle item.
- Combo 3 label: `Biggest saving`
- Combo 3 flag: `Best value`
- Combo 3 title: `Complete home bundle`
- Combo 3 count: `5 products`
- Combo 3 includes: `Kitchen Cleaner, Laundry Detergent, Floor Cleaner, Toilet Cleaner & Handwash`
- Combo 3 supporting copy: `Our biggest saving box.`
- Combo 3 price: `₹799` / `₹1,495` / `Save ₹696`
- Combo 3 fine print: `Inclusive of all taxes · COD available`
- Combo 3 button: `Shop bundle`
- Combo 3 stack labels: `Cuts grease instantly`, `Kills 99.9% germs`, `Gentle hydration for hands`
- Combo 4 label: `You save ₹398`
- Combo 4 title: `Bathroom deep clean`
- Combo 4 count: `3 products`
- Combo 4 includes: `Toilet Cleaner, Tap Cleaner & Magic Eraser`
- Combo 4 supporting copy: `A complete bathroom refresh in one box.`
- Combo 4 price: `₹499` / `₹897` / `Save ₹398`
- Combo 4 fine print: `Inclusive of all taxes · COD available`
- Combo 4 button: `Shop bundle`
- Combo 4 stack labels: `Kills 99.9% germs`, `Melts hard water stains`, `Scrubs away soap scum`
- Combo 5 label: `You save ₹249`
- Combo 5 title: `Hard water solution kit`
- Combo 5 count: `2 products`
- Combo 5 includes: `Tap Cleaner & Toilet Cleaner`
- Combo 5 supporting copy: `A quick, focused fix for hard water stains across the home.`
- Combo 5 price: `₹349` / `₹598` / `Save ₹249`
- Combo 5 fine print: `Inclusive of all taxes · COD available`
- Combo 5 button: `Shop bundle`
- Combo 5 stack labels: `Melts hard water stains`, `Fights limescale in the bowl`

### Repeated card/tile patterns and variants
- Five horizontal combo cards in a snap-scrolling rail.
- The card template repeats: save badge, optional flag, product stack, title, product count, inclusion copy, price row, fine print, CTA.
- Variants present: 2-product bundle, 3-product bundle, 5-product bundle, highlighted best-value bundle, and a `no-image` placeholder tile in the laundry bundle.
- No sold-out state is present.

### CSS that is risky at 375px–768px
- `.comborail` is intentionally horizontal and keeps a fixed card basis: `302px` desktop, `268px` below `760px`, which means the layout always clips side content and depends on horizontal scrolling.
- `margin: 0 -18px` plus padding adjustments can make the first/last cards feel cropped at phone widths.
- `.stack .it .pimg` and `.stack .it .tile` shrink at `max-width:760px`, but the label text beneath them is still fixed-size and can wrap awkwardly.
- The `hero-combo` card has the largest emphasis and can dominate the viewport on 375px devices.

### Animation / transition logic
- Combo cards lift on hover with `transform: translateY(-5px)`.
- The rail itself does not animate in JS, but it relies on horizontal scrolling and scroll snap for navigation.

### Accessibility issues
- The rail is visually swipe-driven but has no explicit previous/next controls.
- `aria-hidden="true"` is used on plus separators, which is good.
- The `no-image` placeholder tile in the laundry bundle relies on a decorative icon and short text, so the meaning depends heavily on surrounding context.
- Horizontal carousels can be keyboard-accessible if focus lands inside them, but the page offers no dedicated focus cue or affordance for moving through all cards.

### Performance issues
- Five cards in a horizontal rail means a lot of content is mounted at once, even though only a subset is visible.
- Multiple duplicated product images are rendered across the combo cards.
- The rail uses `scroll-snap` and overflow scrolling, which is fine, but the large card payload is still fully delivered up front.

## 4) Bundles (`#bundles`)

### Hardcoded merchant-facing content
- Section kicker: `Build your bundle`
- Heading: `One box. Every room.`
- Intro copy: `Mix and match across kitchen, laundry, home and skin. One flat price, no code needed, free shipping either way.`
- Starter badge: `Starter`
- Starter quantity: `2 Products`
- Starter price: `₹349` / `₹598`
- Starter per-product line: `Flat ₹174 per product`
- Starter bullet 1: `Pick any two products`
- Starter bullet 2: `Free shipping across India`
- Starter button: `Build this box`
- Starter tier image alt text: `Purelane tap cleaner and kitchen cleaner combo pack`
- Most popular badge: `Most popular`
- Most popular quantity: `3 Products`
- Most popular price: `₹499` / `₹897`
- Most popular per-product line: `Flat ₹166 per product`
- Most popular bullet 1: `Pick any three products`
- Most popular bullet 2: `Covers kitchen and laundry`
- Most popular bullet 3: `Free shipping across India`
- Most popular button: `Build this box`
- Most popular tier image alt text: `Purelane foaming kitchen cleaner`, `Purelane tap cleaner and limescale remover`, `Purelane organic dishwash liquid gel`
- Whole home badge: `Whole home`
- Whole home quantity: `5 Products`
- Whole home price: `₹799` / `₹1495`
- Whole home per-product line: `Flat ₹160 per product`
- Whole home bullet 1: `Pick any five products`
- Whole home bullet 2: `Every room in one order`
- Whole home bullet 3: `Free shipping across India`
- Whole home button: `Build this box`
- Whole home tier image alt text: `Purelane foaming kitchen cleaner`, `Purelane tap cleaner and limescale remover`, `Purelane natural herbal floor cleaner`, `Purelane non-toxic toilet cleaner`, `Purelane non-toxic laundry detergent`

### Repeated card/tile patterns and variants
- Three vertical bundle cards: 2-product, 3-product, 5-product.
- The middle tier is visually emphasized as `best` and uses the primary CTA style.
- The repeated pattern is quantity block, price block, bullet list, and full-width CTA.
- The `tierpix` row repeats product art across the tiers, including a `five`-item variant.

### CSS that is risky at 375px–768px
- `@media(min-width:760px) .tiers { grid-template-columns: repeat(3,1fr) }` means 760px–768px jumps straight to three narrow columns, which is the tightest zone for this section.
- `tier .qty { font-size:52px }` and `tier .price { font-size:27px }` are large for narrow cards and can force awkward wrapping at the 760px breakpoint.
- The cards rely on the `tierpix` strip for visual hierarchy; if the product art scales down, the price block becomes visually dense.
- On 375px widths, the single-column layout is fine, but the fixed typography still makes the cards very tall.

### Animation / transition logic
- `.tier:hover` lifts each card slightly.
- No JS behavior is attached to `#bundles`.

### Accessibility issues
- The bundle cards are semantically reasonable (`article`, lists, links), with product art hidden from assistive tech via `aria-hidden` on the decorative strip.
- The only variant indicator for the top-tier emphasis is a mix of badge text, border, and button color, so the visual priority depends partly on color.
- Several supporting lines use low-emphasis body text on glass backgrounds, which can be hard to read on smaller screens.

### Performance issues
- This section is mostly static, but it still renders three separate product-art strips and duplicated artwork across tiers.
- No lazy loading is present because the visuals are embedded as SVG/CSS rather than external images.

## 5) Reviews Rail (`#reviews`)

### Hardcoded merchant-facing content
- Section kicker: `That’s what they said`
- Aggregate rating line: `4.8 from 8,000+ reviews`
- Aggregate homes line: `Loved by 12 lakh+ homes`
- Review card 1 stars: `★★★★★`
- Review card 1 title: `Works like a charm`
- Review card 1 body: `Finally an eco option that cleans as well as the chemical detergent I used for years, and it smells better.`
- Review card 1 name / product: `Anita · Laundry detergent`
- Review card 2 stars: `★★★★★`
- Review card 2 title: `Best dishwash ever`
- Review card 2 body: `Our old dishwash left my help with dry, cracked skin. That stopped completely after we switched.`
- Review card 2 name / product: `Priya · Dishwash gel`
- Review card 3 stars: `★★★★★`
- Review card 3 title: `Great product, great packaging`
- Review card 3 body: `Very soft on hands with a lovely fragrance, and it feels good to be using far less plastic.`
- Review card 3 name / product: `Sunita · Liquid handwash`
- Review card 4 stars: `★★★★★`
- Review card 4 title: `Dog friendly`
- Review card 4 body: `We switched because chemical floor cleaners were setting off my dog's allergies. No reactions since.`
- Review card 4 name / product: `Rohit S. · Floor cleaner`
- Review card 5 stars: `★★★★★`
- Review card 5 title: `Sparkling taps again`
- Review card 5 body: `Hard water had ruined our bathroom fittings. Two sprays and the scale wipes straight off, no scrubbing.`
- Review card 5 name / product: `Verified buyer · Tap cleaner`
- Review card 6 repeats review 1.
- Review card 7 repeats review 2.
- Review card 8 repeats review 3.
- Review card 9 repeats review 4.
- Review card 10 repeats review 5.

### Repeated card/tile patterns and variants
- Five unique review cards duplicated once to create a continuous marquee.
- Each card repeats the same structure: star line, title, body copy, author line, product line.
- No sold-out/no-image variants exist here.
- The rail is not a finite list; it is a looping duplicate sequence.

### CSS that is risky at 375px–768px
- `.rcard { width:284px }` and the mobile override `.rcard { width:250px }` still force a horizontally scrolling rail on phones.
- `-webkit-mask-image` / `mask-image` fades the edges of the rail, which can clip card shadows and focus rings at the left/right edges.
- `@media(max-width:760px) .revtrack { animation-duration:40s }` speeds up the marquee slightly on mobile, which can make reading harder.
- The rail has no wrapping fallback, so at 375px every card remains a fixed-width tile.

### Animation / transition logic
- Continuous marquee animation: `marq 52s linear infinite`.
- The marquee pauses on `:hover` and `:focus-within`.
- On mobile, the animation duration changes to 40s.

### Accessibility issues
- The marquee is motion-heavy and repeats content twice without a pause control.
- Duplicated reviews are read twice in the DOM, which can create verbosity for screen readers.
- The rail pausing mechanism depends on hover/focus, but there is no explicit button to stop animation.
- The masked edges can hide parts of cards when tabbing through them.

### Performance issues
- Ten review cards are mounted, but only five are unique; the rail duplicates the same content to support looping.
- The continuous CSS transform animation runs forever.
- The mask overlay adds compositing work on top of the marquee animation.
