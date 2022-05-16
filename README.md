# Project_ADS - Sami Abdelazim / JC Foster

Project Description:

The most state of the art ML tools have not been used to predict crude oil prices, hence the purpose of our investigation was to find a solutionthat uses the most modern ML approaches to anticipate the direction of hourly crude oil prices.
We will do the following in this project:
- creating a methodology of extracting relevant tweets from members of the US Congress, US foriegn policy think tanks, leading global energy corporations, and a collection of large global/domestic news providers; 
- a sentiment analysis on these tweets and the application of a weighting metric on the sentiment score accounting for level of engagement 
- the development and application of an LSTM model to predict twitter sentiment to movement in WTI crude oil prices
- Due to Twitter API limitations we only consider hourly prices from May 11 00:00 to May 13 16:00

This repository contains 4 files:
- Twitter_Collection.ipynb, this was used to collect the various tweets we will use to predict oil prices
- TwitterDataProcessing.ipynb, this fine tunes the GPT-2 model to twitter Data provided in a Kaggle Dataset: https://www.kaggle.com/datasets/kazanova/sentiment140
- Apply-SA-Model.ipynb, this calculates sentiment scores for all the tweets that we collected in the first step, and converts the twitter data into timeseries data with aggregated scores
- Run-LSTM.ipynb, this simply defined a simple LSTM model and uses it to predict the direction of the price, we look at the outcome of deploying a very simple trading strategy. We consider 6 hour, 12 hour, and 18 hour lag in the LSTM model.

All Data (shared with all NYU users): https://drive.google.com/drive/folders/1RbZU6LOeBV6Eo0SnJ4xWyTzpUXEF1Fhj?usp=sharing

All data used is in the folder above ^.

To gather the data from Twitter:
- run the code in the notebook called 'Twitter_Collection.ipynb', in order to run it you need to change three things:
- You need to specify the list of accounts by reading excel file: eg: gov = pd.read_excel("/content/gov_twitter.xlsx")
- You need to get the handles like so: gov_handles = list(gov['handle'])
- Then you need to set handles_list: handles_list = gov_handles
- Note in total there are 4 files of data collected (there's more in file but we only use 4):
  - news_twitter.xlsx
  - finance_twitter.xlsx
  - oil_twitter.xlsx
  - gov_twitter.xlsx


To fine-tune the GPT-2 model, you have to run the TwitterDataProcessing.ipynb notebook in it's entirety. The notebook connects to google drive, and saves the model to this path: 'drive/MyDrive/DS-301_PROJECT/twitter_SA_lw.pth'.

To apply the sentiment analysis model:
- run the notebook called Apply-SA_Model.ipynb
- specify path to fine tuned model: 'drive/MyDrive/DS-301_PROJECT/twitter_SA_lw.pth'
- specify path to collected twitter data: 'drive/MyDrive/DS-301_PROJECT/TwitterData/'
- files names are:
  - news_tweets_clean.csv
  - 'oil_tweets_clean.csv'
  - 'think_tank_tweets_clean.csv'
  - 'gov_tweets_clean.csv'
- the final data is saved in the folder with all the data as 'final_data.csv'

To run the LSTM model:
- run the Run-LSTM.ipynb notebook
- specify path to final_data.csv


Results:
Finetuning accuracy: train_acc: 0.78126 - valid_acc: 0.75270

Accuracy for lag=6: 0.7272727272727273
Final Amount for lag=6: 10145.663324354902

Accuracy for lag=12: 0.8
Final Amount for lag=12: 10257.831171861082

Accuracy for lag=18: 0.4444444444444444
Final Amount for lag=18: 10073.278434128326

In general, when lag was 12 hours we saw the best performance. All of the trading algorithms we came up with were profitable. Ultimately, due to the small dataset size the model is not very robust, and we see variations in performance, however nearly all the time, we generate profitable trading algorithms on the test set.
