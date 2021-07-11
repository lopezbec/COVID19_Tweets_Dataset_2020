-   [Data Organization](#data-organization)
-   [Data Statistics](#data-statistics)
    -   [General Statistics](#general-statistics)
    -   [Language Statistics](#language-statistics)
    -   [English Sentiment Analaysis](#english-sentiment-analaysis)
    -   [English Named Entity Recognition, Mentions, and
        Hashtags](#english-named-entity-recognition-mentions-and-hashtags)
    -   [Spanish Sentiment Analaysis](#spanish-sentiment-analaysis)
    -   [Spanish Named Entity
        Recognition](#spanish-named-entity-recognition)
    -   [Data Collection Process
        Inconsistencies](#data-collection-process-inconsistencies)
-   [Hydrating Tweets](#hydrating-tweets)
    -   [Using our TWARC Notebook](#using-our-twarc-notebook)
        -   [Using Hydrator](#using-hydrator)
        -   [Using Twarc](#using-twarc)
-   [Inquiries](#inquiries)
-   [Licensing](#licensing)
-   [References](#references)

The repository contains an ongoing collection of tweets associated with
the novel coronavirus COVID-19 since January 22nd, 2020.

As of 12/31/2020 there were a total of **1,231,191,599** tweets
collected. The tweets are collected using Twitter’s trending topics and
selected keywords. Moreover, the tweets from [Chen et
al. (2020)](https://github.com/echen102/COVID-19-TweetIDs) was used to
supplement the dataset by hydrating non-duplicated tweets. These tweets
are just a sample of all the tweets generated that are provided by
Twitter, and it does not represent the whole population of tweets at any
given point.

**Citation**

Christian Lopez, and Caleb Gallemore (2020) An Augmented Multilingual
Twitter Dataset for Studying the COVID-19 Infodemic. DOI:
10.21203/rs.3.rs-95721/v1
<a href="https://www.researchsquare.com/article/rs-95721/v1" class="uri">https://www.researchsquare.com/article/rs-95721/v1</a>

Data Organization
-----------------

The dataset is organized by hour (UTC) , month, and by tables. The
description of all the features in all five tables is provided below.
For example, the path
“./Summary\_Details/2020\_01/2020\_01\_22\_00\_Summary\_Details.csv”
contains all the summary details of the tweets collection on January
22nd at 00:00 UTC time.

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 9px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Features Description
</caption>
<thead>
<tr>
<th style="text-align:left;font-weight: bold;">
Table
</th>
<th style="text-align:left;font-weight: bold;">
Feature Name
</th>
<th style="text-align:left;font-weight: bold;">
Description
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Primary key
</td>
<td style="text-align:left;">
Tweet\_ID
</td>
<td style="text-align:left;">
Integer representation of the tweets unique identifier
</td>
</tr>
<tr>
<td style="text-align:left;">
1.Summary\_Details
</td>
<td style="text-align:left;">
Language
</td>
<td style="text-align:left;">
When present, indicates a BCP47 language identifier corresponding to the
machine-detected language of the Tweet text
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Geolocation\_cordinate
</td>
<td style="text-align:left;">
Indicates whether or not the geographic location of the tweet was
reported
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
RT
</td>
<td style="text-align:left;">
Indicates if the tweet is a retweet (YES) or original tweet (NO)
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Likes
</td>
<td style="text-align:left;">
Number of likes for the tweet
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Retweets
</td>
<td style="text-align:left;">
Number of times the tweet was retweeted
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Country
</td>
<td style="text-align:left;">
When present, indicates a list of uppercase two-letter country
codes from which the tweet comes
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Date\_Created
</td>
<td style="text-align:left;">
UTC date and time the tweet was created
</td>
</tr>
<tr>
<td style="text-align:left;">
2.Summary\_Hastag
</td>
<td style="text-align:left;">
Hashtag
</td>
<td style="text-align:left;">
Hashtag (\#) present in the tweet
</td>
</tr>
<tr>
<td style="text-align:left;">
3.Summary\_Mentions
</td>
<td style="text-align:left;">
Mentions
</td>
<td style="text-align:left;">
Mention (@) present in the tweet
</td>
</tr>
<tr>
<td style="text-align:left;">
4.Summary\_Sentiment
</td>
<td style="text-align:left;">
Sentiment\_Label
</td>
<td style="text-align:left;">
Most probable tweet sentiment (neutral, positive, negative)
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Logits\_Neutral
</td>
<td style="text-align:left;">
Non-normalized prediction for neutral sentiment
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Logits\_Positive
</td>
<td style="text-align:left;">
Non-normalized prediction for positive sentiment
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Logits\_Negative
</td>
<td style="text-align:left;">
Non-normalized prediction for negative sentiment
</td>
</tr>
<tr>
<td style="text-align:left;">
5.Summary\_NER
</td>
<td style="text-align:left;">
NER\_text
</td>
<td style="text-align:left;">
Text stating a named entity recognized by the NER algorithm
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Start\_Pos
</td>
<td style="text-align:left;">
Initial character position within the tweet of the NER\_text
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
End\_Pos
</td>
<td style="text-align:left;">
End character position within the tweet of the NER\_text
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
NER\_Label Prob
</td>
<td style="text-align:left;">
Label and probability of the named entity recognized by the NER
algorithm
</td>
</tr>
<tr>
<td style="text-align:left;">
6.Summary\_Sentiment\_ES
</td>
<td style="text-align:left;">
Sentiment\_Label
</td>
<td style="text-align:left;">
Most probable tweet sentiment (neutral, positive, negative)
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Probability\_pos
</td>
<td style="text-align:left;">
Probability of the tweets sentiment being positive (\<=0.33 is negative,
\>0.33 OR \<0.66 is neutral, else positve)
</td>
</tr>
<tr>
<td style="text-align:left;">
6.Summary\_NER\_ES
</td>
<td style="text-align:left;">
NER\_text
</td>
<td style="text-align:left;">
Text stating a named entity recognized by the NER algorithm
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Start\_Pos
</td>
<td style="text-align:left;">
Initial character position within the tweet of the NER\_text
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
End\_Pos
</td>
<td style="text-align:left;">
End character position within the tweet of the NER\_text
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
NER\_Label Prob
</td>
<td style="text-align:left;">
Label and probability of the named entity recognized by the NER
algorithm
</td>
</tr>
</tbody>
</table>

For more information visit: [Twitter
API](https://developer.twitter.com/en/docs) and the [Documentation for
API
Tweet-object](https://developer.twitter.com/en/docs/twitter-api/v1/data-dictionary/overview/tweet-object)

Data Statistics
===============

General Statistics
------------------

As of 12/31/2020:

Total Number of tweets: **1,231,191,599**

Average daily number of tweets: **144,283**

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 12px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Summary Statistics per Month
</caption>
<thead>
<tr>
<th style="text-align:right;font-weight: bold;">
Year
</th>
<th style="text-align:left;font-weight: bold;">
Month
</th>
<th style="text-align:left;font-weight: bold;">
Daily Avg. Original
</th>
<th style="text-align:left;font-weight: bold;">
Daily Avg. Retweets
</th>
<th style="text-align:left;font-weight: bold;">
Daily Avg. Tweets
</th>
<th style="text-align:left;font-weight: bold;">
Total of Orignal
</th>
<th style="text-align:left;font-weight: bold;">
Total of Retweets
</th>
<th style="text-align:left;font-weight: bold;">
Total of Tweets
</th>
<th style="text-align:left;font-weight: bold;">
Total with Geolocation
</th>
<th style="text-align:left;font-weight: bold;">
Max No. Retweets
</th>
<th style="text-align:left;font-weight: bold;">
Max No. Likes
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
5,947
</td>
<td style="text-align:left;">
30,576
</td>
<td style="text-align:left;">
35,501
</td>
<td style="text-align:left;">
1,958,346
</td>
<td style="text-align:left;">
7,852,504
</td>
<td style="text-align:left;">
9,810,850
</td>
<td style="text-align:left;">
1,773
</td>
<td style="text-align:left;">
674,151
</td>
<td style="text-align:left;">
334,802
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
2
</td>
<td style="text-align:left;">
10,978
</td>
<td style="text-align:left;">
29,918
</td>
<td style="text-align:left;">
40,604
</td>
<td style="text-align:left;">
7,624,648
</td>
<td style="text-align:left;">
21,944,443
</td>
<td style="text-align:left;">
29,568,948
</td>
<td style="text-align:left;">
8,103
</td>
<td style="text-align:left;">
469,739
</td>
<td style="text-align:left;">
637,589
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
3
</td>
<td style="text-align:left;">
13,095
</td>
<td style="text-align:left;">
44,714
</td>
<td style="text-align:left;">
56,283
</td>
<td style="text-align:left;">
12,610,824
</td>
<td style="text-align:left;">
46,659,589
</td>
<td style="text-align:left;">
59,270,412
</td>
<td style="text-align:left;">
19,952
</td>
<td style="text-align:left;">
1,064,693
</td>
<td style="text-align:left;">
1,255,858
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
4
</td>
<td style="text-align:left;">
30,091
</td>
<td style="text-align:left;">
89,513
</td>
<td style="text-align:left;">
119,859
</td>
<td style="text-align:left;">
20,591,357
</td>
<td style="text-align:left;">
60,301,889
</td>
<td style="text-align:left;">
80,893,244
</td>
<td style="text-align:left;">
38,213
</td>
<td style="text-align:left;">
649,823
</td>
<td style="text-align:left;">
662,005
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
5
</td>
<td style="text-align:left;">
35,163
</td>
<td style="text-align:left;">
99,928
</td>
<td style="text-align:left;">
135,709
</td>
<td style="text-align:left;">
26,258,213
</td>
<td style="text-align:left;">
73,618,083
</td>
<td style="text-align:left;">
99,876,289
</td>
<td style="text-align:left;">
47,684
</td>
<td style="text-align:left;">
1,007,616
</td>
<td style="text-align:left;">
929,811
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
51,033
</td>
<td style="text-align:left;">
142,569
</td>
<td style="text-align:left;">
193,096
</td>
<td style="text-align:left;">
34,786,076
</td>
<td style="text-align:left;">
95,171,388
</td>
<td style="text-align:left;">
129,957,461
</td>
<td style="text-align:left;">
58,138
</td>
<td style="text-align:left;">
790,652
</td>
<td style="text-align:left;">
882,693
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
53,720
</td>
<td style="text-align:left;">
155,042
</td>
<td style="text-align:left;">
209,738
</td>
<td style="text-align:left;">
39,611,015
</td>
<td style="text-align:left;">
111,876,344
</td>
<td style="text-align:left;">
151,487,359
</td>
<td style="text-align:left;">
56,808
</td>
<td style="text-align:left;">
615,768
</td>
<td style="text-align:left;">
1,287,117
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
8
</td>
<td style="text-align:left;">
51,330
</td>
<td style="text-align:left;">
143,291
</td>
<td style="text-align:left;">
195,037
</td>
<td style="text-align:left;">
37,549,475
</td>
<td style="text-align:left;">
102,834,375
</td>
<td style="text-align:left;">
140,383,850
</td>
<td style="text-align:left;">
55,912
</td>
<td style="text-align:left;">
2,183,434
</td>
<td style="text-align:left;">
860,162
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
50,068
</td>
<td style="text-align:left;">
132,040
</td>
<td style="text-align:left;">
182,947
</td>
<td style="text-align:left;">
35,861,979
</td>
<td style="text-align:left;">
92,957,247
</td>
<td style="text-align:left;">
128,819,226
</td>
<td style="text-align:left;">
32,381
</td>
<td style="text-align:left;">
1,925,489
</td>
<td style="text-align:left;">
839,689
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
54,489
</td>
<td style="text-align:left;">
137,225
</td>
<td style="text-align:left;">
198,708
</td>
<td style="text-align:left;">
41,062,885
</td>
<td style="text-align:left;">
104,195,279
</td>
<td style="text-align:left;">
144,962,625
</td>
<td style="text-align:left;">
319,101
</td>
<td style="text-align:left;">
946,810
</td>
<td style="text-align:left;">
785,385
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
11
</td>
<td style="text-align:left;">
64,125
</td>
<td style="text-align:left;">
111,686
</td>
<td style="text-align:left;">
177,062
</td>
<td style="text-align:left;">
45,096,171
</td>
<td style="text-align:left;">
77,885,575
</td>
<td style="text-align:left;">
122,981,746
</td>
<td style="text-align:left;">
26,488
</td>
<td style="text-align:left;">
1,187,438
</td>
<td style="text-align:left;">
619,643
</td>
</tr>
<tr>
<td style="text-align:right;">
2020
</td>
<td style="text-align:left;">
12
</td>
<td style="text-align:left;">
64,840
</td>
<td style="text-align:left;">
121,149
</td>
<td style="text-align:left;">
186,852
</td>
<td style="text-align:left;">
49,065,436
</td>
<td style="text-align:left;">
87,366,002
</td>
<td style="text-align:left;">
133,179,589
</td>
<td style="text-align:left;">
3,277,244
</td>
<td style="text-align:left;">
1,402,911
</td>
<td style="text-align:left;">
1,038,164
</td>
</tr>
</tbody>
</table>

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Details/Tweets%20per%20Day.png)

There is a total of 3,941,797 tweets with geolocation information, which
are shown on a map below:

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Details/GeoTweets.png)

Language Statistics
-------------------

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 12px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Tweets Language Summary
</caption>
<thead>
<tr>
<th style="text-align:left;font-weight: bold;">
Languages
</th>
<th style="text-align:left;font-weight: bold;">
Total No. Tweets
</th>
<th style="text-align:right;font-weight: bold;">
Percentage of Tweets
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
English
</td>
<td style="text-align:left;">
836,946,873
</td>
<td style="text-align:right;">
68.18
</td>
</tr>
<tr>
<td style="text-align:left;">
Spanish; Castilian
</td>
<td style="text-align:left;">
150,043,766
</td>
<td style="text-align:right;">
12.22
</td>
</tr>
<tr>
<td style="text-align:left;">
Portuguese
</td>
<td style="text-align:left;">
45,749,631
</td>
<td style="text-align:right;">
3.73
</td>
</tr>
<tr>
<td style="text-align:left;">
Bahasa
</td>
<td style="text-align:left;">
32,794,776
</td>
<td style="text-align:right;">
2.67
</td>
</tr>
<tr>
<td style="text-align:left;">
French
</td>
<td style="text-align:left;">
32,717,712
</td>
<td style="text-align:right;">
2.67
</td>
</tr>
<tr>
<td style="text-align:left;">
Others
</td>
<td style="text-align:left;">
129,391,297
</td>
<td style="text-align:right;">
10.54
</td>
</tr>
</tbody>
</table>

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Details/Tweets%20by%20Language%20Line%20plot.png)

English Sentiment Analaysis
---------------------------

The sentiment of all the English tweets was estimated using a
state-or-the-art Twitter Sentiment algorithm
[BB\_twtr](https://arxiv.org/abs/1704.06125). [(See code
here)](https://github.com/leelaylay/TweetSemEval) .

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Sentiment/Tweets%20Sentiment.png)

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Sentiment/Tweets%20Sentiment%20Percentage.png)

English Named Entity Recognition, Mentions, and Hashtags
--------------------------------------------------------

The Named Entity Recognition algorithm of
[flairNLP](https://github.com/flairNLP/flair) was used to extract topics
of conversation about PERSON, LOCATION, ORGANIZATION, and others. Below
are the top 5 NER, Mentions (@) and Hastags (\#)

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 12px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Top 5 Mentions, Hashtags, and NER
</caption>
<thead>
<tr>
<th style="text-align:left;font-weight: bold;">
Mentions
</th>
<th style="text-align:left;font-weight: bold;">
Hashtags
</th>
<th style="text-align:left;font-weight: bold;">
NER Person
</th>
<th style="text-align:left;font-weight: bold;">
NER Location
</th>
<th style="text-align:left;font-weight: bold;">
NER Organization
</th>
<th style="text-align:left;font-weight: bold;">
NER Miscellaneous
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
@realDonaldTrump
</td>
<td style="text-align:left;">
\#covid19
</td>
<td style="text-align:left;">
trump
</td>
<td style="text-align:left;">
us
</td>
<td style="text-align:left;">
cdc
</td>
<td style="text-align:left;">
covid-19
</td>
</tr>
<tr>
<td style="text-align:left;">
14,106,218
</td>
<td style="text-align:left;">
72,109,143
</td>
<td style="text-align:left;">
35,009,016
</td>
<td style="text-align:left;">
19,254,380
</td>
<td style="text-align:left;">
8,213,068
</td>
<td style="text-align:left;">
23,458,865
</td>
</tr>
<tr>
<td style="text-align:left;">
@realdonaldtrump
</td>
<td style="text-align:left;">
\#coronavirus
</td>
<td style="text-align:left;">
biden
</td>
<td style="text-align:left;">
china
</td>
<td style="text-align:left;">
trump
</td>
<td style="text-align:left;">
americans
</td>
</tr>
<tr>
<td style="text-align:left;">
6,958,036
</td>
<td style="text-align:left;">
36,475,102
</td>
<td style="text-align:left;">
5,579,441
</td>
<td style="text-align:left;">
13,541,311
</td>
<td style="text-align:left;">
3,158,280
</td>
<td style="text-align:left;">
13,320,769
</td>
</tr>
<tr>
<td style="text-align:left;">
@joebiden
</td>
<td style="text-align:left;">
\#covid
</td>
<td style="text-align:left;">
covid
</td>
<td style="text-align:left;">
america
</td>
<td style="text-align:left;">
senate
</td>
<td style="text-align:left;">
coronavirus
</td>
</tr>
<tr>
<td style="text-align:left;">
3,037,511
</td>
<td style="text-align:left;">
7,505,813
</td>
<td style="text-align:left;">
5,426,934
</td>
<td style="text-align:left;">
6,981,781
</td>
<td style="text-align:left;">
2,070,061
</td>
<td style="text-align:left;">
8,058,398
</td>
</tr>
<tr>
<td style="text-align:left;">
@JoeBiden
</td>
<td style="text-align:left;">
\#covid\<u+30fc\>19
</td>
<td style="text-align:left;">
donald trump
</td>
<td style="text-align:left;">
uk
</td>
<td style="text-align:left;">
covid
</td>
<td style="text-align:left;">
covid
</td>
</tr>
<tr>
<td style="text-align:left;">
1,901,092
</td>
<td style="text-align:left;">
2,252,353
</td>
<td style="text-align:left;">
3,883,767
</td>
<td style="text-align:left;">
6,531,363
</td>
<td style="text-align:left;">
1,945,187
</td>
<td style="text-align:left;">
7,120,847
</td>
</tr>
<tr>
<td style="text-align:left;">
@narendramodi
</td>
<td style="text-align:left;">
\#stayhome
</td>
<td style="text-align:left;">
fauci
</td>
<td style="text-align:left;">
india
</td>
<td style="text-align:left;">
pfizer
</td>
<td style="text-align:left;">
american
</td>
</tr>
<tr>
<td style="text-align:left;">
1,099,761
</td>
<td style="text-align:left;">
1,303,292
</td>
<td style="text-align:left;">
3,017,147
</td>
<td style="text-align:left;">
4,386,858
</td>
<td style="text-align:left;">
1,212,782
</td>
<td style="text-align:left;">
3,068,408
</td>
</tr>
</tbody>
</table>

Spanish Sentiment Analaysis
---------------------------

The sentiment of all the Spanish tweets was estimated using sentiment
analysis in spanish based on neural networks model of the the python
library [sentiment-analysis-spanish
0.0.25](https://pypi.org/project/sentiment-analysis-spanish/).

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Sentiment_ES/Tweets%20Sentiment%20ES.png)

![](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Summary_Sentiment_ES/Tweets%20Sentiment%20Percentage%20ES.png)

Spanish Named Entity Recognition
--------------------------------

The Spanish Named Entity Recognition algorithm of
[flairNLP](https://github.com/flairNLP/flair) was used to extract topics
of conversation about PERSON, LOCATION, ORGANIZATION, and others. Below
are the top 5 NER of all the Spanish tweets (\* some special character
in Spanish are not correctly represented in the readme file, like
character with accent mark)

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 12px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Top 5 Mentions, Hashtags, and NER
</caption>
<thead>
<tr>
<th style="text-align:left;font-weight: bold;">
NER Person
</th>
<th style="text-align:left;font-weight: bold;">
NER Location
</th>
<th style="text-align:left;font-weight: bold;">
NER Organization
</th>
<th style="text-align:left;font-weight: bold;">
NER Miscellaneous
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
covid
</td>
<td style="text-align:left;">
mÃ©xico
</td>
<td style="text-align:left;">
gobierno
</td>
<td style="text-align:left;">
covid-19
</td>
</tr>
<tr>
<td style="text-align:left;">
1,082,802
</td>
<td style="text-align:left;">
1,248,704
</td>
<td style="text-align:left;">
923,267
</td>
<td style="text-align:left;">
9,353,323
</td>
</tr>
<tr>
<td style="text-align:left;">
nicolasmaduro
</td>
<td style="text-align:left;">
venezuela
</td>
<td style="text-align:left;">
mippcivzla
</td>
<td style="text-align:left;">
covid19
</td>
</tr>
<tr>
<td style="text-align:left;">
563,581
</td>
<td style="text-align:left;">
1,159,499
</td>
<td style="text-align:left;">
722,054
</td>
<td style="text-align:left;">
4,762,873
</td>
</tr>
<tr>
<td style="text-align:left;">
lopezobrador
</td>
<td style="text-align:left;">
espaÃ±a
</td>
<td style="text-align:left;">
oms
</td>
<td style="text-align:left;">
covid
</td>
</tr>
<tr>
<td style="text-align:left;">
170,754
</td>
<td style="text-align:left;">
1,159,220
</td>
<td style="text-align:left;">
549,829
</td>
<td style="text-align:left;">
4,082,791
</td>
</tr>
<tr>
<td style="text-align:left;">
trump
</td>
<td style="text-align:left;">
china
</td>
<td style="text-align:left;">
covid
</td>
<td style="text-align:left;">
coronavirus
</td>
</tr>
<tr>
<td style="text-align:left;">
161,747
</td>
<td style="text-align:left;">
859,735
</td>
<td style="text-align:left;">
444,710
</td>
<td style="text-align:left;">
3,620,825
</td>
</tr>
<tr>
<td style="text-align:left;">
mippcivzla
</td>
<td style="text-align:left;">
madrid
</td>
<td style="text-align:left;">
china
</td>
<td style="text-align:left;">
covidãƒ¼19
</td>
</tr>
<tr>
<td style="text-align:left;">
123,362
</td>
<td style="text-align:left;">
428,891
</td>
<td style="text-align:left;">
443,306
</td>
<td style="text-align:left;">
133,301
</td>
</tr>
</tbody>
</table>

Data Collection Process Inconsistencies
---------------------------------------

Only tweets in English were collected from 22 January to 31 January
2020, after this time the algorithm collected tweets in all languages.
There are also some known gaps of data shown below:

<table class="table table" style="margin-left: auto; margin-right: auto; font-size: 12px; margin-left: auto; margin-right: auto;">
<caption style="font-size: initial !important;">
Known gaps
</caption>
<thead>
<tr>
<th style="text-align:left;font-weight: bold;">
Date
</th>
<th style="text-align:left;font-weight: bold;">
Time
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
2020-08-06
</td>
<td style="text-align:left;">
07:00 UTC
</td>
</tr>
<tr>
<td style="text-align:left;">
2020-08-08
</td>
<td style="text-align:left;">
07:00 UTC
</td>
</tr>
<tr>
<td style="text-align:left;">
2020-08-09
</td>
<td style="text-align:left;">
07:00 UTC
</td>
</tr>
<tr>
<td style="text-align:left;">
2020-08-14
</td>
<td style="text-align:left;">
07:00 UTC
</td>
</tr>
</tbody>
</table>

Hydrating Tweets
================

Using our TWARC Notebook
------------------------

The notebook
[Automatically\_Hydrate\_TweetsIDs\_COVID190\_v2.ipynb](https://github.com/lopezbec/COVID19_Tweets_Dataset/blob/master/Automatically_Hydrate_TweetsIDs_COVID19_v2.ipynb)
will allow you to automatically hydrate the tweets-ID from our
[COVID19\_Tweets\_dataset GitHub
repository](https://github.com/lopezbec/COVID19_Tweets_Dataset).

You can run this notebook directly on the cloud using Google Colab [(see
how to
tutorials)](https://colab.research.google.com/notebooks/welcome.ipynb#scrollTo=xitplqMNk_Hc)
and Google Drive.

In order to hydrate the tweet-IDs using
[TWARC](https://github.com/DocNow/twarc) you need to create a [Twitter
Developer Account](https://developer.twitter.com/en/apply-for-access).

The Twitter API’s rate limits pose an issue to fetch data from
tweed-IDs. So, we recommended using Hydrator to convert the list of
tweed-IDs, into a CSV file containing all data and meta-data relating to
the tweets. Hydrator also manages Twitter API Rate Limits for you.

For those who prefer a command-line interface over a GUI, we recommend
using Twarc.

### Using Hydrator

Follow the instructions on the [Hydrator github
repository](https://github.com/DocNow/hydrator).

### Using Twarc

Follow the instructions on the [Twarc github
repository](https://github.com/DocNow/twarc).

Inquiries
=========

For questions about the dataset, please contact Dr. Christian Lopez at
**<a href="mailto:lopezbec@lafayette.edu" class="email">lopezbec@lafayette.edu</a>**

Licensing
=========

This dataset is licensed under the Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International Public License
([CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)).
By using this dataset, you agree to abide by the stipulations in the
license, remain in compliance with Twitter’s [Terms of
Service](https://developer.twitter.com/en/developer-terms/agreement-and-policy),
and cite the following manuscript:

References
==========

<a name="chen"></a> Emily Chen, Kristina Lerman, and Emilio Ferrara.
2020. \#COVID-19: The First Public Coronavirus Twitter Dataset.
arXiv:cs.SI/2003.07372, 2020

<a href="https://github.com/echen102/COVID-19-TweetIDs" class="uri">https://github.com/echen102/COVID-19-TweetIDs</a>
