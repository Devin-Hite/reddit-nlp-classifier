Problem Statement:
Is it possible to build a prediction model using Natural Language Processing that can discern whether a random post from reddit is likely from the subreddits r/NBA or r/soccer?

To answer this question I first used the requests library in Python to scrape data (reddit posts) from both subreddits. I estimated that 2,000 posts would do the trick. I initially considered using only 1000 posts but decided to broaden that to 2000 in order to overcome possible recency bias. After scraping and storing the data, I began with some preprocessing functions in order to make the data work for the models I intended to use. I tokenized and lemmatized the title columns of both subreddits and used a Count Vectorizer on the remaining data to get counts of common words used in both subreddits. I decided to go with only the title columns since my insider knowledge of r/soccer and r/nba is that they both often have posts that are video links, images, or short clips, thus leaving large amounts of posts that would have nonexistant text in the body section of the posts. I checked for 'deleted' and 'removed' text in the post titles as well and found none. This left me with 2000 posts even for both subreddits, effectively creating a baseline acccuracy score of 50% since you have a 2000/4000 chance to correctly predict the corresponding subreddit of a post with no NLP involved. I also checked the average title length of posts in each subreddit and found them both to be 16 words and thus dismissed that as a potentially helpful metric to consider. There were several words that I expected would be present in both subreddits, since they are both sports-oriented. Words like "game, Spurs, score, win" etc were not going to be helpful with my models. I also checked the top 50 most common words from each subreddit in order to get an idea of whether or not there would be very common words that would be given high-value in my models. Despite both subreddits being sports-oriented with some common words, they had unique words in their top 50 most common words as mostly team names and league names were present. With all of my data sorted, I decided that I would test out Logistic Regression, Naive Bayes, Random Forrests, and Extra Trees models to see which one would have the greatest accuracy. I intented to end up with at least one model that could reach 90%+ accuracy when making these predictions and predict a high likelihood of success since my cleaned up data showed many unique words in high-usage for both subreddits.

My model scores were as follows:
Naive-Bayes model: 98.7% accuracy on train data, 96.2% accuracy on test data
Logistic Regression model: 99.7% accuracy on train data, 95.2% accuracy on test data
Random Forests model: 90.7% mean accuracy
Extra Trees model: 92.3% mean accuracy

My Naive-Bayes model performed the best, having the hihgest accuracy on the test data while only being moderately overfit on the train data. A simple Logistic Regression model was the second best model though was a little more overfit on the train data. The Naive-Bayes model misclassified 30/800 posts on the test data, while Linear Regression misclassified 38/800.

In conclusion, I was successfully able to create several models with 90%+ accuracy, thus vastly improving on the baseline score. The models could have been improved even more with a larger dataset of more posts. They could also be improved by incorporating text posts to increase unique word counts classification. However, since both of the subreddits largely consist of posts with video clips and no text, I felt it would be disengenous to not include those posts. My models predict a wider variety of the types of posts you might expect to see in those subreddits. If one were to include the text body of posts in the subreddits, they might create a better performing model for purely text-based posts, but first would need to drop a significant amount of null posts relating to video clips, which would not be very representative of the subreddits' true form.