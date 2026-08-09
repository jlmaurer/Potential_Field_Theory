# Vendored assets

Third-party assets used by the demos, served locally instead of from a CDN so
the demos work on restricted campus networks and keep working if a CDN goes
away or changes.

| Asset | Version | License | Source |
|---|---|---|---|
| `three.min.js` | r128 | MIT (header retained in file) | https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js |
| `fonts/` + `fonts.css` | — | SIL OFL 1.1 (`fonts/OFL.txt`) | Google Fonts css2 API |

## Regenerating the fonts

`fonts.css` is the Google Fonts stylesheet with the remote `url()` values
rewritten to local paths. To refresh it, request the stylesheet with a modern
browser User-Agent (the response varies by UA — an older one yields `.ttf`
instead of `.woff2`):

```bash
curl -H "User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) \
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36" \
  "https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap"
```

Then download each `url()` target and repoint it at `fonts/`.

Two things to know:

- Only the **latin** and **latin-ext** subsets are kept. The upstream response
  also includes cyrillic, cyrillic-ext, and vietnamese; the demos are English,
  and browsers only download subsets matching the `unicode-range` they need, so
  dropping them costs nothing at runtime.
- **Space Grotesk is a variable font.** All four requested weights resolve to
  the same `.woff2` file per subset, so the file is stored once and the 500/600/
  700 `@font-face` rules point back at the 400 filename. This is intentional —
  the browser instances the weight from the variable font.
