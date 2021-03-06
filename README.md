```
                                       _              _ _    _ _   
 ___ _ __ ___   __ _ _ __  _ __       | |_ ___   ___ | | | _(_) |_ 
/ __| '_ ` _ \ / _` | '_ \| '_ \ _____| __/ _ \ / _ \| | |/ / | __|
\__ \ | | | | | (_| | |_) | |_) |_____| || (_) | (_) | |   <| | |_ 
|___/_| |_| |_|\__,_| .__/| .__/       \__\___/ \___/|_|_|\_\_|\__|
                    |_|   |_|                                      
```

This is an user-friendly python package for interfacing with large collections of tweets. Developped at the SMaPP lab at New York University.


- [MongoTweetCollection](https://github.com/SMAPPNYU/smapp-toolkit#mongotweetcollection)
- [BSONTweetCollection](https://github.com/SMAPPNYU/smapp-toolkit#bsontweetcollection)
- [Shared Collection Functions](https://github.com/SMAPPNYU/smapp-toolkit#shared-collection-functions)
  - [containing](https://github.com/SMAPPNYU/smapp-toolkit#containing)
  - [count](https://github.com/SMAPPNYU/smapp-toolkit#count)
  - [texts](https://github.com/SMAPPNYU/smapp-toolkit#texts)
  - [term_counts](https://github.com/SMAPPNYU/smapp-toolkit#term_counts)
  - [sample](https://github.com/SMAPPNYU/smapp-toolkit#sample)
  - [apply_labels](https://github.com/SMAPPNYU/smapp-toolkit#apply_labels)
  - [since](https://github.com/SMAPPNYU/smapp-toolkit#since)
  - [until](https://github.com/SMAPPNYU/smapp-toolkit#until)
  - [language](https://github.com/SMAPPNYU/smapp-toolkit#language)
  - [user_lang_contains](https://github.com/SMAPPNYU/smapp-toolkit#user_lang_contains)
  - [excluding_retweets](https://github.com/SMAPPNYU/smapp-toolkit#excluding_retweets)
  - [user_location_containing](https://github.com/SMAPPNYU/smapp-toolkit#user_location_containing)
  - [field_containing](https://github.com/SMAPPNYU/smapp-toolkit#field_containing)
  - [geo_enabled](https://github.com/SMAPPNYU/smapp-toolkit#geo_enabled)
  - [non_geo_enabled](https://github.com/SMAPPNYU/smapp-toolkit#non_geo_enabled)
  - [limit](https://github.com/SMAPPNYU/smapp-toolkit#limit)
  - [top_hashtags](https://github.com/SMAPPNYU/smapp-toolkit#top_hashtags)
  - [top_unigrams top_bigrams top_trigrams](https://github.com/SMAPPNYU/smapp-toolkit#top_unigrams-top_bigrams-top_trigrams)
  - [top_urls](https://github.com/SMAPPNYU/smapp-toolkit#top_urls)
  - [top_images](https://github.com/SMAPPNYU/smapp-toolkit#top_images)
  - [top_mentions](https://github.com/SMAPPNYU/smapp-toolkit#top_mentions)
  - [top_links](https://github.com/SMAPPNYU/smapp-toolkit#top_links)
  - [top_user_locations](https://github.com/SMAPPNYU/smapp-toolkit#top_user_locations)
  - [top_geolocation_names](https://github.com/SMAPPNYU/smapp-toolkit#top_geolocation_names)
  - [top_entities](https://github.com/SMAPPNYU/smapp-toolkit#top_entities)
  - [top_X to_csv](https://github.com/SMAPPNYU/smapp-toolkit#top_x-to_csv)
  - [group_by](https://github.com/SMAPPNYU/smapp-toolkit#group_by)
  - [dump_csv](https://github.com/SMAPPNYU/smapp-toolkit#dump_csv)
  - [dump_bson_topath](https://github.com/SMAPPNYU/smapp-toolkit#dump_bson_topath)
  - [dump_bson](https://github.com/SMAPPNYU/smapp-toolkit#dump_bson)
  - [dump_json](https://github.com/SMAPPNYU/smapp-toolkit#dump_json)
- [MongoTweetCollection Only Functions](https://github.com/SMAPPNYU/smapp-toolkit#mongotweetcollection-only-functions)
  - [sort](https://github.com/SMAPPNYU/smapp-toolkit#sort)
- [BSONTweetCollection Only Functions](https://github.com/SMAPPNYU/smapp-toolkit#bsontweetcollection-only-functions)

**Supports Python 2.7**

## Installation
Simplest: using `pip`:
```bash
pip install smapp-toolkit
```

To update to the latest version, if you have an older one installed:
```bash
pip install -U smapp-toolkit
```

Or download the source code using git
```bash
git clone https://github.com/SMAPPNYU/smapp-toolkit
cd smapp-toolkit
python setup.py install
```

or download [the tarball](https://github.com/SMAPPNYU/smapp-toolkit/tarball/master) and install.

#### Dependencies
The `smapp-toolkit` depends on the following packages, which will be automatically installed when installing `smapp-toolkit`:
* [pymongo](http://api.mongodb.org/python/current/), the Python MongoDB driver
* [smappPy](https://github.com/SMAPPNYU/smappPy), a utility library from SMaPP
* [networkx](https://github.com/networkx/networkx), a library for building and analyzing graphs
* [pandas](http://pandas.pydata.org/), a Python data analysis library
* [simplejson](https://simplejson.readthedocs.org/en/latest/)

##Pushing to [PyPi](https://pypi.python.org/pypi)

To bump the version and push to github run, `bash yvanbump.sh`.

To bump the version, push to github, and upload to pypi run `bash upload+to_pypi.sh`.

To upload to pypi you need:

 - to be added with the right permissions to pypi
 - a .pypirc file in your ~ directory
 - to follow this [guide](http://peterdowns.com/posts/first-time-with-pypi.html). 

## Setup Collection Object

## MongoTweetCollection 

This allows you to plug into a running live mongodb database and run toolkit methods on the resulting collection object.
Abstract:
```python
from smapp_toolkit.twitter import MongoTweetCollection

collection = MongoTweetCollection(address='MONGODB-HOSTNAME',
                                  port='MONGODB-PORT',
                                  username='MONGO-DATABASE-USER',
                                  password='MONGO-DATABASE-PASSWORD',
                                  dbname='MONGO-DATABASE')
```

Practical:
```python
from smapp_toolkit.twitter import MongoTweetCollection

collection = MongoTweetCollection(address='superhost.bio.nyu.edu',
                                  port='27017',
                                  username='readWriteUser',
                                  password='readwritePassword',
                                  dbname='GermanyElectionDatabase')
```

`MONGODB-HOSTNAME` is the domain name or ip address of the server that is hosting the database.

`MONGODB-PORT` is the port on which the running monogodb instance is accessible on the server.

`MONGO-DATABASE-USER` is the user on the database that can at least read the database.

`MONGO-DATABASE-PASSWORD`the password on that particular database for that user.

`MONGO-DATABASE` the name of the database running on the mongo instance.

*Returns* an iterable collection object that can be used like so:

for tweet in MongoTweetCollection:
  print tweet

## BSONTweetCollection

This allows you to plug in a bson file and run toolkit methods on the resulting collection object.

Abstract:
```python
from smapp_toolkit.twitter import BSONTweetCollection

collection = BSONTweetCollection('/PATH/TO/FILE.bson')
```

Practical:
```python
from smapp_toolkit.twitter import BSONTweetCollection

collection = BSONTweetCollection('/home/toolkituser/datafolder/file.bson')
```

`/PATH/TO/FILE.bson` the path on your computers filesystem / disk to the bson file.

*Returns* an iterable collection object that can be used like so:

for tweet in MongoTweetCollection:
  print tweet

## Shared Collection Functions

## containing

Gets the tweets that contain one or more terms.

Abstract:
```python
collection.containing('TERM-ONE', 'TERM-TWO', 'ETC')
```

Practical:
```python
collection.containing('#bieber', '#sexy')
```

*Returns* a collection object with a filter applied to it to only return tweet objects where the tweet text contains those terms.

## count

Counts the number of occurrences of a given word. Can be called on a collection object with a chained method.

Abstract:
```python
collection.containing('TERM')
```

Practical:
```python
collection.containing('#bieber')
```

Chained:
```python
collection.containing('#bieber').count()
```

*Returns* the number of tweets in a collection object.

## texts

Gets the texts from a collection object or a collection object with a chained method applied.

Abstract:
```python
texts = collection.texts()
```

Chained:
```python
texts = collection.containing('#bieber').texts()
```

## term_counts

Allows you to count particular terms and split up the counts by a particular time period.

Abstract:
```python
collection.term_counts(['TERM-TWO', 'TERM-ONE'], count_by='TIME-DELIMITER', plot=BOOLEAN)
```

Practical:
```python
collection.term_counts(['justin', 'miley'], count_by='days', plot=False)
```

`count_by` can be in days, hours, or minutes.
`plot` is a True or False variable.

*Returns* a dictionary where each key is the date and each value is another dictionary.
In the sub dictionary the keys are the terms you chose and potentially a `_total` field which to be honest I'm not really sure what the _total field does. I know it isn't the total number of tweets. Dictionary looks like so:

```
{
 '2015-04-01': {'justin': 1312, 'miley': 837},
 '2015-04-02': {'justin': 3287, 'miley': 932}
}
```

# sample 

*WARNING DOES NOT WORK*

Gets a random sample of tweets.
 
Abstract:
```python
collection.sample(FRACTION-OF-1-TO-SAMPLE)
```

Practical:
```python
collection.sample(0.33)
```

Chained:
```python
collection.containing('#bieber').sample(0.33).texts()
```

*Returns* a collection object that will now have a filter to only return then number of tweets as deteremined by the sample randomly.

## apply_labels

 Applies a set of named labels and attaches them to objects from a collection if the certain fields in the collection meet certain criteria. It then outputs a bson file where tweets that matched teh filter have an extra labels field in them with the appropriate labels.

Abstract:

```python
collection.apply_labels(
  list_of_labels
  ,list_of_fields
  ,list_for_values
  ,bsonoutputpath
)
```

Practical:

```python
collection.apply_labels(
  [['religious_rank', 'religious_rank', 'political_rank'], ['imam', 'cleric', 'politician']]
  ,['user.screen_name', 'user.id']
  ,[['Obama', 'Hillary'], ['1234567', '7654321']]
  ,'outputfolder/bsonoutput.bson'
)
```
NOTE: ['1234567', '7654321'] are not the actual ids of any twitter users they are just dummy numbers.

`list_of_labels` is a list with two lists inside it where the first list contains names for labels and the second list
contains the labels themselves. For example: `religious_rank` and `imam` would be a label called religious_rank for the label value imam.

Each field in the `list_of_fields` array is a string that takes dot notation. user.screen_name would be the screen_name 
entry in the user entry in the collection object. You can nest these for as many levels as you have in the collection
object. 

`list_for_values` is a list that contains as many lists as there are fields to match. Each of these lists (inside list_for_
values) is a list of the values you would like that field to match. So if you want the user.screen_name to match 'obama' 
'hillary' or 'lessig' then you would use:

```python
list_of_fields = ['user.screen_name']
list_for_values = [['obama', 'hillary', 'lessig']]
```
as inputs.

`bsonoutputpath` is the path realtive to where you run the script that will be the output file with the new labels.

After you run this method each tweet object in your output BSON will now have a field called 'labels' like so:
```
{
.
.
.
'labels' : {
  '1': {name: “religious_rank”, type: “cleric”},
  '2': {name: ”religious_rank”, type: ”imam'},
  '3': {name: “eye_color”, type :”brown'}
}
.
.
.
}
```

## since

Abstract:
```python
collection.since(DATETIME)
```

Practical:
```python
collection.since(datetime(2014,1,30))
```

Chained:
```python
from datetime import datetime
collection.since(datetime(2014,1,30)).count()
collection.since(datetime(2014,2,16)).until(datetime(2014,2,19)).containing('obama').texts()
```

*Returns* a collection object with the added filter that it will only return objects after a certain date.

Check out a reference on [datetime here](https://pymotw.com/2/datetime/).

## until

Abstract:
```python
collection.until(DATETIME)
```

Practical:
```python
collection.until(datetime(2014,1,30))
```

Chained:
```python
from datetime import datetime
collection.until(datetime(2014,1,30)).count()
collection.since(datetime(2014,2,16)).until(datetime(2014,2,19)).containing('obama').texts()
```

Note: that both 'since(...)' and 'until(...)' are exclusive (ie, they are GT/> and LT/<, respectively, not GTE/>= or LTE/<=) This means that since(datetime(2014, 12, 24)) will return tweets after EXACTLY 12/24/2014 00:00:00 (M/D/Y H:M:S). Datetimes may be specified to the second: datetime(2014, 12, 24, 6, 30, 25) is 6:30 and 25 seconds AM Universal Timezone. If time (hours, minutes, etc) is not specified, time defaults 00:00:00.

## language

Gets all tweets tagged by twitter (and not the user themselves) with a certain language. Get's all tweets twitter thinks are in language X (french, english, etc) and returns a new collection object with those tweets.

Abstract:
```python
collection.language(LANGUAGE-CODE)
```

Practical:
```python
collection.language('en')
```

Chained:
```python
collection.language('en').texts()
collection.language('ru', 'uk') //get tweets in russian or ukranian
```

Returns a collection with an added filter such that all the tweets returned from the collection will be tweets tagged with that language code.

`LANGUAGE-CODE` You can check out the various language codes on [twitter's API page here](https://dev.twitter.com/rest/reference/get/help/languages).

## user_lang_contains

This gets all tweets tagged where the user has marked their own language preference. So It would look for all users who marked language X (french, english, etc) as their language on their user profile and then get tweets that are fro those users that are present in the collection object.

Abstract:
```python
collection.user_lang_contains('LANGUAGE-CODE', 'LANGUAGE-CODE')
```

Practical:
```python
collection.user_lang_contains('de')
collection.user_lang_contains('de', 'fr')
```

Chained:
```python
collection.user_lang_contains('de', 'fr').texts()
collection.user_lang_contains('de', 'fr') //get tweets in German or French
```

*Returns* a collection with an added filter such that all the tweets returned from the collection will be tweets tagged with that language code.

## excluding_retweets
Abstract:
```python
collection.excluding_retweets()
```

Chained:
```python
collection.excluding_retweets().count()
```

*Returns* a collection object filtered to exclude retweets.

## user_location_containing

This gets tweets where the user locations contains certain location names.

Abstract:
```python
collection.user_location_containing('PLACE-NAME', 'PLACE-WORD')
```

Practical:
```python
collection.user_location_containing('new york', 'nyc')
```

Chained:
```python
collection.user_location_containing('new york', 'nyc').texts()
```

*Returns* a collection object filtered to only include tweets where the user's location field matches or contains

## field_containing

This method can be used to query a particular field on a tweet object by using dot notation to dig into each sub object or field.

Abstract:
```python
collection.field_containing('user.description', 'TERM', 'TERM', 'TERM')
```

Practical:
```python
collection.field_containing('user.description', 'kittens', 'imgur', 'internet')
```

Chained:
```python
collection.field_containing('user.description', 'kittens', 'imgur', 'internet').texts()
```

You can see the fields and [tweet structure here](https://dev.twitter.com/overview/api/tweets).

## geo_enabled

Adds a filter to a collection object that only returns geo tweets.

Abstract:
```python
collection.geo_enabled()
```

Chained:
```python
collection.collection.geo_enabled().texts()
```

*Returns* a collection object that only contains tweets that have geo location enabled.

## non_geo_enabled

Abstract:
```python
collection.non_geo_enabled()
```

Chained:
```python
collection.collection.non_geo_enabled().texts()
```

*Returns* a collection object that only contains tweets that do not have geo location enabled.

## limit

Abstract:
```python
collection.limit(NUMBER-TO-LIMIT)
```

Practical:
```python
collection.limit(10)
```

Chained:
```python
collection.sort('timestamp',-1).limit(10).texts()
```

*Returns* a collection object that only contains the number of tweets specified by the limit. This is not a random sample. It should just get the first 10 tweets returned.

```python
collection.sort('timestamp',-1).limit(10).texts()
```

## top_hashtags

Gets the top hashtags

Abstract:
```python
counts = collection.top_hashtags(n=NUMBEROFHASHTAGS)
```

Practical:
```python
counts = collection.top_hashtags(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_hashtags(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top hashtags

## top_unigrams, top_bigrams, top_trigrams

Abstract:
```python
counts = collection.top_unigrams(n=NUMBER-UNIGRAMS)
# or
counts = collection.top_bigrams(n=NUMBER-BIGRAMS)
# or
counts = collection.top_trigrams(n=NUMBER-TRIGRAMS)
```

Practical:
```python
counts = collection.top_unigrams(n=5)
# or
counts = collection.top_bigrams(n=5)
# or
counts = collection.top_trigrams(n=5)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_unigrams(n=5)
# or
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_bigrams(n=5)
# or
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_trigrams(n=5)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top unigrams, bigrams, or trigrams.

## top_urls

Gets the urls from the entities field of a tweet object. The difference between this and top_links is that top links gets both urls and media references.

```python
counts = collection.top_urls(n=NUMBERURLS)
```

Practical:
```python
counts = collection.top_urls(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_urls(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top urls.

## top_images

```python
counts = collection.top_images(n=NUMBERIMAGES)
```

Practical:
```python
counts = collection.top_images(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_images(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top images.

## top_mentions

Gets the top twitter mentions, other twitter screen names marked with @ symbols in front of them. So it gets the X many most mentioned people in a collection.

```python
counts = collection.top_mentions(n=NUMBERMENTIONS)
```

Practical:
```python
counts = collection.top_mentions(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_mentions(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top mentions.

## top_retweets

Gets the top retweets tweet objects from a certain collection.

Abstract:
```python
top_retweets = collection.top_retweets(n=NUMBER-TOP-RETWEETS, rt_columns=['FIELD-ONE', 'FIELD-TWO', 'ETC'])
# or 
top_retweets = collection.top_retweets(n=NUMBER-TOP-RETWEETS)
```

Practical:
```python
top_retweets = collection.top_retweets(n=10, rt_columns=['user.screen_name', 'user.location', 'created_at', 'text'])
# or 
top_retweets = collection.top_retweets(n=10)
```

Chained:
```
top_retweets = collection.since(datetime.utcnow()-timedelta(hours=1)).top_retweets(n=10, rt_columns=['user.screen_name', 'user.location', 'created_at', 'text'])
```

Output:
```python
id            count
123456789     350
123456444     330
987654321     305
987654329     266
987654323     244
554286237     236
554286238     236
231379283     226
874827344     185
482387489     185
```

`rt_columns` is a python list where each element of the list is a field on a tweet object or a nested/compound field on the tweet object. Specify which columns / fields (of the original tweet) to include in the result, by passing thr `rt_columns` argument. The default columns included are `['user.screen_name', 'created_at', 'text']` if no `rt_columns` argument is passed to the function.

*Returns* a [pandas data frame](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) which is like a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) except that it is not one dimensional. The data frame has the columns `id` and `count` and any extra columns you sepcified in your `rt_columns` input parameter if there is one.

## top_links

Gets the urls and media references from the entities field of a tweet object. The difference between this and top_urls is that top urls gets only urls.

```python
counts = collection.top_links(n=NUMBERLINKS)
```

Practical:
```python
counts = collection.top_links(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_links(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top links.

## top_user_locations

Gets the top locations methioned in the user's location field in the [user object](https://dev.twitter.com/overview/api/users) inside each [tweet object](https://dev.twitter.com/overview/api/tweets).

```python
counts = collection.top_user_locations(n=NUMBERLOCATIONS)
```

Practical:
```python
counts = collection.top_user_locations(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_user_locations(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top user locations.

## top_geolocation_names

If the place field exists inside a [tweet object](https://dev.twitter.com/overview/api/tweets) object. Then this will return the top X places on geolocated tweets.

```python
counts = collection.top_geolocation_names(n=NUMBERLOCATIONS)
```

Practical:
```python
counts = collection.top_geolocation_names(n=10)
```

Chained:
```python
counts = collection.since(datetime(2015,1,1)).until(datetime(2015,1,2)).top_geolocation_names(n=10)
```

*Returns* a [pandas data series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) that contains the top geolocation names.

## top_entities

Top entities lets you do multiple top_x methods in one go and have then all be returned in one data structure.

Abstract:
```python
top_entities_returned = collection.top_entities(n=NUMBERENTITIES, urls=TRUE/FALSE, images=TRUE/FALSE, hts=TRUE/FALSE, mentions=TRUE/FALSE, geolocation_names=TRUE/FALSE, user_locations=TRUE/FALSE, ngrams=(1,2), ngram_stopwords=[], ngram_hashtags=TRUE/FALSE, ngram_mentions=TRUE/FALSE, ngram_rts=TRUE/FALSE, ngram_mts=TRUE/FALSE, ngram_https=TRUE/FALSE)
```

Practical 1:
```python
# get the top unigrams, bigrams, and tri grams and return in a dict()
top_entities_returned = collection.top_entities(ngrams=(1,2,3))
```

Output:
```
print top_entities_returned['2-grams']
فيديو قوات          350
الطوارى السعودية    330
قوات الطوارى        305
#السعودية #saudi    266
#ksa #السعودية      244
قوات الطوارئ        236
الطوارئ السعودية    236
#saudi #الرياض      226
يقبضون على          185
السعودية يقبضون     185
dtype: int64
```

Practical 2:
```python
# get the top 5 hashtags and return in a dict()
top_entities_returned = collection.top_entities(n=2, hts=True)
```

Output:
```
print top_entities_returned['hts']
#obamaisoursavior #oregonmilitia
```

*Returns* a python dictionary object with [pandas.Series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) objects for each top entity list in the dictionary.

## top_X to_csv 

for exporting top_X methods:

  - [top_hashtags](https://github.com/SMAPPNYU/smapp-toolkit#top_hashtags)
  - [top_unigrams top_bigrams top_trigrams](https://github.com/SMAPPNYU/smapp-toolkit#top_unigrams-top_bigrams-top_trigrams)
  - [top_urls](https://github.com/SMAPPNYU/smapp-toolkit#top_urls)
  - [top_images](https://github.com/SMAPPNYU/smapp-toolkit#top_images)
  - [top_mentions](https://github.com/SMAPPNYU/smapp-toolkit#top_mentions)
  - [top_links](https://github.com/SMAPPNYU/smapp-toolkit#top_links)
  - [top_user_locations](https://github.com/SMAPPNYU/smapp-toolkit#top_user_locations)
  - [top_geolocation_names](https://github.com/SMAPPNYU/smapp-toolkit#top_geolocation_names)

  and each sub dictionary in:

  - [top_entities](https://github.com/SMAPPNYU/smapp-toolkit#top_entities)

All `top_x()` methods return [pandas.Series](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html) objects. The only one that doesn't is `top_retweets` which returns a matrix/[pandas data frame](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) (for some reason?). These are subclasses of [pandas.DataFrame](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) which can be exported to csv like so:


Abstract:
```python
hashtags = collection.top_hashtags(n=NUMBER-HASHTAGS)
hashtags.to_csv('/path/to/my/output.csv', encoding='utf8')
```

Practical:
```python
hashtags = collection.top_hashtags(n=5)
hashtags.to_csv('~/hashtags-output.csv', encoding='utf8')
```

## group_by

Use the `group_by` method to group tweets by time slices. Supported time slices are `days`, `hours`, `minutes`, and `seconds`. 

Abstract:
```python
collection.group_by('TIME-UNIT')
```

Practical:
```python
# counting by time slice
for time, tweets in collection.group_by('hours'):
    print('{time}: {count}'.format(time=time, count=len(list(tweets))))
```
which outputs:
```python
2015-01-12 17:00:00: 13275
2015-01-12 18:00:00: 23590
```

Chaining 1: (not sure if this works, *MAY NOT WORK*)
```python
#counting by time slice
print collection.since(datetime(2015,6,18,12)).until(datetime(2015,6,18,15)).group_by('hours').count()
```
which outputs:
```python
2015-06-18 12:00:00  164181
2015-06-18 13:00:00  167129
2015-06-18 14:00:00  165057
```

Chaining 2: (not sure if this works, *MAY NOT WORK*)
```python
# countng user locations by time slice
print collection.since(datetime(2015,6,1)).group_by('days').top_user_locations(n=5)
```
which outputs:
```python
  #            London  London, UK  Manchester  Scotland  UK
  # 2015-06-1       4           2           1         1   2
  # 2015-06-2      11           4           9         3   3
  # 2015-06-3      14           1           5       NaN   4
  # 2015-06-4      17           1           5         1   6
  # 2015-06-5      10           3           3         3   3
```

Chaining 3: (not sure if this works, *MAY NOT WORK*)
```python
print collection.group_by('hours').entities_counts()
```
which outputs:
```python
                     _total   url  image  mention  hashtag  geo_enabled  retweet
2015-01-12 17:00:00   13275   881   1428     6612     2001        10628       15 
2015-01-12 18:00:00   23590  1668   2509    12091     3575        19019       36
```

Chaining 4: (not sure if this works, *MAY NOT WORK*)
```python
# counting tweet languages over time slice
print collection.since(datetime.utcnow()-timedelta(minutes=10)).until(datetime.utcnow()).group_by('minutes').language_counts(langs=['en', 'es', 'other'])   
```
which outputs:
```python
                       en   es  other
2015-06-18 21:23:00   821   75    113
2015-06-18 21:24:00  2312  228    339
2015-06-18 21:25:00  2378  196    339
2015-06-18 21:26:00  2352  233    295
2015-06-18 21:27:00  2297  239    344
2015-06-18 21:28:00  1776  173    247
2015-06-18 21:29:00  1825  162    269
2015-06-18 21:30:00  2317  237    326
2015-06-18 21:31:00  2305  233    342
2015-06-18 21:32:00  2337  235    308
2015-06-18 21:33:00  1508  136    228
```

Chaining 5: (not sure if this works, *MAY NOT WORK*)
```python
# counting number of unique users per time slice
unique_users = collection.group_by('minutes').unique_users()
tweets = collection.group_by('minutes').count()
unique_users['total tweets'] = tweets['count']
unique_users
```
which outputs:
```python
                     unique_users  total tweets
2015-04-16 17:01:00           377           432
2015-04-16 17:02:00           432           582
2015-04-16 17:03:00           442           610
2015-04-16 17:04:00           393           531
2015-04-16 17:05:00           504           756
2015-04-16 17:06:00           264           365
```

Note: there is no/minimal chaining on this method. Doing so can create bugs or crashes or worse. This is because the function doesn't return a data type but returns a [generator](https://wiki.python.org/moin/Generators).

*Returns* a [generator](https://wiki.python.org/moin/Generators) that can be iterated through in a for loop. The generator is split into two parts, a time stamp and a list of tweets. So if you decide to group a collection with tweets spanning an entire day by hours this generator loop should fire 24 times (24 hrs in a day), produce 24 time stamps, and produce 24 lists of tweets. Each list of tweets contains tweets from the time slice of 1 hour you asked for. The same logic from above applies to any time slice.

## dump_csv

Takes a collection and dumps its contents to a csv.

Abstract:
```python
collection.dump_csv('/path/to/output.csv')
```

Practical:
```python
collection.dump_csv('~/my_tweets.csv')
# or 
# the desired columns may be specified in the `columns=` named argument.
collection.dump_csv('my_tweets.csv', columns=['id_str', 'user.screen_name', 'user.location', 'user.description', 'text'])
#or 
#If the filename specified ends with `.gz`, the output file will be gzipped.
collection.dump_csv('my_tweets.csv.gz')
```

*Returns* a csv file that will write to disk. Default columns in this csv should be  ['id_str', 'user.screen_name', 'timestamp', 'text']

## dump_bson_topath

This will dump whole tweets in MongoDB's BSON format into a specified file. Note that BSON is a 'binary' format (it will look a little funny if opened in a text editor). This is the native format for MongoDB's mongodump program. The file is NOT line-separated.

Abstract:
```python
collection.dump_bson_topath('/path/to/output.bson')
```

Practical:
```python
collection.dump_bson_topath('~/output.bson')
```
This will dump a bson file of tweets. Once you have this bson you can convert it to JSON formatted bson (a file with a json object on each line) with the bsondump tool (if you have it) like so:

 ```sh
 bsondump output.bson > output.json
 ```

*Returns* a bson file. This is a binary file and is not human readable.w

## dump_bson

Dumps a json formatted BSON. This is not a binary file. It is a list of json objects stored line by line. (At least I'm pretty sure.) This is why we have `dump_bson` and `dump_bson_topath` because the dump_bson method (this method) was not dumping actual binary bson files.

Abstract:
```python
collection.dump_bson('/path/to/output.bson')
```

Practical:
```python
collection.dump_bson('~/output.bson')
# or
# to append BSON tweets to the given filename (if file already has tweets)
collection.dump_bson('~/output.bson', append=True)
```

*Returns* a file that is written to disk that has a json object on each line. This is human readable.

## dump_json 

*MAY NOT WORK*

This will dump whole tweets in JSON format into a specified file, one tweet per line.

Abstract:
```python
collection.dump_json('/path/to/output.json')
```

Practical:
```python
collection.dump_json('~/output.json')
# or 
# to append tweets in the collection to an existing file
collection.dump_json('~/output.json', append=True)
# to write JSON into pretty, line-broken and properly indented format (takes more space)
collection.dump_json('~/output.json', pretty=True)
collection.dump_json('~/output.json', pretty=True, append=True)
```

*Returns* a file with a json object on each line that is written to disk. It is human readable.

## MongoTweetCollection Only Functions 

## sort

Sorts tweets inside a collection by a particular field.

Abstract:
```python
collection.sort('FIELD', ORDER)
```

Practical:
```python
collection.sort('timestamp',-1)
collection.sort('timestamp', 1)
```

Chained:
```python
collection.sort('timestamp',-1).limit(10).texts()
```

*Returns* a collection where the tweets are sorted by the given field.

You can check out the `ORDER` [here](http://api.mongodb.org/python/current/api/pymongo/collection.html).  

-1 means sort in DESCENDING order.
 1 means sort in ASCENDING order.

## BSONTweetCollection Only Functions

##----- none for now in BSONTweetCollection Only Functions -----


### Visualizations
The `smapp_toolkit.plotting` module has functions that can make canned visualizations of the data generated by the functions above.
For more examples, see the [examples](https://github.com/SMAPPNYU/smapp-toolkit/tree/master/examples) folder.

#### Tweets volume with vertical annotation lines
See examples in the [gallery](http://philosoraptor.bio.nyu.edu:82/figure-gallery/#annotated-tweets-oer-time-unit).

#### Stacked bar plots

##### Plotting the proportion of retweets:
```python
from smapp_toolkit.plotting import stacked_bar_plot
data = col.since(datetime(2015,6,18,12)).until(datetime(2015,6,18,12,10)).group_by('minutes').entities_counts()
data['original tweet'] = data['_total'] - data['retweet']

plt.figure(figsize=(10,10))
stacked_bar_plot(data, ['retweet', 'original tweet'], x_tick_date_format='%H:%M', colors=['salmon', 'lightgrey'])
plt.title('Retweet proportion', fontsize=24)
plt.tight_layout()
```

##### Plotting top user locations:
```python
data = col.since(datetime(2015,6,18,12)).until(datetime(2015,6,18,12,10)).group_by('minutes').top_user_locations()

stacked_bar_plot(data, ['London', 'New York'], x_tick_date_format='%H:%M')
plt.title('Tweets from London and New York users', fontsize=18)
plt.tight_layout()
```

See more examples in the [gallery](http://philosoraptor.bio.nyu.edu:82/figure-gallery/#stacked-bar-plots).

### Other visualization functions
The following functions make plots by first getting data from collection and then making the plots. Their use is discouraged as getting the data can sometimes be slow. Always prefer to get the data and make plots separately, saving the data first.

#### Visualizing the volume of tweets
```python
bins, counts = collection.containing('#sexy').tweets_over_time_figure(
    start_time,
    step_size=timedelta(minutes=1),
    num_steps=60,
    show=False)
plt.title('Tweets containing '#sexy'')
plt.show()
```

#### Visualizing volume of selected terms over time
```python
collection.term_counts(['justin', 'miley'], count_by='days', plot=True, plot_total=True)
plt.show()
```

#### Visualize the retweet proportion over time
```python
collection.since(datetime(2015,6,1)).tweet_retweet_figure(group_by='days')
```
you may set `group_by=` to `days`, `hours`, `minutes`, or `seconds`.

#### Visualize proportion of geocoded tweets over time
```python
collection.since(datetime(2015,6,1)).geocoded_tweets_figure()
```

#### Visualize tweets with links, images, mentions
* `collection.tweets_with_urls_figure()`
* `collection.tweets_with_images_figure()`
* `collection.tweets_with_mentions_figure()`
* `collection.tweets_with_hashtags_figure()`


### Iterate over the full tweet objects
```python
for tweet in collection.containing('#nyc'):
    print(tweet['text'])
```
## Exporting
Here are functions for exporting data from collections to different formats.

##### tweet coordinates
For geolocated tweets, in order to get the geolocation out in the csv, add `coordinates.coordinates` to the columns list. This will put the coordinates in [GeoJSON](http://geojson.org/geojson-spec.html#positions) (long, lat) in the column.
*Alternatively*¸ add `coordinates.coordinates.0` and `coordinates.coordinates.1` to the columns list. This will add two columns with the longitude and latitude in them respectively.

### Exporting a retweet graph
The toolkit supports exporting a retweet graph using the `networkx` library. In the exported graph users are nodes, retweets are directed edges.

If the collection result includes non-retweets as well, users with no retweets
will also appear in the graph as isolated nodes. Only retweets are edges in the resulting graph.

Exporting a retweet graph is done as follows:
```python
import networkx as nx
digraph = collection.containing('#AnyoneButHillary').only_retweets().retweet_network()
nx.write_graphml(digraph, '/path/to/outputfile.graphml')
```

Nodes and edges have attributes attached to them, which are customizable using the `user_metadata` and `tweet_metadata` arguments.

* `user_metadata` is a list of fields from the User object that will be included as attributes of the nodes.
* `tweet_metadata` is a list of the fields from the Tweet object that will be included as attributes of the edges.

The defaults are
* `user_metadata=['id_str', 'screen_name', 'location', 'description']`
* `tweet_metadata=['id_str', 'retweeted_status.id_str', 'timestamp', 'text', 'lang']`

For large graphs where the structure is interesting but the tweet text itself is not, it is advisable to ommit most of the metadata. This will make the resulting file smaller, and is done as follows:
```python
import networkx as nx
digraph = collection.containing('#AnyoneButHillary').only_retweets().retweet_network(user_metadata=['screen_name'], tweet_metadata=[''])
nx.write_graphml(digraph, '/path/to/outputfile.graphml')
```

The `.graphml` file may then be opened in graph analysis/visualization programs such as [Gephi](http://gephi.github.io/) or [Pajek](http://vlado.fmf.uni-lj.si/pub/networks/pajek/).

The `networkx` library also provides algorithms for [vizualization](http://networkx.github.io/documentation/networkx-1.9.1/reference/drawing.html) and [analysis](http://networkx.github.io/documentation/networkx-1.9.1/reference/algorithms.html).

## Figures
Smapp-toolkit has some built-in plotting functionality. See the [example scripts](https://github.com/SMAPPNYU/smapp-toolkit/tree/master/examples), and check out the [gallery](http://philosoraptor.bio.nyu.edu:82/figure-gallery/)!

Currently implemented:
* barchart of tweets per time-unit (`tweets_over_time_figure(...)`)
* barchart by language by day (`languages_per_day_figure(...)`)
* line chart (tweets per day) with vertical event annotations (`tweets_per_day_with_annotations_figure(...)`)
* geolocation names by time (`geolocation_names_by_day_figure(...)`)
* user locations by time (`user_locations_by_day_figure(...)`)

In order to get these to work, some extra packages (not automatically installed) need to be installed:
* `matplotlib`
* `seaborn`

## The MongoDB Data Model
SMAPP stores tweets in MongoDB databases, and splits the tweets across multiple MongoDB collections, because this gives better performance than a single large MongoDB collection. The MongoDB Database needs to have a `smapp_metadata` collection with a single `smapp-tweet-collection-metadata` document in it, which specifies the names of the tweet collections.

The `smapp-tweet-collection-metadata` document has the following form:

```
{
  'document': 'smapp-tweet-collection-metadata',
  'tweet_collections': [
    'tweets_1',
    'tweets_2',
    'tweets_3',
  ]
}
```

### Customization
The `MongoTweetCollection` object may still be used if the metadata collection and document have different names:

```python
collection = MongoTweetCollection(..., metadata_collection='smapp_metadata', metadata_document='smapp-tweet-collection-metadata')
```

#### Already have tweets in your own mongo and want to use the smapp-toolkit?
All you need to do is insert the following collection and document into your MongoDB database:

(from the mongo shell)

```
db.smapp_metadata.save({
  'document': 'smapp-tweet-collection-metadata',
  'tweet_collections': [ 'tweets' ]
})
```

and the default behavior will work as advertised.

-----------
Code and documentation &copy; 2014 New York University. Released under [the GPLv2 license](LICENSE).
