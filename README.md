# Project_ADS

All Data: https://drive.google.com/drive/folders/1RbZU6LOeBV6Eo0SnJ4xWyTzpUXEF1Fhj?usp=sharing

All data used is in the folder above ^.

To gather the data from Twitter:
- run the code in the notebook

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
