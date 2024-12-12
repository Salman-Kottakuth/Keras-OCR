<h1 align=center> Keras-OCR</h1>
سيعلمك هذا المرجع كيفية استخدام Keras-OCR لاستخراج النصوص من المستند<br>
(This reference will teach you how to use Keras-OCR for extracting texts from an image)

## خطوات(Steps)
**1. قم بتثبيت  OpenCV**  
(Install OpenCV)
```
pip install opencv-python
```

**2. تثبيت Keras-OCR**  
(Install Keras-OCR)
```
pip install keras-ocr
```
**3. قم بتشغيل الكود أدناه**
(Run The Below Code)
```
import keras_ocr
import matplotlib.pyplot as plt
import cv2

# Step 1: Set up the keras-ocr pipeline
pipeline = keras_ocr.pipeline.Pipeline()

# Step 2: Load the image (replace with your document image path)
image_path = 'img.jpeg'
image = keras_ocr.tools.read(image_path)  # Load image

# Step 3: Perform OCR on the image
predictions = pipeline.recognize([image])  # Perform text recognition

# Step 4: Print Detected Text
print("Detected Text:")
for text, box in predictions[0]:  # predictions[0] since we processed one image
    print(f"Text: {text}")
    
# Step 5: Visualize the results
# Create a copy of the image to draw the boxes and text
image_with_boxes = image.copy()

for text, box in predictions[0]:  # predictions[0] since we processed one image
    # Draw the bounding box
    box = box.astype(int)  # Convert box coordinates to integer
    cv2.polylines(image_with_boxes, [box], isClosed=True, color=(0, 255, 0), thickness=2)
    # Put the detected text near the top-left of the bounding box
    cv2.putText(
        image_with_boxes,
        text,
        (box[0][0], box[0][1] - 10),  # Slightly above the top-left corner of the box
        fontFace=cv2.FONT_HERSHEY_SIMPLEX,
        fontScale=1.5,
        color=(255, 0, 0),
        thickness=1,
    )

# Step 5: Display the image with bounding boxes and detected text
plt.figure(figsize=(10, 10))
plt.imshow(cv2.cvtColor(image_with_boxes, cv2.COLOR_BGR2RGB))  # Convert BGR to RGB for correct colors
plt.axis('off')  # Turn off axis
plt.title("Detected Text and Bounding Boxes")
plt.show()
```
