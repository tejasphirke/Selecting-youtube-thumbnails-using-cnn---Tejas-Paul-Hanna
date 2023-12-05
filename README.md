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

