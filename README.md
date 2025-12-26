# Print Quality Monitoring with ML (Computer Vision)

## The problem I'm trying to solve

Sometimes my printer does weird things:
- **Layer shifts** – One layer is off by a few mm
- **Nozzle clogs** – Filament stops coming out
- **Bed adhesion loss** – Print lifts off mid-way

By the time I notice, I've wasted 1-2 hours of filament and time.

**Goal:** Mount a camera, train a model to spot these issues automatically, and pause the printer before it becomes a disaster.

## What I'm building

A system that:
1. Watches the print via camera
2. Runs YOLOv8 (object detection model) every second
3. If something looks wrong → sends an alert + pauses printer

Status: 🚧 **Work in progress** – Ordered the camera; currently learning PyTorch

## What I DON'T know yet

- Never trained a ML model before
- Never used YOLOv8 before (only watched tutorials)
- Never optimized a model for Raspberry Pi before
- Not sure if my RTX 4060 has enough VRAM (need to test)

## Plan (rough)

1. Get dataset of "good prints" vs "bad prints" (will take a while)
2. Train YOLOv8-nano on my GPU (Windows 11, RTX 4060)
3. Quantize it so it runs on Raspberry Pi
4. Test detection accuracy
5. Integrate with Moonraker to pause prints
6. Hope it doesn't pause randomly on false positives

## Current state

- [ ] Camera ordered (waiting for it)
- [x] Watched ~3 tutorials on YOLOv8
- [ ] Started learning PyTorch basics
- [ ] Read about model quantization (INT8)
- [ ] Scared about how much RAM Raspberry Pi needs

## Technical setup

**Training (my Windows workstation):**
- PyTorch + CUDA (RTX 4060 8GB)
- YOLOv8 pre-trained weights
- OpenCV for image processing
- Custom dataset (building it)

**Inference (Raspberry Pi):**
- ONNX Runtime (lighter than PyTorch)
- Quantized model (INT8) – need to compress by 4×
- 5MP CSI camera
- Moonraker WebSocket connection

## What worries me

1. **Model accuracy** – Will it actually detect real failures, or will it be useless?
2. **False positives** – If it pauses on every shadow, that's worse than no monitoring
3. **Raspberry Pi performance** – 800ms per inference = 1 frame per second. That's slow.
4. **Dataset size** – I need ~1000 failure images to train. I only have like 20 right now.

## Milestones

- **Week 1-2:** Get camera working + streaming to Raspberry Pi
- **Week 3-4:** Collect initial dataset (print some things, take photos)
- **Month 2:** Train first version (even if accuracy sucks)
- **Month 3:** Integrate with Moonraker
- **Month 4+:** Iterate on accuracy

## If you know ML

- Ever trained YOLO on custom data? Tips?
- How do I know if my dataset is big enough?
- Best way to quantize without killing accuracy?
- Is Raspberry Pi 4B+ actually capable of this?

---
