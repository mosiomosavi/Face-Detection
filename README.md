# Face-Detection
Real-Time Face Detection with OpenCV
Prerequisites:
Please make sure the following libraries are installed before running the project:
- numpy
- pandas
- matplotlib
```
import cv2
import tkinter as tk
from tkinter import messagebox
from threading import Thread


face_classifier = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)


video_capture = None
running = False

def detect_bounding_box(vid):
    
    gray_image = cv2.cvtColor(vid, cv2.COLOR_BGR2GRAY)
    
    
    faces = face_classifier.detectMultiScale(gray_image, 1.1, 5, minSize=(40, 40))
    
    
    for (x, y, w, h) in faces:
        cv2.rectangle(vid, (x, y), (x + w, y + h), (0, 255, 0), 4)
        cv2.putText(vid, "Face Detected", (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 2)
    
    
    cv2.putText(vid, f"Faces: {len(faces)}", (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 255), 2)
    cv2.putText(vid, "Press 'Q' to Quit", (10, 60), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (255, 255, 255), 1)
    
    return faces

def start_video():
    """Start the video stream."""
    global video_capture, running
    if running:
        messagebox.showinfo("Info", "Video is already running.")
        return

    running = True
    video_capture = cv2.VideoCapture(0)
    
    def video_loop():
        global running
        while running:
            result, video_frame = video_capture.read()
            if not result:
                break
            
            
            detect_bounding_box(video_frame)
            
            
            cv2.imshow("Face Detection", video_frame)

            
            if cv2.waitKey(1) & 0xFF == ord("q"):
                running = False
                break

        stop_video()
    
   
    Thread(target=video_loop, daemon=True).start()

def stop_video():
    """Stop the video stream."""
    global video_capture, running
    if running:
        running = False
        if video_capture is not None:
            video_capture.release()
        cv2.destroyAllWindows()

def quit_application():
    """Quit the application."""
    stop_video()
    root.quit()


root = tk.Tk()
root.title("Face Detection Menu")
root.geometry("300x200")


menu = tk.Menu(root)
root.config(menu=menu)


file_menu = tk.Menu(menu, tearoff=0)
menu.add_cascade(label="File", menu=file_menu)
file_menu.add_command(label="Start Video", command=start_video)
file_menu.add_separator()
file_menu.add_command(label="Exit", command=quit_application)


start_button = tk.Button(root, text="Start Video", command=start_video, width=15, bg="green", fg="white")
start_button.pack(pady=10)

exit_button = tk.Button(root, text="Exit", command=quit_application, width=15, bg="gray", fg="white")
exit_button.pack(pady=10)


root.mainloop()
```
