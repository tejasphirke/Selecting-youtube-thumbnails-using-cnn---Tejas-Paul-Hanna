# Selecting Youtube Video Thumbnails by Convolutional Neural Networks
### CSCI6366 Neural Network and Deep Learning Project

### Teammates
#### Hanna Song, Tejas Phirke, Paul Derisemu

### Introduction

We are using a model based on research already done by the CS dept of Stanford University. Based on this model, our project aims to build a model that will predict if the thumbnail of a Youtube video will be a good or bad thumbnail. 

For training the model, we have popular channels videos with high views – around 1M– dataset from kaggle (which are considered as good thumbnails in our dataset), and randomly select channels that have subscribers lower than 100K with low views – 1000 to 10,000 –- (which are considered as bad thumbnails). Using this model, we also test on new random videos that are randomly collected from Youtube which have both high and low views. 

Further steps, we used our initial model onto subcategories of news for getting a prediction on good or bad thumbnail by training category’s good and bad thumbnails.

The below output shows that label is good or bad based.
![demo_image](https://raw.githubusercontent.com/tejasphirke/Selecting-youtube-thumbnails-using-cnn---Tejas-Paul-Hanna/main/demo_img.jpg)


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
1. Based on the YouTube popular channels, how can we select thumbnails for new videos to be on trend?
2. Given the Youtube channels, which thumbnails are considered as good for getting a better view?
3. How CNN could be used on predicting labels of thumbnails?


### Modeling Process

#### Step 1 - Exploration of the data:

For datasets, we have collected directly from Youtube API and used Kaggle dataset of Youtube Popular channel videos. 

** Dataset Descriptions**:

Kaggle Dataset used for considered as a good thumbnail train dataset

https://www.kaggle.com/datasets/praneshmukhopadhyay/youtube-thumbnail-dataset/data
https://www.kaggle.com/datasets/praneshmukhopadhyay/youtubers-saying-things/data

Two other datasets are directly collected from Youtube which randomly selected by manually:
Low subscriber numbers and low views considered: bad thumbnail train dataset
Mixed of high and low subscriber numbers and views considered: test dataset

Datasets contain following information: 
YouTube URLs, channel names, category, titles, views, subscriber counts, year, YouTube ID

** Datasets**:
Csv files
Clean_data1.csv: Kaggle dataset with preprocessing for generating thumbnails
Bad_yt1.csv: collected bad videos from Youtube API
Bad_yt_label.csv: preprocessing bad videos with labeled
Final_yt_data.csv: collected good videos from Youtube API
Good_org_label.csv: preprocessing good videos with labeled
News_bad.csv: low subscribers and views
Good_news.csv: high subscribers and views

Folders for thumbnails
Validation thumbnails: Kaggle dataset from clean_data1.csv
Good thumbnails: from Good_org_label.csv
Bad thumbnails: Bad_yt_label.csv
Img_good: good thumbnails on news
Img_bad: bad thumbnails on news
Sky_news: random news thumbnails

**Preprocessing the datasets**:

Remove unwanted rows, columns, and special characters that were present in the data. 
Merge datasets if needed
Generate thumbnails by using video url with python library and functions
Label good or bad thumbnails for train and test datasets

#### Step 2 - Modeling

For modeling, we used good thumbnails from the Kaggle dataset and bad thumbnails that we collected. There are 212 categories each channel containing the images for their videos. 

We will train the CNN model and VGG16 using tensorflow for image classification.
General steps that we proceed:

1. Setting the dimensions for input images to be 224x224 pixels. Using an  ImageDataGenerator to perform data augmentation on the training images. This will include rescaling, shearing, zooming, and horizontal flipping.

2. Creating a generator for the training dataset with specified parameters like target size, batch size, and categorical class mode.

3. Creating a generator for the validation dataset with rescaling as the only augmentation.

4. Setting up a CNN architecture, preparing data generators with augmentation, and training the model on the dataset for image classification.

5. Repeat for VGG16 model

#### Step 3 - Prediction on random thumbnails

With CNN model and VGG16 model, we predicted if the random thumbnails with label matches with our predictions. 


#### Results/Conclusions

For our model layers, we have used input shapes of 224, 224, activation of relu, optimizer of  adam, max pooling, dropout of 0.2 with 9 dense layers. 
Compared to CNN model, VGG16 has better fit of loss while both have similar accuracy of around 75.%. However, limitations on VGG16 we could not proceed with comparison on news datasets. We proceed on CNN model which we got accuracy of around 93%. 


#### Limitations

We tried to mitigate the selection bias with selecting a certain time frame, however, Youtube API is hard to collect within the timeframe. Instead, we have used a number of views and subscribers to mitigate the bias with good and bad thumbnails. Further approach, we will generate more thumbnails with certain time frames to build a classifier to differentiate successful and unsuccessful thumbnails. 

Additionally, limitations on GPU restricted us to get results on VGG16 for subcategories. When we will build this model in the future, we will need to increase our GPU for accuracy.

