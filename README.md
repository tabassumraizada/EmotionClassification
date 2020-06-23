# UNDER DEVELOPMENT
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
2) SEED IV: 15 subjects were shown video clips ellicity happy/sad/neutral/fear emotions and EEG was recorded over 62 channels (with eye-tracking) for 3 sessions per subject (24 trials per session). Refer to the following link for further details about the dataset:
http://bcmi.sjtu.edu.cn/~seed/seed-iv.html#
3) Kaggle EEG Brainwave Dataset:
The data was collected from two people (1 male, 1 female) for 3 minutes per state - positive, neutral, negative. Muse EEG headband was used to record data from TP9, AF7, AF8 and TP10 EEG placements via dry electrodes. Sixty  seconds  of  data  were recorded  from  two subjects  for 6 film  clips  producing 12  minutes (720 seconds) of brain activity data. Six minutes of resting neutral data is also recorded, stimuli used to evoke the emotions are movie clips shown to the participants. Participants  were  asked  to  watch  the  film  clips without  making  any conscious  movements  (eg. drinking  coffee)  to  prevent  the influence of Electromyographic (EMG) signals resulting from muscle movement which are highly prominent given their signal  strength. With  a  variable  frequency  resampled  to  150Hz,  this resulted  in  a  dataset  of  324,000  data  points  collected  from  the waves  produced  by  the brain.  Physiological responses like a smile is indicative of an emotional state hence both  EEG  and  facial  EMG  signals were used. Methodology from earlier study on video browsing strategies was used to   extract  2400  features  through  a  sliding  window  of  1 second beginning  at  t=0  and t=0.5. 
# SEED-IV Model results summary:

| Model run | Test Accuracy  |
| :------------ | -----:|
| Model 1: Single Modality, using DE data from 6-channels (FT7, T7, TP7, FT8, T8, P8) and 3-frequency bands (α, β and γ) | 0.689  |
| Model 2: Single Modality, using eye movement data | 0.7037 (1st run), 0.6962 (2nd run)  |
| Model 3: Multi-Modal with EEG and eye movement data | 0.7111  |
| Model 4: Single Modality, using DE data from 41-channels (0-40) and 5-frequency bands (δ , θ ,α, β and γ) | 0.6037  |
| Model 5: Multi-Modal with EEG {using DE data from 41-channels (0-40) and 5-frequency bands (δ , θ ,α, β and γ)} and eye movement data | 0.7333  |

*Refer to the following file for Models 1-3: SEED_SingleandMultiModalityModels_6channels_V2.ipynb
Refer to the following file for Models 4-5: SEED_SingleandMultiModalityModels_41channels.ipynb*

**Classification Report from Model 3:**
              precision    recall  f1-score   support

     neutral       0.69      0.68      0.68        65
         sad       0.70      0.82      0.75        71
        fear       0.74      0.68      0.71        66
       happy       0.76      0.69      0.72        68


We see from the results above that even though precision (percentage of your results which are relevant) is the highest on happy state, recall (refers to the percentage of total relevant results correctly classified by your algorithm) is high for sad emotion state. Given that the experiments was under a controlled setting and hence the participants are more relaxed hence it is probably harder to elicit a fear response by showing videos. However sad emotion did seem to be more powerful in EEG signals than over emotion states

Given the results of test accuracy between Model 3 and 5 we can see that including data from 35 additional channels and all 5 instead of the earlier 3 frequency bands resulted in a modest improvement. This confirms that the 6 channels FT7, T7, TP7, FT8, T8, P8 are the most useful for emotional state classification.

# References:
[1] J. J. Bird, L. J. Manso, E. P. Ribiero, A. Ekart, and D. R. Faria, “A study on mental state classification using eeg-based brain-machine interface,”in 9th International Conference on Intelligent Systems, IEEE, 2018.

[2] J. J. Bird, A. Ekart, C. D. Buckingham, and D. R. Faria, “Mental emotional sentiment classification with an eeg-based brain-machine interface,” in The International Conference on Digital Image and Signal Processing (DISP’19), Springer, 2019.

[3] Wei-Long Zheng, Wei Liu, Yifei Lu, Bao-Liang Lu, and Andrzej Cichocki, EmotionMeter: A Multimodal Framework for Recognizing Human Emotions. IEEE Transactions on Cybernetics, Volume: 49, Issue: 3, March 2019, Pages: 1110-1122, DOI: 10.1109/TCYB.2018.2797176.

[4] "DEAP: A Database for Emotion Analysis using Physiological Signals", S. Koelstra, C. Muehl, M. Soleymani, J.-S. Lee, A. Yazdani, T. Ebrahimi, T. Pun, A. Nijholt, I. Patras, IEEE Transactions on Affective Computing, Special Issue on Naturalistic Affect Resources for System Building and Evaluation

[5] "What are emotions? And how can they be measured", K.R. Scherer, Social Science Information,vol. 44, no. 4, pp. 695-729, 2005.

[6] Y. Yang, Q. Wu, M. Qiu, Y. Wang and X. Chen, "Emotion Recognition from Multi-Channel EEG through Parallel Convolutional Recurrent Neural Network," 2018 International Joint Conference on Neural Networks (IJCNN), Rio de Janeiro, 2018, pp. 1-7, doi: 10.1109/IJCNN.2018.8489331.
