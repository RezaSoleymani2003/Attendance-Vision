# Attendance Vision

## Introduction

For one of my college classes, I was responsible for taking student attendance using a printed checklist sheet, then manually entering the data into a Google Sheet for the professor.

To automate this repetitive task, I built **Attendance Vision** — a computer vision tool powered by a **Convolutional Neural Network (CNN)**. It takes an image of an attendance column, detects which checkboxes are marked, and automatically writes the results to a Google Sheet.

## Requirements


## Input And Output
The input to the CNN is a 128x4096 image of a column containing attendance checkboxes:


<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/720de306-af1f-4197-99b6-4cf9680d60e5" width="90"/><br/>
      <sub>Image 1: Raw Attendance Column</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f62f871a-ac5b-49f6-a116-59f781e8d061" width="90"/><br/>
      <sub>Image 2: Preprocessed Sample</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/fb573c70-7a96-41d0-87d4-f263e5c4efe2" width="90"/><br/>
      <sub>Image 3: Augmented Image</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ba46250f-cf43-4051-ab2e-d1b1f62d4e2d" width="90"/><br/>
      <sub>Image 4: Model Training Sample</sub>
    </td>
  </tr>
</table>

I give an image like these to the model, then it cuts the image to different checkboxes (using fixed height segments) and classifies each one. Then enters the attendance to the google sheet i provided.I also need to specify the start cell.

## The Model
As mentioned, I use a CNN 
