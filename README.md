# IBM Article Recommendation Study

A notebook-based study of implicit user-article interactions for IBM Watson Studio, exploring popularity, user-user collaborative filtering, content similarity, and matrix factorization. This is an educational analysis, not a deployed service.

## Repository guide

- [Recommendations_with_IBM.ipynb](Recommendations_with_IBM.ipynb): analysis and recommendation functions.
- `data/user-item-interactions.csv` relative to the notebook working directory: interaction data.
- `project_tests.py` and `top_*.p`, where supplied: course helpers and expected answers, not disposable temporary models.

A closely related version exists in `Recommendation-system-IBM`. Compare changes before keeping one public portfolio entry. The checkpoint notebook differs from the main notebook and is retained.

## Setup

```bash
git clone https://github.com/iimaha-AI/recommendation-system.git
cd recommendation-system
python -m venv .venv
```

Activate with `source .venv/bin/activate` on macOS/Linux or `.venv\Scripts\Activate.ps1` in PowerShell, then:

```bash
python -m pip install -r requirements.txt
python -m notebook Recommendations_with_IBM.ipynb
```

The dependency list is a starting environment, not a validated lockfile. Known execution limits are listed below.


## Approach

Inspect missing users and popularity, map user IDs, build a binary user-item matrix, compare similar users, and explore content/latent-factor similarities. Functions depend on notebook state and are not yet an importable application API.

## Validation and limitations

Run from a fresh kernel in cell order. Inspect assertions and printed messages: some course helpers print incorrect-answer messages without raising exceptions. Saved output does not prove a fresh run passes.

Reconstruction metrics on the matrix used for fitting are in-sample diagnostics, not held-out recommendation benchmarks. Add a held-out interaction split, popularity baseline, Recall@K/NDCG@K, coverage, and cold-start evaluation. Clustering and exact-neighbor assertions may vary with initialization and library versions.

## Next development steps

- Resolve the execution issues in [review notes](docs/REVIEW.md).
- Extract pure recommendation functions and test unknown users, empty histories, and duplicate recommendations.
- Lock dependencies after an end-to-end run and publish a small demo with reproducible results.

## Attribution

Based on Udacity Data Scientist Nanodegree material and IBM Watson Studio interaction data. No standalone license file is present; confirm distribution rights before adding one. Data licensing is separate from code licensing.

## Recorded verification

On 2026-09-13, 54 analysis code cells completed in the audit environment without an exception. HTML exports were excluded. This checks execution, not held-out recommendation quality. See [validation scope](docs/REVIEW.md).
