Word Segmentation Utilizing the Scale Space Technique

This algorithm processes an image containing text and produces the identified words as output. Additionally, the words can be organized based on their reading sequence (from top to bottom and left to right).



Installation
Navigate to the root directory of the repository.
Run the command pip install .
Access the tests/ directory and execute pytest to verify the installation.

Usage
This example demonstrates the loading of an image featuring a line of text, its preparation for the detection process (1), the identification of words (2), their organization (3), and the display of the cropped words (4).

from word_detector import prepare_img, detect, sort_line
import matplotlib.pyplot as plt
import cv2

# (1) Prepare the image:
# (1a) Convert to grayscale
# (1b) Scale to the specified height, as the algorithm is not invariant to scale
img = prepare_img(cv2.imread('data/line/0.png'), 50)

# (2) Detect words within the image
detections = detect(img,
                    kernel_size=25,
                    sigma=11,
                    theta=7,
                    min_area=100)

# (3) Organize words in the line
line = sort_line(detections)[0]

# (4) Display word images
plt.subplot(len(line), 1, 1)
plt.imshow(img, cmap='gray')
for i, word in enumerate(line):
  print(word.bbox)
  plt.subplot(len(line), 1, i + 2)
  plt.imshow(word.img, cmap='gray')
plt.show()

The repository includes several examples illustrating the usage of the package:

Install dependencies: pip install -r requirements.txt
Navigate to examples/
Execute python main.py to detect words in line images (IAM dataset).
Alternatively, run python main.py --data ../data/page --img_height 1000 --theta 5 to apply the detector on a page image (also from the IAM dataset).

The package comprises the following functions:

prepare_img: Prepares the input image for detection.
detect: Identifies words within the image.
sort_line: Organizes words in a single line.
sort_multiline: Groups words into lines and sorts each line individually.
For further information regarding the functions and their parameters, utilize help(function_name), for instance, help(detect).

Algorithm
The diagram below illustrates the operational process of the algorithm:

top left: input image
top right: applied.
