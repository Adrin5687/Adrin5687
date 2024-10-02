import cv2
import numpy as np
from moviepy.editor import ImageSequenceClip

# Function to create an image with text
def create_slide(text, filename, width=640, height=480, bg_color=(255, 255, 255), text_color=(0, 0, 0)):
    image = np.zeros((height, width, 3), dtype=np.uint8)
    image[:] = bg_color

    # Set font and text position
    font = cv2.FONT_HERSHEY_SIMPLEX
    font_scale = 1
    thickness = 2
    text_size = cv2.getTextSize(text, font, font_scale, thickness)[0]
    text_x = (width - text_size[0]) // 2
    text_y = (height + text_size[1]) // 2

    # Add text to the image
    cv2.putText(image, text, (text_x, text_y), font, font_scale, text_color, thickness)

    # Save the image
    cv2.imwrite(filename, image)

# Create slides
slides = [
    ("Welcome to the World of Ham!", "slide1.png"),
    ("Types of Ham:\n1. Prosciutto\n2. Black Forest\n3. Honey Baked", "slide2.png"),
    ("How Ham is Made:\nCuring & Smoking Process", "slide3.png"),
    ("Culinary Uses:\nSandwiches, Salads, and more!", "slide4.png"),
    ("Thank You for Watching!", "slide5.png")
]

for text, filename in slides:
    create_slide(text, filename)

# Create a video from the slides
clip = ImageSequenceClip([f"slide{i+1}.png" for i in range(len(slides))], fps=1)
clip.write_videofile("ham_video.mp4", codec="libx264")
<!---
Adrin5687/Adrin5687 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
