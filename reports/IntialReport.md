Data

TMDB movies 20000 records and Goodreads books 30000 records with into_movie flag identifying 1760 adaptations.
I also am looking at folding in a few wikipedia articles to try and find more movies based off books as they have a complete list spread across multiple articles, however 1760 of the most noticible I thought was a good start.

Database

SQLite for portability and zero configuration in the Jupyter environment without requiring server permissions. SQL is also the language im most comfortable in for database manipulation. 

The Python script creates a SQLite database with three tables: movies, books, and book_movie_links. It reads the TMDB movie CSV and Goodreads book CSV from the current directory, cleans the data by selecting relevant columns and handling missing values, then inserts the records into their respective tables. The final verification queries confirm successful loading and display sample adapted books for quick validation.

Hypothesis

There may be textual features (in combination with some others) that can be used to help perdict which peices of fictions adapt well to screen.

Experiment Plan Summary
Feature Engineering

Extract non-textual features from books including rating, voters_count, publication_date, genres, and author metrics. Extract textual features from book descriptions and movie plot summaries using Sentence-BERT embeddings to capture semantic meaning. Compute cosine similarity between each book and its matched movie to measure narrative alignment.

Similarity Scoring

For each adapted book compute the semantic similarity between its description and the movie plot summary. Use this similarity score as a feature alongside structured book features to understand what makes a successful adaptation.

Modeling

Train regression models on adapted books to predict movie vote_average and popularity using book features and similarity scores. Use XGBoost and Random Forest with RMSE and R² evaluation to identify which features drive adaptation success.(will test other models just picked a few to start).

Ranking

Apply the trained models to all unadapted books to predict their potential movie success metrics. Rank unadapted books by predicted vote_average and popularity to generate a recommendation list of high-potential IP.

I want to work on some sort of weighted metric between boxoffice and review score toe create an aggreagate score to more easily compare movies, im thinking of using a weighted average of the percentile of book2movies box office total gross gross to budget and reviews. This should maybe act as a better target varible than box office or reviews individually.  

Output

Produce a ranked list of the top 50 untapped books with highest predicted commercial potential. Include feature importance analysis to explain why each book ranks highly. Deliver recommendations to studio executives for acquisition consideration.