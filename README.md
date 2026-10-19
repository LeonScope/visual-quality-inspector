![Scope Vision — visual quality inspection by LeonScope. From image to documented decision.](assets/cover.png)

**PRODUCT BRIEF / 01** &nbsp; · &nbsp; **English** / [Deutsch](README.de.md) &nbsp; · &nbsp; [Case study](docs/CASE-STUDY.md) &nbsp; · &nbsp; [Verification](docs/VERIFICATION.md)

# Scope Vision

### Finding scratches and missing holes in an image

Scope Vision checks generated images of a metal plate for scratches and missing holes. It shows the original image alongside the areas the model finds unusual. A person can then review the result and save their assessment. The project builds on my experience with camera-based quality inspection; the application was developed from scratch with AI assistance.

| APPLICATION | INSPECTION SETUP | PROJECT STATUS |
| :--- | :--- | :--- |
| Image-based quality inspection | Synthetic plate · fixed perspective | Functional local prototype |

**This repository publishes the presentation only.** Application source, training/calibration/test data, model weights and fitted parameters remain private. No open-source or Creative Commons license is granted for the original material. [Rights notice](RIGHTS.md).

---

## 01 / The image workspace

![Industrial Scope Vision console showing the original image, computed anomaly map, measured score and human review](assets/inspection-desktop.png)

**The example has a missing hole.** The original is on the left, beside the computed anomaly map. The score and human assessment are on the right, with both recorded separately below. Screenshots use their own presentation images, separate from training and testing.

| 01 · Image input | 02 · Model analysis | 03 · Human review |
| :--- | :--- | :--- |
| Choose a synthetic example or local PNG/JPEG. Change lighting as an inspection variant. | Compute the anomaly map, display the index and account for capture conditions. | Record acceptance, rejection or further review. Export the report as JSON/CSV. |

Uploaded images always require a person’s review. The anomaly index relates the score to the calibrated threshold; it is not a probability or permission to release a part. The overlay indicates a rough location rather than measuring the defect.

## 02 / Inspection archive and model validation

<table>
<tr>
<td width="50%" valign="top">
<strong>INSPECTION ARCHIVE</strong><br />Filter and reopen stored inspections. Every added assessment preserves the original model measurement.<br /><br />
<a href="assets/history-desktop.png"><img src="assets/history-desktop.png" alt="Inspection archive with model outcome, anomaly index and human assessment" /></a>
</td>
<td width="50%" valign="top">
<strong>MODEL VALIDATION</strong><br />Frozen model state, separate data splits, baseline comparison and lighting checks inside the application.<br /><br />
<a href="assets/evaluation-desktop.png"><img src="assets/evaluation-desktop.png" alt="Model validation with a classification matrix, baseline comparison and lighting checks" /></a>
</td>
</tr>
</table>

<details>
<summary><strong>Open the mobile view</strong> — the same workflow at 390 pixels wide</summary>

The original image, anomaly map, score and assessment follow vertically on a phone. The workflow was checked without horizontal overflow. Application screenshots show the German interface.

<img src="assets/inspection-mobile.png" width="340" alt="Mobile Scope Vision console with image analysis, human review and inspection record" />

</details>

## 03 / Technical specification

| Item | Implementation and observed result |
| :--- | :--- |
| Image model | Frozen pretrained ResNet18 features + locally fitted Gaussian patch distributions; inspired by PaDiM |
| Fitting and calibration | 160 normal fitting images · 90 calibration images |
| Held-out test | 180 synthetic scenes: 60 normal, 60 scratches, 60 missing holes |
| Model at standard lighting | **120 / 120 defects detected · 0 / 60 false alarms** |
| Grayscale reference baseline | **117 / 120 defects detected · 3 missed · 0 / 60 false alarms** |
| Verification | **46 application/model checks + 8 browser workflows passed** |
| Reproducibility | **436 image hashes verified · 180 test predictions reproduced** |
| Application | Python · FastAPI · PyTorch/TorchVision · React · TypeScript · SQLite |
| Interface | Industrial inspection console: graphite, steel gray, signal orange and functional outcome colors |

Results apply to the project's own synthetic sample set. They do not establish reliability on real production lines or general superiority over simpler methods. The CNN is not fine-tuned; learning here means fitting normal-feature distributions. [Evaluation method, lighting variants and limits](docs/VERIFICATION.md).

### Why the interface is arranged this way

The original and result need to be easy to compare, so the images take up most of the inspection view. Measurements and review controls sit beside them. A progress strip shows which steps are complete. Documented interfaces from Cognex, MVTec and SensoPart informed the layout; the [design notes](docs/DESIGN-NOTES.md) link to those references and explain the choices.

Scope Vision contains no images, drawings, data or source from previous employers or clients. No camera or robot is connected. The application runs locally; there is no public demo, software package, dataset or model download, or GitHub application test run.

---

**LEONSCOPE / ENGINEERING PORTFOLIO**

[Case study](docs/CASE-STUDY.md) · [Verification](docs/VERIFICATION.md) · [Design](docs/DESIGN-NOTES.md) · [Rights notice](RIGHTS.md) · [Profile](https://github.com/LeonScope)
