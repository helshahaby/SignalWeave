# SignalWeave

**Industrial evidence for proactive decisions**

Created by **Hossam Elshahaby** for **Junction X Vaasa 2026**, addressing the ABB challenge **FROM WEAK SIGNALS TO PROACTIVE DECISIONS**.

## Links

- [Live application](https://snap-and-see-pro.lovable.app/)
- [Pitch video](https://youtu.be/i0IXywNXkgk)

## Project description

SignalWeave is an industrial investigation prototype that brings measurements, maintenance notes, alarms and video evidence into a shared workspace. It helps teams inspect weak signals, understand supporting evidence and review proposed actions.

The intended users include maintenance engineers, operations teams and warehouse safety reviewers.

## Problem

A small rise in motor current can appear harmless in isolation. A temperature trend or repeated operator observation may change its meaning. When these signals sit in separate systems, teams must assemble the context manually and may overlook a developing issue.

Video adds context, but detecting a worker or forklift alone does not establish that a near-miss event occurred or that an early warning succeeded.

## Features

- CSV import for measurements and operational context.
- Video evidence with paired MP4 and object annotations.
- Annotation checks and an optional ground-truth overlay.
- Object-detection benchmarks using separate predictions and reference boxes.
- A reviewed event-label editor for early-warning evaluation.
- An investigation and action-review workflow intended to connect evidence with operational decisions.

## Demo guide

1. Open the [application](https://snap-and-see-pro.lovable.app/). Use demo mode if available, or sign in to your project.
2. Import measurements and relevant maintenance notes or alarms.
3. Open **Video evidence** and load a clip with its matching `.object_detection.jsonl` file, or use the built-in demo if available.
4. Check that the files share the same run and camera. Review frame counts and annotation problems.
5. Reveal ground truth to inspect reference boxes, then run the object-detection benchmark.
6. For early warning, review the video and save a genuine event interval using **Benchmarks → Early warning → Create event labels from video**.
7. Complete chronological analysis for that exact clip, then select **Score against recorded analyses**.

If the app reports no completed chronological analysis, early-warning scoring remains unavailable. A completed object-detection benchmark does not satisfy that prerequisite.

## Benchmark inputs

| Evaluation | Reference input | Required prediction output |
| --- | --- | --- |
| Object detection | Matching `.object_detection.jsonl` | Predicted classes and boxes for evaluated frames |
| Early warning | Human-reviewed event intervals | Timestamped warnings from completed chronological analysis |
| Clip classification | Human-reviewed `video_id,class_label` rows | Clip predictions under a fixed class mapping |

Early-warning event-label imports require:

```text
video_id,run_id,event_type,start_seconds,end_seconds
```

Use the exact clip identifier shown in the app. Event times must come from a reviewer observing the clip under a clear event rule.

**Ground truth stays separate from model predictions.** Exported predictions, results JSON and run `.meta.json` files do not replace reviewed event labels. Object annotations contain boxes, rather than reviewed event start and end times.

## Dataset

The development demo uses [NVIDIA PhysicalAI WorldModel Synthetic Warehouse Operations Scenes](https://huggingface.co/datasets/nvidia/PhysicalAI-WorldModel-Synthetic-Warehouse-Operations-Scenes).

These synthetic scenes provide video and companion annotations for detection evaluation. The near-miss archive's scenario category does not establish the exact event interval in every camera view.

Large TAR archives must be extracted to obtain individual files. The browser plays extracted video, not the TAR archive itself. Direct archive import requires a separately hosted extraction worker.

## Evaluation status and limitations

Object-detection runs have appeared in the prototype. The latest reviewed early-warning screenshot in this project's development discussion showed one saved event label, zero recorded chronological analyses and zero matched analyzed clips. It therefore did not establish early-warning performance.

Report detection precision, recall and F1 with the matching policy, evaluated frames and exclusions. Evaluate warning timing separately using independently reviewed events. Include normal scenes and multiple runs before drawing broader conclusions.

Synthetic demo results do not establish performance in a real industrial deployment. Reductions in downtime, incidents or cost remain proposed benefits that require a pilot study.

## Expected impact

SignalWeave aims to reduce the time spent gathering evidence, help teams prioritize investigations and preserve the reasoning behind an action. Practical examples include connecting motor measurement trends with operator observations and reviewing worker–forklift interactions in warehouse footage.

## Next steps

- Verify the complete chronological-analysis and warning-scoring workflow.
- Simplify creation of reviewed clip-classification labels.
- Improve persistence of clips, labels and completed analyses.
- Expand evaluation across multiple runs and normal scenes.
- Validate with real industrial data and measure operational outcomes.

## Project scope

This is an independent hackathon prototype addressing an ABB challenge. It does not claim ABB endorsement, production integration or validated safety-system performance.

## Author

**Hossam Elshahaby**

Junction X Vaasa 2026
