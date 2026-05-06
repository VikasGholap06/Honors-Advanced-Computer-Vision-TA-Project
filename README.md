# YOLO-World Object Detection Project

This project detects many common real-world objects from a webcam, image, or video using Ultralytics YOLO-World.

It is set up to work well for examples like:

- person
- bottle
- pen
- mobile phone
- chair
- laptop / computer monitor
- keyboard
- mouse
- book
- cup

## What makes this project better

- Uses YOLO-World, so you are not limited to the default 80 COCO classes.
- Supports webcam, image, and video input.
- Shows live bounding boxes, confidence labels, FPS, and object counts.
- Lets you extend detection with your own prompts.
- Can save processed image and video outputs.
- Includes a ready prompt file for common indoor and study objects.

## Project files

- `app.py` - main detection app
- `prompts/common_objects.txt` - default object prompts
- `requirements.txt` - Python dependencies

## Install

Create and activate a virtual environment if you want:

```powershell
python -m venv .venv
.venv\Scripts\activate
```

Install dependencies:

```powershell
pip install -r requirements.txt
```

## Run

### 1. Webcam detection

```powershell
python app.py --source 0 --save
```

### 2. Detect objects in an image

```powershell
python app.py --source path\to\image.jpg --save
```

### 3. Detect objects in a video

```powershell
python app.py --source path\to\video.mp4 --track --save
```

### 4. Add more custom objects

```powershell
python app.py --source 0 --prompts "notebook,whiteboard,projector,water bottle"
```

### 5. Use default COCO classes only

```powershell
python app.py --source 0 --use-coco
```

## Useful options

- `--model weights/yolov8s-worldv2.pt` - balanced default model
- `--imgsz 1280` - better for small objects like pens, but slower
- `--track` - keep track IDs in video/webcam streams
- `--save` - save output into the `outputs/` folder
- `--no-show` - run without opening a window
- `--prompts "object1,object2"` - append extra custom object prompts
- `--prompt-file prompts/common_objects.txt` - load prompts from a text file
- `--save-prompt-model custom_study_detector.pt` - save a prompt-specialized model

## Controls while webcam/video is running

- `q` or `Esc` - quit
- `s` - save a snapshot frame

## Important note

No model can reliably detect "every object" in every situation. YOLO-World is much better than a fixed small class list, but results still depend on:

- camera quality
- lighting
- object size
- viewing angle
- whether your prompt text matches the object well

For tiny or very specific objects, do these things for better accuracy:

1. Increase image size with `--imgsz 1280`
2. Bring the object closer to the camera
3. Use clearer prompts such as `mobile phone` instead of `phone`
4. Switch to a larger model like `yolov8m-worldv2.pt` or `yolov8l-worldv2.pt`
5. Train a custom detector if you need very high accuracy for a special object class

## First-run downloads

On first run, Ultralytics may download:

- YOLO-World model weights
- CLIP text-model weights used for custom prompts

The app keeps the CLIP cache inside the project under `.cache_home/` so it does not depend on a global user cache path.

After that, the app can usually reuse the cached files.
