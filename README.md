# Twitter-Sentiment-Analysis
This repository covers the sentiment analysis of any topic by parsing the tweets fetched from Twitter using Python.
Sentiment Analysis is the process of ‘computationally’ determining whether a piece of writing is positive, negative or neutral. It’s also known as opinion mining, deriving the opinion or attitude of a speaker.

## Dependencies & Installation:
* **Tweepy**: Tweepy is the python client for the official Twitter API.
  * Install it using following pip command: 
  pip install tweepy
  
* **TextBlob**: textblob is the python library for processing textual data.
  * Install it using following pip command:
  pip install textblob
  
* **re**: Python has a built-in package called re, which can be used to work with Regular Expressions.

* **csv**: Csv is a simple file format used to store tabular data, such as a spreadsheet or database. For working CSV files in python, there is an inbuilt module called csv
  
## Authentication:
In order to fetch tweets through Twitter API, one needs to register an App through their twitter account. Follow these steps for the same:
  * Open this link and click the button: ‘Create New App’. You need to be logged in twitter.
  * Fill the application details. You can leave the callback url field empty.
  * Once the app is created, you will be redirected to the app page.
  * Open the ‘Keys and Access Tokens’ tab.
  * Copy ‘Consumer Key’, ‘Consumer Secret’, ‘Access token’ and ‘Access Token Secret’.

## We follow these 3 major steps in our program:
* Authorize twitter API client.
* Make a GET request to Twitter API to fetch tweets for a particular query.
* Parse the tweets. Classify each tweet as positive, negative or neutral.

First of all, we create a TwitterClient class. This class contains all the methods to interact with Twitter API and parsing tweets. We use __init__ function to handle the authentication of API client.

In get_tweets function, we search for the topic name and fetch relevant tweets using Twitter API.

In get_tweet_sentiment we use textblob module. TextBlob is actually a high level library built over top of NLTK library. First we call clean_tweet method to remove links, special characters, etc. from the tweet using some simple regex.
Then, as we pass tweet to create a TextBlob object, following processing is done over text by textblob library:
* Tokenize the tweet ,i.e split words from body of text.
* Remove stopwords from the tokens.(stopwords are the commonly used words which are irrelevant in text analysis like I, am, you, are, etc.)
* Do POS( part of speech) tagging of the tokens and select only significant features/tokens like adjectives, adverbs, etc.
* Pass the tokens to a sentiment classifier which classifies the tweet sentiment as positive, negative or neutral by assigning it a polarity between -1.0 to 1.0 .

Here is how sentiment classifier is created:
* TextBlob uses a Movies Reviews dataset in which reviews have already been labelled as positive or negative.
* Positive and negative features are extracted from each positive and negative review respectively.
* Training data now consists of labelled positive and negative features. This data is trained on a Naive Bayes Classifier.

Then, we use sentiment.polarity method of TextBlob class to get the polarity of tweet between -1 to 1.
Then, we classify polarity as positive, neutral and negative based on polarity where -1 refers to negative, 1 positive and 0 neutral.
Finally, parsed tweets are returned. Then, we can do various type of statistical analysis on the tweets. 

## Output Sample:
*Here is how a sample output looks like when above program is run:*

Enter topic name: Elon Musk
Positive tweets percentage: 27.272727272727273 %
Negative tweets percentage: 21.21212121212121 %
Neutral tweets : 0.5151515151515151 %


Positive tweets:
b'"Tesla Autopilot will be able to avoid potholes on the road, says Elon Musk." (Source: Electrek) -- I was hoping fo\xe2\x80\xa6 https://t.co/vbU6LimpOT'
b'Everyone should strive to be a little like Elon Musk; his work ethic and drive is incredible'
b'Tesla Autopilot will be able to avoid potholes on the road, says Elon Musk - Electrek https://t.co/3iqW70VbiA'
b'RT @Smaulgld: Elon Musk Pumping Crypto\nElon Musk: \'Paper money is going away\' "Crypto[currency] is a far better way to transfer value than\xe2\x80\xa6'
b'Elon Musk\'s work ethic: "Be confident on adding high value to someone else and be rigorous, be tenacious and work like hell.'


Negative tweets:
b'RT @thenatbird: april fools is impossible now. i just woke up to \xe2\x80\x9celon musk drops rap single about harambe\xe2\x80\x9d and \xe2\x80\x9cmussolini\xe2\x80\x99s granddaughter\xe2\x80\xa6'
b"Elon Musk on work ethic. Another person it must be terrifying to compete against. (From Ashlee Vance's book) https://t.co/l7AMxFV4Gq"
b"RT @CNBCnow: BREAKING: Judge orders SEC and Elon Musk to confer over next 2 weeks to try to settle issue and doesn't rule on contempt. Elon\xe2\x80\xa6"
b'RT @ElJuanpaZurita: ELON MUSK ES EL TONY STARK DE ESTA GENERACI\xc3\x93N BRO'
b'RT @AIejaguar: Elon Musk: babe why\xe2\x80\x99re you mad?\n\nGrimes: https://t.co/bFmgUBvG2A'
