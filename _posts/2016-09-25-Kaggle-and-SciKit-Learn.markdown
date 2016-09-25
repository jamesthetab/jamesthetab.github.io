---
layout: post
title:  "Kaggle and SciKit-Learn"
date:   2016-09-25 20:19:28 +0100
categories: jekyll update
---

A few weeks ago a data scientist friend suggested I look at Kaggle.com and tackle some of their machine learning challenges.

Like all first time users, I began with the Titanic datset, and trying to understand which of the known background about the passengers led to a higher chance on survival. You are provided with around 1500 training cases, where you are told whether passengers survived or not, and have to make a prediction for the reamining 600 test cases. Kaggle have their own tutorials on how to get started and I began by reinterpret these as Jupyter notebooks and posted them on my GitHub.

I begin by expanding the Kaggle tutorial on how to use ```NumPy``` and ```CSV``` packages in "[1. Titanic - NumPy and CSV packages.ipynb](https://github.com/jamesthetab/Kaggle/blob/master/1.%20Titanic%20-%20NumPy%20and%20CSV%20packages.ipynb)" - this makes a model based on "train.csv" and applies it to "test.csv". I output two predictions - a "1a. ModelBasedonGenderAlone.csv", and then a "1b. ModelBasedonGenderClass.csv"

I then use a ```DataFrame``` in ```Pandas``` to streamline this process using ```Pandas```'s powerful built-in tools in "[2. Titanic - Pandas .ipynb](https://github.com/jamesthetab/Kaggle/blob/master/2.%20Titanic%20-%20Pandas%20.ipynb)". I repeat the ideas of my NumPy model to produce "2. genderclassmodel-pandas.csv".

I then analyse the data using ML in "3. Titanic - Random Forests.ipynb" and work in terms of ```Random Forests``` using the ```scikit-learn``` package to produce "[3. FamSizeAgeClassForest.csv](https://github.com/jamesthetab/Kaggle/blob/master/3.%20Titanic%20-%20Random%20Forests.ipynb)".

I look forward to going deeper into machine lerning using these examples over the coming weeks.