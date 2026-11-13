# drug-discovery-ai

Working through molecular machine learning from the ground up — SMILES and
fingerprints, then graph neural networks, then property prediction with honest
evaluation.

Part of a four-month skills plan (Nov 2026 – Mar 2027). The question running
through it: **when does a computational result fail to mean what it appears to
mean?**

## Setup

Python 3.10, RDKit 2026.9.1.

## Week 01 — SMILES, fingerprints and similarity

**Done so far**

- Loaded 7 drugs as SMILES from PubChem and parsed them with RDKit
- Drew them as a labelled grid, saved to `outputs/molecules.png`

**Molecules used:** [list your seven here]

**Still to do**

- Morgan fingerprints and a Tanimoto similarity heatmap
- logP vs molecular weight scatter
- Radius 2/3/4 comparison

## Gotchas

Things that cost me time, recorded so they don't cost it twice.

- **`Draw.MolsToGridImage` doesn't return a PIL image in a notebook.** It
  returns an IPython display object, which has no `.save()`. The PNG bytes are
  in `.data`, so write them directly with `path.write_bytes(img.data)`. Passing
  `returnPNG=False` gives a real PIL image instead if you need one. With
  `useSVG=True`, `.data` is SVG *text*, so it's `write_text` into a `.svg`.

- **`Chem.MolFromSmiles` returns `None` on a bad SMILES rather than raising.**
  A typo fails silently and only surfaces later as a confusing crash, so check
  for `None` right after parsing.

## What I learned

- Having the smiles it's easy to code to view the structiure but that does not answer how the structure is formed. Still something I am learning
