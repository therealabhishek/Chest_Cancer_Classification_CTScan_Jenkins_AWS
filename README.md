# Chest_Cancer_Classification_CTScan_Jenkins_AWS

### In this computer vision project, our objective is to classify based on the CT scan images as having cancer or not.

### Why do we need this Chest Cancer Classification app using AI and how can we achieve it?

- Traditionally, the CT scans have been interpreted by the radiologists.

- But, when the radiologist is overburdened, we may need to find faster ways to for the CT scans to be interpreted.

- Thus, we can use state of the art computer vision models to classify whether the patterns are there in the image for a particular disease, in this case a type of chest cancer.

- Such type of solutions will definately help relieve the burden on radiologists and their expertise can be used for more critical cases.

- A lot of care also needs to be taken while developing such applications, e.g. we need to take care that our app does not classify people having cancer as not having cancer, it may lead to unwanted situations.

### STEPS INVOLVED IN THE PROJECT:

1. Data Ingestion

In data ingestion, we can use many ways to ingest the data eg. S3 bucket etc. 

But, for our project, we shall be storing our data in Google Drive and ingestion the data from there.

The data from the google drive will be downloaded in the form of a zip file in the artifacts folder, the file will then be unzipped so that we can further use the data.


2. Base Model Preparation

We shall be using the VGG-16 model for our project, although there are amny models that can be used.

Here, we shall be using the transfer learning approach, where, we shall use the weights of the imagenet dataset used for VGG-16 in our project as well.

We will modify the dense layers in VGG-16 suited to our project, namely, changing the number of classes from 1000 to 2, changing the batch size, learning rate etc.