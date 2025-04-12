# Attendance Vision

## Introduction

For one of my college classes, I was responsible for taking student attendance using a printed checklist sheet, then manually entering the data into a Google Sheet for the professor.

To automate this repetitive task, I built **Attendance Vision** — a computer vision tool powered by a **Convolutional Neural Network (CNN)**. It takes an image of an attendance column, detects which checkboxes are marked, and automatically writes the results to a Google Sheet.

## Requirements


## Input
The input to the CNN is a 128x4096 image of a column containing attendance checkboxes:

<div style="display: flex; justify-content: center; gap: 20px;">
  <div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/720de306-af1f-4197-99b6-4cf9680d60e5" width="20"/>
    <div>Image 1: Raw Attendance Column</div>
  </div>
  <div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/f62f871a-ac5b-49f6-a116-59f781e8d061" width="20"/>
    <div>Image 2: Preprocessed Sample</div>
  </div>
  <div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/fb573c70-7a96-41d0-87d4-f263e5c4efe2" width="20"/>
    <div>Image 3: Augmented Image</div>
  </div>
  <div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/e110d772-e99f-491c-99ef-7a8005da1a51" width="20"/>
    <div>Image 4: Model Training Sample</div>
  </div>
</div>


