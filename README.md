# Partner Blueprint

A privacy-first, science-informed tool that builds a portrait of **your ideal
partner** from your own answers — who they are and what they're like. It runs
entirely in your browser: no accounts, no servers, no tracking. It's a
structured self-reflection and decision-support tool, **not** a clinical or
diagnostic instrument.

Live: served as a static GitHub Pages site (`index.html`). It also works when
opened directly from disk (`file://`).

## What it does

You answer a few short modules about **yourself and what you're looking for**,
and get a portrait of the ideal partner for you. Nobody else has to participate.

**You answer a few modules — only about yourself**
- **Values, Communication, Affection, Lifestyle, Shared Meaning, Finances** —
  just where *you* stand on each. The app derives your ideal partner from these
  (someone aligned with you), so there's nothing to specify "about them."
- **Personality** — the Big Five via the validated **TIPI** (Gosling et al. 2003).
- **Attachment & conflict** — attachment anxiety/avoidance via the **ECR-S**
  (Wei et al. 2007) and your Gottman conflict style + the **Four Horsemen**.
- **Non-negotiables** — hard dealbreakers (childbearing, relocation, substances,
  religion).

**You get your ideal partner**
- An **archetype** (e.g. "The Secure Anchor") and a written portrait.
- Their **values and lifestyle**, taken from what you said you're looking for.
- Their **personality and attachment style, auto-derived from relationship
  science** using *your own* results — e.g. if you lean anxious, it recommends a
  secure partner and explains why. (This describes who they are, not how they
  look.)
- An **8-axis compass** and an **attachment quadrant**.

## Size up someone real (optional)

Considering a specific person? Add them and answer a few questions with **your
best read on them** — they never have to participate. You'll see:

- a **Fit to your ideal** score (how well your read on them matches what you're
  looking for, weighted by what matters most to you),
- an **attachment pairing** read (their style vs. yours), and
- the same hard **dealbreaker gate** — a conflict on a non-negotiable excludes
  them outright, no matter how well everything else fits.

You can also log **post-date check-ins** over time, since lived experience is the
strongest signal (Joel et al. 2020).

## Privacy & data

- **Local only.** State is stored in the browser's **IndexedDB** and auto-saved.
- **Optional passphrase encryption.** Enable it under *Privacy & data* to encrypt
  your data at rest with the Web Crypto API (**PBKDF2-HMAC-SHA256, 600,000
  iterations → AES-GCM-256**).
- **No password reset.** If you lose the passphrase, encrypted data is
  unrecoverable — keep an exported backup.
- **Durable backup.** Browser storage can be evicted, so export a
  `partner-blueprint.json` (optionally encrypted) as your real backup.

You can change who you're looking for (woman / man / partner) any time in
settings — it only tailors the wording. Export format carries a `schemaVersion`;
older `version: 1` exports are migrated automatically on import.

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
