# -Sketch-Transformation-with-OpenCV


Sketch Transformation with OpenCV
Project Title
Sketch Transformation with OpenCV

Project Description
This project captures video from a webcam and allows the user to select a region of interest (ROI) in the video feed. The selected ROI is then transformed into a sketch-like image using edge detection and thresholding techniques. The transformed ROI is displayed on the original video feed in real-time, creating a dynamic sketch effect.

Table of Contents
Project Goals
Installation
Usage Instructions
Code Explanation
Credits
Additional Notes
Project Goals

Capture real-time video feed from a webcam.
Allow the user to select a region of interest (ROI) in the video feed.
Transform the selected ROI into a sketch-like image.
Display the transformed ROI on the original video feed in real-time.
Installation

cd sketch-transform-opencv
Install required libraries:
Make sure you have Python installed. Then, install the necessary libraries using pip:

sh
Copy code
pip install numpy opencv-python matplotlib
Ensure you have a webcam connected:
The project uses the default webcam (device 0). Make sure your webcam is properly connected and working.

Usage Instructions
Run the script:
Execute the Python script to start the sketch transformation.

sh
Copy code
python sketch_transform.py
Interacting with the program:

The program will first open a window displaying the video feed.
Select the region of interest (ROI) by clicking and dragging a rectangle on the video feed. Press Enter to confirm the selection.
The selected ROI will be transformed into a sketch-like image and displayed on the original video feed.
Press the q key to exit the program.
Code Explanation
Imports and Function Definitions:

Import necessary libraries: cv2, numpy, and matplotlib.
Define the sketch_transform function which converts an image to a grayscale sketch:
python
Copy code
def sketch_transform(image):
    image_grayscale = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    image_grayscale_blurred = cv2.GaussianBlur(image_grayscale, (7,7), 0)
    image_canny = cv2.Canny(image_grayscale_blurred, 10, 80)
    _, mask = image_canny_inverted = cv2.threshold(image_canny, 30, 255, cv2.THRESH_BINARY_INV)
    return mask
Webcam Capture and ROI Selection:

Capture video from the webcam:
python
Copy code
cam_capture = cv2.VideoCapture(0)
Allow the user to select an ROI:
python
Copy code
_, im0 = cam_capture.read()
showCrosshair = False
fromCenter = False
r = cv2.selectROI("Image", im0, fromCenter, showCrosshair)
Real-Time Sketch Transformation:

Continuously capture video frames:
python
Copy code
while True:
    _, image_frame = cam_capture.read()
    rect_img = image_frame[int(r[1]):int(r[1] + r[3]), int(r[0]):int(r[0] + r[2])]
    sketcher_rect = sketch_transform(rect_img)
    sketcher_rect_rgb = cv2.cvtColor(sketcher_rect, cv2.COLOR_GRAY2RGB)
    image_frame[int(r[1]):int(r[1] + r[3]), int(r[0]):int(r[0] + r[2])] = sketcher_rect_rgb
    cv2.imshow("Sketcher ROI", image_frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
Clean Up:

Release the webcam and close all OpenCV windows:
python
Copy code
cam_capture.release()
cv2.destroyAllWindows()


Credits
This project uses the following libraries:

OpenCV for image and video processing.
NumPy for numerical operations.
Matplotlib for plotting (though not used in the main script, it may be useful for future enhancements).
Additional Notes
You can modify the parameters in the sketch_transform function to adjust the sketch effect.
Experiment with different threshold values and edge detection parameters to achieve the desired sketch effect.
This project demonstrates basic techniques in image processing and computer vision, which can be extended for more complex applications.
