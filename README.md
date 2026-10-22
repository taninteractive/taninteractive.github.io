# taninteractive.github.io
Tan Interactive website: game pages and privacy policies.

- `index.html`: landing page listing the studio's games with store buttons. The list is read from `promo/catalog.json` (a store button shows only when that store is `live`; the rest sit under "Coming soon"), so going live in a store is one catalog edit. Hungry Frog is the featured game (`assets/hungry-frog/`: 720p trailer cut, poster, feature graphic for link previews).
- `frog/`: short link `taninteractive.github.io/frog` for places where a link can't be tapped (YouTube Shorts descriptions, in-video text, Instagram/TikTok bios). Android goes straight to Google Play, Fire tablets to Amazon Appstore; desktop and iPhone get the store buttons plus a QR (`frog/qr.svg`, encodes `/frog/?s=qr`). The Play `referrer` carries `utm_medium=shortlink` and `utm_source` = `?s=` if given, else the referring site, else `direct` (a typed address). `?stay` shows the page on a phone. `hungry-frog/index.html` forwards the long name to it.
- `<game>/privacy*.html`: privacy policies.
- `promo/`: cross-promo catalog, see `promo/README.md`.
