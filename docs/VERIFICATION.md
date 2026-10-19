# Scope Vision — verification

**English** · [Deutsch](VERIFICATION.de.md) · [Project](../README.md)

These tests ran locally during development on **18 October 2026**. They were not run by an independent testing body or through public CI. Repeating them requires the private source, model and data files.

## Application verification

After the industrial interface redesign, the separate test copy was updated to the new source version. The same 46 Python tests and eight browser workflows passed again, including checks of the progress strip. Model and evaluation files kept their original checksums. Installed dependencies were reused without changes; the earlier clean-install results still refer to that earlier run.

| Check | Observed result |
| --- | --- |
| Separate local verification checkout | Private source commit `2c12b09cb562f324ae9d19d59ca191712811e395` |
| Dependency installation | Previously clean-installed environments reused; dependency files unchanged for the interface revision |
| Type checking and production frontend build | Passed |
| Python application/model checks | **46 passed** |
| Browser workflows | **8 passed**, no retries |
| Data integrity | **436 of 436 image hashes matched** |
| Frozen-model replay | **180 test predictions reproduced**; model and baseline aggregate metrics matched |
| Model state during replay | Existing private artifacts verified; no refitting or threshold changes |
| Screenshots | Captured from the verified revision in the separate checkout; presentation examples only |

Environment: macOS 26.6 on arm64, Python 3.12.14, Node.js 24.19.0, Chrome 155.0.8059.84. Model inference uses CPU with two PyTorch threads. Dependency versions are recorded privately, including PyTorch 2.14.1 and TorchVision 0.29.1.

The Python suite emits an upstream Starlette deprecation warning about its httpx-based test client; the 46 checks pass. It concerns the test client and did not cause an application test to fail.

The eight browser workflows cover actual image-dependent inference; append-only review and downloads; lighting changes; local uploads; confirmed/cancelled deletion; history filtering and reopening; model evidence with presentation screenshots; and a 390-pixel mobile workflow without horizontal overflow.

Python checks cover data lineage and artifact integrity, frozen-result replay bindings, responses to changed image content, decision bands, capture checks, persistence, retention/cascade deletion, review limits, input validation, hostile origins, private-file isolation, failed/concurrent inference, image metadata removal and CSV formula handling. These are bounded tests, not a penetration test or production security certification.

## Data separation

| Split | Images | Use |
| --- | ---: | --- |
| Training | 160 normal | Fit normal feature distributions |
| Calibration | 90: 30 per class | Select model and baseline thresholds |
| Held-out standard-light test | 180: 60 per class | Evaluate the frozen state |
| Presentation | 6: 2 per class | Separate UI examples; selected views may be published |

All splits use different scene seeds from the same synthetic generator. Images vary slightly in placement, texture and brightness. This is **not** separation across physical parts, cameras, factories or real production batches. All training, calibration and test images remain private, including their masks and per-image predictions.

## Model and threshold

Model version: `scope-vision-1.0` · model identifier: `199b18fad8e11f73`.

Frozen pretrained ResNet18 features feed a compact spatial Gaussian patch model. The calibration rule maximizes balanced accuracy, then favors fewer missed defects and then the higher threshold. The resulting raw threshold is **12.225147247314453**. Image scores above it are anomalous; the UI's index is score divided by this threshold. Index 0.85–1.15, known capture-quality issues or any own upload require manual review.

The threshold was fixed before held-out evaluation. The stored report is bound to the model metadata and artifact checksums. Training/evaluation refuse to overwrite the existing fitted state/report. The verification-checkout replay uses the frozen state; it is not a second training experiment.

## Standard-light results

| Actual input | Model unremarkable | Model anomalous |
| --- | ---: | ---: |
| 60 normal images | 60 | 0 |
| 60 scratched + 60 missing-hole images | 0 | 120 |

Both defect types were detected in **60 of 60** test images. The simple grayscale baseline detected **117 of 120** defects, missed **3**, and generated **0 of 60** false alarms. Each method's threshold was selected on calibration, not on this test.

Standard-light UI triage: 60 unremarkable, 120 anomalous, 0 manual-review outcomes. These results apply to this limited set of generated images. Future images can still produce errors. The spatial accuracy of the heat map was not measured.

## Paired lighting observations

| Lighting variant | Manual review required | Raw detected defects | Raw false alarms |
| --- | ---: | ---: | ---: |
| Reduced light | 180 / 180 | 120 / 120 | 0 / 60 |
| Added glare | 110 / 180 | 120 / 120 | 0 / 60 |

These are the **same 180 held-out scene seeds** with two lighting transformations, not 360 additional independent scenes. The raw model remains correct on these variants, while the capture gate diverts some or all images to a human. The 70 glare variants without a review flag demonstrate that the gate is not an exhaustive detector of all lighting changes. Behavior under other lighting conditions remains untested.

## Timing and observable limits

On the original local CPU evaluation, per-image model calculation measured **12.2 ms median** and **13.4 ms p95**, across 180 standard-light test images. Timing starts after image loading and includes feature extraction and distance computation; it excludes model loading, image generation, upload, overlay rendering, storage and browser work. The interface's per-inspection measurement additionally includes overlay generation. These values are observations on one machine, not an end-to-end latency promise.

![Evidence view showing confusion counts, baseline and paired lighting checks](../assets/evaluation-desktop.png)

## Published material

This repository contains bilingual documentation, an original cover illustration, four selected screenshots and a rights notice. It has a separate presentation history. It does not contain application source, an application build, executable packages, training/calibration/test images, model parameters, weights, private logs or customer/employer data. The screenshots' plate images come exclusively from the presentation examples.

There is no public deployment, public application CI, factory integration or industrial acceptance evidence. [Case study](CASE-STUDY.md) · [Rights](../RIGHTS.md).
