# Higher Performance Group website: audit-002 revisions

This repo holds the revised Duda page snippets for higherperformancegroup.com, produced from **audit-002** (a full-site anti-slop and UI/UX audit, 2026-09-25) on top of that day's mobile fixes.

The site keeps its navy-and-gold look. The changes make it readable, keyboard-friendly, consistent across pages and free of AI-writing tells. Nothing is live until the files are pasted into Duda.

## See it
- **Preview (online):** https://andireyes06-maker.github.io/hpg-website-audit/preview/. Each revised page renders on its own, and each card has before/after screenshots and a link to today's live page. Offline, open [`preview/index.html`](preview/index.html).
- **What changed and why:** [`DECISIONS.md`](DECISIONS.md) (one line per decision), [`docs/audit-002-2026-09-25.md`](docs/audit-002-2026-09-25.md) (the full audit with evidence), and [`DESIGN.md`](DESIGN.md) (the house design system these changes follow).

## What changed, page by page

| File | Live page | Main changes (audit-002 finding #) |
|---|---|---|
| `home-duda-inject.html` | / | Em dashes (17), contrast (19), logo bar tab stops halved (22), form labels + autofill (28, 44), "Send My Request" (35), fonts (29), popup: focus trap, 44px close button, focus return (49), "Tap or hover" hint (47), dead code removed (42) |
| `bio-duda-inject.html` | /dr-joe-hill | Em dashes (17), contrast (19), "1,050 leadership teams" (26), fonts: Cormorant/Lora → house pair (29), ☕ → line icon (32) |
| `the-show.html` | /the-show | Em dashes (17), "1,050" wording (26), `rel="noopener"` on 23 new-tab links (40) |
| `the-proof.html` | /the-proof | Em dashes (17), contrast on 12 label styles (19) |
| `burnout-force-duda-inject.html` | /burnout-force | **Taken from the live site** (see note below); em dashes (17), contrast (19), dash list markers → gold rules |
| `tq-advantage-duda-inject.html` | /team-intelligence | Em dashes (17), contrast (19), ☕ → line icon (32), hero button fix from the mobile audit |
| `team-institute-duda-inject.html` | /team-institute | Em dashes (17), contrast (19), ☕ → line icon (32) |
| `tq-assessment-duda-inject.html` | /tq-assessment | Em dashes (17), contrast (19), fonts: Lora/Poppins → house pair (29) |
| `p2p-duda-inject.html` | /p2p-page | **Gold CTA band restored to navy text, 2.29 → 7.98:1** (18); em dashes (17); arrows off download/submit buttons (31); "Send My Topic" (35); autofill (44); ticker pauses on hover (27); fonts (29) |
| `speaker-page-duda-inject.html` | /speaker | Brought into the house style: fonts and palette mapped to house tokens (30); "1,050" wording (26) |
| `research-duda-inject.html` | /research | "Email Me the PDF" (35), "leverage" reworded (36), autofill (44), swipe-hint fade (46), download cards announce a dialog (41), fonts (29) |
| `blog-duda-inject.html` | /blog | Contrast (19), signup button "Subscribe" + autofill (35, 44), card thumbnails hidden from screen readers (52), "1,050" wording (26) |
| `bookstore-duda-inject.html` | /bookstore | Contrast (19), ✦ ornaments removed (32), swipe-hint fade on tabs (46), fonts (29) |
| `guest-preparation.html` | /guest-instructions | Em dashes (17), dash bullets → gold rules, contrast (19) |
| `header.html` | site header | **Dropdowns open by keyboard** (focusable triggers, `aria-expanded`, Escape) (21); emoji → line icons (32); "Book a Call" (35); fonts (29) |
| `qr-book-duda-inject.html` | (no live URL) | Em dashes (17), fonts (29) |
| `sample-report.html` | (no live URL) | Em dashes (17), fonts (29) |

**Every page** also gets the shared accessibility layer (#20, #27, #43, #45, #50, #51):
- a visible gold focus ring
- a press state on buttons
- anchor jumps that clear the mobile header
- a new-tab cue on external text links
- bigger tap areas on inline links
- a reduced-motion stop

It's the same short CSS block in each file, described in DESIGN.md.

Most pages also get two more changes:
- labels and small text raised to a 12px minimum (#34)
- elements that were falling back to Duda's theme font (Be Vietnam Pro) given the house font their own CSS intended (#29)

### Review fixes (2026-09-25)
These came from the client-preview review. They're applied identically in audit-002 and audit-003.
- **Burnout Force:** a "Take the Assessment" button (to `/tq-assessment`) next to "Talk It Through", in both the hero and the final call to action. It's outlined, so gold stays on the main button.
- **Speaker, on phones:** the hero photo is now its own band above the text. The name and buttons no longer sit on Dr. Joe's face.
- **One house form everywhere.** Every ActiveCampaign form now matches Home's form: a light card, white fields with visible borders, a gold full-width button and left-aligned labels. That covers the Research and Bookstore download popups, the Blog sign-up and P2P's topic form.
- **Blog:** the post list paints its own light background. Before, it relied on Duda's row colour, so the titles vanished anywhere else (including the preview).
- **P2P:** the "Next Session" tag no longer clips on the card edge, and Register and Download PDF are full 44px buttons.

### Note: Burnout Force
The local file named `burnout-force-duda-inject.html` in the original folder is actually an **older TQ Advantage page** (it has a TQ heading and a contact form). The real Burnout Force page was taken from the live site on 2026-09-25 and revised here. The mislabelled file is kept, unedited, in [`_not-live/`](_not-live/README.md).

## Needs the client
These were left exactly as they are live today; they need facts only HPG has.

1. **Broken or wrong links**
   - The #cancelaverage T-shirt store is closed (Bookstore).
   - Trust-bar logos for Cuyahoga CC, IOJU and SCSC point to domains that no longer resolve; GCC and Coconino time out.
   - The Chandler-Gilbert logo points to a student login page instead of cgcc.edu.
   - One trust-bar logo still links to `example.com`.
2. **Sources for these statistics:**
   - TQ Best-Fit split 43 / 9 / 30 / 11 / 7%
   - "94% of cohorts still running at 12 months"
   - "$400K burning annually" / "$1M investment"
   - The Show's 55% / 78% / 4×: which report?
   - QR Book's "significantly higher implementation success"
   - A link for each "Source: Gallup" line
3. **The Group** is decommissioned but `/thegroup` is still published. Unpublish or redirect it in Duda.
4. **Blog** (managed in Duda's blog tool):
   - drop the "Higher Performance Insights |" title prefix
   - give posts their own images
   - remove the duplicate "Your Leadership Team Needs More Drama"
5. **Duda editor check:** can you still resize the Bio, The Show and TQ Assessment widgets? Their height overrides date from the mobile audit.
6. **Trust-bar loop:** the marquee's two halves differ by two logos (Utica and USD 116 in one, Champaign and MDSD in the other), so the loop jumps once per cycle. Choose which four belong.

## Publishing to Duda
Each `*.html` file is one Duda HTML widget. To publish:
1. In Duda, open the page's HTML widget.
2. Replace its content with the whole file.
3. Put `header.html` into the site header's HTML widget.

Everything else on the page stays as it is. The originals are still in the parent `HPG Website/` folder if anything needs rolling back.

## How it was checked
Every revised page was rendered **inside the real live page**: the copy's widget and header were swapped into the Duda page, and its scripts were run. It was checked at desktop 1440, iPhone 15 Plus, 320px and a 768px tablet. Form submissions were blocked at the network layer throughout, so nothing reached HPG's Google Sheet or ActiveCampaign.

| Check | Result |
|---|---|
| Sideways scroll, all 14 pages × 4 sizes | **None** |
| Em dashes in rendered text | **0** (was 239 on these pages) |
| Stray spaces before punctuation | **0** |
| Text below WCAG AA contrast | **0** on real backgrounds (was 113 styles). A before/after colour diff found **no** text that passed before and fails now |
| Fonts in use | **Playfair Display + DM Sans only** (was 8 families, plus Duda's Be Vietnam Pro fallback) |
| Labels under 12px | Lifted to 12px (~190 styles) |
| Keyboard focus ring | Visible on every stop; header dropdowns open by keyboard and report `aria-expanded` |
| Home popup | Focus moves into it, Tab and Shift+Tab stay inside, Escape closes it, focus returns; close button 44×44 |
| Reduced motion | **0** looping animations with "reduce motion" on (was 5) |
| JavaScript errors | **0** |

Two caveats:
- The preview shell leaves out Duda's footer and phone header, so edges differ slightly from the live site.
- A few The Show thumbnails don't load when the preview is opened from disk. They load normally on the site.

