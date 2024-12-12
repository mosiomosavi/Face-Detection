
This script creates a GUI application that starts a video stream and detects faces in real-time using OpenCV’s Haar cascade. Here’s how it works:

Key Features:
Face Detection: Uses cv2.CascadeClassifier to detect faces in the video frame.
Tkinter GUI: Provides a graphical interface with buttons to start the video and exit the application.
Threading: Ensures the GUI remains responsive while the video stream runs in the background.
Steps:
Install Required Libraries:

Install OpenCV: pip install opencv-python
Tkinter is included in Python by default.
Run the Script:

Save the script as face_detection_gui.py.
Run the script using Python: python face_detection_gui.py.
Usage:

Click Start Video to open the video stream.
Faces detected will have bounding boxes and a face count displayed.
Press Q to stop the video feed.
Click Exit to close the application.
Notes:
Ensure you have a working webcam.
The script uses the Haar cascade XML file bundled with OpenCV.
You can customize the detection sensitivity by adjusting the scaleFactor and minNeighbors parameters in detectMultiScale.
Let me know if you’d like additional functionality or modifications!
