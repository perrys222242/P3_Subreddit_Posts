# Predict the Epic Sci-Fi Universe
### ("How to skip SJW-drama")
by p.Shyr

   The natural-language problem explored asks whether or not Star-Trek post-titles can be identified from a set of science-fiction franchise posts. The subreddits from which the post-titles originated, were 'StarWars' and startrek.'  Our positive class is any post from 'r/startrek' and our baseline model predicts that a science-fiction post always originates from Star-Trek fans.

### Executive Summary:

   The Social-Justice Warriors are taking a bashing among fans of the post-Lucas Star-Wars-Extended-Universe. On the other hand, all is relatively quiet on the Star-Trek-Extended-Universe front. The average Sci-Fi enthusiast would do well to avoid the toxic tension of the former fandom in the media.
   There’s a huge bummer associated with encountering a spoiler. Whether it be in sports or movies, wouldn’t it be great to avoid that algorithmicly? We need a reliable way to identify if a post or media article is talking about Star Wars and what are the most important words to look for to make that identification.
   My supervised classification model can generalize new post-titles for the source and thereby the expected level of tameness in the contents.  Trained from the combined titles of 1829 'r/startrek' and 'r/StarWars' posts in the two classes, one can be almost 90% sure which flavor of the galactic genres one is about to read.
   There are distinct collections of words that make the separation between the two subjects possible, such that only 10-15% of posts are truly ambiguous.  This can be done using one for two classifier models.
   Don’t wait.  Subscribe to our filtering guide today and save yourself the aggravation of reading another SJW-battering comment.  Get out of the Dark Side, once and for all.
   

## Contents

| Notebook | Description |
| --- | --- |
| 01 | Data Collection |
| 02 | Preprocessing |
| 03 | Modeling |
| 04 | Model Evaluation |


### Findings:
#### Data Collection and Preprocessing
a) No promotional ads pulled during data collection.
b) With incomplete text contents (72% for Star Trek and 27.5% for Star-Wars posts), only titles were modeled.
c) The "Star"/"star" should be removed from references in posts to the franchise titles; regex seems to the best technique to do that.
d) Star-Trek posts (my positive class) were more active on the 'r/startrek' subreddit at the start of data collection, but 'r/StarWars' posts became more active a week later.
#### Modeling
e) The initial search for hyperparameters produced some bizarre settings of "1" for 'min_df' and "0.183" for 'max_df.'  I opted to set 'min_df' in the TF-IDF vectorizer to "2" and 'max_df' to "0.5" despite the results of that GridSearch-pipeline.
f) Bi-grams were incorporated into modeling, but with minor significance
g) The Multinomial Naive-Bayes model was the most overfit model.
h) The kNN-model performed the worst of all five models tested, although it was the least overfit.
i) Random-forests modeling produced the second-worst results.
j) The "linear" kernel seemed to work the best for the Support-vector machine modeling.
k) Logistic-regression, Naive-Bayes and SVM gave accuracy scores in the high 80-percentiles. 
#### Model Evaluation
l) Testing on fresh unique posts yielded quite good results for logistic regression as well with misclassification under 11%.
m) The Random-forests score were lower if anything, but generalized as well or better than expected for the positive class.
n) The new test data was more unbalanced than the training data and may have affected the Random-forests model negatively.  However, the results did not seem to be impacted much by this.
o) The Random-forests model has learned to find the "signal" for the positive class much better than the negative class, even when the former is the minority class.
p) There are many more wildy-incorrect predictions made by the Random-forests model than the Logistic-Regression model.  This may be from a combined effect of not learning the negative class as well and negative class being the unbalanced majority.
q) the likelihood of wildly-incorrect predictions does not seem to be related to the number of incorrect predictions as a group, but how it generally predicts one class or the other.
r) We might have benefitted from either lemmatizing or stemming, prior to modeling.


### Research
N/A


# Summary of Methodology and Results

#### Cleaning and Exploration of Data

861 Star-Wars posts and 968 Star-Trek posts were gathered for model training.

#### Pre-processing of Data in advance of Modeling

There should be a well-defined function for removing the "Star"/"star" strings from the references to the franchise titles, but there were challenges that still needed to be worked through to come up with elegant code.

#### Models Fit and Compared

| Model | f1-score |
| --- | --- |
| Logistic Regression | 0.89 |
| SVM | 0.87 |
| Naive-Bayes | 0.86 |
| Random Forests | 0.83 |
| KNN | 0.47 |

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

   It makes sense that training with more data would only improve the accuracy of each of the models.  There were wildly-confident misclassifications where lemmatizing or stemming would have been effective.  The reason for the generally high predictability of the model may lie in the rich distinctiveness of the language built in each franchise.
   
   Our best models beat our baseline model without a doubt.  They provide a means to identify 'r/startrek' post-titles and a more tempered Sci-Fi universe with compelling stories as well as balanced character diversity.


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
| cvec | Count-Vectorizer data |
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



### Pickle-file Contents:

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







