# Module 6 Challenge: data_sourcing_challenge

## Problem Statement
Retrieve information about movies, in particular, movie reviews, from two data sources, The New York Times and The Movie Database. Merge the data into one and export it into a `.csv` datafile.

## Solution
The solution proceeds through the following steps:
1. Retrieve movie reviews from the New York Times database for movies released between 01/01/2013 and 05/31/2023 containing the word "love" in the headline. Store the data in a Pandas dataframe.  
   There are 200 movies in the New York Times databse that fit the search criteria, however, the New York Times only returns 10 results at a time. Therefore, a total of 20 calls to the New York Times database have to be made to retrieve all movie reviews.
2. After normalizing the data, extract the titles of the movies retrieved from the New York Times from the `headline.main` column.
   > [!Note]
   > I am using the following `Lambda` function, `lambda st: st[st.find("\u2018")+1:st.find("\u2019 ")]`, instead of the given `lambda st: st[st.find("\u2018")+1:st.find("\u2019 Review")]` since in this application it returns more valid titles.

   If present, remove trailing commas from the extracted titles. 
3. Use the movie titles extracted in the previous step to retrieve the following movie details from The Movie Database.
   * Title,
   * Original Title,
   * Budget,
   * Original Language,
   * Homepage,
   * Overview,
   * Popularity,
   * Runtime,
   * Revenue,
   * Release Date,
   * Vote Average,
   * Vote Count,
   * Genres,
   * Spoken Languages, and
   * Production Countries.

   Store the data in a Pandas dataframe.
4. Use the Pandas `merge` function to combine the data into one Pandas dataframe using the title as the column on which to merge.
5. Clean the combined data by
   * Removing the characters "[", "]", and "'" from the columns `genres`, `spoken_languages`, and `production_countries`.
   * Removing the `byline.person` column.
   * Removing duplicate lines.
   * Resetting the index.

   The final dataframe contains the following columns:
   * `title`,
   * `original_title`,
   * `budget`,
   * `original_language`,
   * `homepage`,
   * `overview`,
   * `popularity`,
   * `runtime`,
   * `revenue`,
   * `release_date`,
   * `vote_averag`e,
   * `vote_count`,
   * `genres`,
   * `spoken_languages`,
   * `production_countries`,
   * `web_url`,
   * `snippet`,
   * `source`,
   * `keywords`,
   * `pub_date`,
   * `word_count`,
   * `headline.main`,
   * `headline.kicker`,
   * `headline.content_kicker`,
   * `headline.print_headline`,
   * `headline.name`,
   * `headline.seo`,
   * `headline.sub`,
   * `byline.original`, and
   * `byline.organization`.
6. Export the data into a `.csv` file called `movie_data.csv`, omitting the index.