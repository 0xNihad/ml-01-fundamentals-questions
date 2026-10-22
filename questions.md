# Chapter 1 — Theory questions

Answers in my own words. Questions paraphrased; numbering follows the book (Chapter 1, *The Machine Learning Landscape*).

## 1. How would you define machine learning?
Machine learning is building systems that improve at a task by learning from data instead of following rules a programmer wrote by hand. More formally: a program learns from experience E on task T, measured by performance P, if its performance on T, as measured by P, improves with E.

## 2. Name four types of applications where ML shines.
(1) Problems where hand-written rules would be endless or brittle, such as spam filtering. (2) Problems with no known algorithmic solution, such as speech recognition or image classification. (3) Changing environments, where the system has to keep adapting to new data (fraud detection, recommendations). (4) Getting insight from large amounts of data, i.e. data mining: finding patterns humans would not spot.

## 3. What is a labeled training set?
A training set in which every instance comes with the desired output (its label or target): for example emails each marked spam/ham, or houses each with their sale price.

## 4. What are the two most common supervised tasks?
Classification (predict a category: spam or ham, which digit) and regression (predict a number: a price, a temperature).

## 5. Name four common unsupervised tasks.
Clustering (group similar instances), dimensionality reduction (compress features while keeping the structure), anomaly/novelty detection (flag unusual instances), visualisation (map high-dimensional data to 2-D/3-D), and association rule learning (find items that occur together).

## 6. Which kind of algorithm would let a robot learn to walk on varied, unknown terrain?
Reinforcement learning: the robot (agent) acts, gets rewards or penalties from the environment (e.g. distance covered without falling) and learns a policy that maximises reward over time.

## 7. Which kind of algorithm would segment customers into groups?
If the groups are not defined in advance, a clustering algorithm (unsupervised), such as k-means or DBSCAN. If the business already knows the groups it wants and has labeled examples, it becomes a classification task (supervised).

## 8. Is spam detection a supervised or an unsupervised problem?
Supervised: we train on emails that are labeled spam or ham, and the model learns to predict that label for new emails.

## 9. What is an online learning system?
A system that learns incrementally: it is fed data one instance or one mini-batch at a time, and each learning step is cheap, so it can adapt continuously as new data arrives (as opposed to batch learning, which retrains on the whole dataset).

## 10. What is out-of-core learning?
Training on datasets too big to fit in memory: the algorithm loads one chunk, takes a learning step, discards it and moves on to the next chunk. It uses online-learning algorithms, but usually runs offline, so "incremental learning" describes it better.

## 11. Which type of algorithm relies on a similarity measure to make predictions?
Instance-based learning. The system memorises the training examples and predicts for a new instance by comparing it with the stored ones using a similarity (or distance) measure, as k-nearest neighbors does.

## 12. What is the difference between a model parameter and a hyperparameter?
A model parameter is learned from the data during training (for example the slope and intercept of a linear model). A hyperparameter is a setting of the learning algorithm, fixed before training and not learned by the model itself (for example the amount of regularisation, or k in k-NN). It is tuned by trying values and comparing validation performance.

## 13. What do model-based algorithms search for, how, and how do they predict?
They search for the parameter values that make the model generalise best to new instances. The usual strategy is to minimise a cost function that measures how bad the model is on the training data, plus a regularisation penalty if the model is regularised. To predict, they plug the new instance's features into the model with the learned parameters.

## 14. Name four main challenges of machine learning.
Too little training data, nonrepresentative training data (sampling bias), poor-quality data (errors, outliers, missing values), irrelevant features, overfitting, underfitting, and deployment issues (data drift, scaling, monitoring).

## 15. A model is great on training data but poor on new instances: what is happening, and what can you do?
It is overfitting: it learned noise and quirks of the training set. Fixes: get more training data; simplify the model (fewer parameters, fewer features) or regularise it more; clean the data (fix errors, remove outliers).

## 16. What is a test set, and why use it?
Data held out and never used for training or model selection. It is used once at the end to estimate the generalisation error on new instances, i.e. how the model will do in production.

## 17. What is the purpose of a validation set?
To compare models and tune hyperparameters without touching the test set: train candidates on the reduced training set, keep the one that does best on the validation set, then retrain it on the full training set. Cross-validation repeats this over several splits to make the comparison less noisy.

## 18. What is the train-dev set, when do you need it, and how do you use it?
A slice of the *training* data held out from training. It matters when the training data does not match production data (e.g. web photos for training but phone photos in production), and the validation/test sets come from the production distribution. If the model does poorly on train-dev, it is overfitting the training set. If it does well on train-dev but poorly on validation, the problem is data mismatch, and the fix is making training data look more like production data.

## 19. What can go wrong if you tune hyperparameters on the test set?
The hyperparameters get fitted to that particular test set, so its error becomes an optimistic estimate. The model then performs worse in production than the test score promised.
