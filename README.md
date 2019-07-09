# Image-and-Video-Face-Recognition
This program uses the face_recognition and OpenCV module to detect faces in the images and videos and simultaneously identifying the person in the image. The arguments must be provided to this program via command line.

### encode_faces.py
Fist the encode_faces.py file is run to generate the 128-d feature vector of the images of the people in the dataset and the feature vectors are saved into a file encodings.pickle using the pickle library of python. Then these encodings are used as data points to match the encodings of the test image/video on which the face classification is to performed. 

<b>Input</b>
>> python --dataset (path to the directory for dataset) --encodings (path to where you want to save encodings.pickle file) --detection-method (cnn or hog / default value is cnn)

### recognize_faces_image.py
This file uses the encodings from encodings.pickle file and uses it to classify all the faces it has detected in the test images.

<b>Input</b>
>> python --encodings (path to encodings.pickle file) --image (path to the test image) --detection-method (cnn or hog / default value is cnn)

### recognize_faces_video.py
This file uses the encodings from encodings.pickle file and uses it to classify face detected in the frames of the video stream (in this case - webcam).

<b>Input</b>
>> python --encodings (path to encodings.pickle file) --output (path to where you want ot save the output video) --display (0 or 1 / default=1) --detection-method (cnn or hog / default value is cnn)

### recognize_faces_video_file.py
This file uses the encodings from encodings.pickle file and uses it to classify face detected in the frames of the video (in this case - any video file in the system).

<b>Input</b>
>> python --encodings (path to encodings.pickle file) --input (path to the input video file) --output (path to where you want ot save the output video) --display (0 or 1 / default=1) --detection-method (cnn or hog / default value is cnn)

This project uses an already trained classifier (by Davis King on a dataset of ~3 million images, on the Labeled Faces in the Wild (LFW) dataset, reaching about 99.48% accuracy) from the face_recognition module for classifiaction purpose.

Just like KNN algorithm, the feature vector of the faces that are the closest (like euclidean distance) to the feature vector of the stored encodings, that face in the test image/video will be assigned the name of the person whose stored feature vector it has matched with. 

If any face in any image or video is encountered whose encodings do not match with those that are stored in the database, the classifier labels the face as UNKNOWN.

### Detection method
Every python file of this program asks the user for an input about what kind of detection method does he/she want: Histogram of Oriented Gradients (hog) or Convolutional Neural Network (cnn).

Refer the following link for a brief understanding of HOG:-
https://www.learnopencv.com/histogram-of-oriented-gradients/

Refer the following link for a brief understanding of CNN:-
https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53

### Dataset
I created a dataset with 64 images of Monica, 70 images of Rachel, 80 images of Phoebe, 62 images of Ross, 76 images of Chandler and 76 images of Joey of the FRIENDS comedy serial. The dataset was a folder which contained 6 folders, each contained images of the above mentioned people (one folder per person).

I didn't include images of me in the dataset for training and therefore in the WebcamOutputs folder, the images show that the classifier either classifies me as one of the six people that were used for training purpose or as an UNKNOWN.

### Note
The cnn detection method is computationally expensive, takes a lot of time but it yields very high accuracy. On the other hand, hog is computationally inexpensive, quick but does not give good accuracy. I would advise to run this program in linux or MacOS with GPU as processing this code without GPU especially in windows would take a lot of time. I had compiled my code in windows with GPU withh cnn as detection method. The computer would always hang after encoding 10-15 images. Therefore I had to go with hog detection method, which resulted in easy flow of the program but couldn't yield as good results as cnn would have.
