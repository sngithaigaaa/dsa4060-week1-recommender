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

## How to Run

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/YOUR-USERNAME/dsa4060-week1-recommender.git](https://github.com/YOUR-USERNAME/dsa4060-week1-recommender.git)
   cd dsa4060-week1-recommender
