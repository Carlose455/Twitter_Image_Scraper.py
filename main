import tweepy #https://github.com/tweepy/tweepy
import requests 
import os
import shutil

consumer_key = "CJlZjc6NFWvFPKVgns7sf8DFI"
consumer_secret = "VKVwZxskVWolRMrZa1ulYRFJAz3moLIDwHj0wWzTsEJETwdc7L"
access_key = "1439595757414363142-I4dnAOpSL1nZ0Xg1NDeil6CzBTHb5A"
access_secret = "YfkcE5oJVuj3GjAX16KxSI5YlDGBhfc3H0REcXTjWQqBq"

screen_name = 'Twitter'

path = 'C:\\Users\\User\\OneDrive\\Desktop\\Twitter_scraped'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_key, access_secret)
api = tweepy.API(auth, wait_on_rate_limit=True)

image_links = []

for tweet in tweepy.Cursor(api.user_timeline, screen_name=screen_name, tweet_mode="extended", include_rts=False).items():
    if 'media' in tweet.entities:
        try:
            for image in tweet.extended_entities['media']:
                print(tweet.created_at)
                print(image['media_url'])
                image_links.append(image['media_url'])
        except:
            continue

folder_name = '%s_tweets' % screen_name

newpath = path + '\\' + str(folder_name)

if not os.path.exists(newpath):
    os.makedirs(newpath)
else:
    shutil.rmtree(newpath)        
    os.makedirs(newpath)

for index, link in enumerate(image_links):
    try:
        res = requests.get(link)
        name = link.split('/')[-1]
        with open(newpath + '/' + str([index+1]) + str(name), 'wb') as f:
            f.write(res.content) 
    except Exception as error:
        print(error)
        continue

