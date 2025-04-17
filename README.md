# Attendance Vision

## Introduction

For one of my college classes, I was responsible for taking student attendance using a printed checklist sheet, then manually entering the data into a Google Sheet for the professor.

Inspired by this, I built **Attendance Vision** — a computer vision model powered by a **Convolutional Neural Network (CNN)**. It takes an image of an attendance column, detects which checkboxes are marked, and automatically writes the results to a Google Sheet.

It has an accuracy of about **95%** on test data and generalizes well.  
In some cases, the model misclassifies even clearly marked checkboxes. This usually happens with checkboxes that differ significantly in style, size, or alignment compared to those in the training set. Improving this would require more diverse training data or additional preprocessing.

## Requirements

- Python 3.x  
- TensorFlow  
- NumPy  
- OpenCV  
- gspread  
- Google Auth (for Sheets integration)

## Input and Output

The input to the CNN is a `128x4096` image of a column containing attendance checkboxes:

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/720de306-af1f-4197-99b6-4cf9680d60e5" width="90"/><br/>
      <sub>Sample Input 1</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f62f871a-ac5b-49f6-a116-59f781e8d061" width="90"/><br/>
      <sub>Sample Input 2</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/fb573c70-7a96-41d0-87d4-f263e5c4efe2" width="90"/><br/>
      <sub>Sample Input 3</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ba46250f-cf43-4051-ab2e-d1b1f62d4e2d" width="90"/><br/>
      <sub>Sample Input 4</sub>
    </td>
  </tr>
</table>

I give an image like these to the model. Then it slices the image into 128x128 segments and classifies each one. Afterward, it writes the attendance to the Google Sheet I provided. I also specify the start cell.

## Generating Data and Augmentation

A `128x4096` checkbox column image is sliced into 32 `128x128` checkbox images. These are saved in their appropriate folders.

Since I didn’t have much training data initially, I used data augmentation. After extracting checkbox images from the training data, I created 5 new samples per checkbox by randomly zooming, shifting, and brightening or darkening them.

## The Model

Initially, I tried a regular neural network (MLP), but it didn’t perform well. Switching to a CNN significantly improved accuracy.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a1d976df-b8ed-4d52-8d9c-5f376980b248" alt="the_last_model_architecture">
</p>

I trained it for **10 epochs** using **902** training samples and **181** test samples.

I experimented with different architectures and datasets. This one gave the best result, saved as **the_last_model.h5**. Some other models are also saved in the project folder.

## Accuracy and Generalization

Although the model shows some signs of overfitting, it performs well in real use cases. That’s mostly because both the training and input images follow a consistent structure.

Still, some obvious checkboxes may be misclassified, especially if they differ in style or alignment.

## Using the Model

In the output folder, I included some images that aren’t part of the training or test data. The model:

1. Predicts each checkbox
2. Saves the checked ones in `output-checkfolder` and unchecked ones in `output-uncheckfolder`
3. Writes the attendance to a Google Sheet

To allow writing, I created a Google **Service Account** and added it as an **editor** to the sheet. The start cell can be specified.

Here's the bot :

![bot](https://github.com/user-attachments/assets/17acf7f5-40a7-4410-b1ba-880140d2c4b0)


## Demo

As seen below, I used 2 images — `final3` and `final4`.  
First, the model slices them into checkboxes and saves them to the output folder. Then it predicts each one and saves them accordingly.

In this example, one checked box was misclassified as unchecked.

Then the model writes attendance to a Google Sheet called **Sample Attendance**, starting at cell `W2`.

> Note: `final4` is written first.

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/1852b7ea-b094-4bc5-a46a-3346ade5ce38" width="90"/><br/>
      <sub>final3</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/9013a07a-a72a-467c-8531-7c447b8cd9e1" width="90"/><br/>
      <sub>final4</sub>
    </td>
  </tr>
</table>

🎥 [Video Demo](https://github.com/user-attachments/assets/9e3eefbe-7fdc-49de-a614-c4239eef0ce3)

📄 [View Sheet](https://docs.google.com/spreadsheets/d/1M-Neh3nGHSXbEVnhWBz5aAZYTcTsWpbCQ3SmS0fH-XU/edit?gid=0#gid=0)

## Conclusion

The model has learned well and generalizes to the task.  
The main challenge was the lack of training data — which causes occasional misclassifications — but overall, it works well for this specific use case.
