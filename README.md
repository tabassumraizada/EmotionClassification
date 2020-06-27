# Project Background and Description
Human emotions are an important aspect of Human-Computer interaction. It can be inferred from multiple modalities like facial expressions, eye movements, skin temperature, EKG, electroencephalogram (EEG) measurement to name a few. Being able to predict a person’s emotional state correctly can have can have several practical applications for e.g. for a pilot about to go on an important mission, patients in rehabilitation centers, mental state of doctors and healthcare workers in stressful positions, risk  and  safety  management  system  used  by mental-health  practitioners or even personalized gaming experience. Dolyb Labs who are known for producing great sound effects in cinema use g.Nautilus PRO wearable EEG device to study emotional responses of their audiences while they are watching videos. The scientists at Dolby Labs try to better understand what makes the audience engaged, what makes their skin blush, increase their heart-rate or give them goose bumps.
# Project Scope
For this practicum project I intend to work with one or more of the publicly available datasets that have emotions data for multiple modalities. These dataset that I have requested access to as follows:
1)	DEAP (dataset for emotional analysis using EEG, Physiological and Video signals (http://www.eecs.qmul.ac.uk/mmv/datasets/deap
2)	SEED IV dataset (http://bcmi.sjtu.edu.cn/~seed/contacts.html)
3)	Kaggle : EEG Brainwave Dataset: Feeling Emotions. https://www.kaggle.com/birdy654/eeg-brainwave-dataset-feeling-emotions  (MUSE  EEG headband using  sensors TP9, AF7, AF8 and TP10)
# Deliverables
The primary goal of the project is to be able to classify EEG data using deep neural networks into the various emotion states. In addition I will try to combine EEG data with other modalities like eye movements and evaluate the impact on accuracy. We will try to compare these results with other conventional shallow methods for e.g. SVM. 
# Experimental Setup and description of the above datasets:
1) DEAP(Dataset of Emotion Analysis using EEG and Physiological and Video Signals) 
This is a benchmark dataset for emotion analysis using the EEG, physiological and video signals. Thirty-two participants are shown 40 videos each with one-minute duration. The facial expressions and the EEG signals were recorded for each participant. The EEG signals were recorded from 32 different channels. Most of the publicly available EEG datasets have fewer amounts of data per participant. For further details refer to:
http://www.eecs.qmul.ac.uk/mmv/datasets/deap/readme.html

2) SEED IV: 15 subjects (8 females, 7 males) were shown video clips to ellicit happy/sad/neutral/fear emotions and EEG was recorded over 62 channels (with eye-tracking) for 3 sessions per subject (24 trials per session). EEG data from 62-channels was collected at 1000hz sampling rate as the participants watched the videos to elicit the expected emotional response. This raw EEG data was down sampled to a 200 Hz sampling rate and then processed with a bandpass filter between 1 Hz to 75 Hz. The EEG feature smooth files contains two types of features, power spectral density (PSD) and differential entropy (DE), which was extracted using short-term Fourier transforms with a 4 s time window without overlapping. These features were extracted along five frequency bands for each channel: 
      1.	delta: 1–4 Hz
      2.	theta: 4–8 Hz;
      3.	alpha: 8–14 Hz
      4.	beta: 14–31 Hz
      5.	gamma: 31–50 Hz

Alpha, Beta and Gamma have been found to have the most impact on emotion analysis results [3]

Eye movement data was also recorded using [eye-tracking glasses](https://imotions.com/hardware/smi-eye-tracking-glasses/). For eye movements, various features from different detailed parameters as shown below were available in the dataset:

![](/images/Eye_Movement_Features.JPG)
Eye raw data includes blink, event, fixation, PD, pupil, saccade files for each experiment along with eye features smooth file with pre-processed data.

Refer to the following link for further details about the dataset:
http://bcmi.sjtu.edu.cn/~seed/seed-iv.html#

3) Kaggle EEG Brainwave Dataset:
The data was collected from two people (1 male, 1 female) for 3 minutes per state - positive, neutral, negative. Muse EEG headband was used to record data from TP9, AF7, AF8 and TP10 EEG placements via dry electrodes. Sixty  seconds  of  data  were recorded  from  two subjects  for 6 film  clips  producing 12  minutes (720 seconds) of brain activity data. Six minutes of resting neutral data is also recorded, stimuli used to evoke the emotions are movie clips shown to the participants. Participants  were  asked  to  watch  the  film  clips without  making  any conscious  movements  (eg. drinking  coffee)  to  prevent  the influence of Electromyographic (EMG) signals resulting from muscle movement which are highly prominent given their signal  strength. With  a  variable  frequency  resampled  to  150Hz,  this resulted  in  a  dataset  of  324,000  data  points  collected  from  the waves  produced  by  the brain.  Physiological responses like a smile is indicative of an emotional state hence both  EEG  and  facial  EMG  signals were used. Methodology from earlier study on video browsing strategies was used to   extract  2400  features  through  a  sliding  window  of  1 second beginning  at  t=0  and t=0.5. 

# SEED-IV Model development:

It was important to pre-process the data from different experiments to same size by padding with zeros as the shape varied across the files for different experiments. The following functional API model was used to combine EEG Differential entropy data with Eye Movement pre-processed data:

![](/images/SEED_Multi-Modal.png)

We ran this model first using data from the 6 electrodes that the paper [3] determined to have the most impact on emotion classification results using 3 frequency bands. For comparison we used a larger dataset with DE data from 41 electrodes and all frequency bands. Although a convolutional layer is often followed by a pooling layer we did not use it here as pooling layer reduces dimensionality as a result some information. Compared to image data used in computer vision field we do not have very-dimensionality data here. 

# SEED-IV Model results summary:

| Model run | Test Accuracy  |
| :------------ | -----:|
| Model 1: Single Modality, using DE data from 6-channels (FT7, T7, TP7, FT8, T8, P8) and 3-frequency bands (α, β and γ) | 0.689  |
| Model 2: Single Modality, using eye movement data | 0.7037 (1st run), 0.6962 (2nd run)  |
| Model 3: Multi-Modal with EEG and eye movement data | 0.7111  |
| Model 4: Single Modality, using DE data from 41-channels (0-40) and 5-frequency bands (δ , θ ,α, β and γ) | 0.6037  |
| Model 5: Multi-Modal with EEG {using DE data from 41-channels (0-40) and 5-frequency bands (δ , θ ,α, β and γ)} and eye movement data | 0.7333  |

*Refer to the following file: 

Models 1-3: SEED_SingleandMultiModalityModels_6channels_V2.ipynb

Models 4-5: SEED_SingleandMultiModalityModels_41channels.ipynb*

**Classification Report from Model 3:**
              precision    recall  f1-score   support

     neutral       0.69      0.68      0.68        65
         sad       0.70      0.82      0.75        71
        fear       0.74      0.68      0.71        66
       happy       0.76      0.69      0.72        68


We see from the results above that even though precision (percentage of your results which are relevant) is the highest on happy state, recall (refers to the percentage of total relevant results correctly classified by your algorithm) is high for sad emotion state. Given that the experiments was under a controlled setting and hence the participants are more relaxed hence it is probably harder to elicit a fear response by showing videos. However sad emotion did seem to be more powerful in EEG signals than over emotion states

Given the results of test accuracy between Model 3 and 5 we can see that including data from 35 additional channels and all 5 instead of the earlier 3 frequency bands resulted in a modest improvement. This confirms that the 6 channels FT7, T7, TP7, FT8, T8, P8 are the most useful for emotional state classification.

# DEAP Model development:

Model 1: Hybrid deep learning model (Parallel Convolutional Recurrent Neural Network) [6]

Original shape of data for each subject is in the shape: 

Trials	Channels, EEG Signals down sampled to 128 Hz
(40,    40,       8064)

![] (/images/InputShape_DEAP.JPG)

[Pre-processing](https://github.com/tabassumraizada/EmotionClassification/blob/master/Models/Deap/Deap_Preprocess_v2.ipynb) applied to the above dataset for each subject:

1. The EEG signals are pre-processed to account for variation to base signal [6] : 
![](/images/base_signal.JPG)

    a.	Take pre-trail signal and cut into segment of size 1sec. 
    b.	We calculate mean value for this baseline segment by doing element-wise addition
    c.	Next the remaining EEG raw data is also divided into 1 sec segment and base mean values calculated in the above step subtracted from it

2. Spatial features are extracted by using a 9 x 9 matrix

This was another unique application used in this paper [6] where instead of using chain like EEG data sequence we convert it into a 2D spatial frame as show below ():
![](/images/2dMatrix.JPG)

Out of the pre-processing step:

      CNN model output of shape:

      (2400, 128, 9, 9)

      RNN Model output of shape:

      (2400, 128, 32)

[Hybrid Model](https://github.com/tabassumraizada/EmotionClassification/blob/master/Models/Deap/Deap_Video_SpatialEEG_MultiModal_Classification_s01.ipynb) is run Without/With taking into account the role of the 3-second-long baseline signals. This method takes the baseline signals as a basic emotional representation state first, then calculates the difference between it and real emotion signals, and uses this difference to represent the emotion state.
1.Uses Parallel CNN convolution layers followed by a depth concatenate layer which helps convert the 2-D shape of the spatial data we saw above into a 3D cube. CNN layers help in extracting spatial features from 2D channel frames.
2.RNN model used for extracting temporal features. Long Short-Term Memory (LSTM) models the context information for streaming 1D data vectors

Model 2: Multi-Model using CNN preprocessed data with EEG temporal features along with Video data

We break the one-minute video into 60 frames. Each frame then corresponds to the 1 sec segment obtained from EEG enabling up to combine the data-set for multi-modal processing.
Here a valence of 5 is used as a threshold to divide the trials into two classes - High and Low category which corresponds to value >5 and <=5 respectively. We first run the [model with only video data](https://github.com/tabassumraizada/EmotionClassification/blob/master/Models/Deap/Deap_Video_Naive_Classification_s01.ipynb) by subject. 

We used a VGG16 pretrained model which takes an input image of shape (224 X 224 X 3). Since our images are in a different size (576, 720, 3) we had to reshape all of them using resize() function of skimage.transform to do this. In addition we also used preprocess_input() function of keras.applications.vgg16 to preprocess the input data as per the model’s requirement. 
![](/images/Model_Video_EEG.JPG)

# DEAP Model results summary:

**Model 1: Hybrid neural network (CNN+RNN model) **
| | Valence Classification | Arousal Classification|
| | With Baseline | Without baseline data removal| | With baseline | Without baseline data removal|
| :------------ | ------:| -----:| -----:| -----:|
| Subject 01 (for 10 epochs, 2 fold run) |82.50| 51.89 |91.75| 56.50|
| Subject 02 (for 10 epochs, 2 fold run fold) |83.12| 56.10 |86.49| 50.12|
| Subject 03 (for 10 epochs, 2 fold run fold) |89.59| 55.70 |93.10| 65.19|

Performance with and without the use of baseline data has almost a 30 point difference in accuracy. The mean accuracy of 10 folds cross-validation is used in the original papers. Hence we can expect the overall results to be better than shown above.

**Model 2: Multi-Modal using EEG and Video Data**

| Subject | Test Accuracy for Model using video data only | Test Accuracy for Functional model using video and temporal EEG data |
| :------------ | ------:| -----:|
| Subject 01 | 97.36 | 98.28 |
| Subject 02 | 98.15 | 98.74 |
| Subject 03 | 97.89 | 98.62 |
| Subject 09 | 98.03 | 99.27 |

Note that we ran the above models for one subject with 2400 data points corresponding to 40 trails x 60 segments per trail i.e. 2400 data points. It would need a lot of power to use the entire dataset available i.e video data for 22 participants which would have resulted in input data of size 52,800 x 576, 720, 3. Hence even though the results compared to the hybrid model look more promising we do not know how well we can generalize the results across subjects.

# References:
[1] J. J. Bird, L. J. Manso, E. P. Ribiero, A. Ekart, and D. R. Faria, “A study on mental state classification using eeg-based brain-machine interface,”in 9th International Conference on Intelligent Systems, IEEE, 2018.

[2] J. J. Bird, A. Ekart, C. D. Buckingham, and D. R. Faria, “Mental emotional sentiment classification with an eeg-based brain-machine interface,” in The International Conference on Digital Image and Signal Processing (DISP’19), Springer, 2019.

[3] Wei-Long Zheng, Wei Liu, Yifei Lu, Bao-Liang Lu, and Andrzej Cichocki, EmotionMeter: A Multimodal Framework for Recognizing Human Emotions. IEEE Transactions on Cybernetics, Volume: 49, Issue: 3, March 2019, Pages: 1110-1122, DOI: 10.1109/TCYB.2018.2797176.

[4] "DEAP: A Database for Emotion Analysis using Physiological Signals", S. Koelstra, C. Muehl, M. Soleymani, J.-S. Lee, A. Yazdani, T. Ebrahimi, T. Pun, A. Nijholt, I. Patras, IEEE Transactions on Affective Computing, Special Issue on Naturalistic Affect Resources for System Building and Evaluation

[5] "What are emotions? And how can they be measured", K.R. Scherer, Social Science Information,vol. 44, no. 4, pp. 695-729, 2005.

[6] Y. Yang, Q. Wu, M. Qiu, Y. Wang and X. Chen, "Emotion Recognition from Multi-Channel EEG through Parallel Convolutional Recurrent Neural Network," 2018 International Joint Conference on Neural Networks (IJCNN), Rio de Janeiro, 2018, pp. 1-7, doi: 10.1109/IJCNN.2018.8489331.
