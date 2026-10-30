# Golden Service Website

## What This Is

Website for Golden Service Mobile Bar & Catering, a licensed mobile bar for events in Halifax and across Nova Scotia. Success on the site is a completed quote request.

Website: goldenservice.ca
Repo: heyokaytk/goldenservice.ca (GitHub)
Hosting: GitHub Pages (`CNAME`), fronted by Cloudflare DNS/proxy.
Quote form: Web3Forms (`https://api.web3forms.com/submit`), delivering to hello@goldenservice.ca.

`PRODUCT.md` holds the audience, positioning, evidence on hand and product principles. Read it before writing copy: no bar prices, no licence fees, no invented proof, no em dashes in site copy.

---

## Stack

Static HTML, one `index.html` per page, no build step. Pages: home, `corporate/`, `weddings/`, `wedding-bar-guide/`, `liquor-licence-guide/`, `venues/` (partner sheet, noindex), `404.html`.
SEO files: `sitemap.xml` (indexable pages only), `robots.txt`, `llms.txt`.

After any site change: push to `main` (Pages rebuilds automatically). If the change doesn't appear live, purge the Cloudflare cache.

---

## Design System

`styles.css` holds the tokens and every component used on more than one page. Every page links `/styles.css` (absolute path) before its own `<style>` block, which holds only that page's sections.

**Rules**
- No raw hex colours or font stacks in pages. Use the `--gs-*` tokens; add a new token to `:root` in `styles.css` if one is genuinely missing. `rgba()` is fine inside hero scrims, gradients and shadows only.
- Don't redefine a `styles.css` rule in a page. If a page really needs something different, override only the property that differs.
- Media queries in `styles.css` run widest first (980 → 760 → 620 → 560) so the narrower one wins; keep that order.
- Reuse before inventing: `.gs-shell`, `.gs-title` (+ `em` in gold), `.gs-lede`, `.gs-btn-primary`, `.gs-text-link` / `.gs-link-on-dark`, `.gs-trust` strip, `.gs-spec` (label/answer rows), `.gs-tiers` (bar styles), FAQ `details`, the quote form (`.gs-card`, `.gs-field`, `.gs-input`, `.gs-choice`, `.gs-submit`, `.gs-status`), `.gs-mbar` (mobile quote bar), nav, footer, `data-reveal`.

**Palette**: white and warm paper (`--gs-paper`, `--gs-paper-deep`) with near-black ink and one gold. `--gs-gold` for buttons, large type and icons; `--gs-gold-deep` for any small gold text (AA). Dark sections use `--gs-ink` with the `*-on-dark` tokens. Running text is `--gs-body`; `--gs-muted` is for secondary notes only.

**Type**: Playfair Display (`--gs-font-display`) for headings, the logo and pull quotes; DM Sans (`--gs-font-body`) for everything else. Body text is 16px; nothing below 13px.

**Shape**: buttons 3px, inputs and status boxes 5px, photos 6px, the form card 8px.

**Hero**: one shared version in `styles.css` (scrim, height, h1 with the gold italic second line, sub). A page sets only its photo in `.gs-hero::before`. The homepage uses an `<img>` instead (for load speed) and keeps its taller, bottom-aligned layout. Headlines stay at two lines at every width; shorten the words before shrinking the type.

**Primary CTA**: one gold `.gs-btn-primary` per view, pointing at the quote form. On phones, the `.gs-mbar` quote bar carries it.

---

## Pre-Push Checks (every push)

Quick and mechanical, no write-up needed unless something fails:
- Every JSON-LD block still parses.
- New or renamed indexable pages are in `sitemap.xml`; internal links resolve.
- The quote form still posts to Web3Forms with the right access key.
- Copy follows `PRODUCT.md` (no bar prices, no licence fees, no unverified claims).
