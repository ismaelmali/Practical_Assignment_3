# Comparing Classifiers: Bank Marketing Campaign

## Overview

This project uses a Portuguese bank's telemarketing data to predict whether a client will subscribe to a term deposit. The data comes from 17 marketing campaigns run between May 2008 and November 2010, and is from the UCI Machine Learning Repository.

Link to Jupyter Notebook: https://github.com/ismaelmali/Practical_Assignment_3/blob/f96ed111867fe182aee2eb888ee59b00631b6e90/prompt_III.ipynb 

## Business Objective

Build a classification model that predicts whether a client will subscribe to a term deposit, so the bank's marketing team can prioritize which clients to contact. The goal is to increase the success rate of calls while cutting down on wasted contacts, time, and cost.

## Approach

- Used only basic client info as features for the first pass: age, job, marital status, education, default status, housing loan, and personal loan.
- Left out call duration on purpose, since it's not known before a call happens and would make the model unusable for real targeting.
- Encoded categorical features with one-hot encoding, scaled age with StandardScaler, all inside a sklearn Pipeline.
- Compared four classifiers: Logistic Regression, KNN, Decision Tree, and SVM.
- Tuned each with GridSearchCV, using recall as the scoring metric since missing a client who would say yes is more costly than an unnecessary call.
- When swicthing performance metrics, I chose recall because missing a potential subscriber costs the bank more than an extra call

## Key Findings

Only about 11% of clients contacted actually subscribed, so the baseline (always guess "no") already gets ~89% accuracy. Any useful model needs to beat that.

Basic demographic features alone turned out to be weak predictors. The untuned models barely beat the baseline. After tuning for recall, models started catching more actual subscribers, but at a real cost: one tuned Decision Tree caught 91% of true subscribers but was wrong overall about 70% of the time. This is a tradeoff that is sometimes costly and how far to push it depends on how the bank weighs a wasted call against a missed sale.

A few client traits stood out as predictive: being a student or retired increased the odds of subscribing, while an unknown default status or a blue collar job decreased it.

## Recommendations

1. Don't target based on demographics alone. This first model isn't strong enough on its own.
2. Bring in campaign and contact history data (prior outcomes, number of contacts) and economic indicators (interest rates, employment trends) for the next iteration. The original research behind this dataset found these matter more than client demographics.
3. Students and retirees are a reasonable low cost group to prioritize now, while a stronger model is built.
4. Decide on an acceptable recall/accuracy tradeoff before tuning further, based on actual call cost vs. missed opportunity cost.
5. Never use call duration in a model meant to run before a call takes place.
