# Kaggle Irrigation

## Kaggle Homework 1

### Referenced Notebooks

- https://www.kaggle.com/code/rohit8527kmr7518/ps-s6e4-catboost-pipeline
- https://www.kaggle.com/code/saamhm/eda-baseline-model-fe-cv-ensemble-blend
- https://www.kaggle.com/code/chovyxu/playgrounds2026-ep4-neural-network

### EDA Notebook

- https://github.com/amuelrath/gsb-s545/blob/master/kaggle/eda.ipynb

### Model Notebooks

- https://github.com/amuelrath/gsb-s545/blob/master/kaggle/bagging.ipynb
- https://github.com/amuelrath/gsb-s545/blob/master/kaggle/boosting.ipynb

### Discussion

**Discuss your modeling approaches. What did you try? What worked well? What didn't work well? Were model improvements
meaningful or small? Make sure to use performance metrics in your discussion. Also provide leaderboard scores for the
models. A table might be useful for organizing the metrics and leaderboard scores.**

I took very simple approaches. First, I train a default model.
Then I create a fine-tuned version. Hyperparam tuning only had a marginal effect on outcomes and took a lot of time to train for the RandomForest.
The CatBoost model improved greatly from hyperparameter tuning and didn't take long training on the GPU. The only problem I encountered was that cross-validation
was tricky with `catboost`. They have their own `cv` and the `CatBoost` doesn't play nicely with `sklearn`'s `cross_val_score`.

We use `balanced_accuracy` as the performance metric: it is what the competition scores on.

| Model     | Leaderboard Place | Balanced Accuracy Score |
|-----------|-------------------|-------------------------|
| `best_rf` | -                 | 0.94561                 |
| `best_cb` | 1801              | 0.95586                 |


**How did boosting versus bagging compare for your work?** 

To be blunt...bagging was not great. At least from the perspective of a novice/intermediate-low machine-learner, RandomForests just aren't good to use for making predictions in datasets with complex features or patterns.
I have seen them mostly used for diagnostic purposes or testing features, probabilities, etc.

Boosting was faster, more performant, and easier to tune.

**What is your "phase 2" plan to improve your model performance? Note that although the leaderboard is fun to watch, you are not graded on it (and a shake up often occurs at the end!)**

Definitely some feature engineering. This is the key way we can actually improve models by large magins.