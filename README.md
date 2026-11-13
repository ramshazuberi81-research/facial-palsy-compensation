# Compensation-aware facial palsy assessment

Research prototype that measures, from phone photos or video, how much each side of the face moves and whether the healthy side over-moves to hide weakness ("compensation"). It has two parts:

| Folder | What it is |
|---|---|
| `notebooks/` | Colab notebook: landmark extraction (MediaPipe), IPD-normalised per-side range of motion, asymmetry, compensation vs. a healthy norm, longitudinal logic, reliability (ICC) and validation tests. |
| `app/` | Single-file browser app: camera or upload, on-device face landmarks, left/right measures. No server, images never leave the device. |

> **Not a medical device and not a diagnosis.** Nothing here is validated clinically. Compensation scores need a validated healthy-control norm, and treatment or dose output must not be used for patient care. Sudden facial droop needs emergency care.

## Status

- Pipeline runs end to end on ParFace; only a few videos have known palsy sides, so no conclusions yet.
- Needed before any claim: palsy-side/grade labels, healthy controls (e.g. Toronto NeuroFace), repeat-capture reliability (ICC, minimal detectable change), clinician-graded pilot.
- See `docs/validation_plan.md`.

## Run the app locally

```bash
cd app
python -m http.server 8000      # then open http://localhost:8000 (camera works on localhost)
```
The camera needs HTTPS or localhost. The app loads MediaPipe from jsDelivr and the face model from Google storage, so it needs an internet connection.

## Deploy the app (GitHub Pages)

1. Push this repo to GitHub.
2. Settings → Pages → Source: **GitHub Actions**.
3. Push to `main`; the workflow in `.github/workflows/pages.yml` publishes `app/`.

## Run the notebook

1. Open `notebooks/facial_palsy_compensation_parface_v4.ipynb` in Google Colab.
2. Put your own copy of ParFace at `MyDrive/ParFace.zip` (see `DATA.md`).
3. Run cells top to bottom; restart the session once after the install cell.
4. Put palsy sides in `MyDrive/ParFace_outputs/author_labels.csv` (`video_id,palsy_side[,patient_id,grade,visit]`, `L` = subject's left). Unlabeled videos are excluded, never guessed.
5. Add control videos as folders named `VideoC01`, `VideoC02`, … with `palsy_side = none`.

## Measures

Per side, in inter-pupillary-distance (IPD) units after rotating the pupil line horizontal: brow raise, eye opening, mouth-corner lift, mouth-corner width.
Asymmetry = (healthy − palsy) ÷ (healthy + palsy). Compensation = healthy-side movement above (control mean + 1.5 SD).

## Data and privacy

No images or patient data are in this repo, and `.gitignore` blocks the usual data files. See `DATA.md`. Never commit identifiable face images.

## Citation and credits

- ParFace: J. M. Díaz Barros et al., *In-Domain Inversion for Improved 3D Face Alignment on Asymmetrical Expressions*, FG 2024. Dataset available from the authors for research use.
- Toronto NeuroFace: A. Bandini et al., *A New Dataset for Facial Motion Analysis in Individuals With Neurological Disorders*, IEEE JBHI 25(4), 2021. Access by request.
- Landmarks: MediaPipe Face Landmarker.

## License

MIT for the code (see `LICENSE`). Datasets keep their own terms.
