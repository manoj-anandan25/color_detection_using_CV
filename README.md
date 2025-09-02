# Color Detection Using OpenCV – Full Project Overview 
**Project Type:** Real-Time Object Color Detection
**Purpose:** Detect and highlight objects of a specific color using Python and OpenCV.

---

## 1. Overview

This project captures video from a webcam and detects objects of a specific color in real-time. The detection is based on the **HSV (Hue, Saturation, Value) color space**, which is more robust than BGR/RGB for detecting colors under varying lighting conditions.

**Key Features:**

* Real-time color detection and bounding box visualization.
* Uses HSV color space for accurate detection.
* Supports any color by modifying configuration.
* Simple setup; no advanced hardware required.

---

## 2. Color Spaces

OpenCV uses **BGR (Blue, Green, Red)** format by default. However, BGR is sensitive to lighting changes. To improve color detection:

1. Convert the BGR frame to **HSV (Hue, Saturation, Value)**:

   ```python
   hsv_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
   ```

2. **HSV Explanation:**

   * **Hue (H):** Defines the type of color (0-179 in OpenCV).
   * **Saturation (S):** Intensity/purity of the color (0-255).
   * **Value (V):** Brightness of the color (0-255).

Using HSV allows better separation of colors even in different lighting conditions.

---

## 3. Camera Setup

* Default camera: `cv2.VideoCapture(0)`

  * **0** → Default built-in webcam.
  * **1, 2, …** → External webcams if connected.

```python
cap = cv2.VideoCapture(0)  # Change index if using multiple cameras
```

**Tip:** If the webcam is not detected, ensure:

* Correct camera index.
* No other application is using the webcam.
* Proper drivers are installed.

---

## 4. How Detection Works

### 4.1 Define Target Color

Define the color to detect in **BGR format**, e.g., yellow:

```python
yellow = [0, 255, 255]  # BGR
```

Then, convert to HSV range using `get_limits(color)` function.

---

### 4.2 Create Mask

* `cv2.inRange()` generates a binary mask of the target color:

```python
mask = cv2.inRange(hsv_frame, lowerLimit, upperLimit)
```

* White pixels → Detected color
* Black pixels → Background

---

### 4.3 Find Object and Draw Bounding Box

* Convert mask to PIL image for bounding box detection:

```python
mask_ = Image.fromarray(mask)
bbox = mask_.getbbox()
```

* If a bounding box exists, draw it:

```python
if bbox:
    x1, y1, x2, y2 = bbox
    cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)
```

* Green rectangle highlights the detected object.

---

### 4.4 Display Frame

Show the processed video feed:

```python
cv2.imshow("frame", frame)
```

* Press **`q`** to quit.

---

## 5. Step-by-Step User Instructions

1. Install dependencies:

```bash
pip install opencv-python numpy Pillow
```

2. Clone the repository and navigate to the folder:

```bash
git clone https://github.com/yourusername/color-detection-cv.git
cd color-detection-cv
```

3. Run the script:

```bash
python color_detection.py
```

4. The webcam window will open.
5. Move the object of target color in front of the camera.
6. Green bounding box appears around detected object.
7. Press **`q`** to exit.

---

## 6. Troubleshooting

| Problem                 | Cause               | Solution                                     |
| ----------------------- | ------------------- | -------------------------------------------- |
| Camera not detected     | Wrong index or busy | Check camera index, close other apps         |
| No color detected       | Incorrect HSV range | Verify `get_limits()` and BGR color value    |
| Window freezes          | High resolution     | Reduce webcam resolution or optimize code    |
| Error: module not found | Missing packages    | Run `pip install opencv-python numpy Pillow` |

---

## 7. Customization

* **Change Color:** Modify `yellow = [B,G,R]` and `get_limits()` accordingly.
* **Multiple Cameras:** Change `cv2.VideoCapture(0)` to `1,2,...` depending on external cameras.
* **Multiple Colors:** Create multiple masks and bounding boxes for different colors.

---



