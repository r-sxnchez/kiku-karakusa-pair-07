# Kiku Karakusa, Pair 07: craft passport prototype

Kyoto AI Innovation Lab FA26, Team A. A page an NFC tag opens for one pair of WLK HANAO SHOES (Kiku Karakusa strap, dyed by Iwai Senkou).

Static site, no build step. Vercel deploys `main` as is.

- `index.html`: the whole page (styles, markup, script)
- `img/`: WebP photos, the engraved stamp, pre-rendered brush glyphs (g-*.webp), the 27 s film (film.mp4, 1.9 MB, loads only after the first tap) and its poster
- `fonts/`: subset WOFF2 fonts (only the characters the page uses; re-subset with pyftsubset if you add new kanji)
- `lib/`: GSAP 3.15 and SplitText

Bilingual (EN / 日本語): all words live in the `T` object in index.html; the switch is top right, and Japanese is the default on phones set to Japanese. Plate texts in Japanese come from Kazu's WLK page copy; the interface lines are drafts for the Kyoto members to check.

Page 01 is the workshop bio: its quote is Iwai Senkou's own line from the film subtitles; the body is from Kazu's WLK page copy.

Every page is exactly one screen tall (100dvh, container query units, mandatory scroll snap).

Flows: first tap (mine / gift / show me), gift recipient, returning owner. State lives in localStorage (key `kk-pair07-v5`); the footer has demo buttons to switch flows.

Photographs belong to Whole Love Kyoto, lent for Demo Day only. Remove them after Demo Day.

## Live items (Supabase)

Each NFC chip is written with its own link: `https://kiku-karakusa-pair-07.vercel.app/?id=WLK-0001` (to WLK-0005). The page reads that pair's row from the Supabase project **Kyoto-AI-Lab** (table `passports`). Without `?id` the page runs the old local demo.

- `get_passport(id)` public read; never returns the claim code.
- `claim_passport(id, code, name, country, date)` buyer claims once with the code on the card in the box. A sealed gift is claimed by the recipient without a code.
- `seal_gift(id, code, to, message, from, date)` buyer seals a letter instead.
- The table itself is closed to the public key (RLS on, no grants); only these functions are callable.
- The phone that claimed is remembered in localStorage (`kk-own-<id>`); every other phone sees a view-only record.
- `token_id` and `token_chain` are empty until minting; when filled, they show on the stamp back and the stamp page.
- To reset a pair for testing, in the Supabase SQL editor: `update passports set status='unclaimed', owner_name=null, owner_cc=null, claimed_at=null, pm_date=null, gift_to=null, gift_msg=null, gift_from=null, gift_sealed_at=null where id='WLK-0001';`
