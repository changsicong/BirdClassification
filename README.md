# Bird Identification  
### Problem description 
This project is to classify bird images of 555 kinds.

### DataSet
Our dataset includes 7.42G training images and 1.92G testing images. The training images of one type are in different folders. We also have a csv file which maps each folder to a type name.

### Video overview
https://drive.google.com/file/d/1_vqr9Aho951UMGMDG8pVzSU9rWETi4GP/view?usp=sharing
### Video about changes
https://drive.google.com/file/d/1UZy1SMEa6z5TvP5e39JkWtdsJn4zZgGZ/view?usp=sharing
### Code
https://colab.research.google.com/drive/1LtwOPv8OmH1J12qPN8CuDUMZ4xjwBP7V?authuser=2#scrollTo=QfNBKXAXdD8u
### Previous work (including what you used for your method i.e. pretrained models)  
I use a widely pertained image classification model, which is Resnet50.
The code is based on code provided by instructor.
### Your approach  
Use transfer learning technique to transfer image classification model resnet50 to this bird classification task. In this way I can use a already trained model instead of starting training from scratch. I first split the training dataset to train and validation set with ratio 1:10. Then resize and do some data augmentation on training data. During the training process, I start with Resnet50, then train with learning rate 0.01 for several epochs, then descend the learning rate to 0.001 and then train with another several epochs. Finally, do the labeling on test data with multi view labeling.
### Results  
My accuracy is 80% on testing data and 90% on training data. The training loss is eventually 0.4.
### Discussion  
The first problem I need to solve is to know the performance of the model. I use cross validation. I randomly split 10% training data out for validation. It turns out that the accuracy on validation set is consistent with the accuracy on test data.

The second problem I have is to decide the model I want to transfer. I need to consider both the physical storage limit and permormance. I finally choose to use Resnet50. There are many reasons thay I didn't choose other networks. Vgg net is too large to fit in colab. Resnet18 is too small for this problem(not enough parameters).

The Third problem I have is to decide the learning rate of the training process. I first tried 0.1 and found that the loss didn't go down. Thus I switch to 0.01 and train the model. After 7 epochs, I found that the loss stays again at about 1. Thus I change the learning rate to 0.001 and then train for another 3-4 epochs and the loss stays at around 4. Then, if I continue to use a smaller rate, the loss didn't change because the learning rate is too small to decend the loss.

The forth problem I have is to solve overfitting problem. The method I choose is to add some data augmentation. The augmentation I use is ColorJitting and some random rotation. I also do a normailization at the end. I also train with some weight decay and momentum.

The fifth problem I have is to increase predicting accuracy. I choose to do some data augmentation on the testing data also and get 16 slightly augmented picture for each test picture. I then predict on all these images and then average the result. This slightly improves testing accuracy for about 4%.

Lastly, I use larger image size to train becasue larger image size can save more information about the image, thus result in a larger testing accuracy.

If I have more time I would add data loading acceleration feature since the training process now is very slow.
