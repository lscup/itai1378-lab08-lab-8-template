# Lab 8: Interactive Image Processing Application

Welcome to Lab 8! In this lab, you'll build an interactive image processing application using OpenCV, Matplotlib, and ipywidgets in a Jupyter Notebook environment. You'll create a user-friendly interface with controls for image browsing, processing, and visualization.

### Objectives
- Understand how to integrate OpenCV and Matplotlib for image processing in Python.
- Learn to use ipywidgets for creating interactive controls in Jupyter Notebooks.
- Implement real-time image processing operations like grayscale conversion, brightness adjustment, resizing, and rotation.

### Prerequisites
- Basic understanding of Python programming.
- Familiarity with Jupyter Notebooks.
- Introduction to image processing concepts.

---

## 2. Algorithm/Concept Background
Image processing involves performing operations on images to enhance or extract information. In this lab, you'll use OpenCV, a powerful library for computer vision tasks, and Matplotlib for visualization. ipywidgets will help create interactive UI elements.

### Key Concepts
- **OpenCV**: A library for real-time computer vision. Used for reading, processing, and saving images.
- **Matplotlib**: A plotting library for visualizing images and data.
- **ipywidgets**: A library for creating interactive widgets in Jupyter Notebooks.

Below is a simple example demonstrating image loading and displaying using OpenCV and Matplotlib:
```python
import cv2
import matplotlib.pyplot as plt

# Load an image using OpenCV
image_bgr = cv2.imread('example.jpg')
# Convert to RGB (OpenCV loads images in BGR)
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)

# Display using Matplotlib
plt.imshow(image_rgb)
plt.axis('off')
plt.show()
```

**Important Properties**
| Property | Description |
|----------|-------------|
| Time Complexity | Varies per operation (e.g., O(n) for pixel-wise operations) |
| Key Libraries | OpenCV, Matplotlib, ipywidgets |

---

## 3. Your Coding Environment

### Workspace Layout
| Area | What It Does |
|------|--------------|
| Code Editor (left) | Edit your files using the tabbed editor |
| Terminal (right) | See output when you click the **Run** button |
| AI Tutor (chat panel) | Ask your AI Tutor for help — it knows this lab and can guide you step by step |

### Workflow
1. Edit your code in the editor tabs
2. Click **Run** to execute and see output in the terminal
3. When ready, click **Commit** to save your work to GitHub and trigger the autograder
4. A ✅ (green check) or ❌ (red X) will appear showing whether tests passed

*Tip: Commit early and often to track your progress!*

---

## 4. Project Structure
```plaintext
/
├── notebook.ipynb  # YOUR WORK
└── README.md       # your lab report
```

---

## 5. Step-by-Step Implementation

### Step 1: Import Libraries and Initialize
Start by importing the necessary libraries and setting up global variables and output areas.
```python
# Import necessary libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
import ipywidgets as widgets
from IPython.display import display, clear_output

# Initialize global variables
original_bgr = None
original_rgb = None
processed_rgb = None

# Create output areas
msg_out = widgets.Output()
img_out = widgets.Output()
hist_out = widgets.Output()
```
This code sets up the environment required for image processing and displaying results.

### Step 2: Define Helper Functions
Create functions to display images and histograms.
```python
def show_images(original_rgb, processed_rgb):
    """
    Display the original and processed images side by side.
    """
    with img_out:
        clear_output(wait=True)
        fig, axes = plt.subplots(1, 2, figsize=(10, 5))
        axes[0].imshow(original_rgb)
        axes[0].set_title('Original Image')
        axes[0].axis('off')
        axes[1].imshow(processed_rgb)
        axes[1].set_title('Processed Image')
        axes[1].axis('off')
        plt.show()
```
This function clears previous output and displays the two images side by side.

### Step 3: Implement Callbacks
Define callback functions for the interactive controls. For example, implement the callback to browse and load an image:
```python
def browse_image_callback(change):
    """
    Callback function to browse and load an image
    """
    from google.colab import files
    uploaded = files.upload()
    if uploaded:
        for filename in uploaded:
            global original_bgr, original_rgb, processed_rgb
            original_bgr = cv2.imread(filename)
            if original_bgr is not None:
                original_rgb = cv2.cvtColor(original_bgr, cv2.COLOR_BGR2RGB)
                processed_rgb = original_rgb.copy()
                show_images(original_rgb, processed_rgb)
                with msg_out:
                    clear_output(wait=True)
                    print(f"Image '{filename}' loaded successfully.")
            else:
                with msg_out:
                    clear_output(wait=True)
                    print("Failed to load image.")
```
This function allows users to upload an image and updates the interface with the loaded image.

### Step 4: Create and Connect Controls
Create controls using ipywidgets and connect them to their respective callback functions.
```python
# Define controls
browse_btn = widgets.Button(description='Browse Image')
# Connect controls to their callback functions
browse_btn.on_click(browse_image_callback)

# Arrange layout and display
controls = widgets.VBox([browse_btn])
layout = widgets.HBox([controls])
display(layout)
```
This code snippet creates a button for browsing an image and connects it to the `browse_image_callback` function.

Continue implementing other controls and callbacks similarly. Once all steps are completed, the application should be interactive and ready for use.

### Complete Solution
Here is the complete implementation for your reference:
```python
# (Complete solution code here)
```

---

## 6. Testing Your Code

### Run Your Code
Click **Run** to execute and check the output in the terminal.

### Submit for Grading
Click **Commit**, enter a message, and look for ✅ or ❌.

Expected output:
```plaintext
Welcome! Click 'Browse Image' to start.
```

---

## 7. Autograding

| Test | Points | What It Checks |
|------|--------|----------------|
| Syntax Check | 20 | Ensures there are no syntax errors in the notebook |
| Browse Image Functionality | 20 | Tests if image loading works correctly |
| Convert to Grayscale | 20 | Checks grayscale conversion functionality |
| Adjust Brightness | 15 | Tests brightness adjustment |
| Resize Image | 15 | Checks image resizing functionality |
| Save Image | 10 | Ensures the image is saved correctly |

Total Points: 100

---

## 8. Lab Report

Click the README.md tab and fill in your lab report.

```markdown
# Lab 8 Report

## Student Information
- **Name**: 
- **Date**: 

## Key Concepts
- Describe the role of each library used in this lab.

## Tracing/Analysis
- Provide a detailed analysis of an image processing function implemented.

## Complexity or Performance Analysis
| Function | Time Complexity | Space Complexity |
|----------|-----------------|------------------|
| Function Name | O(n) | O(1) |

## Reflection Questions
1. What was the most challenging part of this lab?
2. How did you ensure the interactive components work smoothly?
3. What improvements would you suggest for this application?
```

---

## 9. Submission Checklist

- [ ] All functions implemented
- [ ] Click Run — output matches expected
- [ ] Click Commit — autograder shows green check
- [ ] Lab report completed in README.md
- [ ] Final commit with completed lab report

---

Good luck with your lab, and remember to ask your AI Tutor if you need any help!