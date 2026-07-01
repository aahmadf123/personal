# Partner Blueprint

A privacy-first, scientifically grounded **romantic compatibility engine** that runs
entirely in your browser. No accounts, no servers, no tracking — your data never
leaves your device. It's a structured self-reflection and decision-support tool,
**not** a clinical or diagnostic instrument.

Live: served as a static GitHub Pages site (`index.html`). It also works when
opened directly from disk (`file://`).

## What it does

You build a **blueprint** of what you're actually looking for across six modules,
then test real candidates against it.

**Six assessment modules**
- **Values, Communication, Affection, Lifestyle** — reciprocal preference items
  (your answer · what you'd accept in a partner · how much it matters).
- **Shared Meaning & Finances** — rituals of connection, life goals, and the
  highest-signal money-compatibility questions.
- **Personality** — the Big Five via the validated **TIPI** (Ten-Item Personality
  Inventory, Gosling et al. 2003).
- **Attachment & Conflict** — attachment anxiety/avoidance via the **ECR-S**
  (Wei et al. 2007) and Gottman conflict style + the **Four Horsemen**.
- **Non-negotiables** — hard dealbreakers (childbearing, relocation, substances,
  religion).

**Three-tier matching engine**
1. **Non-compensatory gate** — a mismatch on a hard non-negotiable (or a candidate
   with high Contempt) *excludes* them from ranking; strong scores elsewhere cannot
   compensate.
2. **Reciprocal geometric match** — OkCupid-style. Each side's satisfaction is
   scored from importance-weighted preferences and combined with a **geometric mean**,
   which penalizes one-sided matches.
3. **TOPSIS ranking** — ranks surviving candidates across benefit criteria
   (reciprocal match, agreeableness, emotional stability, shared values, finances)
   and cost criteria (attachment anxiety/avoidance, conflict volatility).

**Visual decision-support**
- 8-axis **Joint Compass** (your ideal vs. a candidate).
- **Attachment Style Quadrant** (anxiety × avoidance, four quadrants).
- **Post-date check-ins** that log lived experience over time (Joel et al. 2020).

## Candidates & reciprocity

For a true mutual score, a candidate fills out **their own** questionnaire and
sends you the file:

1. Share the candidate link (`…/index.html#candidate`) — it opens a standalone
   questionnaire in the same page.
2. They complete it on their device and download `candidate-blueprint.json`.
3. You import it (**Add candidate → Import their questionnaire**).

Two fallbacks exist when that isn't possible: a **proxy** estimate (you answer on
their behalf, flagged lower-confidence) and a **quick** six-slider estimate.

## Privacy & data

- **Local only.** State is stored in the browser's **IndexedDB** and auto-saved.
- **Optional passphrase encryption.** Enable it under *Privacy & data* to encrypt
  your data at rest with the Web Crypto API (**PBKDF2-HMAC-SHA256, 600,000
  iterations → AES-GCM-256**).
- **No password reset.** If you lose the passphrase, encrypted data is
  unrecoverable — keep an exported backup.
- **Durable backup.** Browser storage can be evicted, so export a
  `partner-blueprint.json` (optionally encrypted) as your real backup.

Export format carries a `schemaVersion` (currently `2`); older `version: 1`
exports are migrated automatically on import.

## Tech

Single self-contained `index.html` — HTML5 + vanilla ES6 + inline CSS, **zero
dependencies, no build step**. SVG charts, IndexedDB, and Web Crypto are all
native browser APIs.

## Development

There is nothing to build. Edit `index.html` and open it, or serve locally:

```
python3 -m http.server 8099
# then open http://localhost:8099/index.html
```

A built-in assertion harness for the scoring math is available at
`index.html#selftest`.

> Educational / self-reflection use only. Not therapy, not a diagnosis, and not a
> substitute for professional advice.
