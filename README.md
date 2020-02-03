# insight
My project for [Insight Boston](https://www.insighthealthdata.com/) Health Data Science 2020A. Predicts book ratings based on data from [Goodreads](https://www.goodreads.com/), collected from the [UCSD Book Graph](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home?authuser=0). All code associated with the [web app](https://insight-novelist.herokuapp.com/) can be found at my [NoveList](https://github.com/megthommes/noveList) repository.

# Motivation
[Goodreads](https://www.goodreads.com/) is a "social cataloging website" that enables users to track which books they've read and would like to read, review the books they have read, and much more. However, there is no easy way to sort through your "To-Read" books. [NoveList](https://insight-novelist.herokuapp.com/) takes books you have read and books you would like to read, and predicts how much you would enjoy the books you want to read (from 1 to 5 stars).

# Organization
Due to memory limitations, I ran some of my scripts locally and others on [Google Colab](https://colab.research.google.com). Those that were run on [Google Colab](https://colab.research.google.com) are in their own specified folder.

## Workflow
### Importing the Data
[load_reviews_data](https://github.com/megthommes/insight/blob/master/scripts/load_reviews_data.ipynb) parses the ['goodreads_reviews_dedup.json.gz'](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/reviews?authuser=0) file into smaller csv files, then aggregates the "important" information ('user_id', 'book_id', 'rating', 'read_at', and 'started_at') into a dataframe and saves that dataframe to 'reviews.gz' (not linked due to size constraints). Both the 'user_id' and 'book_id' are mapped to different values according to ['user_id_map.csv'](https://github.com/megthommes/insight/blob/master/data/user_id_map.csv) and ['book_id_map.csv'](https://github.com/megthommes/insight/blob/master/data/book_id_map.csv) to decrease the size of the dataframe.

### Exploratory Data Analysis
[reviews_eda](https://github.com/megthommes/insight/blob/master/scripts/colab/reviews_eda.ipynb) loads 'reviews.gz' and removes 0 star ratings, books with less than 10 ratings, and users with less than 25 ratings. It saves this 'trimmed' data as 'reviews_trimmed.gz' (not linked due to size constraints) and examines the ratings distributions by stars, user, and book.

### Assessing Models
[build_training_sets](https://github.com/megthommes/insight/blob/master/scripts/colab/build_training_sets.ipynb) builds training sets of different sizes for 5-fold cross validation assessment of different models. Build training sets using 10k, 50k, 100k, 500k, 1M, and 5M reviews. These training sets were used in
- [model_cf_10k](https://github.com/megthommes/insight/blob/master/scripts/colab/model_cf_10k.ipynb)
- [model_cf_50k]()
- [model_cf_100k](https://github.com/megthommes/insight/blob/master/scripts/colab/model_cf_100k.ipynb)
- [model_cf_500k]()
- [model_cf_1M](https://github.com/megthommes/insight/blob/master/scripts/colab/model_cf_1M.ipynb)
- [model_cf_5M]()
to assess a variety of models for collaborative filtering.

# Built With
- [Jupyter Notebook](https://jupyter.org)
- [Google Colab](https://colab.research.google.com)
- [scikit-surprise](https://surprise.readthedocs.io/en/stable/)

Dependencies can be found in the environment.yml file, and this file can be used to create a conda environment with
```console
foo@bar:~$ conda env create -f environment.yml
```

# License
MIT @ [Meghan Thommes](https://meghanthommes.com/)
