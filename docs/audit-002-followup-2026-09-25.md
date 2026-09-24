# audit-002 follow-up: fixes applied and verified (2026-09-25)

Fixes applied in `HPG Website/audit-002-pages/`. The originals in `HPG Website/` are unchanged: none of them has been modified since 02:48, before this work started. The per-finding decisions are in `audit-002-pages/DECISIONS.md`.

## How the fixes were checked
- **The real page, not a mock-up.** Every revised page was swapped into the live Duda page (widget plus site header, scripts re-run) and tested at desktop 1440, iPhone 15 Plus, 320px and a 768px tablet.
- **Contrast** was measured on the rendered background of every text element, before and after.
- **Keyboard:** a tab-walk of the first 14 stops on every page.
- **Home popup:** focus-trap test.
- **Reduced motion:** emulated.
- **Forms:** POST requests were blocked the whole time, so no data left the browser.

## Before and after, by finding

| # | Finding | Before | After | Status |
|---|---|---|---|---|
| 17 | Em dashes | 239 in visible text | 0. Rewritten per Appendix A (and 20 drafted the same way on the live Burnout Force page); list-marker dashes → gold rules | Fixed |
| 18 | P2P gold band | White on gold, 2.29:1 | Navy on gold, 7.98:1; the dark "Register" button stays white on navy | Fixed |
| 19 | Low contrast | 113 styles below AA | 0. A colour diff confirmed no passing text now fails | Fixed |
| 20 | Form fields without focus | P2P: no ring | Gold ring on every focusable element on all pages | Fixed |
| 21 | Header dropdowns | 8 invisible tab stops; mouse-only | Triggers focusable; menus open on focus, report `aria-expanded`, close on Escape; hidden links leave the tab order | Fixed |
| 22 | Home logo bar | 94 tab stops | 47. The repeated set is hidden from keyboard and screen readers | Fixed |
| 24 | /thegroup still published | Live (200) | Unchanged: Duda / client | Client |
| 23, 25, 26 (sources) | Dead links, unsourced stats | See README "Needs the client" | Unchanged, flagged | Client |
| 26 | Research-base wording | 6 variants | "1,050 leadership teams" on Bio, Blog, Speaker and The Show | Fixed |
| 27 | Motion under reduce-motion | 5 looping animations | 0; P2P ticker also pauses on hover | Fixed |
| 28 | Unlabelled fields | Home: placeholder-only | Accessible labels on every Home form field | Fixed (the "Burnout Force form" was the mislabelled file, see below) |
| 29 | Fonts | 8 families; Be Vietnam Pro fallback | Playfair Display + DM Sans only, confirmed on every page | Fixed |
| 30 | Speaker brand | Its own palette and fonts | House tokens and fonts; layout unchanged | Fixed |
| 31 | Arrows | On submits and downloads | Only on links that go somewhere | Fixed |
| 32 | Emoji icons | 8 header emoji, 4 ☕, 4 ✦ | Gold line icons; ✦ removed | Fixed |
| 33 | Offering template | n/a | Kept as a series template; documented in DESIGN.md | Documented |
| 34 | Small labels | 7.5–11.5px | 12px minimum (~190 styles); mock book-cover text excluded | Fixed |
| 35 | Generic buttons | "Get Started", "Submit" | "Book a Call", "Send My Request", "Email Me the PDF", "Send My Topic", "Subscribe" | Fixed |
| 36 | Buzzword | "leverage" | "use" | Fixed |
| 37 | Amazon orange | n/a | Kept on Amazon links only; documented | Documented |
| 39 | "stupifany" | n/a | Kept (Dr. Joe's coinage) | Kept |
| 40 | `rel="noopener"` | 29 missing | Added | Fixed |
| 41 | `href="#"` triggers | Unannounced | `aria-haspopup="dialog"` on the Research and Bookstore download cards | Fixed |
| 42 | Dead placeholder check | Present | Removed | Fixed |
| 43 | Press state | None | 1px press-down on all buttons | Fixed |
| 44 | Autofill | None | `autocomplete` / `inputmode` on the Home, P2P, Research and Blog forms | Fixed |
| 45 | Anchor offset | None | `scroll-margin-top: 80px` | Fixed |
| 46 | Swipe cue | None | Right-edge fade on the Research strips and Bookstore tabs | Fixed |
| 47 | "Hover down" hint | Mouse wording | "Tap or hover a path to see how it works" | Fixed |
| 48 | The Group form | n/a | Removed (decommissioned) | n/a |
| 49 | Popup focus | Tab escaped; 30px close | Focus in, trapped, returned; 44×44 close | Fixed |
| 50 | Tap areas | 14–22px inline links | Enlarged hit area | Fixed |
| 51 | New-tab cue | None | ↗ plus screen-reader text on external text links | Fixed |
| 52 | Blog cards | Thumbnail text read first | Thumbnails hidden from screen readers (the audit's diagnosis was corrected) | Fixed |
| 53 | Source links | n/a | Home already linked; the Gallup lines need URLs from the client | Client |

## Corrections to audit-002
1. **Burnout Force, wrong file.** `burnout-force-duda-inject.html` in `HPG Website/` is an older TQ Advantage page. The real Burnout Force page was taken from the live site and revised. Audit-002's Burnout Force references to a form (#28, #35, #44) and to ☕ don't apply to the live page.
2. **#52.** Each Blog card was already one link; the real issue was its decorative thumbnail text.
3. **New for the client:** the Home trust-bar marquee halves differ by two logos, so the loop jumps once per cycle.

## Delivery Gate: the touched items (Block 1, Hard Gate)

| Rule | Result | Evidence |
|---|---|---|
| R-02 em dashes | PASS | 0 in the rendered text of all 14 pages (desktop and iPhone) |
| R-03 mobile | PASS | 0px sideways scroll on 14 pages × 4 sizes |
| R-17 unsourced numbers | **OPEN, client** | Listed in the README: 94%, $400K / $1M, the TQ split, The Show's stats, QR Book |
| R-24 / R-26 dead links | **OPEN, client** | T-shirt store; 5 trust-bar domains; example.com logo |
| R-25 contrast | PASS | 0 failures on real backgrounds; 0 regressions |
| R-26 interactive | PASS | Download modals, dropdowns, popup, forms (validation only) all work; 0 JS errors |
| R-32 keyboard | PASS | Ring on every stop; dropdowns keyboard-operable; popup trap and Escape |
| R-38 real content | **OPEN, client** | `/thegroup` still published |

The pages built here pass every hard-gate rule they can control. What's still open needs facts or a Duda action from the client, and is listed in `audit-002-pages/README.md` under "Needs the client".
