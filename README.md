def read_file(file_path):
    """Read a file and return a list of lines."""
    with open(file_path, 'r') as file:
        return file.read().splitlines()

def sentiment_score(tweet, positive_words, negative_words):
    """Calculate the sentiment score of a tweet."""
    score = 0
    words = tweet.split()
    for word in words:
        if word.lower() in positive_words:
            score += 1
        elif word.lower() in negative_words:
            score -= 1
    return score

def main():
    # Read data from files
    tweets = read_file('tweets.txt')
    positive_words = set(read_file('words_positive.txt'))
    negative_words = set(read_file('words_negative.txt'))

    # Calculate sentiment scores for each tweet
    tweet_scores = [(tweet, sentiment_score(tweet, positive_words, negative_words)) for tweet in tweets]

    # Sort tweets by sentiment score (most positive first)
    sorted_tweets = sorted(tweet_scores, key=lambda x: x[1], reverse=True)

    # Display sorted tweets
    for tweet, score in sorted_tweets:
        print(f"Score: {score}, Tweet: {tweet}")

if __name__ == "__main__":
    main()

