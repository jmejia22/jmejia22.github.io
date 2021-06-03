---
layout: post
title: Project Reflection
---

### Overall, what did you achieve in your project? 
In my project, I created a meaningful, life impacting tool that can be used at the intersection of data science, machine learning, and neurology. I learned how data science tools can be utilized in the clinical setting and hopefully one day be used to save lives and detect brain tumors in MRI images before they become terminal. Furthermore, I achieved a plethora of new data science skills that I feel can be applied to any projects I work on in the future. 

###  What are two aspects of your project that you are especially proud of? 
An aspect of my project that I am especially proud of is the results that we got from our implemented convolutional neural network model. When building our model structure, we ran into various issues and had to research, debug, and preprocess our data in such a way that it was compatible with our model. I was happy to see that we were able to classify images correctly about 94% of the time since in the real world our model has the potential to save someone's life thus accurate results are a necessity. It was fulfilling knowing that we had built a model that could make a difference. Another aspect of my project that I am especially proud of is the way in which we dealt with machine learning bias. We could have simply trained the model on all of the data we had, however, we took the initiative to make sure we had an equal number of samples for each target class. I am proud of the realistic image augmentations that we created and overall how we built a model that is not biased towards any one class.

### What are two things you would suggest doing to further improve your project? 
One thing that I would suggest doing to further improve my project is changing the manner in which we predict tumor position. We used a linear regression model that was effective in predicting the location of tumors for some images however not all. I hypothesize that our linear regression approach would work well if all images were taken at the same angle (ex side view, top down, etc). One approach that I would suggest to improve upon our method of predicting tumor position would be to utilize the convolutional layers from our CNN model which might be helpful in indicating where a tumor might be. The performance of this new method would be not be hindered by the angle at which the image is taken at and would thus be an improvement to our current model. An additional improvement that I would suggest would be to have different models for different image angles. For instance, if we trained a model with only images that were taken from a side view, top down view, etc then we might get even better results since our model would easily be able to distinguish which tumor is occuring where. This implementation might be difficult since there don't exist data sets that are well separated so we would somehow have to find a way to classify image angle. 

### How does what you achieved compare to what you set out to do in your proposal? 
With regards to what we wanted to achieve based on our proposal, we were able to achieve what we deemed as "half-success" (a code repository on Github that demonstrates the machine learning pipeline we created which could be used by others should they want to use or build upon our algorithm). We were unable to build the web application in which users could upload an image and get a result due to us only being a team of two, the amount of time it took to build our machine learning pipeline, and the responsibilities demanded by other classes. A personal goal that I have in mind is to complete the web app sometime this summer so that I have a refined space to show what I was able to achieve through this project.

### What are three things you learned from the experience of completing your project?
Three of the most significant things that I learned from the experience of completing my project were: creating complex convolutional neural networks using `Keras` and `Tensorflow` capable of classifying images accurately, image augmentation techniques, and applying previously learned machine learning algorithms like linear regression to predict important positions within images. 

### How will your experience completing this project help you in your future studies or career? 
One of the most important skills that I think this project taught me is to be patient when it comes to coding. Throughout this project I ran into plenty of error messages, bugs, etc and thought that I wasn't going to be able to figure out the problem at times. However, this project gave me the confidence to debug large blocks of code and pinpoint areas where things were going wrong. As an aspiring computer/data scientist, this skill will surely help me because when I approach new problems and run into difficulties, I can reflect on this project and know that I will figure out the obstacles I am presented with. Lastly, this project has also given me the confidence to attack large, complicated projects. When first starting the project it was intimidating thinking about all the tasks that had to get done however in the end they were all accomplished. Through this project, I have gained confidence in my overall abilities which will help me tremendously in my career. 


```python

```
