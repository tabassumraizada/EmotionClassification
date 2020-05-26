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
2) 15 subjects were shown video clips ellicity happy/sad/neutral/fear emotions and EEG was recorded over 62 channels (with eye-tracking) for 3 sessions per subject (24 trials per session). Refer to the following link for further details about the dataset:
http://bcmi.sjtu.edu.cn/~seed/seed-iv.html#
3) Kaggle EEG Brainwave Dataset:
The data was collected from two people (1 male, 1 female) for 3 minutes per state - positive, neutral, negative. Muse EEG headband was used to record data from TP9, AF7, AF8 and TP10 EEG placements via dry electrodes. Sixty  seconds  of  data  were recorded  from  two subjects  for 6 film  clips  producing 12  minutes (720 seconds) of brain activity data. Six minutes of resting neutral data is also recorded, stimuli used to evoke the emotions are movie clips shown to the participants. Participants  were  asked  to  watch  the  film  clips without  making  any conscious  movements  (eg. drinking  coffee)  to  prevent  the influence of Electromyographic (EMG) signals resulting from muscle movement which are highly prominent given their signal  strength. With  a  variable  frequency  resampled  to  150Hz,  this resulted  in  a  dataset  of  324,000  data  points  collected  from  the waves  produced  by  the brain.  Physiological responses like a smile is indicative of an emotional state hence both  EEG  and  facial  EMG  signals were used. Methodology from earlier study on video browsing strategies was used to   extract  2400  features  through  a  sliding  window  of  1 second beginning  at  t=0  and t=0.5. 

# References:
J. J. Bird, L. J. Manso, E. P. Ribiero, A. Ekart, and D. R. Faria, “A study on mental state classification using eeg-based brain-machine interface,”in 9th International Conference on Intelligent Systems, IEEE, 2018.

J. J. Bird, A. Ekart, C. D. Buckingham, and D. R. Faria, “Mental emotional sentiment classification with an eeg-based brain-machine interface,” in The International Conference on Digital Image and Signal Processing (DISP’19), Springer, 2019.

Wei-Long Zheng, Wei Liu, Yifei Lu, Bao-Liang Lu, and Andrzej Cichocki, EmotionMeter: A Multimodal Framework for Recognizing Human Emotions. IEEE Transactions on Cybernetics, Volume: 49, Issue: 3, March 2019, Pages: 1110-1122, DOI: 10.1109/TCYB.2018.2797176.

"DEAP: A Database for Emotion Analysis using Physiological Signals", S. Koelstra, C. Muehl, M. Soleymani, J.-S. Lee, A. Yazdani, T. Ebrahimi, T. Pun, A. Nijholt, I. Patras, IEEE Transactions on Affective Computing, Special Issue on Naturalistic Affect Resources for System Building and Evaluation

"What are emotions? And how can they be measured", K.R. Scherer, Social Science Information,vol. 44, no. 4, pp. 695-729, 2005.
