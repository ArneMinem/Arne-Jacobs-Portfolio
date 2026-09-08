# Identifying the Nutritional Score of a Prepared Meal
`20th of September 2025 – 7th of December 2025`

**Repository:** source code is hosted in a private academic repository due to university policy.

However, the project report is available [here](F21DL_Final_Report.pdf).

## Project Overview

Promoting healthier eating is a vital public health priority, and visual indicators like the Nutri-Score significantly improve consumers' ability to choose healthier products. However, Nutri-Scores are traditionally restricted to packaged foods with nutrition labels, leaving a major gap for unlabelled items, restaurant dishes, and homemade meals.

This project builds artificial intelligence models to bridge that gap by mapping the nutritive values of packaged foods to their Nutri-Scores, extending predictions to homemade meals using their photos and ingredient compositions.

## Datasets

The project leverages two primary datasets sourced from Kaggle:

* **Food Ingredients and Recipe Dataset with Images:** Contains 13,300 prepared meals featuring titles, ingredients, instructions, and images.
* **Open Food Facts Dataset:** Provides 350,000 food products across 163 features, including detailed nutritional values, additives, and official Nutri-Scores (`nutrition_grade_fr`).

## System Architecture & Methodology

* **Nutri-Score Prediction:** Evaluated multiple classification models including a Single-Layer Perceptron baseline, Multi-Layered Perceptrons (MLP) with hyperparameter tuning, and Random Forest classifiers, to predict Nutri-Scores (A to E) from nutritional macro features.
* **Meal Clustering:** Applied K-Means clustering on normalized ingredient proportion vectors from the recipe dataset, utilizing silhouette score validation to determine the optimal cluster count ($k=18$).
* **Image Classification & Bridging:** Implemented Convolutional Neural Networks (CNNs) to classify meal images into ingredient-based clusters, subsequently bridging the modules by mapping cluster ingredient compositions to macro values to predict final Nutri-Scores.

---

## My Contributions (Arne Jacobs)

As a core member of the team, my work spanned data engineering, collaborative machine learning modeling, repository architecture, and technical writing:

* **Data Preprocessing:** Developed the `Ingredients_Data.ipynb` script to clean and standardize the 13,300-meal dataset. This involved parsing complex quantities and units, converting measurements to grams, stripping noise and descriptive text, and utilizing AI assistance to handle unstructured ingredient strings.
* **Collaborative Modeling:** Assisted Ali with K-Means clustering implementation, CNN architecture design and tuning, and bridging the modular pipeline from meal images to ingredient clusters and final macronutrient mapping.
* **Repository & Team Management:** Established the core documentation structure within the GitHub repository and coordinated team management workflows.
* **Technical Writing:** Authored key sections of the formal project report, specifically the *Introduction*, *Related Work*, and the *Dataset Description and Analysis* (covering dataset properties and the meals preprocessing pipeline).

## Project Team

* **Arne Jacobs**
* **Ali Amir**
* **Hannah Davidson**
* **Karol Loskot**
* <small> Wajid Ali </small>