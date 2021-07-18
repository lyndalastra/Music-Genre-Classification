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
- **Source:** http://marsyas.info/downloads/datasets.html	 	 			
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
- **Note:** each chroma has 12 bins and spectral contrast 7 of them

## EDA					
- My EDA consisted in analysing the audio files downloaded from Marsyas, explaining complex concepts of sound (we went through some of them earlier) and visualising individual features as well as the correlation between them.				
- Individual features’ visualisation signalled the presence of outliers, which I decided to keep as my dataset is small.					
- The most important features in my dataset are Mel Frequency Cesptral Coefficients (MFCCs) as there are 40 of them. MFCCs capture timbral/textural aspects of sound. 
- They are frequency domain features and their advantage is that they approximate the human auditory system - they try to model the way we perceive frequencies. 
					
## Modelling (Machine Learning)
- I chose Logistic Regression (LR) and Support Vector Classifier (SVC) to build my classification models. LR is a low-variance, high-bias algorithm; while, SVC is a high-variance, low-bias one. Using algorithms with different bias and variance allowed me to see if the scores obtained were very different. I also chose SVC because it is regarded as one of the best multi-class classification algorithms. The test scores of both models weren’t differing by much. LR had a test score of 0.695, while SVC’s test score was 0.735. However, there was a large gap between the training and cross validated mean scores. LR’s training score was 0.861, while SVC’s was 0.966. Similarly, the cross validated mean score of SVC was much higher than that of LR, 0.887 and 0.770 respectively. We can see that overall, SVC is performing better than LR.

<p>&nbsp;</p>
<p align="center"><img width="800" alt="LR model" src="https://user-images.githubusercontent.com/66631458/125605214-ddc0362a-2bce-4374-86f7-2d3206079192.png"></p>

<p align="center"><img width="800" alt="SVC model" src="https://user-images.githubusercontent.com/66631458/125605350-7ba0ad60-1218-4a77-892e-db22d0b28f7d.png"></p>
<p>&nbsp;</p>

- As mentioned in the EDA, my LR model has demonstrated that MFCCs are the most important features for music genre prediction. The feature importances couldn’t be computed with SVC because of the complexity of interpretation of dual coefficients and support vectors.	
- The test set confusion matrix of my LR and SVC models have both shown that classical has the most true positives. 
<p>&nbsp;</p>
<p align="center"><img width="700" alt="Screenshot 2021-07-14 at 11 15 07" src="https://user-images.githubusercontent.com/66631458/125605450-6244da85-8ddd-4681-98c3-88de3520ef7c.png"></p>
<p>&nbsp;</p>

## [Data augmentation](#https://github.com/lyndalastra/Music-Genre-Classification/blob/main/MGC_Data_Augmentation.ipynb)
Data augmentation was performed by:
- Adding noise to the signal. White noises are random samples distributed at regular intervals with mean of 0 and standard deviation of 1.
- Shifting time, i.e. moving the waveform to the right by sample_rate/10 factor along the time axis.
- Shifting pitch by 5 steps. 

## Modelling (Deep Learning)
- The Rectified Linear Unit (ReLU) activation function was used in hidden layers because of its computational simplicity, while the Softmax was used in the output layer because it can solve multiclass classification problems.  
- The Deep Learning model had a test score of 72.00, higher than Logistic Regression but lower than SVC.   
<p>&nbsp;</p>
<p align="center"><img width="800" alt="DL test score" src="https://user-images.githubusercontent.com/66631458/125606113-59f71f4c-68ed-46b1-b936-dea7e2a9b01e.png"></p>
<p>&nbsp;</p>

## Testing on new data
- All models correctly predicted the labels of new classical and disco songs. 
- LR and SVC also managed to get the genre of new metal songs. 
- SVC did well at guessing jazz and reggae. 
- The deep learning model got interesting results for new pop songs. In fact, it firstly guessed the genre of 'Sorry' by Madonna - which wasn't achieved by the SVC and LR models. On top of that, even though Michael Jackson is the King of Pop, a lot of his songs are also classified as disco. 'Thriller' is classified as pop by Google but as disco by Wikipedia. The DL model guess was closer to the classification of Wikipedia but interestingly pop comes as the second genre with the highest contribution.

## Conclusion
- My first analysis of the GTZAN dataset didn’t use data augmentation or a deep learning model. On top of that, the original dataset was created by someone else and I later added more features to this dataset. However, the problem with the latter is that we might have used different characteristics to build our features. 
- The limitations of my first analysis pushed me to use data augmentation which improved the cross validated scores of the SVC and LR models. I also used a simple deep learning model to check if it performed better than the machine learning models. The simple deep learning model accuracy was better than that of LR but worse than SVC. Moreover, I created a dataset from scratch to get consistent data. 
- As mentioned earlier the best results were obtained by the SVC algorithm, which correctly predicted the labels of new disco, classical, metal, jazz and reggae songs. The deep learning model got interesting results for new pop songs. More data is needed for blues, rock, country and hip- hop.

## Key learnings
- Data augmentation improved the cross validated mean scores but didn’t change the test scores by much. It also didn’t decrease the training scores.
Using a high number of MFCCs slightly improved my scores since most of the information is contained in the first order coefficients.
- Creating my own dataframe from scratch was very useful as it allowed me to have complete control of my data and I also used my feature engineering to test my models on new songs.
- SVC is a very powerful algorithm when it comes to multi-class classification.

## Next steps
- Check whether removing outliers improves my scores.
- Analyse all features extracted - I only analysed MFCCs and chroma.
- Add a convolutional layer to my deep learning model and see if the accuracy improves.
- Add more hip-hop, rock, blues and country songs so that my models can do better at guessing their label. 

## How to run the project
Python as well as the following libraries are required to run the project: 
- Pandas,
- Numpy,
- Seaborn,
- Matplotlib,
- Scikit-Learn,
- Scikit-plot,
- Librosa,
- TensorFlow,
- Keras.




