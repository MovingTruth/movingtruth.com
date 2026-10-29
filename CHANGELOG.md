# CHANGELOG — MovingTruth
*Technical changes only. Content additions are tracked in the workspace RELEASE_LOG.*
*All dates Eastern Time.*

---

## 2026-10-29

- `themes/temple/assets/js/reflect.js` — After the reader starts reflection and completes the countdown, the overlay Continue button navigates directly to the next localized story. The final story returns to series selection. Replaces the return-to-footer/support-link pulse; existing timer, progress persistence, blessing and closing modes remain intact.

- `themes/temple/layouts/_default/baseof.html`, `themes/temple/assets/js/mt-notice.js` — Show the reading-order notice automatically only on the Moving Truth section index, in every locale. Landing pages, other series, and individual stories no longer auto-open it or consume its acknowledgement. Preserve once-per-session acknowledgement, manual footer help, keyboard handling, and progress reset.

## 2026-10-19

- `.release-fabric/localization.json` — Added a translation ledger. Every canonical English Markdown source (66) and every interface key (91) has a stable, language-neutral ID and the SHA-256 of its English. For each of the 13 other languages it records the translation's hash, the English that translation corresponds to, and its review state. It also records the reason each of seven English sources has no translated siblings: the home page is localized through templates; `/craft/`, `/log/` and the four legacy `/apps/` redirect pages are English-only by design. The existing translations are recorded as published drafts, observed as of commit `ebd0d16`: this marks where future English changes are measured from, and is not a claim that they were reviewed. When English changes, its translations are now reported stale until each is updated or a person reaffirms it. Nothing on the published pages changes because of this file.
- `i18n/*.yaml` — Added the interface strings that were missing. `new_gallery_heading` (the "New in the Gallery" heading on What's New, shown only when the gallery has additions from the last 14 days) existed only in German, so in the other 13 languages that heading would render empty. It now has English and 12 draft translations. Spanish was missing `menu_craft` and `craft_view_source`, so Spanish pages showed the English "Technical Craft" menu label (Hugo's fallback). `craft_view_source` is used only on the English-only `/craft/` page, so the Spanish value is added for completeness of the catalog. This corrects the 2026-08-04 entry below, which said both had been added in all 14 locales. All new strings are drafts, not reviewed.
- `i18n/ar.yaml`, `i18n/ko.yaml`, `i18n/th.yaml` — Fixed `new_days_ago` (the "N days ago" label on What's New). These three languages used `%d`, a placeholder the site's templates do not fill, so they showed a literal "%d" instead of the number of days. They now use `{{ . }}`, as English and the other ten languages do. The wording is otherwise unchanged and remains a draft.
- `themes/temple/layouts/craft/single.html`, `README.md` — The repository was renamed from `MovingTruthLanding` to `movingtruth.com`; the "View the source on GitHub" link and the README build badge now use the new name. The README no longer says every page exists in every language: it names the English-only routes and the translations' draft status.

## 2026-10-16

- `static/apps/inner-sign/formula.html` — Brought the public Inner Sign formula page into agreement with the current app, which offers exactly two reading lenses: Traditional 12 and Astronomical 13. Removed the retired fourteen-sign lens everywhere it still appeared: the third legend entry and wheel ring in Fig. I, the panel that made Cetus a birth sign carved from Pisces, the third span-bar tier in Fig. III, the `realAstrology` boundary table that drew both, and the related captions, comments and margin note. Fig. II now sets the Traditional twelve beside the Astronomical thirteen, and the wheel's two rings were widened to fill the space the third ring left. The page now uses the app's user-facing term "Inner Sign third" instead of "decan", and the worked example no longer shows the internal bucket key. Proposition II now also names its result the Universal Day Number, as the app does. The reading note keeps only what current source supports: changing lens changes the sign and its Inner Sign third, nothing else. The sign date boundaries and Propositions II and III are unchanged by this change; Proposition IV and the diagram arithmetic were corrected separately, as recorded below.
- `static/apps/inner-sign/formula.html` — Proposition IV (the Moon) now describes how the app actually works out the phase. The app reads a shared 1900–2099 daily table built from NASA JPL's DE440s ephemeris: the Moon's apparent angle from the Sun at 12:00 UTC, sorted into eight 45° phases centred on their true angles. The old mean-month formula and its 2026 correction counts are replaced by the table's rule, a worked example for 17 July 2026 (waxing crescent, read from the app's table), and a margin note naming the published observatory phases the table is checked against.
- `static/apps/inner-sign/formula.html` — The diagrams now print. Chrome drops colour emoji from PDF output, so the wheels printed empty, and on macOS the zodiac signs showed as purple emoji tiles. The zodiac signs now use the text-presentation selector (U+FE0E) with a symbol font list, so they render as ink-coloured symbols. The Chinese zodiac wheel uses the twelve earthly-branch characters (子 through 亥, Rat through Pig) instead of animal emoji. The Moon phases are drawn as SVG lit discs, both on the Proposition IV wheel and in the flow diagram.
- `static/apps/inner-sign/formula.html` — Print-only layout: Fig. I prints as a full-page plate (500 px wheel) instead of a small wheel above a half-blank page, and Fig. II's print type is slightly tighter so that Fig. II, Fig. III and the reading note fit on one page. The printout drops from 9 to 8 pages, and the screen layout is unchanged.
- `static/apps/inner-sign/formula.html` — The Fig. I wheel and Fig. III span bars now count days on the app's fixed nominal leap-year calendar 2000 (366 days, 29 February included) instead of a 365-day year, so their proportions match the app: Traditional Pisces is 31 days and Astronomical Aquarius 24, and each lens totals 366. Proposition I now says so, and states plainly that this is a counting rule rather than the length of the year: the Sun's cycle is about 365¼ days, and its actual crossing of a boundary can fall a day or more either side of the fixed date.
- `static/apps/inner-sign/formula.html` — Ophiuchus is now drawn by the page itself, as an ink-coloured SVG shape (a U crossed by the serpent's wave), in the Fig. I wheel and the Fig. III span bar. Its Unicode character (U+26CE) is an emoji by default, and iOS Safari showed it as a purple emoji tile even with the text-presentation selector. The other twelve signs already render as text and are unchanged.

## 2026-08-04 (2)

- `hugo.toml` — Set `markup.highlight.noClasses = false`. Hugo's default (`true`) bakes Chroma's syntax-highlighting colors into an inline `style="color:...;background-color:..."` on every fenced code block, which no stylesheet rule can override and which ignores the site's dark/light theme entirely. It happened to look correct in dark mode by coincidence (Chroma's fixed dark background is close to `--bg-card`) and was badly broken in light mode on the new `/craft/` page (dark box, near-black text — the owner caught this from a live screenshot after the previous deploy). With `noClasses = false`, Chroma emits a plain `class="chroma"` with no attached stylesheet, so code blocks fall through cleanly to `temple.css`'s theme-aware `.standalone-body pre`/`code` rules in both themes. Verified in the browser in both themes before redeploying.

## 2026-08-04

- `content/craft.md`, `themes/temple/layouts/craft/single.html` — Added an English-only `/craft/` page, "Building Moving Truth," adapted from a standalone writeup of the platform's architecture (Markdown-first authoring, the AI-assisted editorial pipeline, the 14-language localization system, and the Hugo/GitHub Actions/GitHub Pages deploy path). The layout widens the standard `.standalone-page` column, adds an eyebrow/byline/read-time header, a "by the numbers" stats table, a source-link footer, and page-scoped `TechArticle` JSON-LD (the site's first structured-data block) so the page is legible to both readers and retrieval/AI-answer systems. Not translated into the other 13 languages — it documents the platform itself rather than reader content, matching the existing English-only precedent set by `content/log.md`.
- `themes/temple/assets/css/temple.css` — Added general Markdown-element styling under `.standalone-body` (h2/h3, lists, blockquotes, inline/block code, tables) that previously had no rules, since About/Support only ever used paragraphs and bold text. Added a `.standalone-page--wide` modifier and the `.craft-*` classes for the new page's header/footer chrome. Purely additive — no existing selectors changed.
- `themes/temple/layouts/_default/baseof.html` — Added a "Technical Craft" entry to the hamburger menu's "More" section, between "About this site" and "From the Creator." Links by absolute path (`/craft/`) rather than `relLangURL`, since no translated page exists to link to in other locales — documented inline.
- `i18n/*.yaml` (all 14 locales) — Added `menu_craft` (the nav label, translated into all locales even though the destination page is English-only, consistent with translating all site chrome) and `craft_view_source` (the page's "View the source on GitHub" footer link).

## 2026-07-31

- `themes/temple/layouts/index.html` — Removed the deployment date and commit marker from the doorway image page so the landing experience remains visually clean. The marker remains available on interior pages.

## 2026-07-25

- `themes/temple/layouts/_default/baseof.html`, `themes/temple/layouts/index.html`, and `.github/workflows/deploy.yml` — Added a subtle footer stamp to every page, including the doorway homepage, showing the Eastern Time deployment date and the deployed commit's short SHA. The values are injected by the production workflow, so the marker identifies the code actually built and published.
- `content/log.md` and `themes/temple/layouts/log/single.html` — Added an unlisted, English-only `/log/` page that renders this canonical changelog directly. The page is excluded from search indexing and the sitemap so there is no second release record to maintain or public navigation entry to expose.
- `themes/temple/assets/css/temple.css`, reflection templates, and `i18n/*.yaml` — Removed the final unused email/Substack subscription styles and translation strings. No subscription form or notice remains in the active site templates. Consolidated obsolete duplicate reflection-overlay keys onto the canonical blessing/closing translations and completed localized countdown suffixes so production builds no longer emit translation warnings.

## 2026-07-24

- `hugo.toml`, `content/**/*.it.md`, `content/**/*.nl.md`, `content/**/*.hi.md`, `i18n/*.yaml`, and the remaining gallery translations — Expanded MovingTruth.com to the same 14-language set used by the app family, completed all public content and interface translations, preserved Arabic right-to-left rendering, and removed silent English interface fallbacks.
- `themes/temple/layouts/_default/baseof.html` — Changed both Apps navigation links to the canonical `apps.movingtruth.com` hub while preserving the visitor's selected language, including the `pt` → `pt-BR` and `zh` → `zh-Hans` mappings. Legacy local Apps routes now redirect to the hub or the corresponding individual app site.

## 2026-07-21

- `static/images/inner-sign-icon.png` — Replaced the Inner Sign app icon shown on MovingTruth.com with the new gold elemental-circle artwork, exported as a 1024×1024 PNG for consistent app and web use.

## 2026-07-18

Fixes from a full deployment review (storage/cookie state bugs, dead navigation code, memory leaks, minor security/accessibility hardening). Full findings in the review report.

- `themes/temple/assets/js/mt-storage.js` — Added `MT.getValue()/setValue()` (durable string values, e.g. theme/language) and `MT.getSessionValue()/setSessionValue()/removeSessionValue()` (true session-scoped storage: sessionStorage + a session cookie with no `expires`, cleared when the browser session actually ends) alongside the existing boolean `get()/set()/remove()`. Needed because the existing API only stored boolean flags, but theme and language need real values.
- `themes/temple/layouts/_default/baseof.html` — Swapped `mt-storage.js` to load before `mt-theme.js` (was the reverse). `mt-theme.js` reads `MT` at the top level, before `DOMContentLoaded`, to apply the stored theme before first paint — with the old order, `MT` didn't exist yet when that ran.
- `themes/temple/assets/js/mt-theme.js` — Replaced its own local `localStorage`/`sessionStorage` helpers with `MT.getValue/setValue/getSessionValue/setSessionValue/remove/removeSessionValue`, so theme choice gets `MT`'s cookie fallback instead of silently failing to persist when `localStorage` is blocked.
- `themes/temple/assets/js/mt-lang.js` — Replaced direct `localStorage.getItem/setItem('mt_lang', …)` calls with `MT.getValue/setValue`, for the same cookie-fallback reason. This was the most fragile of the stored prefs — it had no fallback at all.
- `themes/temple/assets/js/mt-notice.js` — The "before you begin" notice now uses `MT.getSessionValue/setSessionValue('mt_noticed', …)` instead of the durable `MT.get/set`, so it's genuinely per-session (was persisting via localStorage with no expiry plus a 365-day cookie, contradicting its own "shown once per session" behavior). Also rescoped the global "Reset progress" button (`doReset`) to only remove keys matching `_reflected_`, `_accepted_`, or `_closing`, instead of every `mt_`-prefixed key — it was silently deleting `mt_lang` and `mt_support_prompted` too, resetting a reader's language and re-arming the 3-piece support interrupt every time they reset their reading progress.
- `themes/temple/assets/js/series-progress.js` — Per-series "Reset progress" now also clears `mt_{slug}_accepted_{part}` keys (blessing acceptance), not just `_reflected_`/`_closing`. Previously a reset on the Blessings series left accepted-blessing state behind, so a reset piece still read "Accept this blessing again." Updated the file's header comment to document the `_accepted_` key.
- `themes/temple/assets/js/reflect.js` — Wired the blessing/closing overlay's "I receive this." / "I am free." button to actually navigate to the series page (`seriesPage`, from `data-series-page`) after the fade-out — this was documented behavior (see `single.html`'s template comments) that was never implemented; the overlay just dismissed in place. Added a `pageshow`/`event.persisted` listener that forces a reload on a bfcache restore, since a reflect countdown can't resume from one (`DOMContentLoaded` doesn't fire again). Added a `blessingRunning` guard so rapid re-clicks on the blessing button don't accumulate `pagehide`/click listeners, while still allowing a legitimate re-acceptance after a cycle completes.
- `themes/temple/assets/js/gallery.js` — Added a keyboard focus trap to the lightbox (Tab/Shift+Tab now cycle between its three buttons instead of escaping into the page behind it), matching the pattern already used for the hamburger menu.
- `themes/temple/layouts/series/single.html` — Added `rel="noopener"` to the Substack signup `<form target="_blank">`, which was missing it (every `<a target="_blank">` in the theme already had it).
- `.github/workflows/deploy.yml` — Pinned `hugo-version` to `0.163.1` (was `"latest"`), matching the locally installed version, so deploys are reproducible and don't silently pick up an unreviewed upstream Hugo release.

## 2026-07-13


## 2026-06-23

- `themes/temple/layouts/_default/list.html` — Back to Home on series listing pages (e.g. /blessings/, /moving-truth/) was still pointing to /. Changed to /series/. Missed in the previous navigation pass.

---

## 2026-06-22

- `themes/temple/layouts/_default/baseof.html` — Menu "Home" link changed from `/` to `/series/`. Added `.mt-menu-header` block at top of menu panel containing a brand link (logo + "MovingTruth.com") that navigates to the doorway page — the only remaining in-menu path to `/`. Close button moved inside the header row.
- `themes/temple/assets/css/temple.css` — Added `.mt-menu-header`, `.mt-menu-brand`, `.mt-menu-brand-logo` styles. Removed `align-self: flex-end` and `margin-bottom` from `.mt-menu-close` (now handled by the header wrapper).

---

## 2026-06-22

- `themes/temple/layouts/_default/single.html` — "Back to Home" now links to `/series/` (the main Series hub) instead of `.Parent.Permalink` (the specific series). `data-series-page` updated to match — reflect.js completion flow (closing, blessing, final piece) now also lands on `/series/`. The logo remains the only path back to the landing/doorway page. Updated comments to match.

---

## 2026-06-22

- `CHANGELOG.md` — Created. Backfilled from release log history.

---

## 2026-06-22

- `themes/temple/layouts/_default/single.html` — Renamed "Back to Main" button to "Back to Home". Changed link target from site root (`/`) to series index page (e.g. `/moving-truth/`) so readers return to the series they came from, not the landing page.

---

## 2026-06-17

- `themes/temple/layouts/_default/single.html` — Rewrote piece navigation to use `part` front matter instead of Hugo's default section sort order. Navigation now always flows 1→2→3→4 regardless of file date or filename.

---

## 2026-06-16

- **Site released** — GitHub repo created (`MovingTruth/MovingTruthLanding`), GitHub Pages enabled, custom domain `movingtruth.com` wired via Cloudflare DNS (DNS only, not proxied), HTTPS enforced via GitHub Pages managed cert.
- GitHub Actions deploy workflow added (`.github/workflows/deploy.yml`).

---

## 2026-06-15

- **Site built** — Hugo site created with custom Temple theme. Dark/light theme system, reflect/lock reader flow, series navigation. Two pieces written and added.

---
