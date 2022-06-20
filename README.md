# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Reddit Classification & NLP


## Problem Statement

Reddit is a website full of many different subreddits. Subreddits are their own forums pertaining to that specific topic, and there are many different ones to look through. After gathering data from two different subreddits, I wanted to see if I could build a binary classification model that could classify text as belonging to either one subreddit or the other. The two subreddits I chose were r/Marvel and r/harrypotter. To measure success, I will be looking at the accuracy score, and whether it beats the baseline model.

## Data Collection

The data used in this analysis/modeling was collected using the Reddit Pushift API. A function was written to pull the data from whichever subreddits I chose (in this case r/Marvel and r/harrypotter) and then concated into a pandas dataframe. The data ranged from December 2021 to April 2022. Initally 15,000 posts from each subreddit was collected, but after the data cleaning process, I wound up having 6109 posts from r/harrypotter and 3491 posts from r/Marvel.

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**link_flair_text**|*object*|subreddit|Tags that users place on their submissions.|
|**over_18**|*bool*|subreddit|Whether the user is over or under 18.|
|**selftext**|*object*|subreddit|The text in the body of the post.|
|**subreddit**|*object*|subreddit|The name of the subreddit the information comes from.|
|**title**|*object*|subreddit|The text that comes from the title of the post.|

## Summary of Analysis

For this project, the first part was the data collection and cleaning that was described above. After the data was cleaned, EDA was performed on the text to see which words and phrases were most prevalent in each subreddit. After that came the modeling. I tried several different models, but wound up sticking with Logistic Regression and Count Vectorizer for the text. I used 'english' stop words and a min_df of 2 for the vectorizer. The features included in the model were 'selftext' and 'title'. This model wound up with an accuracy score of 0.97, which well beat the baseline model.

## Conclusions and Recommendations

During the modeling process, I found the good 'ol Logistic Regression model to work the best. It performed remarkably well with these two subreddits, and my hypoethesis is that the two subreddits are so different that the model was easily able to pick up on that. There was a consistent pattern where in the r/harrypotter subreddit, the word 'harry' was both the most common word in the title and selftext and also had the most impactful coefficient. Similarly, in the r/Marvel subreddit the word 'marvel' was both the most common in title and selftext and also carried the most weight with the coefficient. See some of those coefficients below, with the most impact on the model:

|Word|Location|Coefficient|Interpretation|
|---|---|---|---|
|**harry**|*title*|8.23|This word was 8.23 times more likely to be in r/harrypotter vs r/Marvel.|
|**harry**|*selftext*|7.81|This word was 7.81 times more likely to be in r/harrypotter vs r/Marvel.|
|**hogwarts**|*title*|5.91|This word was 5.91 times more likely to be in r/harrypotter vs r/Marvel.|
|**books**|*selftext*|4.52|This word was 4.52 times more likely to be in r/harrypotter vs r/Marvel.|
|**voldemort**|*title*|4.34|This word was 4.34 times more likely to be in r/harrypotter vs r/Marvel.|
|**hogwarts**|*selftext*|4.10|This word was 4.10 times more likely to be in r/harrypotter vs r/Marvel.|
|**dumbledore**|*title*|4.03|This word was 4.03 times more likely to be in r/harrypotter vs r/Marvel.|
|---|---|---|---|
|**marvel**|*title*|-0.94|This word is 94% more likely to be in r/Marvel vs r/harrypotter.|
|**marvel**|*selftext*|-0.94|This word is 94% more likely to be in r/Marvel vs r/harrypotter.|
|**comics**|*selftext*|-0.89|This word is 89% more likely to be in r/Marvel vs r/harrypotter.|
|**comic**|*selftext*|-0.88|This word is 88% more likely to be in r/Marvel vs r/harrypotter.|
|**mcu**|*title*|-0.87|This word is 87% more likely to be in r/Marvel vs r/harrypotter.|
|**mcu**|*selftext*|-0.85|This word is 85% more likely to be in r/Marvel vs r/harrypotter.|
|**moon**|*title*|-0.79|This word is 79% more likely to be in r/Marvel vs r/harrypotter.|

For this project, I didn't go into the missclassifications the model was making, but that is something that would be worth looking into moving forward. Another interesting thing to try would be to add the words 'harry' and 'marvel' to the stop words list to see if the model is still as effective at distinguishing between the two subreddits. There are also other words and bigrams that would be interesting to add to the stop words as well.

My recommendations for this model would be to continue to gather data for different time periods moving forward and testing the model. Since both of these fields change fairly regularly, any new data could potentially affect the accuracy of the model. Many of the words that were showing up in each subreddit frequently corresponded to current shows and/or movies that are airing or releasing during the time period of the posts. If we were to collect new data 6 months from now, I'm sure some of those most frequent words would be different to reflect the newer stuff that is popular. 
