# Antarctica Truth Project — Website

A single-page, offline-capable research site that separates the **documented history**
of Antarctica in the 20th century from the **constructed mythology** built on top of it,
and celebrates the continent's genuine **deep-time** history (170+ million years before
the first humans).

The visual system is a **declassified intelligence dossier**: the conspiracy myth is
presented as the *classified fabrication* — redacted, stamped, suspect — while the
documented record is the *DECLASSIFIED truth*, rendered in cyan. Classification banners,
an ink-stamped cover sheet, registration marks, and monospace data furniture carry that
concept through every section.

Everything lives in one self-contained file: **`index.html`**. No build step, no external
image files, no JavaScript frameworks. Just open it in a browser.

```
antarctica-truth/
├── index.html   # the entire site (HTML + Tailwind config + CSS + vanilla JS)
└── README.md    # this file
```

---

## What's inside `index.html`

- **Tailwind CSS 3.4+** via the official Play CDN (`https://cdn.tailwindcss.com`) with a
  custom MILSPEC `tailwind.config` palette (dark-only, AA+ contrast):
  - Base surfaces: ink `#05080D` · panel `#0A0F16` · raised `#0E1521` · steel hairlines `#26323F`
  - Text: muted `#AEBAC6` · bright `#EAF2F8`
  - Primary "scan" accent (the DECLASSIFIED record side, active states, reticles,
    neutrino canvas): cyan `#22D3EE` with `#67E8F9` highlight
  - Warning accent (classification stamps, banners, ideological-context flags, caution
    striping): amber `#FFB000` with `#FFC94D` highlight
- **Google Fonts**: JetBrains Mono (technical monospace workhorse — labels, data,
  headers, case numbers) + Saira Condensed (condensed grotesque display headings) +
  Inter (readable sans for long body prose), with graceful system fallbacks offline.
- **Declassified-dossier design language**:
  - Fixed **classification banners** top *and* bottom of the page
    ("UNCLASSIFIED // FOR PUBLIC RELEASE" / case-file footer), as on real classified docs.
  - A rotated **TOP SECRET → DECLASSIFIED ink stamp** in the hero (CSS-only, with a
    gradient mask for ink breakup, strike-through bar, and authority/date line).
  - **Sharp corners only** — 1px steel hairlines, no rounded cards, no glassmorphism
    blur, no soft shadows; panels read as printed report sections.
  - **L-shaped registration/crop marks** (`.crop`) on panel corners that draw in on
    hover/focus; corner reticles + a 90°S latitude motif on the cover sheet.
  - Dossier **section headers**: mono kicker ("SECTION II // MYTH-vs-RECORD LEDGER"),
    condensed display title, ruled line, right-aligned metadata cluster (FIG./ANNEX/REF).
  - Subtle **graph-paper coordinate grid** behind everything and an optional low-opacity
    **scanline overlay** (hidden under `prefers-reduced-motion` and in print).
  - **Amber diagonal hazard striping** on ideological-context flags (Zündel/Serrano) —
    grave and clear, not flippant.
  - Rectangular mono **bracketed buttons** ("[ EXPLORE THE EVIDENCE ]") with crisp
    invert-on-hover; no emoji anywhere (inline SVG line icons + ASCII glyphs only).
- **All imagery is code** — CSS gradients, inline SVG, and two `<canvas>` visuals
  (hero ice-sheet/starfield, and an IceCube neutrino-path schematic). HTML comments mark
  every place a real photo/dataset should be swapped in, with credit notes.
- **Data-driven content**: the Myth-vs-Record ledger and the Genealogy timeline are
  rendered from three JS arrays — `MYTH_RECORDS` (**50 records**), `GENEALOGY`
  (**21 nodes**), and `PERSONS` (**15 subject dossiers**) — near the bottom of the file.
  **Edit those arrays to add or refine
  content; the UI regenerates automatically.** (v2 adds `caseId`/`origin` per myth record
  and `log`/`tag` per genealogy node for the case-file numbers and the chain-of-custody
  strip; v4 adds the Maria Orsic / Vril Society dossier; v5 adds the Goebbels / SS /
  "Wunderwaffe" dossier plus an optional per-record `flag`/`flagNote` field for
  documented-atrocity context; **v6 (batch 3)** adds the Pseudo-history / Flat-Earth /
  Modern-Viral dossier, a headline **Provenance / Citation Network** section, and a
  Deep-Time science enrichment; **v7 (batch 4)** adds the **Persons of Interest** dossier
  section (the `PERSONS` array), the **Source Tradecraft** field manual, and the
  Esoteric / Pop-culture / Real-secret records — see below.)

### Sections
1. Classification banners (fixed, top + bottom) + sticky nav + mobile menu + REV badge
2. Hero "cover sheet" (case-file header, DECLASSIFIED stamp, typewriter tagline)
3. SECTION I — Project brief / executive summary (mono count-up readouts)
4. SECTION II — Interactive **Myth vs Record** ledger (search, filter, sort, redaction
   reveal, case-file modal, chain-of-custody Source Trail)
5. SECTION III — **Genealogy of the Fabrication** routing-log timeline (1871 → today)
6. SECTION III-A — **Provenance / Citation Network** (`#provmap`, v6): data-derived SVG
   node-link diagram — 50 claims collapse onto 17 origins (text/table fallback on phones)
7. SECTION III-B — **Persons of Interest** (`#persons`, v7): 15 subject dossier cards for
   the origin-authors, with derived downstream counts and documented-only ethical flags
8. SECTION III-C — **Source Tradecraft** (`#tradecraft`, v7): the six-principle field
   manual for reading any claim (printable; for educators & journalists)
9. SECTION IV — **Verified Expedition Records** (Neuschwabenland, Ahnenerbe Tibet,
   Operation Highjump — as Exhibits A–C)
10. SECTION V — **Deep Time annex** (Gondwana, Eocene forests & dinosaurs, ice onset ~34 Ma,
    Gamburtsev Mountains, ~400 subglacial lakes incl. Lake Vostok, 91+ buried volcanoes,
    radar mapping)
11. SECTION VI — **Instrument Testimony** (Clean Air Sector, IceCube, ANITA, buried
    Neumayer stations)
12. SECTION VII — Open Research Leads & How to Help
13. SECTION VIII — Source Register (categorized bibliography)

### Extra features
- **Redaction reveal**: in the ledger, each fabricated claim sits under a solid black
  redaction bar (with a mono "// REDACTED — HOVER TO LIFT" hint) that lifts on row hover
  *and* keyboard focus. The real text stays in the DOM for screen readers; only the
  visual bar is `aria-hidden`, and print removes the bars entirely.
- **Chain-of-custody strip** in the case-file modal, e.g.
  `FIRST LOGGED: 1947 · ORIGIN: L. SZABO (PRESS) · ROUTED → BERNARD 1964 → ZÜNDEL 1970s
  → SERRANO 1978–84` — routing hops are derived from the `GENEALOGY` data.
- **Myth Detector** mini-tool: type/select a claim → instant first-appearance year + author,
  rendered as a trace printout.
- Side section-navigation ticks + thin scroll-progress rule under the top banner.
- **Download CSV** of the current claim ledger (now includes the case-file column).
- **Print one-pager** (`window.print()`) with a dedicated `@media print` stylesheet for the
  table and timeline (white bg, black text, banners/stamp/scanlines removed — a plain-text
  control line replaces them — no page-break inside rows).
- Micro-interactions, all reduced-motion-safe: one-time **typewriter** hero tagline with a
  blinking block cursor, mono **count-up** stat readouts, a one-time **scanline sweep** on
  card reveal, and registration corners that draw in on hover.
- Scroll-triggered reveals via `IntersectionObserver`.
- Full `prefers-reduced-motion` support (typewriter/count-up render their final state
  immediately; sweeps, blinking, and the scanline field are disabled; canvases show a
  single static frame).

### Mobile optimization (v2.1)
- **No horizontal overflow at any width** — `overflow-x: clip` guard on `html`/`body`,
  the rotated DECLASSIFIED stamp is scaled/constrained below `sm`, long mono strings
  (chain-of-custody line, case ids) wrap with `overflow-wrap: anywhere`, and the only
  intentionally-wide element (the ledger table on tablets) scrolls inside its own
  `overflow-x: auto` wrapper.
- **Card ledger on phones**: below `sm` the Myth-vs-Record table renders as stacked
  dossier index-cards built from the same `MYTH_RECORDS` data and the same
  search/filter/sort state (a dedicated mobile sort select drives the table's
  `sortState`). Each card is keyboard-focusable, opens the case-file modal via
  Enter/Space/tap, and carries an explicit `[ OPEN CASE FILE ]` button. Print and
  CSV always use the real table/data.
- **Touch redaction reveal**: every amber `[FABRICATION]` redaction bar is overlaid by a
  real `<button>` (>= 44x44px hit area) with `aria-pressed` and the label
  *"Lift redaction to reveal fabricated claim"* — tap or Enter/Space toggles the reveal
  without opening the modal; hover/focus reveal is unchanged on desktop, and the bar's
  printed hint switches to "TAP TO LIFT" on touch devices.
- **Responsive classification banners**: banner height is a CSS variable (28px desktop,
  22px on phones) that also drives the nav offset, `scroll-padding-top` /
  `scroll-margin-top`, body bottom padding, and modal clearance; banners pad into the
  notch/home-indicator safe areas (`viewport-fit=cover` + `env(safe-area-inset-*)`).
  On small screens the decorative bottom banner auto-hides while scrolling down
  (kept `fixed` to preserve the both-edges dossier motif) and returns on scroll-up.
- **Dynamic viewport hero**: the cover sheet uses `100dvh` with a `100vh` fallback, so
  mobile browser chrome neither crops nor jumps the hero.
- **44px touch targets everywhere**: bracketed buttons enforce `min-height: 44px`,
  mobile menu links / search / filter / sort / detector inputs / modal close /
  timeline disclosures all clear 44px, and control rows wrap instead of overflowing.
- **Mobile-friendly modal**: dvh-capped panel that scrolls internally between a sticky
  case header (large close button, never under a banner) and a sticky action footer
  (`[ SOURCE TRAIL ]`); background scroll is position-locked while open and the exact
  scroll offset is restored on close.
- **Mobile menu** opens above the fixed banners (z-index raised while expanded) and
  scrolls internally when taller than the viewport.
- **Battery-aware canvases**: both the hero and the IceCube neutrino canvas pause their
  `requestAnimationFrame` loops via `IntersectionObserver` when offscreen; the neutrino
  schematic now scales to its container width at the device pixel ratio (capped at 2)
  so it stays crisp on retina phones.

### GODMODE pass (v3) — mobile-native UX

- **Bottom command bar** (phones only, `< md`): a fixed thumb-zone "field-device control
  strip" with five ≥48 px targets — **BRIEF / LEDGER / GENEALOGY / DEEP TIME / MORE** —
  each a crisp inline-SVG line icon over a mono micro-label. The active section is lit
  cyan with `aria-current`, synced to scroll position by the same `IntersectionObserver`
  that drives the desktop side ticks. **MORE** opens a small sheet listing the remaining
  sections (Expeditions, Instruments, Open Leads, Sources) with `aria-expanded`; it
  closes on selection, Escape (focus returns to the button), outside tap, or scroll-hide.
  The bar **auto-hides on scroll-down and returns on scroll-up** like a native app.
  *Stacking decision:* the bottom classification banner keeps the true page edge
  (`bottom: 0`, as on a real dossier) and the command bar docks directly **on top of
  it**; both share the same auto-hide trigger so they move as one bottom-chrome unit and
  can never overlap each other, and `body` padding reserves room for **both**, so the
  footer is never covered. Safe-area insets are respected (the banner pads the home
  indicator, keeping the bar's targets clear of the iOS swipe zone). Hidden at `md+`
  and in print; fully keyboard operable.
- **PWA / add-to-home-screen polish**: `apple-mobile-web-app-capable`,
  `black-translucent` status bar, `mobile-web-app-capable`, a reticle/crosshair
  **app icon as an inline `data:` SVG** (favicon + `apple-touch-icon`), and a minimal
  **web-app manifest embedded as a `data:application/manifest+json` URI**
  (name *Antarctica Truth*, `display: standalone`, theme/background `#05080D`). The
  page remains one self-contained file — no external assets. (The manifest deliberately
  omits an icon array: iOS uses the `apple-touch-icon`, and nesting a double-encoded
  `data:` icon inside a `data:` manifest is brittle for no practical gain.)
- **Touch ergonomics**: `-webkit-tap-highlight-color: transparent` plus custom
  `:active` press feedback (bracketed buttons invert and scale 3 %, list rows tint
  cyan), momentum scrolling on every internal scroll container, and no hover-only
  affordances anywhere (the redaction toggle buttons already cover the ledger).
- **Collapsible dense annexes**: Deep Time (4 subsections), Instrument Testimony
  (4 logs), Open Leads, and all 4 Source Register columns use **native
  `<details>/<summary>`** styled as mono dossier tab headers with `[ + ] / [ − ]`
  chevrons. All are **authored `open`** (crawlers, no-JS readers, and print always see
  full content); JS collapses them once **on small screens only** and force-opens them
  at `md+`, where the tab summaries are hidden (or rendered inert for the source
  columns whose summaries contain the real headings) — **desktop layout is unchanged**.
  A `beforeprint` handler opens every disclosure and `afterprint` restores it. A
  capture-phase `toggle` listener pings `resize` so the IceCube canvas re-measures when
  its log is opened.
- **Performance**: the scroll handler is passive **and rAF-throttled** with batched
  reads/writes; canvases stay `IntersectionObserver`-gated with DPR capped at 2; the
  dev console note is deferred to `requestIdleCallback`.

### GODMODE pass (v3) — MILSPEC maximalism

- **Boot sequence** (first visit per session, `sessionStorage`-gated): a < 1.6 s
  teletype overlay — `ESTABLISHING SECURE LINK … / DECRYPTING CASE FILE AT-P/1938-47 …
  / CLEARANCE: PUBLIC // FOR RELEASE / ACCESS GRANTED` — with a visible **[ SKIP ]**
  button (Escape also skips). The real page is in the DOM underneath the whole time:
  the overlay ships `hidden` and a tiny pre-paint inline script unhides it **only**
  when JS is on, motion is allowed, and it hasn't run this session. On dismissal the
  node is **removed from the DOM** — nothing can trap focus or block scroll. Entirely
  skipped under `prefers-reduced-motion`. No audio.
- **Persistent HUD status readout**, integrated into the existing top classification
  banner (zero extra vertical space): live **SECTOR** name, `90°00′00″S`, `REV 02`,
  and a **PAGE n/N** scroll-progress counter, all driven by the shared section
  observer; the bottom banner's page number updates too. Compact on phones (coords/REV
  drop out, the sector ellipsizes; below 390 px the bottom banner drops its lead phrase
  so the case number + page always fit). Decorative telemetry is `aria-hidden`; the
  banner keeps its accessible classification label.
- **Portion marks**: subtle low-opacity mono `(U)` marks prefix every section kicker
  plus the mission statement and executive summary, as on real declassified releases.
- **Record-side ink stamps**: small cyan double-ruled stamps with the same
  imperfect-ink mask as the hero stamp — **VERIFIED** on each expedition exhibit,
  **CROSS-REFERENCED** and **PROVENANCE LOGGED** in the case-file modal. Exhibit stamps
  sit inside `overflow-hidden` banners; modal stamps are in normal flow — contained at
  every viewport width by construction.
- **Header furniture**: registration crop marks now **draw in once on reveal**
  (keyframe-based, so the hover-extend behavior is untouched), section header rules get
  faint mono `+` registration crosses at both ends, one very faint **radar sweep**
  turns behind the Instrument Testimony section (removed under reduced motion / print),
  and the footer closes with a **CSS barcode + coordinate machine-line** flourish.
- **Ethically flagged actors**: the Zündel and Serrano genealogy nodes now carry a
  stark **`CAUTION // ETHICALLY FLAGGED ACTOR`** panel — amber hazard-chevron strip,
  bold mono heading, and the documented context (neo-Nazi activism / Holocaust-denial
  function) always visible, no longer tucked inside the disclosure — plus a compact
  inline `CAUTION // FLAGGED` badge beside the title. The footer's ethical note gains
  the same chevron strip. Grave and clear, never flippant.

### Content expansion (v4) — the Maria Orsic / Vril Society dossier

Ten new myth records (**AT-M-009 … AT-M-018**, at the time bringing the ledger to **18 records**)
and three new genealogy nodes (at the time bringing the routing log to **10 entries**) cover the
"Vril Society" / Maria Orsic / Haunebu mythos — every claim presented strictly as a
**fabrication** with its documented invention trail (first-appearance year + author):

- **AT-M-009** — the "Vril Society" occult order: no archival trace; a 1960 literary
  construction (Pauwels & Bergier) built on Willy Ley's 1947 aside.
- **AT-M-010** — Maria Orsic as real medium/leader: no contemporaneous documentation;
  a biography assembled in 1990s German esoteric-neonazi publishing.
- **AT-M-011** — "vril" as suppressed free energy: a fictional force invented by
  Edward Bulwer-Lytton in an 1871 novel; treated as real by occultists from 1877.
- **AT-M-012** — Haunebu/Vril discs "engineered from channeled designs": no wartime
  engineering record; "specs" first appear in *Das Vril-Projekt* (1992).
- **AT-M-013** — the "Vril maiden" photographs: unprovenanced; no chain of custody
  before the 1990s.
- **AT-M-014** — the 1945 escape (to Aldebaran / the Antarctic base): a 1990s narrative
  motif welded onto the separately debunked "Base 211."
- **AT-M-015** — "Willy Ley 1947 proves an SS Vril program": a misreading — Ley's
  article catalogued pseudoscience and mentions no SS office, engineering, or saucers.
- **AT-M-016** — Thule Society + Vril Society as joint disc engineers: Thule (1918) was
  a real völkisch-occult political group, not an engineering body; the pairing is a
  1990s fusion.
- **AT-M-017** — "independent corroboration": Strube (2013) shows the whole modern
  corpus traces to one small 1990s author-circle copied forward.
- **AT-M-018** — the Vril saucers as the occult Reich's link to the Antarctic redoubt:
  two postwar fabrications spliced together (Zündel-era pamphlets supplied the fusion).

New genealogy nodes: **1871** Bulwer-Lytton (*The Coming Race* — the fictional origin
of "vril"), **1947** Willy Ley (*"Pseudoscience in Naziland"* — the misread seed), and
**1992–93** Jürgen-Ratthofer / Ettl (*Das Vril-Projekt*) and "Jan van Helsing" (Jan Udo
Holey, *Geheimgesellschaften*, 1993) — where the Orsic legend was manufactured. The
1992–93 node carries the same **`CAUTION // ETHICALLY FLAGGED ACTOR`** hazard treatment
as the Zündel/Serrano nodes: the modern Orsic/Vril mythology is embedded in documented
esoteric neo-Nazism, and van Helsing's 1993 book carries antisemitic conspiracy content
(seized in Germany). The new nodes are filed with inserted routing numbers (LOG-00,
LOG-02A, LOG-05A) so the seven original LOG-01…07 designations are untouched; the
rendered ENTRY nn/NN counters are computed from array position.

A new ledger category **`occult` (“Occult / Vril”)** is wired into the filter select and
`CATEGORY_LABEL`; the Myth Detector gained keyword routes for all ten records; the CSV
export, record counts, datalist, and chain-of-custody provenance strips all update
automatically from the arrays.

**New Source Register entries** — history & source criticism: Julian Strube, *Vril:
Eine okkulte Urkraft in Theosophie und esoterischem Neonazismus* (2013, the definitive
study); Eric Kurlander, *Hitler's Monsters* (2017); Jason Colavito (documentation of the
Orsic hoax). Myth-makers (primary texts): Bulwer-Lytton, *The Coming Race* (1871);
Willy Ley, "Pseudoscience in Naziland," *Astounding Science Fiction* (May 1947);
Pauwels & Bergier, *The Morning of the Magicians* (1960); Jürgen-Ratthofer/Ettl,
*Das Vril-Projekt* (1992) and "Jan van Helsing," *Geheimgesellschaften* (1993), with
their ideological context noted.

### Content expansion (v5) — the Goebbels / SS / "Wunderwaffe" dossier

Ten further myth records (**AT-M-019 … AT-M-028**, bringing the ledger to **28 records**)
and three further genealogy nodes (bringing the routing log to **13 entries**) center on
the **genuine German record** — Joseph Goebbels' propaganda ministry, the SS "special
projects" complex, and the wonder-weapon program — and the postwar mythology built on
top of it. The method is unchanged: every claim is presented strictly as a
**fabrication** with its documented invention trail, set against the real, sourced
record it distorts. Key factual anchor: **Goebbels was Reich Minister of Propaganda —
not SS, not military** — and his ministry's real 1944–45 "Wunderwaffe" morale campaign
(V-weapons and jets hyped as war-winning miracles) is precisely why postwar
"secret Nazi superweapon/saucer" myths found fertile ground.

- **AT-M-019** — "Goebbels' ministry confirmed miracle weapons *and saucers*": the
  1944–45 campaign is real and documented; it referenced V-weapons and jets, never
  saucers or Antarctica. The saucer gloss is postwar (in print via Lusar 1957).
- **AT-M-020** — "the Goebbels diaries reference the Antarctic Reich / saucers": the
  Fröhlich critical edition documents rocket/jet propaganda in detail and contains no
  such passages — a careful debunk-by-absence (the claim circulates with no page
  citation, because none exists).
- **AT-M-021** — "Die Glocke" (the SS anti-gravity Bell): no archival evidence;
  manufactured by Igor Witkowski (*Prawda o Wunderwaffe*, 2000) from documents he said
  he was shown but could not copy; popularized in English by Nick Cook (2001) and
  elaborated by Joseph P. Farrell. A post-2000 construction.
- **AT-M-022** — "Hans Kammler escaped with the saucer technology": Kammler is real
  (SS-Obergruppenführer over V-2 production and late-war special projects) and is
  documented as having vanished, presumed dead, in May 1945; the genuinely uncertain
  fate is what the escape myth colonizes (Karlsch/Döbert, *Kammlers Wunderland*, 2021).
- **AT-M-023** — "Project Riese was the Bell/saucer factory": Riese is a real,
  unfinished SS tunnel complex in the Owl Mountains (purpose — HQ and/or armaments —
  debated), dug by Gross-Rosen concentration-camp prisoners; the Bell attachment is
  post-2000 myth (cf. the debunked 2015 Wałbrzych "gold train").
- **AT-M-024** — "Viktor Schauberger built working Nazi saucers": a real inventor
  coerced into SS-supervised "implosion" work; no operational aircraft resulted; the
  saucer attribution is postwar fringe embellishment.
- **AT-M-025** — "foo fighters were secret Nazi saucers": the 1944–45 sightings are
  real and documented — by **both** sides, each suspecting the other; no matching
  German program exists in the captured records.
- **AT-M-026** — "the captured SS files prove the saucer program": the archives
  (Bundesarchiv; NARA captured-records microfilm) are real, open, and heavily used —
  they document rockets, jets, and the slave-labor system, and no saucer program.
- **AT-M-027** — "the wonder-weapons were near-complete war-winners": the V-weapons
  were real but strategically marginal (Neufeld 1995); the "miracle" frame **is**
  Goebbels' 1944–45 propaganda, extrapolated postwar — the myth's first author is on
  file, and it is the propaganda ministry itself.
- **AT-M-028** — "the secret-weapons program was a technological marvel" — **flagged**
  with the site's documented-atrocity treatment: the real V-2 program ran on
  concentration-camp slave labor at **Mittelwerk / Mittelbau-Dora**, where roughly
  **20,000 prisoners died** — more people died *building* the V-2 than were killed by
  it. The glamour myth erases a crime against humanity (Neufeld 1995; Mittelbau-Dora
  Memorial).

New genealogy nodes (filed with inserted routing numbers — **LOG-01A, LOG-02B,
LOG-06A** — so all prior LOG designations stay untouched): **1944–45** the real
Goebbels "Wunderwaffe" campaign (the documented propaganda that seeded the
"secret superweapon" template — carries the **`CAUTION // ETHICALLY FLAGGED ACTOR`**
hazard treatment: Goebbels was the regime's chief propagandist, and the campaign's
glamour concealed the Mittelbau-Dora slave-labor reality); **1957** Rudolph Lusar
(*German Secret Weapons of the Second World War* — the early print seed of the
Nazi-saucer literature, cited critically); **2000–01** Witkowski → Cook (where
"Die Glocke" was manufactured).

A new ledger category **`wunderwaffe` ("Wunderwaffe / SS")** is wired into the filter
select and `CATEGORY_LABEL`. A new **optional per-record field `flag`/`flagNote`** (used
on AT-M-028) renders a grave amber **`CAUTION // DOCUMENTED ATROCITY CONTEXT`** panel in
the case-file modal (reusing the flagged-actor furniture) plus a compact caution line in
the table row and mobile card. The Myth Detector gained keyword routes for all ten
records; the CSV export, record counts, datalist, and chain-of-custody provenance
strips all update automatically from the arrays.

**New Source Register entries** — history & source criticism / primary access:
Michael J. Neufeld, *The Rocket and the Reich* (1995); Elke Fröhlich (ed.),
*Die Tagebücher von Joseph Goebbels* (critical edition — documents the propaganda,
silent on saucers and Antarctica); Karlsch/Döbert, *Kammlers Wunderland* (2021);
Mittelbau-Dora Concentration Camp Memorial; Bundesarchiv (SS/Ahnenerbe/Speer-ministry
records) and the U.S. National Archives (captured-records microfilm). Myth-makers
(primary texts, cited critically as origin points, never as proof): Rudolph Lusar
(1957); Igor Witkowski, *Prawda o Wunderwaffe* (2000); Nick Cook, *The Hunt for Zero
Point* (2001).

### Content expansion (v6, batch 3) — Pseudo-history / Flat-Earth / Modern-Viral, the Provenance Network, and Deep-Time enrichment

Twelve further myth records (**AT-M-029 … AT-M-040**, bringing the ledger to **40
records**) and five further genealogy nodes (bringing the routing log to **18 entries**)
extend the method into three new lineages, each wired into the filter `<select>` and
`CATEGORY_LABEL` as new categories: **`pseudo-history` ("Pseudo-history")**,
**`flat-earth` ("Flat Earth")**, and **`viral` ("Modern / Viral")**. Every claim is
presented strictly as a **fabrication** dated to its author/origin — never as plausible.

- **AT-M-029** — "the 1513 Piri Reis map shows an ice-free Antarctica": a genuine Ottoman
  map; the reading is Hapgood (1966); cartography (McIntosh) reads the coast as distorted
  South America / speculative Terra Australis.
- **AT-M-030** — "Earth's crust suddenly shifted (pole shift)": Hapgood, *Earth's Shifting
  Crust* (1958); Einstein's foreword was **conditional interest, not endorsement**;
  glaciation ~34 Ma via plate tectonics + CO₂.
- **AT-M-031** — "ancient maps prove a lost advanced civilization mapped Antarctica":
  Hapgood (1966), recycled by von Däniken (1968); no archaeological evidence (Feder).
- **AT-M-032** — "Antarctica is Atlantis": Hancock, *Fingerprints of the Gods* (1995),
  reviving Hapgood; the ice predates humanity by tens of millions of years.
- **AT-M-033** — the flat-Earth "ice wall": post-2015 revival; refuted by
  circumnavigation and the austral midnight sun (24-hour daylight).
- **AT-M-034** — "the Antarctic Treaty blocks access to the secret": the 1959 treaty
  demilitarizes and guarantees free science + inspection; it bars weapons, not people.
- **AT-M-035** — "artificial pyramids": natural pyramidal peaks (nunataks/glacial horns),
  e.g. in the Ellsworth Mountains.
- **AT-M-036** — "VIP visits prove a secret pilgrimage": Kerry (climate science, Nov
  2016), Aldrin (medical evacuation, Dec 2016), Kirill (Bellingshausen base visit, Feb
  2016) — three documented, mundane trips.
- **AT-M-037** — the **fabricated Buzz Aldrin "tweet"** ("We are all in danger. It is evil
  itself"): a hoax/misattributed quote; Aldrin was medically evacuated (fluid in the lungs).
- **AT-M-038** — the Wilkes Land anomaly as "UFO/hidden city": a real ~2006 East-Antarctic
  gravity/mass anomaly (a mascon; a debated buried impact structure) — geophysics, not a craft.
- **AT-M-039** — "they reached Lake Vostok and went silent": drilling reached the lake in
  Feb 2012; debated microbial signals (with contamination concerns) were openly published.
- **AT-M-040** — the hoax "Inner Earth Byrd diary": not a genuine Byrd document; circulated
  from ~1990 via Beckley / Inner Light Publications (ties to the hollow-Earth record AT-M-003).

New genealogy nodes (filed with inserted routing numbers — **LOG-02C, LOG-03A, LOG-03B,
LOG-05B, LOG-06B** — so all prior LOG designations stay untouched): **1958** Hapgood
(crustal displacement — the pseudo-history engine); **1966** Hapgood (*Maps of the
Ancient Sea Kings*); **1968** von Däniken (*Chariots of the Gods?*); **1995** Hancock
(*Fingerprints of the Gods*); and the **2015–16 viral Antarctica wave** (flat-Earth ice
wall + the fabricated Aldrin quote flagged as misinformation).

**Headline feature — the Provenance / Citation Network (`#provmap`, "Section III-A").**
A new section renders a vanilla-JS/SVG node-link diagram, **data-derived** from
`MYTH_RECORDS` plus two small, auditable maps in the script (`PROV_ORIGINS`, `ORIGIN_OF`).
It proves the thesis visually: the **40 "independent" claims collapse onto 15 origin
authors** — the appearance of many independent sources is really one chain, copied
forward. Origin authors are the larger **amber** nodes (arranged by lineage: Nazi-survival
/ Hollow-Earth / Vril / Wunderwaffe / Pseudo-history / Flat-Earth / Modern-Viral); each
claim is a smaller **cyan** node wired to its author and labelled with its year. Layout is
**precomputed (no physics library)**. Hover/focus/tap an author to highlight all its
downstream claims (dimming the rest); hover a claim to trace its edge back; a live readout
names the author, count, and first year, and Enter on a claim opens its case file.
**Accessibility:** every node is a focusable `<g>` with an aria-label, and a full
**text/table fallback** (`#provFallback`) lists each origin author with its lineage, first
year, downstream count, and exact claim ids — screen-reader accessible at all sizes, the
primary view on phones, and printed in full. The SVG lives in its own `overflow-x:auto`
scroller (fixed 820-unit width) so it can **never widen the page**; highlighting is an
instant style change (reduced-motion-safe).

**Deep-Time enrichment (Part C).** Five scientifically accurate wonders added to the
annex (`FILE V-5`): Antarctic **meteorites / ALH84001** (the ANSMET blue-ice meteorite
trap and the 1996 Martian-microfossils debate, McKay et al.); **Blood Falls** (Taylor
Glacier — iron brine sealed ~1.5 Ma, lightless/oxygen-free microbes, Mikucki et al.);
**Lake Vostok** (sealed ~15 Ma — the real science, contra AT-M-039); the **EPICA Dome C**
ice core (~800,000-year CO₂ archive, 2004; *Beyond EPICA — Oldest Ice* toward ~1.5 Ma);
and the **2023** discovery of a river-carved landscape preserved beneath the East
Antarctic ice (Jamieson et al., 2023, *Nature Communications*).

**New Source Register entries** — Gregory McIntosh, *The Piri Reis Map of 1513* (2000);
Kenneth Feder, *Frauds, Myths, and Mysteries*; Hapgood (1958, 1966), von Däniken (1968),
Hancock (1995) as primary myth texts cited critically; McKay et al. (1996) with NASA/JPL
& ANSMET; Mikucki et al. (Blood Falls); EPICA Community Members (2004) & *Beyond EPICA*;
Jamieson et al. (2023); and the Antarctic Treaty (1959) primary text. The Myth Detector
gained keyword routes for all twelve records; the CSV export, "40 records on file" header,
datalist, section counters (HUD `PAGE n/N`, side ticks, command bar), and chain-of-custody
strips all update automatically from the enlarged arrays. Section navigation (desktop nav,
mobile menu, side ticks, HUD sector) gained a **Provenance** entry.

### Content expansion (v7, batch 4) — Persons of Interest, Source Tradecraft, and the Esoteric / Pop-culture / Real-secret records

Ten further myth records (**AT-M-041 … AT-M-050**, bringing the ledger to **50 records**),
three further genealogy nodes (bringing the routing log to **21 entries**), and **two new
sections** between the Provenance Map and the Expeditions annex. Debunking discipline
unchanged: every claim is a **fabrication** dated to its author/origin, never presented
as plausible; ethical flags appear **only where documented**.

**Headline feature — Persons of Interest (`#persons`, "Section III-B").** The companion
to the Provenance Map: **15 intelligence-style subject dossier cards**, rendered from a
new `PERSONS` data array, for the origin-authors behind the mythos — Szabó, Siegmeister
("Bernard"), Pauwels & Bergier, Ley, Zündel, Serrano, Hapgood, von Däniken, Hancock,
Jürgen-Ratthofer, Holey ("van Helsing"), Witkowski, Cook, Beckley, and Quayle & Marzulli.
Each card carries documented dates/nationality/role (kept minimal where a detail is not
reliably established — e.g. Szabó "fl. 1940s"), the subject's **specific contribution and
first year**, and a **downstream-claims count derived from the same record-id assignments
the Provenance Map uses** (`ORIGIN_OF`), so the two annexes reconcile by construction —
each case-file chip is a real button that opens the record's modal. Ethical discipline:

- **Full amber CAUTION hazard panels** (matching the flagged genealogy nodes) only for
  the documented cases — **Zündel** (neo-Nazi activist, convicted Holocaust denier),
  **Serrano** (open, lifelong neo-Nazi ideologue), and **Holey/"van Helsing"** (documented
  antisemitic conspiracy content; 1993 book seized in Germany).
- **Ratthofer** carries a sober *milieu* context line (documented esoteric-neonazi
  publishing milieu, per Strube 2013) — noted, not hazard-striped.
- **Willy Ley** is framed as a **MISREAD SOURCE**, explicitly *not* a myth-maker: a
  rocket scientist whose 1947 *debunking* article was later distorted into "proof."
- **Hapgood, von Däniken, Hancock, Witkowski, Cook, Beckley, Quayle, Marzulli** are
  described by their documented roles (pseudo-scholarship, amplification, fringe or
  religious-fringe publishing) and are **not** branded extremists.
- A visible **reconciliation note** explains why 15 cards ↔ 17 network origins (shared
  nodes, amplifiers without nodes, and non-person origins: a novel, a ministry, a film,
  two anonymous online waves).

**Source Tradecraft (`#tradecraft`, "Section III-C").** A printable six-principle field
manual — the site's method stated for reuse: (1) **date the first appearance**; (2)
**demand the primary source**; (3) **unravel citation laundering** (links to the
Provenance Map); (4) **treat archival silence as data** (Goebbels diaries / SS files);
(5) **follow the motive** (links to the flagged subjects); (6) **watch the
fiction→evidence loop**. Each principle carries a concrete worked example from the case
files.

**The ten new records**, in three new categories wired into the filter `<select>` and
`CATEGORY_LABEL` — **`esoteric` ("Esoteric / Religious")**, **`pop-culture`
("Pop-culture Feedback")**, and **`real-secret` ("Real Secret / Mundane")**, the last
being the credibility contrast: *yes, Antarctica had real secrets — declassified, they
are documented and boring*:

- **AT-M-041** — "Agartha lies beneath Antarctica": a 19th-century esoteric legend
  (Saint-Yves d'Alveydre 1886/1910; Ossendowski 1922), relocated under the ice by
  Serrano-era writing. Literature, not geography.
- **AT-M-042** — "Nephilim / fallen angels frozen under the ice": 2010s Christian-fringe
  publishing (Quayle, *Empire Beneath the Ice*, 2017; Marzulli), fused with the 2016–17
  viral wave. Religious-fringe genre, noted as such — no extremism flag.
- **AT-M-043** — "a reptilian / elite bunker": a 2010s viral graft of Icke's 1999
  "reptilian" thesis (Barkun cited on the genre); the bedrock is openly radar-mapped.
- **AT-M-044** — "a Nazi base on the Moon/Mars": 1990s Vril/"Aldebaran" fiction
  crystallized by the comedy *Iron Sky* (2012), whose clips recirculate as "evidence" —
  the fiction→evidence feedback loop.
- **AT-M-045** — "a secret wartime op proves the Nazi base": the REAL secret was
  Britain's **Operation Tabarin** (1943–45) — sovereignty, meteorology, mapping; the
  "secret Antarctic war" retellings are dismissed by Summerhayes & Beeching (2007).
- **AT-M-046** — "post-war secrecy hid the aliens": **Operation Deep Freeze** (1955–) was
  the U.S. Navy's *open* IGY logistics program that built McMurdo and Amundsen–Scott.
- **AT-M-047** — "secret polar nukes": the real obscure fact is the announced **PM-3A
  ("Nukey Poo")** reactor at McMurdo, 1962–72 — decommissioned and remediated; often
  conflated with Greenland's Camp Century / Project Iceworm (the other pole).
- **AT-M-048** — "the continent is off-limits, proving a cover-up": the 1959 Treaty +
  1991 **Madrid Protocol** regime is geopolitics + environmental protection (seven frozen
  claims, permits, inspections, legal tourism) — distinct from AT-M-034's flat-Earth variant.
- **AT-M-049** — "the 1946 **ghost rockets** were Nazi saucers": real Scandinavian
  sightings investigated by Sweden's defence staff (Soviet-test hypothesis unproven, most
  resolved to meteors); the Nazi-craft reading is Lusar-era retro-annexation — kept
  distinct from AT-M-025's 1944–45 foo fighters.
- **AT-M-050** — "Google Earth blur spots hide the base": mosaic/tile/low-sun imaging
  artifacts on maps that show every station openly (REMA/LIMA are downloadable at higher
  quality).

**New genealogy nodes** (filed with inserted routing numbers — **LOG-00A, LOG-06A1,
LOG-06C** — so all prior LOG designations stay untouched): **1886/1922** the Agartha
legend (Saint-Yves → Ossendowski); **2012** the *Iron Sky* fiction-as-evidence loop; and
the **2010s** Quayle/Marzulli Nephilim fusion (religious-fringe, noted as such).

**Provenance Network update.** +2 origin nodes (**Quayle/Marzulli**, **"Iron Sky"**) and
+2 lineage groups (**Esoteric/Religious**, **Pop-culture**): the diagram, its live
readout, and its text/table fallback now show **50 claims → 17 origins**, all derived
from the same arrays.

**New Source Register entries** — Saint-Yves d'Alveydre (1886/1910) and Ossendowski
(1922) as the Agartha legend's paper trail (cited critically); Icke (1999), Quayle (2017)
/ Marzulli (2010s), and *Iron Sky* (2012, filed as fiction) as origin points, never
proof; Barkun, *A Culture of Conspiracy*; Haddelsey (with Carroll), *Operation Tabarin*
(2014) + British Antarctic Survey official histories; the 1946 Swedish defence-staff
ghost-rocket investigation records; U.S. Navy / NSF Operation Deep Freeze and PM-3A
records; the Madrid Protocol (1991); and REMA / LIMA open polar imagery.

**Wiring.** The Myth Detector gained keyword routes for all ten records; the CSV export,
"50 records on file" header, `QUERY RETURNED n / 50` counter, datalist, and
chain-of-custody strips update automatically from the enlarged arrays. Section
navigation gained **Persons** and **Tradecraft** entries everywhere: desktop nav (xl+,
with a comment explaining the lg-width tradeoff), mobile menu, desktop side ticks, the
mobile **MORE** sheet, and the HUD (now `PAGE n/12`, with `PERSONS OF INTEREST` /
`TRADECRAFT` sectors). A pre-existing nav defect was also fixed: the `REV: JUL 2026`
badge clipped at 1024–1099px and is now shown only from 1100px up (`min-[1100px]`).

---

## Accessibility & performance already implemented

**Accessibility**
- Semantic landmarks (`<nav>`, `<main>`, `<header>`, `<footer>`, `<section>`, `<article>`).
- Skip-to-content link; visible `:focus-visible` rings throughout.
- ARIA: dialog semantics on the modal, `aria-sort` on sortable headers, `aria-expanded`
  on the mobile menu, `aria-live` on the result/count regions, labelled controls, and
  `aria-label`/`role="img"` on decorative and informative SVG/Canvas.
- Keyboard support: table rows AND mobile cards open with Enter/Space; modal closes with
  Escape / backdrop; focus is returned to the triggering element on close. Redaction bars
  lift on keyboard focus as well as hover, and the redacted text is never hidden from
  assistive tech.
- Touch accessibility: redaction bars are real toggle buttons (>= 44px hit area,
  `aria-pressed`, descriptive label) so the reveal works without hover; all interactive
  controls meet the 44x44px minimum touch-target size; opening a case file is a separate,
  explicit affordance from lifting a redaction.
- High-contrast (AA+) cyan/amber accents on near-black ink; dark-only by design;
  `prefers-reduced-motion` honored throughout (including the scanline overlay, the
  banner auto-hide transition, and both canvas animations).

**Performance**
- Zero runtime dependencies beyond the Tailwind CDN; no images to download.
- `IntersectionObserver` (not scroll handlers) for reveals; passive scroll listener for
  the progress bar and the mobile banner auto-hide; canvases cap `devicePixelRatio` at 2
  and reveal-once/unobserve.
- Both canvas animations pause automatically when scrolled offscreen
  (`IntersectionObserver`-gated `requestAnimationFrame`) — a meaningful battery saving
  on phones — and render a single static frame under `prefers-reduced-motion`.
- Content rendered from small in-memory arrays — instant filter/sort/search on both the
  desktop table and the mobile card ledger.

> **Production note:** the Tailwind Play CDN is intended for prototyping. For a real
> deployment, install Tailwind as a build dependency and ship a purged, minified stylesheet
> (see below) so you are not compiling CSS in the browser.

---

## Expanding into a proper Next.js or Astro project

The site is intentionally structured so the migration is mostly mechanical.

### Astro (recommended for a content-first research site)
1. `npm create astro@latest antarctica-truth` and choose a minimal template.
2. `npx astro add tailwind` — move the `tailwind.config` palette from `index.html` into
   `tailwind.config.mjs`.
3. Split the page into components under `src/components/`:
   `Nav.astro`, `Hero.astro`, `MythLedger.astro`, `Genealogy.astro`, `Expeditions.astro`,
   `DeepTime.astro`, `IceTestifies.astro`, `Sources.astro`, `Footer.astro`.
4. Move `MYTH_RECORDS` and `GENEALOGY` into `src/data/*.json` (or content collections with
   a Zod schema) and import them. Keep the small vanilla-JS interactions as island scripts
   or a tiny client component.
5. Static-generate; add an RSS feed for "dossier updates."

### Next.js (recommended if you want dynamic features/APIs)
1. `npx create-next-app@latest --ts --tailwind`.
2. Port the palette into `tailwind.config.ts`; drop the Play CDN `<script>`.
3. Recreate sections as React components; move the data arrays into `lib/data.ts` typed with
   TypeScript interfaces (`MythRecord`, `GenealogyNode`).
4. Reimplement the modal/table/timeline logic with React state + hooks (or keep them as
   framework-light components). Consider a small headless table lib only if the dataset grows.
5. Add API routes for a newsletter signup or a submissions endpoint (see next-features).

---

## Recommended real image / data sources (swap-in)

Each is marked in `index.html` with an HTML comment at the point of use. Always credit.

- **NASA** — Operation IceBridge aerial imagery, BedMachine Antarctica visualizations,
  Earth Observatory. (Credit: *NASA*; most NASA imagery is public domain.)
- **USGS** — Antarctic geology and mapping.
- **British Antarctic Survey (BAS)** — landscape photography, Bedmap datasets, fossil imagery.
  (Credit per BAS terms.)
- **Polar Geospatial Center (PGC)** — REMA (Reference Elevation Model of Antarctica).
- **IceCube / NSF** — detector diagrams and photos. (Credit: *IceCube Collaboration/NSF*.)
- **Unsplash** — freely licensed Antarctic photography (e.g., Derek Oyen, Cassie Matias) for
  hero/backgrounds when a specific scientific image isn't needed.
- **Paleogeographic reconstructions** — Ron Blakey / Colorado Plateau Geosystems or PALEOMAP
  for the Gondwana-breakup figure (check licensing/permission).

When swapping in raster images, keep them responsive (`max-width:100%`), provide descriptive
`alt` text, and serve modern formats (AVIF/WebP) with width-appropriate `srcset`.

---

## Suggested next features

- **Interactive map** with Leaflet (or MapLibre GL) showing expedition routes, station
  locations (Neumayer I/II, Amundsen–Scott, Vostok), and subglacial-lake positions.
- **PDF generation** of the claim ledger and a printable dossier (e.g., server-side with
  Puppeteer, or client-side with `pdf-lib` / the browser print pipeline already wired up).
- **Newsletter signup** for dossier revisions (Next.js API route + a provider like Buttondown).
- **Submissions workflow** so researchers can propose citation corrections (PR-based or a
  lightweight form → issue).
- **Full-text search** across sources (e.g., Pagefind for a static build).
- **Localization** (i18n) — the source-critical method travels well across languages.
- **Deep-time scrollytelling** — a scroll-driven paleogeography animation for the Gondwana
  breakup, and a bed-elevation cross-section slider.

---

## Content discipline

Every myth element in `MYTH_RECORDS` / `GENEALOGY` carries a **first-appearance year and
author**. This is the core method: claims are dated to their origin (Bulwer-Lytton 1871,
the Goebbels ministry's 1944–45 Wunderwaffe propaganda, Szabo 1947, Ley 1947 as misread
seed, Lusar 1957 as the Nazi-saucer print seed, Pauwels & Bergier 1960, Bernard 1964,
Zündel 1970s, Serrano 1978–84, Jürgen-Ratthofer/Ettl 1992 and "van Helsing" 1993,
Witkowski 2000 and Cook 2001 for "Die Glocke"), never presented as plausible. Where key
myth-makers (Zündel, Serrano, the 1990s Vril authors) are named, their documented
neo-Nazi milieu and the legend's historical function as soft-entry mythology for
Holocaust denial and antisemitic conspiracy are noted explicitly.

The Wunderwaffe records follow the same rule with two further disciplines. First,
**role accuracy**: Goebbels was Reich Minister of Propaganda — not SS, not military —
and his real 1944–45 morale campaign (documented in the Fröhlich critical edition of
the diaries, which are silent on saucers and Antarctica) is treated as the documented
template later myths exploit, never as evidence for them. Second, **atrocity clarity**:
the real "secret weapons" story is a crime against humanity — V-2 production ran on
concentration-camp slave labor at Mittelwerk / Mittelbau-Dora, where roughly 20,000
prisoners died — and the site names that record wherever the glamour myth would erase
it (Neufeld 1995; Mittelbau-Dora Memorial). Kammler's May 1945 disappearance is treated
as genuinely uncertain (Karlsch/Döbert 2021) without endorsing any escape narrative;
"Die Glocke" is dated to its manufacture (Witkowski 2000 → Cook 2001 → Farrell).

The Orsic/Vril records follow the same rule: "vril" is fiction (Bulwer-Lytton 1871);
no contemporaneous archival evidence exists for a saucer-building Vril-Gesellschaft or
for Maria Orsic as portrayed; the detailed legend is a 1990s construction (Strube 2013
is the controlling scholarly reference, with Goodrick-Clarke 2002, Kurlander 2017, and
Colavito's hoax documentation).

Deep-time content uses established scientific consensus only. When updating figures, cite the
dataset/paper (BedMachine, Bedmap, REMA, IceBridge, van Wyk de Vries et al. 2017, etc.).

Content is consistent with the *Antarctica Truth Research Dossier — Second Edition, July 2026*.

---

## License / attribution

Site code is original for this project. Replace placeholder art with properly credited media
before public deployment. Verify all bibliographic editions and page references against the
original documents.
