# Goodreads_rating_prediction

 ML analysis of goodreads data

##Introduction:

The data used in this project was scraped from Goodreads and posted on Kaggle. Goodreads is a website hosted by Amazon that collates book reviews submitted by users. The user reviews are used to fuel an algorithm that recommends books to users based on their reading history.

A particularly important feature of the dataset is genre. Many readers gravitate to certain genres to the exclusion of others, so the genre categorization of a book dramatically affects the audience who becomes aware of that book. Because introducing a book to the correct audience is crucial to its success, we should work to find an optimal method categorizing books.

All of this raises an interesting question: can we break down an artistic medium, such as fiction, into numerical values? Algorithms increasingly control which books we are exposed to, but how effectively we can predict a book’s popularity from its numerical descriptors?


##Questions:

1.	Can you predict the popularity of a book from numerical data?

2.	Are our conventional genre categories the best way of classifying books?

3.	How many genres do we really need to represent this data?


##Data Description:

Source: [Kaggle](https://www.kaggle.com/datasets/austinreese/goodreads-books/data)

The dataset has 52199 data samples, where each sample is a distinct book, and 31 features. Many of these features are unusable for this analysis; the ISBN feature, for examples, consists of numerical identifiers that tell us nothing meaningful about the books they identify.

Some of the interesting features are: the publishing date, the length of the book, the publisher, the awards won by the book, and the genres in which users have classified a book.

In the genre feature, each book is associated with multiple genre-count pairs, where “count” is the number of users who classified a book in that genre. 871 distinct genres are represented, so the genre feature can be expanded into 871 distinct features where each feature contains the “count” entries. This restructuring provides useful numerical features; however, these columns are missing many entries, which may make this data difficult to work with.

The “description” feature contains user-submitted, textual descriptions of the books.


##Methods:

First, we perform dimensionality reduction on the 871 genre variables. This is necessary because many of the genres are clearly redundant: “young adult”, “young adult-coming of age”, and “young adult-high school” are undoubtedly colinear. By reducing the dimensions of this space, we can answer Question 3.

Question 1 can be answered using classification and regression models. The feature space can include all the features described in the previous section. The target variable is called “average rating”; this feature is the average of all user-submitted ratings on a five-star scale. This is a continuous variable, however, it can be easily converted to a categorical variable.

For the continuous variable, we use SGD regressor to try and map the feature space to the target. For the categorical variable, we use the Decision Tree, Random Forest, and XGBoost classifiers. We evaluate the accuracy achieved by these models to determine whether the feature space contains sufficient information to predict the popularity of a book.

We employ clustering algorithms, such as PCA and UMAP, to answer question 2. We cluster on the feature space (book length, awards, etc) and then see if any of the automatically identified clusters match the established genres. If they do not, then perhaps these clusters represent a better way of categorizing the books than by genre.

The Term Frequency Inverse Document Frequency (TF-IDF) Vectorizer is used to embed the "description" feature in numerical space.
