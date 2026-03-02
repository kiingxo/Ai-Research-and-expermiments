# Social Media APIs for NLP Data Collection

## Twitter/X API

**Use Case**: Sentiment analysis, topic modeling, trend detection, conversational AI training

**Key Features**:
- Stream real-time tweets or search historical data
- Filter by hashtags, keywords, language, user
- Access tweet metadata (likes, retweets, replies)

**Getting Started**:
```python
import tweepy

# Authentication
client = tweepy.Client(bearer_token="YOUR_BEARER_TOKEN")

# Search recent tweets
query = "machine learning -is:retweet lang:en"
tweets = client.search_recent_tweets(query=query, max_results=100)

for tweet in tweets.data:
    print(tweet.text)
```

**Rate Limits**: Varies by API version (free tier: 300,000 tweets/month)
**Cost**: Free tier available, enterprise pricing for higher volume
**Documentation**: https://developer.twitter.com/en/docs

---

## Reddit API (PRAW)

**Use Case**: Conversational data, domain-specific discussions, question-answering datasets

**Key Features**:
- Access posts and comments from any subreddit
- Filter by score, date, sorting
- Get user comments across subreddits

**Getting Started**:
```python
import praw

reddit = praw.Reddit(
    client_id='YOUR_CLIENT_ID',
    client_secret='YOUR_SECRET',
    user_agent='your_agent'
)

# Get posts from a subreddit
subreddit = reddit.subreddit("MachineLearning")
for submission in subreddit.new(limit=100):
    print(f"Title: {submission.title}")
    print(f"Text: {submission.selftext}")
    print(f"Comments: {submission.num_comments}\n")
```

**Rate Limits**: ~60 requests/minute per IP
**Cost**: Free
**Documentation**: https://praw.readthedocs.io/

---

## YouTube API

**Use Case**: Transcripts from videos, comments analysis, subtitle datasets

**Key Features**:
- Search videos by keywords
- Get video metadata and statistics
- Fetch video transcripts (if available)
- Extract comments

**Getting Started**:
```python
from youtube_transcript_api import YouTubeTranscriptApi

# Get transcript from video
transcript = YouTubeTranscriptApi.get_transcript("dQw4w9WgXcQ")

# Combine transcript text
full_text = " ".join([item['text'] for item in transcript])
print(full_text)
```

**Rate Limits**: 10,000 quota units/day (free)
**Cost**: Free tier available
**Documentation**: https://developers.google.com/youtube/v3

---

## TikTok API

**Use Case**: Trending topics, short-form content analysis, hashtag trends

**Key Features**:
- Search videos by hashtag or keyword
- Get video metadata and statistics
- Access creator profiles

**Getting Started**:
```python
from TikTokApi import TikTokApi

api = TikTokApi()
videos = api.search_videos(keyword="AI", count=30)

for video in videos:
    print(f"Description: {video.desc}")
    print(f"Likes: {video.stats.diggCount}\n")
```

**Rate Limits**: Limited for free tier
**Cost**: Free tier available, enterprise options
**Documentation**: https://developers.tiktok.com/

---

## Hacker News API

**Use Case**: Tech discussions, problem-solving conversations, opinion mining

**Key Features**:
- No authentication required
- Free to use
- JSON-based interface

**Getting Started**:
```python
import requests

# Get top stories
response = requests.get('https://hacker-news.firebaseio.com/v0/topstories.json')
story_ids = response.json()[:30]

for story_id in story_ids:
    story = requests.get(f'https://hacker-news.firebaseio.com/v0/item/{story_id}.json').json()
    print(f"Title: {story['title']}")
    print(f"URL: {story.get('url', 'N/A')}\n")
```

**Rate Limits**: None (be respectful)
**Cost**: Free
**Documentation**: https://github.com/HackerNews/API

---

## Comparison Table

| API | Language | Real-time | Volume | Cost | Auth |
|-----|----------|-----------|--------|------|------|
| Twitter | English, multilingual | Yes | Very High | Free+ | Required |
| Reddit | English, multilingual | No | High | Free | Required |
| YouTube | Multilingual | No | High | Free quota | Required |
| TikTok | Multilingual | Limited | High | Free+ | Required |
| HN | English | No | Low-Med | Free | No |

---

## Best Practices

✅ **Do**:
- Check rate limits before bulk collection
- Respect API terms of service
- Cache data to avoid redundant calls
- Use pagination for large datasets
- Handle errors gracefully

❌ **Don't**:
- Scrape data the API provides
- Exceed rate limits intentionally
- Store PII without consent
- Use data for purposes against ToS
- Bypass authentication mechanisms
