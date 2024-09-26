#Using pandas for loading and handling the data
import pandas as pd

# Reading the smaller file for simplicity (same approach for larger file in chunks)
file_path = '/content/correct_twitter_201904 (1).tsv'
df = pd.read_csv(file_path, sep='\t')

# To check the columns of data
df.columns

#How many tweets were posted containing the term on each day
def tweets_per_day(term, df):
    term_df = search_term_data(term, df)
    return term_df.groupby(term_df['ts1'].dt.date)['id'].count()

    #How many unique users posted a tweet containing the term
def unique_users(term, df):
    term_df = search_term_data(term, df)
    return term_df['retweeted_author_id'].nunique()

    #How many likes did tweets containing the term get on average
def avg_likes(term, df):
    term_df = search_term_data(term, df)
    return term_df['likes'].mean()

    # Where (in terms of place IDs) did the tweets come from
def tweet_places(term, df):
    term_df = search_term_data(term, df)
    return term_df['place_id'].unique()

    #What times of day were the tweets posted at
def tweet_times(term, df):
    term_df = search_term_data(term, df)
    term_df['time'] = term_df['date'].dt.time
    return term_df['time'].value_counts()

    #Which user posted the most tweets containing the term
def top_user(term, df):
    term_df = search_term_data(term, df)
    return term_df['user_id'].value_counts().idxmax()
