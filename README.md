# Face_detection
Face Detection with OpenCV: Real-time detection of faces in webcam video using OpenCV's Haar Cascade classifier. Highlights detected faces with bounding rectangles. Efficient and straightforward Python implementation for quick deployment and integration.

""" CODE """
import cv2

# Load the Haar Cascade file for face detection
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

# Initialize video capture from the default webcam (0)
video_cap = cv2.VideoCapture(0)

while True:
    # Capture frame-by-frame
    ret, frame = video_cap.read()
    
    if not ret:
        print("Failed to grab frame")
        break

    # Convert the frame to grayscale
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Detect faces in the frame
    faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

    # Draw rectangles around the detected faces
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (255, 0, 0), 2)

    # Display the resulting frame
    cv2.imshow("Video_Capture", frame)

    # Break the loop on 'a' key press
    if cv2.waitKey(10) & 0xFF == ord('a'):
        break

# When everything is done, release the capture
video_cap.release()
cv2.destroyAllWindows()
