# httfacelond

Hardware-accelerated AI face swap studio for images and videos. Built with Python, Gradio, ONNX Runtime, InsightFace, MediaPipe, and OpenCV.

## Features

### Image Swap

- Swap a face from a source image onto a target image.
- Batch image swap for multiple target images at once.
- Upload a whole target image folder from the web UI.
- Paste a local target folder path directly, for example `C:\Users\test1234\Pictures\targets`.
- Automatically saves batch results to an output folder.
- Creates `swapped_batch_results.zip` for batch outputs.
- Shows batch results in a gallery inside the web UI.
- Supports `.jpg`, `.jpeg`, `.png`, `.webp`, `.bmp`, `.tif`, and `.tiff` images.

### Video Swap

- Swap a face from a source image onto a target video.
- Preview any selected video frame before rendering the full video.
- Estimate processing time based on frame count and CPU/GPU mode.
- Display real-time progress, speed, ETA, and logs during rendering.
- Use frame step/skip controls to reduce processing time.
- Configure threaded execution with selectable concurrent workers.
- Merge the original audio track back into the output video.

### Face Detection And Masking

- Uses InsightFace SCRFD as the default face detector.
- Includes YOLOv11-Face as an optional target face detector.
- Automatic threshold fallback when no face is detected at the initial confidence level.
- Auto-rotation recovery for tilted, sideways, or rotated faces.
- InsightFace 106-point landmark mask.
- MediaPipe FaceMesh 468-point mask.
- MediaPipe FaceMesh 3D Pose mask option.
- Soft feathering to reduce hard face edges and visible seams.

### Realism And Enhancement

- Face restorer/enhancer options:
  - GFPGANv1.4
  - CodeFormer
  - GPEN-BFR-512
  - GPEN-BFR-1024
- Adjustable enhancement strength.
- Lighting and skin tone matching through color transfer.
- Face shape aspect ratio matching.
- Face swap blend strength control for identity strength and realism.
- Face crop upscale resolution from 128 to 2048.
- Occlusion masking to preserve foreground objects such as hands, hair, arms, and clothing.

### Hardware And Models

- GPU mode through ONNX Runtime CUDA when a compatible GPU is available.
- CPU-only mode.
- GPU device selection for multi-GPU systems.
- Swapper model selection:
  - `inswapper_128_fp16.onnx`
  - `inswapper_128.onnx`
- Clear VRAM button to unload models during a session.

## Installation And Setup

### Windows PC (venv)

1. Install Python 3.12 and add Python to PATH.
2. Double-click `install_windows_venv.bat`.
3. After installation finishes, launch the app with `run_studio.bat`.

### Linux (Debian / Ubuntu - Conda)

```bash
chmod +x install_linux_conda.sh
./install_linux_conda.sh
conda activate httfacelond
python app.py
```

## Web Interface

After launching the app, open:

```text
http://127.0.0.1:7860
```

or:

```text
http://localhost:7860
```

## Quick Usage

### Single Image Swap

1. Upload `Source Face`.
2. Upload `Target Image`.
3. Choose the model and settings you want.
4. Click `Start Face Swap`.

### Batch Image Swap With A Folder

1. Upload `Source Face`.
2. Upload a folder in `Batch Target Images / Folder Upload`.
3. Or paste a folder path in `Batch Target Local Folder Path`.
4. Click `Start Batch Folder Swap`.
5. Results appear in the gallery, output folder, and zip file.

### Video Swap

1. Upload `Source Face Image`.
2. Upload `Target Video`.
3. Select a frame and generate a preview if needed.
4. Click `Start Face Swap Video`.

## Model Sources And Credits

The AI models are automatically downloaded from these sources:

- Face Swapper FP16: [inswapper_128_fp16.onnx](https://huggingface.co/hacksider/deep-live-cam/resolve/main/inswapper_128_fp16.onnx)
- Face Swapper FP32: [inswapper_128.onnx](https://huggingface.co/ezioruan/inswapper_128.onnx/resolve/main/inswapper_128.onnx)
- Face Restorer GFPGAN: [GFPGANv1.4.onnx](https://huggingface.co/Neus/GFPGANv1.4/resolve/main/GFPGANv1.4.onnx)
- Face Occluder: [face_occluder.onnx](https://huggingface.co/Rookiehan/facefusion/resolve/main/face_occluder.onnx)
- CodeFormer: [codeformer.onnx](https://huggingface.co/facefusion/models-3.0.0/resolve/main/codeformer.onnx)
- GPEN-BFR-512: [GPEN-BFR-512.onnx](https://huggingface.co/datasets/Gourieff/ReActor/resolve/main/models/facerestore_models/GPEN-BFR-512.onnx)
- GPEN-BFR-1024: [GPEN-BFR-1024.onnx](https://huggingface.co/datasets/Gourieff/ReActor/resolve/main/models/facerestore_models/GPEN-BFR-1024.onnx)
- YOLOv11-Face: [yolov11n-face.onnx](https://huggingface.co/AdamCodd/YOLOv11n-face-detection/resolve/main/model.onnx)

## License

Copyright (c) 2026. All rights reserved. Modification, distribution, or reproduction without prior written permission is strictly prohibited.
