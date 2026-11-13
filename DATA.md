# Data

This repository contains **no datasets**.

| Dataset | How to get it | Use here |
|---|---|---|
| ParFace (palsy patients, video frames) | Email the maintainers (see the ParFace GitHub page, `jilliam/ParFace`). Research use, cite the FG 2024 paper. Do not redistribute. | Palsy-side movement and asymmetry. Palsy side/grade must come from the authors or a clinician. |
| Toronto NeuroFace (ALS, stroke, healthy controls) | Data access request form on the University of Toronto Speech-Language Pathology dataset page (processed in a few business days). Cite Bandini et al. 2021 and use the required acknowledgment. | Healthy-control norm. Check which tasks are included before using a task-specific norm. |

Rules for this project:
- Do not commit data, labels derived from private clinical records, or credentials/share links.
- Label files (`meta.csv`, `author_labels.csv`) stay outside the repo (`.gitignore` covers them).
- Patient photos for any pilot need ethics approval and informed consent first.
