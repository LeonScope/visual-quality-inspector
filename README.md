# Scope Vision · Visual Quality Inspector

**English** · [Deutsch](README.de.md)

**Local visual inspection with model-generated anomaly maps and a traceable human review.** Built by LeonScope with AI assistance as an independent portfolio project.

Scope Vision inspects a fictional plate for scratches and missing holes. It connects an actual image model to a usable workflow: inspect an image, examine the marked areas, record a human assessment, and export the inspection report.

**Presentation repository only. Application source, training/calibration/test data, model weights and fitted parameters remain private.** The screenshots use separately generated presentation examples. No open-source or Creative Commons license is granted for original material; see [Rights](RIGHTS.md).

![Scope Vision inspection station with an actual anomaly map and a recorded human assessment](assets/inspection-desktop.png)

*A missing hole in a synthetic presentation example. The colored overlay is computed from the image; the human assessment is stored separately from the model result.*

## The workflow

- Inspect synthetic examples or a local PNG/JPEG upload.
- Compare the original image with an approximate anomaly map.
- Distinguish **unremarkable**, **anomalous** and **manual review required** outcomes.
- Append human assessments without changing the original model measurement.
- Reopen the local inspection history and export JSON or CSV reports.
- Examine the frozen model's evaluation and lighting checks inside the application.

Every own upload requires human review, because its distribution has not been validated. The anomaly index is a distance relative to a calibrated threshold, not a probability or manufacturing acceptance decision.

## Measured on a deliberately narrow task

The fixed standard-light test contains **180 separate synthetic scenes**: 60 normal plates, 60 with scratches and 60 with missing holes. The decision threshold was selected before this test.

| Method | Detected defects | Missed defects | False alarms on normal images |
| --- | ---: | ---: | ---: |
| Frozen CNN features + fitted patch distributions | 120 / 120 | 0 | 0 / 60 |
| Simple grayscale reference comparison | 117 / 120 | 3 | 0 / 60 |

These are observations on the project's own synthetic generator. They do not establish performance on real factory images or general superiority over simpler methods. [Full verification and limitations](docs/VERIFICATION.md).

## Engineering evidence

**46 automated application/model checks and 8 browser workflows passed in a fresh local copy**, with independently installed pinned dependencies. The sealed private model bundle was reused and verified; it was not retrained during this check. All **436 image hashes** matched, and the **180 held-out predictions** reproduced the recorded aggregate results.

Python · FastAPI · PyTorch/TorchVision · React · TypeScript · SQLite · pytest · Playwright.

The detector uses frozen pretrained ResNet18 features and locally fitted Gaussian patch distributions inspired by PaDiM. It does not train a foundation model or fine-tune the CNN. [Method and implementation decisions](docs/CASE-STUDY.md).

## More views

![Local inspection history with separate model outcomes and human assessments](assets/history-desktop.png)

<details>
<summary>Model evidence and mobile workflow</summary>

![Model evidence, baseline comparison and paired lighting observations](assets/evaluation-desktop.png)

<img src="assets/inspection-mobile.png" width="350" alt="Scope Vision inspection and human review on a 390-pixel mobile viewport" />

</details>

## Context and boundaries

This independent project connects LeonScope's experience in robotics and camera-based quality inspection with a new local application. It contains no employer images, client data, industrial drawings or prior employer code. It does not connect to a camera, robot or production line.

The application is a working local prototype, not a hosted service or industrially accepted inspection system. This public repository provides documentation and selected screenshots; it does not provide a runnable package, public training dataset, model download or public application CI.

[Case study](docs/CASE-STUDY.md) · [Verification](docs/VERIFICATION.md) · [Rights](RIGHTS.md) · [LeonScope](https://github.com/LeonScope)
