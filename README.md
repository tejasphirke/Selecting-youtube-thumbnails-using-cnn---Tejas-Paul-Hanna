# Selecting Youtube Video Thumbnails by Convolutional Neural Networks
### CSCI6366 Neural Network and Deep Learning Project

### Teammates
#### Hanna Song, Tejas Phirke, Paul Derisemu

### Introduction

We are using a model based on research already done by the CS dept of Stanford University. We are planning to build a model that will select the best thumbnail from the frames of a given video. We are going to train the model with both successful and unsuccessful videos and their respective thumbnails to extract the features that indicate the success of a video. We will differentiate successful vs unsuccessful videos based on the number of views the video acquired. Any video with more than 1M views is considered successful and videos less than 1000 views are considered unsuccessful.

To mitigate the selection bias, we will collect the videos data in the same time frame, randomly build datasets for successful and unsuccessful thumbnails and then we will build a classifier to differentiate between successful and unsuccessful thumbnails. From the learnings of this classification architecture we will build a model that will select thumbnails by choosing from each video the frames that have the highest probability of being good thumbnails.

### Research on the project

- Selecting Youtube Video Thumbnails via Convolutional Neural Networks
chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/http://cs231n.stanford.edu/reports/2017/pdfs/710.pdf

The paper presents a convolutional neural network approach for selecting high-quality YouTube video thumbnails by first training a model to classify thumbnails as "good" or "bad", and then using the model they score and rank frames from a video to pick the best thumbnail. 
	
- Automatically generate thumbnails, animated gifs and summary from youtube videos : https://github.com/yahoo/hecate
Thumbnail Selection with Convolutional Neural Network Based on Emotion Detection 
https://dergipark.org.tr/en/download/article-file/1652393

From the frames in the video it will convert frames to images. Based on small images it will preprocess the images of the people and it will detect the emotions of the people based on the repeating faces in the images
Creating cover photos of a movie or TV series using image processing and convolutional neural networks. These cover photos were selected based on mpst repeating faces and frames were labeled to attract the users' attention.

### Project Questions
Based on the YouTube channels which thumbnails represent which channel?
Given the YouTube channels, which thumbnails are considered ‘good’ for getting a better view?
How CNN could be used on the thumbnails and by using the model how we can predict the labels for the images?


### Modeling Process

#### Step 1 - Exploration of the data:

We currently have a dataset available with good thumbnails which has the highest number of views and high subscriber counts: 

Our data preparation initially starts with getting the feasible datasets for our project. We got the dataset from kaggle and based on the Youtube API datasets we will get Youtube channels with lower views, as we want to test the lower views dataset. 

Datasets we will be using and the dataset we have: 

- Dataset of good thumbnails as of now, but we are currently scraping at bad thumbnails that have low views
- Train classifier to distinguish between two categories.

For the dataset available, we have explored the following things:

The dataset contains two files: 
- One data file named ‘data’ contains all YouTube URLs, channel names, category, titles, views, subscriber counts, year, YouTube ID (by using youtube id we can fetch YouTube video).
- Second file named ‘metadata’ which contains youtube id, channel name, category and title

Dataset link: 
https://www.kaggle.com/datasets/praneshmukhopadhyay/youtube-thumbnail-dataset/data
https://www.kaggle.com/datasets/praneshmukhopadhyay/youtubers-saying-things/data

We have done preprocessing of the dataset:

- Removed unwanted paragraphs, special characters that were present in the data. Removing URLs, and numbers in the dataset. After cleaning the dataset we left with 2048 rows. 
It is shared with a cleaned dataset file named clean_data_1’ which is a clean dataset. The metadata file contains 2516 rows.
- We merged two datasets:  data and metadata based on the youtube id named ‘merged_data_metadata’. 
Now we are left with 2015 rows, which means we have the data with YouTube id’s as well as URLs.

(Future Steps at December 4th, 2023)

#### Step 2 - Pre-Training the thumbnails using transfer learning:

We have a “generated thumbnails” folder which contains generated thumbnails based on the cleaned merged data for 2015 rows. We will use those for testing because those images are not classified based on the YouTube channels. 

We will train images from the Kaggle (https://www.kaggle.com/datasets/praneshmukhopadhyay/youtube-thumbnail-dataset/data) and generated thumbnails (https://drive.google.com/drive/folders/1hmNbjIaTWUoHGVL1fUmsXfapLFhcALYj). In the thumbnails folder, we have 91 folders each one presenting channels and those channels contain the images for their respective channels.

Using the transfer learning, we will follow the below steps:

1. Pre-training models using VGG16 or inception V3 has not been decided yet.
2. Remove the final classification layer(s) of the pre-trained model.
3. Add new layers that match the number of classes in your dataset.
4. Fine-tune the model on your dataset.


#### Step 3 - Tuning the model

We will train the CNN model using tensorflow keras API for image classification. General steps that need to be done:

1. Setting the dimensions for input images to be 224x224 pixels. Using an  ImageDataGenerator to perform data augmentation on the training images. This will include rescaling, shearing, zooming, and horizontal flipping.

2. Creating a generator for the training dataset with specified parameters like target size, batch size, and categorical class mode.

3. Creating a generator for the validation dataset with rescaling as the only augmentation.

4. Setting up a CNN architecture, preparing data generators with augmentation, and training the model on the dataset for image classification.
