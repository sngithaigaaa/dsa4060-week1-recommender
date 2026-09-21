# DSA 4060 Week 1: Popularity-Based Movie Recommender

## Student
* **Name:** Your Name
* **Student Number:** Your Student ID Number
* **Course:** DSA 4060 - Recommender Systems
* **Date:** September 21, 2026

---

## Project Overview
This project explores the MovieLens latest-small user-item interaction dataset to build and evaluate two non-personalized movie recommendation baselines: a **Minimum Rating Threshold Baseline** and a **Bayesian Weighted Rating Baseline**. 

Non-personalized recommenders provide a uniform ranked list of popular items to all users. They serve as essential home-page baselines for cold-start scenarios where individual user preference history is not yet available[cite: 1].

---

## Dataset
* **Source:** [GroupLens MovieLens Datasets](https://grouplens.org/datasets/movielens/)
* **Dataset Variant:** MovieLens `latest-small`[cite: 1]
* **Files Used:**
  * `movies.csv`: Contains `movieId`, `title`, and `genres`[cite: 1].
  * `ratings.csv`: Contains `userId`, `movieId`, `rating` (0.5 to 5.0 scale), and `timestamp`[cite: 1].
* **Access Date:** September 21, 2026

---

## Methods
1. **Exploratory Data Analysis (EDA):**
   * Validated missing values, record duplicates, and identifier consistency across datasets.
   * Calculated matrix sparsity and analyzed user-item interaction distributions.

2. **Minimum Rating Popularity Baseline:**
   * Aggregated ratings by movie to calculate average rating ($\bar{R}$) and total rating count ($v$).
   * Filtered candidates requiring a minimum of $m = 50$ ratings before ranking by average rating.

3. **Weighted Rating Baseline (IMDb Formula):**
   * Implemented a Bayesian smoothing formula that pulls sparse rating averages toward the global mean ($C$):
     $$\text{Weighted Score} = \left(\frac{v}{v + m}\right) \times R + \left(\frac{m}{v + m}\right) \times C$$
   * Selected $m$ dynamically using the 90th percentile of rating counts across all rated movies.

---

## Reflection Questions

### 1. What did the popularity baseline do well?
The popularity baseline provided a clean, robust, and transparent non-personalized recommendation list. It effectively filtered out obscure movies with artificially high ratings (e.g., a single 5-star review) and successfully identified universally acclaimed blockbusters that appeal to a general audience. It serves as a reliable default home-page recommendation for new users with no prior interaction history.

### 2. Which users or movies might be disadvantaged by this approach?
* **Users:** Niche viewers or fans of specific non-mainstream genres (e.g., foreign films, cult classics, independent documentaries) are disadvantaged because they receive the exact same mainstream list as everyone else[cite: 1].
* **Movies:** Lesser-known, high-quality, or newly released movies are disadvantaged[cite: 1]. Because they lack a high volume of ratings, they cannot meet the minimum threshold ($m$) or score high enough on the weighted formula, leading to a "rich-get-richer" popularity bias[cite: 1].

### 3. What additional data would be needed to personalize recommendations?
To personalize recommendations, we would need:
* **User demographic or explicit preference data:** Age, gender, self-selected favorite genres, or preferred languages[cite: 1].
* **User interaction history:** Historical ratings, watch logs, clicks, or bookmark history per individual user ID[cite: 1].
* **Contextual & implicit data:** Device type, time of day, location, or implicit feedback such as search history and watch duration[cite: 1].

### 4. Which result would you use as the home-page baseline and why?
I would use the **Weighted Score Baseline** as the home-page baseline[cite: 1]. Unlike the rigid cutoff of the minimum-rating threshold (which completely discards movies below $m$), the weighted Bayesian formula smoothly adjusts a movie's score based on statistical confidence[cite: 1]. It naturally pulls low-volume movies toward the global mean rating ($C$) while allowing highly rated movies with substantial evidence to rise to the top[cite: 1].

### 5. What will you change in the next version of the recommender?
In the next version, I will:
1. Implement a **Content-Based Filtering** or **Collaborative Filtering** model (such as Matrix Factorization/SVD or user-item KNN) to deliver personalized recommendations based on individual user interaction vectors[cite: 1].
2. Add explicit evaluation metrics (such as Precision@K, Recall@K, and RMSE) by splitting the interaction data into train and test sets[cite: 1].
3. Introduce diversity and novelty metrics so the system does not solely recommend the top 10 well-known blockbusters[cite: 1].
