---
layout: post
title: "Twitter Stream Exploration"
date: "2016-03-17 17:35:59 -0600"
comments: true
tags: notebook, english, twitter, exploration
---
Twitter is a great source of live data, which can be used in many different areas, all concurring to the core of it's functionality: social data. In this exploratory analysis I will go from extracting twitter data to doing some basic analysis on it.

For a live exploration of twitter data, the stream must be accessed. For more information on the twitter stream take a look at the [documentation](https://dev.twitter.com/).

For this study the StreamListener from the [tweetpy](https://github.com/tweepy/tweepy) library will be used. I will also be using TextBlob for sentiment analysis and pandas, json and matplotlib for handling data.

```python
from tweepy.streaming import StreamListener
from tweepy import Stream
from tweepy import OAuthHandler

from textblob import TextBlob

import json
import pandas as pd

%matplotlib inline
import matplotlib.pyplot as plt
```

### Import keys
I usually have a git-ignored file with personal configurations in my repos. In this case the file is `myKeys.py` and contains my oauth keys. These are my personal keys, you can get yours [here](https://apps.twitter.com/).


```python
import myKeys

api_key = myKeys.api_key
api_secret = myKeys.api_secret
access_token_key = myKeys.access_token_key
access_token_secret = myKeys.access_token_secret
```

### Create a listener to handle everey tweet

This class defines a handler for the tweet event. This class is the spine of this exploration's processing. It receives every tweet and loads it from the json format, along with the tweet sentiment into a pandas DataFrame. It adds the score of every tweet to a sentimentIntegral variable that stores the result score of the labels being tracked.


```python
class ColorListener(StreamListener):

    def __init__(self):
        self.sentimentIntegral = 0
        self.tweets = pd.DataFrame(columns=('tweet', 'sentiment'))

    def on_data(self, data):
        try:
            tweet = json.loads(data)
            blob = TextBlob(tweet['text'])
            self.sentimentIntegral += blob.sentiment[0]
            print "{0:.2f}".format(round(blob.sentiment[0],2)), "{0:.2f}".format(round(self.sentimentIntegral,2))
            row = pd.Series([tweet['text'], blob.sentiment[0]], index=['tweet', 'sentiment'])
            self.tweets = self.tweets.append(row, ignore_index=True)
        except UnboundLocalError:
            raise UnboundLocalError
        except:
            pass
        return True

    def getTotalScore(self):
        return self.sentimentIntegral

    def on_error(self, status):
        print "Error: ", status
```

### Instance and running

The listener object is created and hooked to the twitter stream with the proper authentication. The stream is later filtered with a specific search term, which is selected to represent a specific social phenomena.


```python
cListener = ColorListener()
auth = OAuthHandler(api_key, api_secret)
auth.set_access_token(access_token_key, access_token_secret)

stream = Stream(auth, cListener)

# Start reading stream for english tweets with the color words
stream.filter(languages=['en'], track=['red', 'green','blue'])
```

### Analize DataFrame

Now we hawe a pandas dataframe inside the cListener object we can analyze.


```python
df = cListener.tweets
print len(df.index) # Number of rows
```

    1115



```python
df.head() # How the data looks like
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RT @5REDVELVET: [OFFICIAL] 160315 RED VELVET #...</td>
      <td>-0.375000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RT @WampsBraintree: Wamp Train scheduled for 5...</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RT @thickred3x: Order Red &amp;amp; @JovanJordanXX...</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@lipdistrikt Thks 4 following! - Please vote f...</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>RT @UFCONFOX: Dustin Poirier vs. Bobby Green j...</td>
      <td>-0.200000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.plot(figsize=(16, 8)) # Plot the sentiment as a time series
```


![png]({{ site.static_folder }}/img/notebooks/twitter01.png)



```python
df['sentiment'].plot.kde(figsize=(16, 8))
```


![png]({{ site.static_folder }}/img/notebooks/twitter02.png)


### Mining text
The regular expressions library will be used to mine text


```python
import re
```

And a function created to separate the different terms tracked


```python
def wordInText(word, text):
    word = word.lower()
    text = text.lower()
    match = re.search(word, text)
    if match:
        return 1
    return 0
```

Create new columns corresponding to term in tweet.


```python
# New column equals applying the wordInText function to every element of the column text
df['red'] = df['tweet'].apply(lambda tweet: wordInText('red', tweet))
df['green'] = df['tweet'].apply(lambda tweet: wordInText('green', tweet))
df['blue'] = df['tweet'].apply(lambda tweet: wordInText('blue', tweet))
```


```python
df.head() # How the data looks like
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet</th>
      <th>sentiment</th>
      <th>red</th>
      <th>green</th>
      <th>blue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RT @5REDVELVET: [OFFICIAL] 160315 RED VELVET #...</td>
      <td>-0.375000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RT @WampsBraintree: Wamp Train scheduled for 5...</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RT @thickred3x: Order Red &amp;amp; @JovanJordanXX...</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@lipdistrikt Thks 4 following! - Please vote f...</td>
      <td>0.166667</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>RT @UFCONFOX: Dustin Poirier vs. Bobby Green j...</td>
      <td>-0.200000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
print df['red'].value_counts()
```

    0    654
    1    461
    Name: red, dtype: int64



```python
df[['red','green','blue']].sum()
```


    red      461
    green    249
    blue     410
    dtype: int64


```python
df[['red','green','blue']].sum().plot(kind='bar',color=['r','g','b'],figsize=(16, 8))
```

![png]({{ site.static_folder }}/img/notebooks/twitter03.png)
