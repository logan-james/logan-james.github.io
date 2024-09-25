---
layout: page
title: Profanity Detector 
description: a machine learning project that detects profanity
img: assets/img/gui.jpeg
importance:
category: work
related_publications: true
---
**Machine Learning**

My profanity detection system employs a Logistic Regression model for binary classification to predict whether a given tweet or comment contains profanity. Here's a detailed breakdown of our machine learning approach:

`What`: We chose Logistic Regression as our core algorithm. It's a probabilistic classifier that excels in binary classification tasks. In our context, it predicts the probability of a text being profane based on its features. This algorithm is best suited for the task, considering factors such as accuracy, computational time, and scalability.

`How`: The development of our machine learning model involved several key steps:
1. Feature Extraction: We converted the text data into TF-IDF vectors, limiting to 5,000 features. This process captures relevant word patterns and their importance across the dataset.
2. Model Training: We trained the Logistic Regression model on a resampled dataset after applying SMOTE to handle class imbalance. We used default hyperparameters for initial training.
3. Model Saving: Once trained, we saved the model and vectorizer using pickle, allowing for easy reuse in our Streamlit application.

`Why`: We selected Logistic Regression for several compelling reasons:
1. Efficiency: It provides quick predictions, making it suitable for real-time applications like content moderation.
2. Simplicity and Interpretability: The algorithm is relatively easy to understand and explain, which is crucial for transparency in content moderation systems.
3. Probabilistic Output: Logistic Regression offers flexibility with probability thresholds. This allows for adjusting the strictness of the moderation policy as needed.
4. Low Computational Cost: Both for training and real-time use, Logistic Regression is computationally inexpensive, making it ideal for deployment in various environments.

While more complex models like neural networks could potentially offer higher accuracy, we found that Logistic Regression provided a good balance between performance, interpretability, and computational efficiency for our specific use case.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/piechart.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/heatmap.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/matrix.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Our application includes three key visualizations that provide insights into the model's performance and the nature of the dataset. These visualizations are accessible through the Streamlit GUI and offer valuable information for both technical and non-technical users.
</div>


A `pie chart` showcases the percentage distribution of profane versus non-profane tweets in the test dataset. This visualization provides an immediate overview of the class balance in our data, highlighting any potential imbalances that might affect the model's performance or interpretation of results.

This `heatmap` visualizes the precision, recall, and F1-scores for both profane and non-profane classes. The color intensity represents the magnitude of each metric, allowing for quick comparison across different performance aspects of the model. This visualization is particularly useful for identifying areas where the model excels or needs improvement, facilitating targeted optimization efforts.

This heatmap displays the `confusion matrix`, illustrating the number of correct and incorrect predictions for both profane and non-profane tweets. The matrix is color-coded, with darker colors representing higher numbers of predictions. This visualization allows users to quickly assess the model's overall accuracy and identify any significant patterns in misclassifications.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/gui.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This is the simple graphical interface that allows users to test the model.
</div>