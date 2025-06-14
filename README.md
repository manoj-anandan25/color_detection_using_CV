# color_detection_using_CV
# Color-Detection
Detecting color with python and OpenCV using HSV colorspace.

Required libraries
opencv-python
numpy
Pillow

This code captures video from the webcam using OpenCV and processes it to detect yellow objects. Here's a breakdown of what each part of the code does:

1. Color Definition: 
   - The variable `yellow = [0, 255, 255]` defines yellow in BGR color space (used by OpenCV).

2. Video Capture:
   - `cap = cv2.VideoCapture(0)` initializes the webcam capture.

3. Frame Capture Loop:
   - In the `while True` loop, each frame from the webcam is captured and converted to HSV (Hue, Saturation, Value) color space using `cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)`.

4. Get Color Limits:
   - `get_limits(color=yellow)` returns the lower and upper bounds for detecting yellow in the HSV color space. This function is presumably defined elsewhere (likely in `util.py`), which is why I can't provide its implementation here.

5. Mask Creation:
   - `cv2.inRange(hsvImage, lowerLimit, upperLimit)` creates a binary mask where pixels within the range of the yellow color will be white (255), and everything else will be black (0).

6. Bounding Box:
   - `mask_ = Image.fromarray(mask)` converts the NumPy array to a PIL image to use the `getbbox()` method. This method finds the bounding box of the white region in the mask.
   - If a bounding box is found (i.e., there is a yellow object detected), the coordinates `x1, y1, x2, y2` are used to draw a green rectangle around the object on the frame.

7. Displaying the Frame:
   - The processed frame is displayed in a window titled "frame" using `cv2.imshow()`.

8. Exit Condition:
   - The program will exit the loop when the user presses the 'q' key (`cv2.waitKey(1) & 0xFF == ord('q')`).

9. Release Resources:
   - After the loop is finished, the `cap.release()` method is called to release the video capture object, and `cv2.destroyAllWindows()` is used to close any OpenCV windows.

Potential Issues or Improvements:
- Ensure the `get_limits` function is correctly defined and returns appropriate HSV bounds for yellow.
- Make sure the webcam is accessible and OpenCV is properly installed.
- If you need to handle situations where no yellow objects are detected (i.e., when `bbox` is `None`), you could add additional logic to handle that case or notify the user.

