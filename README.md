# WeRateDogs-Data
Udacity Nanodegree Project 2: Data Wrangling 

## Project Objective
The project was to wrangle the WeRateDogs Twitter data to provide appropriate analysis and insights

## Project Details
In the wrangle WeRateDogs Twitter data, we gather data from three sources: **twitter_archive-enhanced.csv, Image prediction.tsv and tweet-json.txt**. As part of the project, we are only interested in the original tweets and not the retweets. The twitter_archived-enhanced file has close to about 5000 tweets and likely to dump some entries as we clean the retweets. Additionally, only 8 quality issues and 2 tidiness issues are tackled under the this processes as tweets beyond August 1st, 2017 will not be included. Little insights are drawn from the data just to augment the wrangled activities.

## Gathering the data
There were three data source where data was to be gathered from – such as from the enhanced twitter archive file , the twitter(Tweepy) api, and the image predictions file.

**The twitter_archive_enhanced.csv** file is given to us through a download link on Udacity
The **image_predictions.tsv** file predicts which dog breed is which based on its tweet image. This was predicted using an algorithm through Udacity’s neural network and was downloaded programmatically retrieved using python’s Requests library: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv

The Tweet data containing the retweet and favorite count, was suppose to be queried from twitter’s api. However, due to API access restrictions, the tweet_json.txt was used.

All the data were converted to pandas dataframes for easy analysis using the pandas library.

## Accessing the data
There were two ways used to access the gathered data. These were visiual assessment and programatic assessment. Data was asssessed based on finding 8 quality issues and 2 tidiness issues. Although issues such as 'NaN' values, 'None' entries were visually accessible, issues of datatypes, data description, total null values, total columns and rows entries were best assessed programatically. So, methods such as: .head(), .sample(), .duplicated(), .info(),.isnull(), .value_counts() were applied on the datasets. After their application, the following issues were detected.

### Quality Issues
The timestamp and retweet_status_timestamp are in incorrect format and data type.They must be in a datetime format(the +000 in the date will be dropped)
There are 59 missing/null entries in the 'expanded_urls' column in the data 'data_twitter'.
Incorrect datatypes for columns 'tweet_id'
Some of the 'rating_denominator' and 'rating_numerator' columns have values which are out of range.
The name column has misssing value as 'None', 'an', 'a' and others which are not necessary for this analysis instead of real dog names.
The 'Source' column has HTML formated string.
The p1, p2, p3 columns are in uppercase
The columns retweet_status_id, retweeted_status_user_id, retweeted_status_timestamp necessary for this analysis.

### Other Issue:
The same dog could be recorded twice or more in cases of retweets and the same dog could be recorded twice or more in cases of reply.
### Tidiness Issues
The columns 'doggo', 'floofer', 'pupper', and puppo should be in one column 'dog stage'.
All the datasets should be combined into one datasets.
Cleaning the data
The detected issues were cleaned programatically.
Issues of incorrect date type was converted using the pandas Datetime method.
The tweet_id type was converted to string.
Columns which were not neccessary for the analysis were dropped.(i.e, We dropped the columns in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, and retweeted_status_timestamp)
The 59 missing entries were dropped from the expanded_urls column 5.The unmatched capitalized and lower cased names in the p1, p2, and p3 columns were all converted to lower case letter.
The HTML tags on the 'source' was converted to normal string format.
Error in dog names such as actually, an, a , the etc. were changed to 'None'
Hyperlinks on the text colunm was removed.
All the three dataset were combined(merged) for the analysis
The columns doggo, floofer, pupper, and puppo can be merged into one column called Dog_stage
Remove retweet and reply rows

## Storing the data
The final cleaned dataset was stored in a csv format named: twitter_archive_master.csv.
