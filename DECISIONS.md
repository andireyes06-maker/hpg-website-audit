# audit-002 decisions (2026-09-25)

These are the choices made on each audit-002 finding (`../anti-slop/audit-002-2026-09-25.md`). Every change in this folder follows from them. The originals in `HPG Website/` are untouched.

## Approved and applied here

| # | Finding | Decision |
|---|---|---|
| 17 | Em dashes | All 218 rewrites applied as drafted in Appendix A, including the 13 inside testimonial quotes |
| 18 | P2P gold band white text | Restore the intended navy text on gold |
| 19 | Low contrast | Faint labels on navy → `#a7b6c8`; gold text on white → `#8c6b23`; gold text on cream → `#7a5c1c` |
| 20 | Form fields with no focus ring | Shared gold `:focus-visible` ring |
| 21 | Header dropdown | Keyboard-openable (`:focus-within`); hidden panels removed from the tab order |
| 22 | Home logo bar | The repeated logo set is hidden from keyboard and screen readers |
| 27 | Reduced motion | Marquees, tickers and pulses stop under `prefers-reduced-motion` |
| 28 | Form labels | Real accessible labels on the Home and Burnout Force form fields |
| 29 | Fonts | **Playfair Display + DM Sans on every page** |
| 30 | Speaker page | Brought into the house style: house fonts, navy/gold tags; the layout and cream sections stay |
| 31 | Arrows | Kept only on links that go to another page or site; removed from submits, downloads and modal buttons |
| 32 | Emoji icons | Replaced with thin-line gold SVG icons |
| 33 | Offering pages share one template | **Kept.** The Proof, Burnout Force, TQ Advantage and Team Institute are a deliberate series template; this is recorded in DESIGN.md, with no layout change |
| 35 | Generic buttons | Header "Book a Call"; Home and Burnout Force forms "Send My Request"; Research modals "Email Me the PDF"; P2P "Send My Topic"; Blog "Subscribe" |
| 36 | Buzzword | "leverage" reworded on Research |
| 37 | Amazon-orange buttons | **Kept**, on Amazon links only; the reason is documented |
| 26 | Research base wording | "**1,050 leadership teams**" on every page; "987 leadership analyses" stays only as its own separate stat |
| 39 | "stupifany" | **Kept**: Dr. Joe's own coinage |
| 40–47, 49–53 | Hygiene and small UX touches | All applied |

## Needs the client

These stay exactly as they are on the live site and are listed in the README.

| # | What's needed |
|---|---|
| 23 | Correct URLs, or say to remove the entry: Bookstore #cancelaverage T-shirt store (closed); trust-bar logos for Cuyahoga CC, IOJU and SCSC (the domains don't resolve), GCC and Coconino (time out), Chandler-Gilbert (points at a student login page); the example.com placeholder logo |
| 24 | Unpublish or redirect `/thegroup` in Duda (decommissioned, but still live) |
| 25 | Sources for: TQ Best-Fit split 43/9/30/11/7%; "94% of cohorts"; "$400K / $1M"; The Show 55% / 78% / 4× (which report); QR Book "significantly higher implementation success" |
| 38 | Blog, which is managed in Duda's blog tool: drop the "Higher Performance Insights \|" title prefix, give posts their own images, remove the duplicate "Needs More Drama" post |
| - | Duda editor check: can you still resize the Bio, The Show and TQ Assessment widgets? (The height overrides there date from the mobile audit.) |

## Out of scope
- The Group (`thegroup-duda-inject.html`): decommissioned, so it isn't copied here.
- Test copies (`*-antislop-test.html`, `header-whitespace-test.html`) and `Miscellaneous/`.

## Corrections found while applying the fixes
- **Burnout Force: the wrong file was audited.** `HPG Website/burnout-force-duda-inject.html` is an older **TQ Advantage** page (TQ heading, contact form), not the live Burnout Force page. The real page was taken from the live site and revised here; the mislabelled file is in `_not-live/`, unedited. So audit-002's Burnout Force "form" items (#28, #35, #44 there) don't apply: the live Burnout Force page has no form.
- **#52 Blog cards:** each card is already a single link, so the audit's "several links per card" was wrong. The real problem was the decorative "Higher Performance Insights / TEAM INSIGHTS" thumbnail text opening every card's accessible name. The thumbnails are now hidden from screen readers.
- **#53 Source links:** Home's "Source: State of Campus Culture" already links to its report. The "Source: Gallup" lines have no URL to link to, so they moved to *Needs the client*.
- **Trust-bar loop (new, for the client):** the marquee's two halves differ by two logos (Utica and USD 116 in the first; Champaign and MDSD in the second), so the loop jumps once per cycle.
- **Contrast rules** are scoped so they don't override sibling variants. Home's gold "With Team Intelligence" cell keeps its gold. A before/after colour diff confirmed that no text which passed before fails now.
