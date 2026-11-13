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

**Done**

- Loaded 7 drugs as SMILES from PubChem and parsed them with RDKit
- Drew them as a labelled grid → `outputs/molecules.png`
- Generated Morgan fingerprints (radius 2, 2048 bits) using `rdFingerprintGenerator`
- Computed Tanimoto similarity: one molecule against the rest, then all-vs-all
- Built a 7×7 similarity matrix and plotted it → `outputs/similarity_heatmap.png`

**Molecules used:** Omeprazole, Aspirin, Diazepam, Ibuprofen, Amoxicillin, Acetaminophen(paracetamol), Levothyroxine

**Results**

- Most similar pair: [names] at [score]
- Least similar pair: [names] at [score]
- [anything that surprised you, or "nothing stood out yet"]

**Open question**

Whether the fingerprint clustering matches real drug-family groupings — I don't
yet know enough medicinal chemistry to judge this. Returning to it once I know
more about what these drugs actually do and how they're classified.

**Still to do**

- logP vs molecular weight scatter
- Fingerprint radius 2/3/4 comparison
- Revisit the clustering question above

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

  - **`AllChem.GetMorganFingerprintAsBitVect` is deprecated.** Most tutorials
  online still use it. Current API is `rdFingerprintGenerator.GetMorganGenerator
  (radius=2, fpSize=2048)` then `gen.GetFingerprint(mol)`.


