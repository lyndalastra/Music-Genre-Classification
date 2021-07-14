# Music Genre Classification

## Why this project 	 	 		
- When looking for new songs on music streaming platforms, information overload can result in less satisfied, less confident, and more confused users.
- There are a variety of characteristics that allow us to distinguish between different genres, which makes music production very complex.
- It looked fun and I wanted to learn more about sound and signal processing. 
					

## Goals		
- Identify music genres based on audio features so that audio streaming companies can place useful recommendations for customers and create a genre filter on their platforms.
- Make music composition easier. 

## Success metrics										
- Users spend less time and energy researching songs and feel happier. 		
- Music streaming platforms generate an increase in traffic as content users spread word of mouth.
- Music composers can produce music for the right target audience. 
	
## Data
- Source: marsyas.info/downloads/datasets.html#	 	 			
- The dataset consists of 1000 audio tracks, each 30 seconds long. It contains 10 genres, each represented by 100 tracks. The tracks are all in .wav format.
				
## Overall approach
- Feature Engineering using Librosa, a library for audio analysis.
- Exploratory Data Analysis (EDA)  and a lot of research on signal processing.
- Modelling using machine learning algorithms (Logistic Regression and SVC).
- Data augmentation on the training set, which improved my scores.
- Development of a simple deep learning model using Keras and TensorFlow.
- Testing of models on new data.

## Feature engineering				
- 97 features were extracted from audio files, mainly: chroma stft, chroma cqt, chroma cens, rms, spectral centroid, spectral contrast, spectral bandwidth, spectral rolloff, spectral flatness, poly features, tonnetz, zero crossing rate and 40 mfccs.
- Even though lower order mfccs contain most of the information about the waveform, I decided to extract 40 of them to add more complexity to my models. 
- Note: each chroma has 12 bins and spectral contrast 7 of them

## EDA					
- My EDA consisted in analysing the audio files downloaded from Marsyas, explaining complex concepts of sound (we went through some of them earlier) and visualising individual features as well as the correlation between them.				
- Individual features’ visualisation signalled the presence of outliers, which I decided to keep as my dataset is small.					
- The most important features in my dataset are Mel Frequency Cesptral Coefficients (MFCCs) as there are 40 of them. MFCCs capture timbral/textural aspects of sound. 
- They are frequency domain features and their advantage is that they approximate the human auditory system - they try to model the way we perceive frequencies. 
					
## Modelling (Machine Learning)
- I chose Logistic Regression (LR) and Support Vector Classifier (SVC) to build my classification models. LR is a low-variance, high-bias algorithm; while, SVC is a high-variance, low-bias one. Using algorithms with different bias and variance allowed me to see if the scores obtained were very different. I also chose SVC because it is regarded as one of the best multi-class classification algorithms. The test scores of both models weren’t differing by much. LR had a test score of 0.695, while SVC’s test score was 0.735. However, there was a large gap between the training and cross validated mean scores. LR’s training score was 0.861, while SVC’s was 0.966. Similarly, the cross validated mean score of SVC was much higher than that of LR, 0.887 and 0.770 respectively. We can see that overall, SVC is performing better than LR.

<img width="1204" alt="LR model" src="https://user-images.githubusercontent.com/66631458/125605214-ddc0362a-2bce-4374-86f7-2d3206079192.png">

