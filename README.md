# Kiku Karakusa, Pair 07: craft passport prototype

Kyoto AI Innovation Lab FA26, Team A. A page an NFC tag opens for one pair of WLK HANAO SHOES (Kiku Karakusa strap, dyed by Iwai Senkou).

Static site, no build step. Vercel deploys `main` as is.

- `index.html`: the whole page (styles, markup, script)
- `img/`: WebP photos, the engraved stamp, pre-rendered brush glyphs (g-*.webp), the 27 s film (film.mp4, 1.9 MB, loads only after the first tap) and its poster
- `fonts/`: subset WOFF2 fonts (only the characters the page uses; re-subset with pyftsubset if you add new kanji)
- `lib/`: GSAP 3.15 and SplitText

Flows: first tap (mine / gift / show me), gift recipient, returning owner. State lives in localStorage (key `kk-pair07-v5`); the footer has demo buttons to switch flows.

Photographs belong to Whole Love Kyoto, lent for Demo Day only. Remove them after Demo Day.
