# #poweroutages
## Team Members
- Dawn Graham | [dawngraham.github.io](https://dawngraham.github.io/)
- Sharnique Beck | [github.com/sharnb](https://github.com/sharnb)
- Yalim Demirkesen | [github.com/demirkeseny](https://github.com/demirkeseny)

## Problem Statement
During a disaster, residential areas often experience massive power outages, that in many cases last for days. Traditional methods to map power outages include live feeds and data that is provided by major utility companies as well as on satellite data that capture the extent of light emitted at night. This tool will utilize news feeds and/or posts on social media to identify “hot spots” of concern and areas suffering from power outages (assuming that these posts are reported via social media applications on mobile phone). Following an event, the tool will scan relevant news or social media websites to identify localities likely to suffer from power outage.

## Objectives
The goal of this project is to utilize news feeds and/or posts on social media to identify “hot spots” of concern and areas suffering from power outages (assuming that these posts are reported via social media applications on mobile phone) for a non-profit client. Following an event, the tool will scan relevant news or social media websites to identify localities likely to suffer from power outage.

## Methodology
We focused on Twitter because people often use it to provide live text updates and it has a well-documented API. We ultimately used [TwitterScraper](https://github.com/taspinar/twitterscraper) and [Data Miner](https://data-miner.io/) to get historical information from Twitter. Using keyword and location-based queries, we scraped over 38,000 tweets. We focused on the New England area (CT, NH, MA, ME, NY, RI, VT) from September 2009 through December 2012 as a starting point. We had to come up with several techniques to understand the location of the tweet in order to identify possible areas affected by outages. 

We used [15 Years Of Power Outages](http://insideenergy.org/2014/08/18/data-explore-15-years-of-power-outages/) data compiled by Inside Energy from the Department of Energy to determine times and locations of verified outages.

After preparing our data, we used Bokeh to create frequency charts to indicate the usage of certain words related to power outages. On this graph, we were able to identify sudden increases in the usage of some keywords and phrases. To understand the traffic between the accounts during the power outages we created a network graph using Bokeh and displayed the interaction of the accounts that might be helpful in identifying hot spots. 

In the modeling stage, we used Logistic Regression to get words most associated with tweets made during times of power outages. These words are used again in the frequency chart to verify their correlation with the event. After removing punctuations and stop words, lemmatizing, and vectorizing, we obtained a Logistic Regression model with 71.6% accuracy. During modeling, we also utilized k-Means clustering. The model clustered all the tweets into three subgroups based on the vectorized text. They seem to be grouped according to tweets that: 1) are about “storm”, 2) are about “power”, and 3) include a link. Further refinement of the k-Means model could prove helpful in identifying tweets that are reporting outages in specific areas.

## Constraints
Twitter’s free API will only return the past 7 days of tweets. Location data for historical tweets seems to be available beginning September 2009. Twitter assigns tweet location both by in-app geolocation (which the majority of users do not turn on) and from the location info that the user writes into their profile. Location info from profiles are not very reliable: The user might be in a different location now than where they were a few years ago, or they may be tweeting from a location other than the one listed in their profile.

Natural language processing presents a challenge. People do tweet about locations of power outages, but in varied ways: a specific street address with no city, city with no state, a neighborhood or region name, abbreviations (`brklyn` for Brooklyn), etc.
## Materials
### Data

Under *raw-data* file there are the initial CSV files that we cleaned and transformed to derive the files under the *data* file. Under the *raw-data*, there are the files that are scraped from each state in New England, the utility companies that are operating nationwide and record of all power outages in the last 15 years.


Under the *data* file:


|Document Name|Description|  
|-|-|
|combined_monthlytweets|state and handle combined tweets with the  corresponding queries|
|combined_tweet_outages|contains all info from combined_monthly_tweets plus ‘outage’ column, where 1 means the tweet occurred during a verified power outage|
|Grid_Disruption_00_14_standardized_clean|cleaned dataset of Grid_Disruption_00_14_standardized|
|monthlytweets_cleaned|cleaned dataset of monthlytweets|
|monthlytweets_cleaned_2|non-English characters removed|
|outages|includes power outage start & end time, respondent, geographic area, state, and number of customers affected|


### Notebooks


Under the *notebooks* folder, there are files that we run all our analysis and modeling. Since we also did a prework to understand what the most efficient way is to scrape  works, there is a subfolder called scraping including all the tests that we run to improve our scraping:

|Document Name|Description|  
|-|-|
|01_scrape_by_month|scraper to get a month of tweets at a time|
|02_clean_grid_disruption_00_14_standardized_data|cleaning the historical records about all the power outages in the last 15 years|
|03_preprocessing|cleaning the monthlytweets|
|04_tweet_source|understanding the source and the destination of the tweets|
|05_creating_network_outages|network diagram for the interactions between the users|
|06_outages_state_and_time|The first part of this notebook assigns location of power outages (as state abbreviations) to power outages. It then transforms event and restoration info to datetime values. The last adds a column to tweets data indicating if the tweet was at the same time as a verified outage.|
|07_frequency_charts|creating the frequency chart to understand the word usage from September 2009 until December 2012|
|08_tweet_vectorizer_clustering|running the logistic regression and k-means clustering models|



### Slides

View the [presentation slides](https://docs.google.com/presentation/d/e/2PACX-1vT1wu3kyhYFbNV-HBbfR1TkeqLgsnL7mhZenoh2zy8E3OUZ-6ajqjmyId31ukWqv99IyPwecIYg9hgB/pub?start=false&loop=false&delayms=3000&slide=id.p).


## Implementation

The Twitter API can be used to compile live tweets based on queries identified here. Following a disaster, event-specific keywords (such as the name of the event paired with a location - `sandy`, `masandy`, `nhsandy`, etc.) can be added to queries to collect relevant tweets.

## Future Developments

- Look more into Natural Language Processing(NLP) in order to pull locations mentioned in tweets, and usernames
- Compile a comprehensive list of State cities, towns, boroughs, and neighborhoods.
- If user location is not available use (NLP) to verify states from users or handles mentioned
- Refine k-Means clustering to help identify relevant tweets
- Do additional modeling incorporating more features to better locate hotspots
- Use location information to generate a map visualizing relevant tweets
- Connect models to live Twitter feed using Twitter API
- Integrate notebooks and create a pipeline to move data through needed processes
- Develop an app with a dashboard for live data



## References

- [Resources for Research on Crisis Informatics](http://crisisnlp.qcri.org/)
- [Using Social Sensors for Detecting Power Outages in the Electrical Utility Industry](https://pdfs.semanticscholar.org/60df/7d51b2e479ab0737b034b2e6375940eaca18.pdf)
- [Identifying and tracking power outages worldwide through social media](https://geospatial.blogs.com/geospatial/2017/07/identifying-and-tracking-power-outages-worldwide-through-social-media.html)
- [Best #poweroutage hashtags (for Instagram)](<http://best-hashtags.com/hashtag/poweroutage/>)
- [NationalGridus.com](https://www.nationalgridus.com/MA-Home/Storms-Outages/Outage-Map)
- [Twitter API Docs](https://developer.twitter.com/en/docs)
- [How to get a count of followers from Twitter API and trendline](https://stackoverflow.com/questions/4084909/how-to-get-a-count-of-followers-from-twitter-api-and-trendline)
- [Accessing the Twitter API with Python](https://stackabuse.com/accessing-the-twitter-api-with-python/)
- [Tweepy library docs](http://www.tweepy.org/)
- [Prompt Cloud](https://www.promptcloud.com/blog/scrape-twitter-data-using-python-r)
