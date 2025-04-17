# Attendance Vision

## Introduction

For one of my college classes, I was responsible for taking student attendance using a printed checklist sheet, then manually entering the data into a Google Sheet for the professor.

To automate this, I built **Attendance Vision** — a computer vision tool powered by a **Convolutional Neural Network (CNN)**. It takes an image of an attendance column, detects which checkboxes are marked, and automatically writes the results to a Google Sheet.

It has an accuracy of about 95% on test data and generallizes good.
In some cases, the model misclassifies even clearly marked checkboxes. This usually happens with checkboxes that differ significantly in style, size, or alignment compared to those in the training set. Improving this would require more diverse training data or additional preprocessing.

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

## Generating Data And Augemntation
An 128x4096 checkbox column image is sliced to 32 128x128 checkbix image. The images are saved in their appropriate folder.

I also had to augment some images based on the original images, because I didn't have much train data in the first place. Most of the train data is augmented. After extracting the train data's checkboxes, I made 5 new checkboxes for each train sample by randomly zooming, shofting and brighten or darkening the checkbox image. 

## The Model
Initially, I experimented with a normal neural network (MLP), but it didn't yeild good results. Switching to a Convolutional Neural Network (CNN) significantly improved the accuracy.
This is my model's architecture: 
<p align="center">
  <img src="https://github.com/user-attachments/assets/a1d976df-b8ed-4d52-8d9c-5f376980b248" alt="the_last_model_architecture">
</p>

I trained it for 16 epochs and train data of 902 checkbox images and test data of 181 images.

I experimented with different architecrures and traind data, this was my best result. I saved it as final_model.h5. The were some other good models that I saved on the project folder.

## Accuracy And Generalization
Although the model shows signs of overfitting, it still performs well in real use cases. This is largely because both the training data and real-world input follow the same consistent format. The model is designed for this specific task. So in general ot works good in this problem.

## Using The Model
In the output folder, I created some new images that are not in the train and test data. The model predicts each checkbox and copies each one in the appropriate folder. Then it writes the attendence in a google sheet.
To do that, a google **Service Account** was created and added as an **editor** to the attendance sheet.
The model writes predictions directly to the sheet using the **Google Sheets API**.
Start cell is specified for where attendance should be written.
