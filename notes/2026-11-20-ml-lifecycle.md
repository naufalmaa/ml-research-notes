# The ML lifecycle we use, 2026-11-20

**Source:** [CRISP-DM 1.0 guide](https://s2.smu.edu/tfomby/eco5385_eco6380/data/SPSS/CRISPWP-0800%20Data%20Mining%20Standards.pdf) · [Rules of ML](https://developers.google.com/machine-learning/guides/rules-of-ml) · Huyen, *Designing ML Systems*, ch. 1–2
**Project / stage it serves:** all projects · all stages

## In one sentence
A model is only as trustworthy as its split and its baseline, and only as useful as the way its results are communicated, so these get their own stages.

## Key points
1. 8 stages: framing → data → EDA & quality contract → **split & leakage** → **baseline** → features & model → evaluation & error analysis → **communication** → deployment & monitoring.
2. Split comes *before* features: otherwise features silently peek at the future (leakage).
3. The baseline is the status quo. A model that cannot beat it is a finding, not a failure (Rules of ML #1–3).
4. Error analysis sends you back to earlier stages. The lifecycle is a loop; record each loop as an ADR.
5. Two habits across all stages: reproducibility (one command, seeded, versioned data) and iteration.

## How I will use it
Every repo is generated from `ml-project-template`, which has one artefact per stage.

## New terms → glossary
- baseline, data leakage, ADR (added ✅)
