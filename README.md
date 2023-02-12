# Crypto Predic AI

This project aims to predict the trend (up or down) of the Bitcoin (BTC) price using historical data and information about Wikipedia edits about Bitcoin. The data consists of two parts: one is the daily close prices of Bitcoin and the other is the number of Wikipedia edits about Bitcoin. The project uses machine learning algorithms (RandomForestClassifier and XGBoostClassifier) to train the model and make predictions. The performance of the model is evaluated using precision score. Additionally, the project computes several rolling averages and other statistics over different time horizons and uses them as additional predictors. The final results show the precision score of the predictions made by the model.

## Installations

This project requires the following packages to be installed:

- `yfinance`: A library for downloading financial data from Yahoo Finance.
- `mwclient`: A Python framework to access the MediaWiki API.
- `transformers`: A library for natural language processing (NLP) tasks such as text classification, translation, and text generation using pre-trained transformers models.
- `statistics`: A module in Python's Standard Library that implements mathematical statistics functions.

To install these packages, run the following commands in your terminal:

pip install yfinance
pip install mwclient
pip install transformers
pip install statistics

Once you have installed these packages, you can now run the project.

## Collect Crypto Data From Yfinance

The code above is written in Python and is used to collect historical data for Bitcoin (BTC) using the yfinance library.

The code starts by importing the required libraries, which are yfinance and pandas. Then, it defines the ticker for Bitcoin, which is "BTC-USD". After that, it uses the yfinance library to collect the historical data for the ticker and stores it in a variable called "btc".

The code then converts the index of the data to a datetime format and removes two unwanted columns from the data. The code then converts the names of the columns to lower case and plots the close price over time using the plot.line method. Finally, it saves the data to a csv file on the disk.

Note: The file path for saving the data to a csv file is set to /content/drive/MyDrive/Colab Notebooks/Data/Crypto Predict AI - v01/btc_data.csv which is specific to a Google Colab environment. You may need to change this file path to a different location on your local machine.


## Collect Wikipedia Revison data for sentiment analyze

This is a Python code that retrieves revision data from the English Wikipedia page for Bitcoin and performs sentiment analysis on the comments accompanying each revision. The code uses the mwclient library to connect to the English Wikipedia site and retrieve all revisions of the Bitcoin page. The sentiment analysis is performed using the sentiment-analysis model from the Hugging Face Transformers library. The sentiment score for each day is calculated as the mean sentiment score for the comments of all revisions made on that day. The final result is stored in a CSV file.

The code first imports the required libraries, connects to the English Wikipedia site, and retrieves all revisions of the Bitcoin page. It then sorts the revisions based on their timestamps and uses the sentiment-analysis model to find the sentiment of each comment accompanying a revision. The sentiment scores are stored in a dictionary along with the edit count for each day, and the mean sentiment score and negative sentiment ratio are calculated for each date. The dictionary is then converted to a Pandas DataFrame and saved to a CSV file.

##  Train the Model

The script starts by importing the required libraries such as Pandas and scikit-learn. Then it reads in two data files, one containing historical data of the Bitcoin (BTC) price and the other containing information about Wikipedia edits related to Bitcoin.

The two dataframes are then merged based on the date index and a new feature "tomorrow" is created, which is the close price of the next day. Another feature "target" is then created, which is a binary feature indicating whether the price went up or down from the current day to the next day.

A random forest classifier from scikit-learn is then created and trained on a portion of the data. The precision score of the predictions on the test data is calculated and printed.

A helper function "predict" is defined that trains the model on a given train dataset and returns the predictions on the test data. Another helper function "backtest" is defined that repeatedly calls the "predict" function on different portions of the data, to evaluate the performance of the model over time.

The script then replaces the random forest classifier with an XGBoost classifier and re-runs the backtesting process to evaluate the model's performance using XGBoost. The precision score of the predictions is calculated and printed.

Finally, another feature engineering step is performed to compute rolling averages and trends based on different time horizons and the model is trained and evaluated again on the updated dataset. The final precision score is printed as the output.


