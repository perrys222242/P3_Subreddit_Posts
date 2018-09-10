# The Most Epic Data-Science Problem
### ("How to bypass SJW-drama")

   The data-science problem investigated here is trying to answer where a given post originates. The main subreddits from two popular science-fiction franchises, 'Star Wars' and 'Star Trek' were chosen for this problem. Two of the most effective binary classifiers are examined in detail to provide the answer to the sourcing problem and in the process explain the most significant language features of the solution..

### Executive Summary:

   The Social-Justice Warriors are taking a bashing among fans of the post-Lucas Star-Wars-Extended-Universe. On the other hand, all is relatively quiet on the Star-Trek-Extended-Universe front. The average Sci-Fi enthusiast would do well to avoid the toxic tension of the former fandom in the media.
   There’s a huge bummer associated with encountering a spoiler. Whether it be in sports of movies, wouldn’t it be great to avoid that algorithmicly? We need a reliable way to identify if a post or media article is talking about Star Wars and what are the most important words to look for to make that identification.
   My model can generalize new posts for the source and thereby the expected level of tameness in the contents.  Trained from the titles of about 900 posts, one can be almost 90% sure which flavor of the galactic genres one is about to read.
   There are distinct collections of words that make the separation between the two subjects possible, such that only 10-15% of posts are truly ambiguous.  This can be done using one for two classifier models.
   Don’t wait.  Subscribe to our filtering guide today and save yourself the aggravation of reading another SJW-battering comment.  Get out of the Dark Side, once and for all.
   

## Contents

| Notebook | Description |
| --- | --- |
| 1 | Data Collection |
| 2 | Preprocessing |
| 3 | Modeling |
| 4 | Model Evaluation |


### Findings
a) No promotional ads pulled during data collection.
b) The "Star"/"star" should be removed from references in posts to the franchise titles; no value added.
c) Opted to set "min_df" in TF-IDF vectorizer to 2.
d) Bi-grams were incorporated into modeling, but with minor significance
e) Star-Trek posts were more active at the start of data collection, but Star-Wars posts became more active a week later.
f) The KNN-model turned into a fail for this data/project.
g) Random-forests modeling produced the second-worst results.
h) Logistic-regression, Naive-Bayes and SVM gave accuracy scores in the high 80-percentiles.
i) Testing on fresh unique posts yielded quite good results for logistic regression as well with misclassification under 11%
j) The new test data was more unbalanced than the training data and may have affected the Random-forests model negatively.

### Research
None.


# Summary of Methodology and Results

#### Cleaning and Exploration of Data

861 Star-Wars posts and 968 Star-Trek posts were gathered for model traing.

#### Pre-processing of Data in advance of Modeling

There should be a well-defined function for removing the "Star"/"star" strings from the references to the franchise titles, but there were challenges that still needed to be worked through to come up with elegant code.

#### Detailing the Two Classification Models using Logistic-Regression and Random-Forests

| Log-Reg | f1-score |
| --- | --- |
| S-Wars | 0.93 |
| S-Trek | 0.85 |
| Average | 0.89 |


| Random-forests | f1-score |
| --- | --- |
| S-Wars | 0.81 |
| S-Trek | 0.85 |
| Average | 0.83 |


#### Honorable-mention Classification Models, using Naive-Bayes and SVM

The f1-scores for the Naive-Bayes and SVM models came in at 0.86 and 0.87, respectively.

#### Statistical Metrics to Evaluate the Models

The size of the new test data at 441 posts happened to be around the same size of the 458 posts in the split-test data.  Unfortunately, it was more unbalanced with about 65% of the posts coming from the Star-Wars subreddit.

The test results showed that the models generalize relatively consistently.  The models also seem to show robustness in the face of more unbalanced sampling.

| Log-Reg | f1-score |
| --- | --- |
| S-Wars | 0.92 |
| S-Trek | 0.85 |
| Average | 0.89 |


| Random-forests | f1-score |
| --- | --- |
| S-Wars | 0.85 |
| S-Trek | 0.77 |
| Average | 0.82 |


#### Conclusion

The subreddit subjects chosen in this project seem to present a unique opportunity to demonstrate the strength of generalization by three of the five classifiers studied.  There is plenty of evidence that with the exception of KNN, models can perform considerably better than the baseline model and/or random choice.  In fact, with logistic regression, there can be almost 90% accurate classification of posts from the troubled Star-Wars fandom.


# Appendix

### Data-file Contents:

#### JSON-type

| Name | Description |
| --- | --- |
| swars | 25 SW-posts from Aug-29 |
| swars_0830_2020 | 25 SW posts from Aug-30 |
| trek_0831 | 1000 posts from Aug-31 |
| trek_0902 | 1000 posts from Sep-02 |
| trek_0904 | 1000 posts from Sep-04 |
| trek_0906 | new test data from Sep-06 |
| wars_0902 | 1000 posts from Sep-02 |
| wars_0904 | 1000 posts from Sep-04 |
| wars_0906 | new test data from Sep-06 |


#### CSV-type

| Name | Description |
| --- | --- |
| combined | data from both rubreddits with full franchise references |
| combined_no_star | data without "Star"/"star" for show/movie |
| combined_new_test_no_star | new test data without "Star"/"star" for show/movie |
| new_st_0906 | new test data from Sep-06 |
| new_sw_0906 | new test data from Sep-06 |
| posts_trek | training data from Sep-02 |
| posts_wars | training data from Sep-02 |
| postsL_trek0830_2051 | data from looping |
| postsL_wars0830_2051 | data from looping |
| tfidf_trek | vectorized matrix from Sep-04 |
| tfidf_wars | vectorized matrix from Sep-04 |
| X_test | train-test-split from Sep-07 |
| X_train | train-test-split from Sep-07 |
| y_test | train-test-split from Sep-07 |
| y_train | train-test-split from Sep-07 |


#### PKL-type

| Name | Description |
| --- | --- |
| naive_bayes | NB-model |
| p3_knn | KNN-model |
| p3_log_reg | Logistic-regression model |
| p3_log_reg_MinDF2 | LogReg-model with 'min_df' = 2 |
| p3_randomforests | Random-Forests model |
| p3_SVM | SVM-model |
| p3_xtest_transform | vectorized split data |
| p3_xtrain_transform | vectorized split data |
| tfidf | tuned vectorizer |







