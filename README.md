# nucleus-platemap-corpus

Test fixtures for the `build-platemap` and `extract-conditions` skills in
[nucleus-eng/nucleus-skills](https://github.com/nucleus-eng/nucleus-skills).

## What is this

A regression corpus. Every file here earned its place by catching a specific
failure — either in real bench data or as a synthetic adversarial case.
`manifest.yaml` records what each file exercises and why it was added.

## Layout

```
manifest.yaml          index of all fixtures and their expected findings
fixtures/
  synthetic/           generated files — mutate a clean platemap to trigger
                       one blocking rule each; no disclosure issue
  platereader/         real platereader bench sheets (once cleared)
  microscope/          real microscopy bench sheets (once cleared)
```

## Adding a fixture

1. Add an entry to `manifest.yaml` first — record origin, owner, and
   exactly which finding the file exercises. This is the part that decays
   fastest.
2. Set `tier` honestly:
   - `derived` — correct by construction (synthetic cases); always gates CI
   - `confirmed` — you have verified the expected output against the real
     data by hand; gates CI
   - `asserted` — one agent's output, not yet independently checked; never
     gates CI
3. Add the file to `fixtures/` and update `path` in the manifest.
4. Do not add files because they look representative. Each case should have
   a row in the errors-found log in `PLATEMAP-STAGING.md` or a new finding
   that justifies it.

## Disclosure

Real bench data goes in `fixtures/platereader/` or `fixtures/microscope/`
only after the data owner has confirmed it can be public. Until then the
manifest entry exists with `disclosure: pending` and `path: pending` —
recording the intent without moving the data.
