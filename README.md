# MeXE402_Finals_Cullos_Kristina-Verroya_Patrick

## INTRODUCTION
  
Face detection is a fundamental problem in computer vision, with applications ranging from security systems to augmented reality and social media filters. It involves identifying and locating human faces within digital images or video streams. The significance of face detection lies in its role as a precursor to more advanced tasks such as facial recognition, emotion analysis, and human-computer interaction.

This project, titled *"Detecting Faces of Harry Potter Characters,"* applies face detection techniques using OpenCV and Haarcascade clasifier to identify characters from the Harry Potter series. By focusing on a themed dataset, this project not only explores the technical challenges of face detection but also demonstrates how computer vision can be tailored to specific contexts. This project will also serve as a practipe to enhance the students skills and knowledge when it comes machine learning.This playful yet practical implementation highlights the versatility of OpenCV in solving real-world problems while offering a platform for learning and innovation in computer vision.  

--- 

## ABSTRACT

* This project, titled *"Detecting Faces of Harry Potter Characters,"* focuses on developing a computer vision system using OpenCV to effectively identify and detect faces of characters from the Harry Potter series. It seeks to showcase OpenCV's face detection capabilities through a creative and themed application in computer vision.  


* The methodology includes compiling a dataset of Harry Potter character images, preprocessing the data, and utilizing OpenCV's Haar cascades or deep learning-based face detection methods. The system will undergo training and testing to achieve reliable performance. Challenges such as variations in lighting, pose, and image quality will be tackled using appropriate preprocessing and optimization techniques.  

* The anticipated outcome is the accurate detection of Harry Potter character faces in images or video streams. This project aims to demonstrate the adaptability of computer vision tools for specialized tasks, blending technical expertise with imaginative applications. Ultimately, it highlights the potential of OpenCV in handling unique detection challenges and contributes to a deeper understanding of face detection and recognition technologies.


Dor this project here are the objectives that studsents aim to achieve for the face detection project using OpenCV:

* To develop a Python program using OpenCV that accurately detects and highlights human faces in real-time or static images.
* To implement a Haar Cascade Clasifier detection algorithm for detecting faces from Harry Potter.
* To provide a visual output where detected faces are marked with bounding boxes.
* To achieve high detection accuracy across various lighting conditions and facial orientations.

## PROJECT METHODS

- **Dataset Collection**:  
  - Gather images of Harry Potter characters from various sources.  
  - Ensure diversity in lighting, angles, and expressions within the dataset.  
  - Organize images into labeled categories for each character.  

- **Dataset Collection**:  
  - Gather images of Harry Potter characters from various sources.  
  - Ensure diversity in lighting, angles, and expressions within the dataset.  
  - Organize images into labeled categories for each character.  

- **Implementation and Deployment**:  
  - Develop a script or application using OpenCV to detect faces in real-time or static images.  
  - Integrate functionality to highlight detected faces and label corresponding characters.  

- **Testing and Validation**:  
  - Measure detection accuracy using metrics like precision, recall, and F1 score.  
  - Compare model performance on different subsets of the dataset.  

- **Documentation and Presentation**:  
  - Document all steps, observations, and results.  
  - Present findings, including model performance and visual demonstrations of the detection system.  

## CONCLUSION



## ADDITIONAL MATERIALS

# Code

- **Importing Libraries**

To bring in the necessary functionality for image handling, file searching, and face detection.

```python

#Import open cv
import cv2

#Folder library
import glob
```

- **Defining Folder and Image Location**
### Define the folder containing images and retrieve all image files (.jpg and .png).
  
```python
# Specify the folder containing images
folder_path = "Harry Potter Group Photo"  # Replace with your folder path

# Use glob to get a list of all image files in the folder (e.g., jpg, png, etc.)
image_paths = glob.glob(folder_path + "/*.jpg") + glob.glob(folder_path + "/*.png")  # Adjust extensions as needed

# Sort the image paths (optional, for consistent order)
image_paths.sort()
```


- **Load Haar Cascade for Face Detection**
- Load the Haar Cascade XML file used for detecting frontal faces.

```python
 # Load Haar Cascade for face detection
haarcascade = "haarcascade_frontalface_default.xml"
face_cascade = cv2.CascadeClassifier(haarcascade)
```

- **Loop Through and Read Images**
- Start a loop to process and display each image.
```python
while True:
    # Load the current image
    image = cv2.imread(image_paths[index])

    # Check if the image was loaded successfully
    if image is None:
        print(f"Error: Could not load image {image_paths[index]}. Skipping to next image.")
        index = (index + 1) % len(image_paths)
        continue
```

- **Resizing and Converting Images to Greyscale**
- Resize the image for better viewing and convert it to grayscale for face detection.

```python
    try:
        # Resize image for better organization
        scale_percent = 50  # Resize to 50% of the original size (adjust as needed)
        width = int(image.shape[1] * scale_percent / 100)
        height = int(image.shape[0] * scale_percent / 100)
        dim = (width, height)
        image_resized = cv2.resize(image, dim)

        # Convert the image to grayscale for face detection
        gray_image = cv2.cvtColor(image_resized, cv2.COLOR_BGR2GRAY)
```

- **Apply Face Detection**
- Detect faces using face_cascade.detectMultiScale() with parameters correspond and unique for the image's index.
```python
        # Apply different parameters for face detection based on the index
        if index == 0:  # If this is the first image (index starts at 0)
            faces = face_cascade.detectMultiScale(
                gray_image, scaleFactor=1.1, minNeighbors=5, minSize=(70, 70)
            )
        elif index == 1:
            faces = face_cascade.detectMultiScale(
                gray_image, scaleFactor=1.1, minNeighbors=8, minSize=(50, 50)
            )
        else:
            faces = face_cascade.detectMultiScale(
                gray_image, scaleFactor=1.068, minNeighbors=5, minSize=(10, 10)
            )
```

- **Draw Rectangles Around Detected Faces**
- Highlight detected faces by drawing green rectangles on the image.
```python
        # Draw rectangles around detected faces
        for (x, y, w, h) in faces:
            cv2.rectangle(image_resized, (x, y), (x + w, y + h), (0, 255, 0), 2)

```

- **Display the Image**
- Show the processed image in an OpenCV window.
```python
  # Display the image with detected faces
  cv2.imshow("Photo Viewer with Face Detection", image_resized)
```

- **Photo Viewer Controls**   
- Use keyboard inputs to navigate between images or exit the program.
```python
    except Exception as e:
        print(f"Error processing image {image_paths[index]}: {e}")
        index = (index + 1) % len(image_paths)
        continue

    # Wait for a key press
    key = cv2.waitKey(0)

    # Navigate based on key press
    if key == 27:  # ESC key to exit
        print("Exiting Photo Viewer.")
        break
    elif key == ord('d') or key == 83:  # Right arrow or 'D' key
        index = (index + 1) % len(image_paths)  # Move to next image
    elif key == ord('a') or key == 81:  # Left arrow or 'A' key
        index = (index - 1) % len(image_paths)  # Move to previous image
```

- **Exit**   
- Release all resources by closing the OpenCV windows or pressing esc.

```python
# Close all OpenCV windows
cv2.destroyAllWindows()
```















