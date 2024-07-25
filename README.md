# Chest_Cancer_Classification_CTScan_Jenkins_AWS

### In this computer vision project, our objective is to classify based on the CT scan images as having cancer or not. We are classifying the CT scan image as 'Normal' or for 'Adinocarcinoma' cancer. The image below illustrates the same.

![Local Deploy](https://github.com/therealabhishek/Chest_Cancer_Classification_CTScan_Jenkins_AWS/blob/main/cc_assets/local_deploy.PNG)

### Why do we need this Chest Cancer Classification app using AI and how can we achieve it?

- Traditionally, the CT scans have been interpreted by the radiologists.

- But, when the radiologist is overburdened, we may need to find faster ways to for the CT scans to be interpreted.

- Thus, we can use state of the art computer vision models to classify whether the patterns are there in the image for a particular disease, in this case a type of chest cancer.

- Such type of solutions will definately help relieve the burden on radiologists and their expertise can be used for more critical cases.

- A lot of care also needs to be taken while developing such applications, e.g. we need to take care that our app does not classify people having cancer as not having cancer, it may lead to unwanted situations.

### STEPS INVOLVED IN THE PROJECT:

- Data Ingestion

In data ingestion, we can use many ways to ingest the data eg. S3 bucket etc. 

But, for our project, we shall be storing our data in Google Drive and ingestion the data from there.

The data from the google drive will be downloaded in the form of a zip file in the artifacts folder, the file will then be unzipped so that we can further use the data.


- Base Model Preparation

We shall be using the VGG-16 model for our project, although there are amny models that can be used.

Here, we shall be using the transfer learning approach, where, we shall use the weights of the imagenet dataset used for VGG-16 in our project as well.

We will modify the dense layers in VGG-16 suited to our project, namely, changing the number of classes from 1000 to 2, changing the batch size, learning rate etc.


- Model Trainer Stage

In the model trainer stage, we are training the model on our available data. 

As we are training the model using a cpu, we shall just train it for a single epoch.

We shall perform runtime train test split on the data that we have saved during data ingestion.

While preparing the model trainer, we have scaled the data, also, we have applied various data augumentation techniques, then we have split the data as 80% train and 20% validation. 

As we have considered only a single epoch, we are getting very low model metrics.

The trained model has been saved under training directory which is under artifacts directory.


- Model Evaluation Stage

  ![Model Evaluation](https://github.com/therealabhishek/Chest_Cancer_Classification_CTScan_Jenkins_AWS/blob/main/cc_assets/dagshub_mlflow_1.PNG)

  ![Model Evaluation](https://github.com/therealabhishek/Chest_Cancer_Classification_CTScan_Jenkins_AWS/blob/main/cc_assets/dagshub_mlflow_2.PNG)


In the model evaluation stage, we are considering 30% of our data.

Here, we are considering multiple experiments by changing some model parameters.

We are tracking the model parameters and model metrics using Mlflow via Dagshub.

- Pipeline Tracking using DVC

Using DVC, we are tracking project execution pipeline.

The pipeline tracking avoids the re-running of already executed code unless there are any changes.

The image below shows the DVC DAG, which shows the relationship between the pipeline components.

  ![Pipeline Tracking](https://github.com/therealabhishek/Chest_Cancer_Classification_CTScan_Jenkins_AWS/blob/main/cc_assets/dvcdag.PNG)