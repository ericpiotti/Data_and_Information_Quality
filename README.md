# Data Quality & Cleaning Pipeline 

This repository contains the complete Data Quality and Cleaning pipeline applied to the official registry of public establishments (bars, restaurants, cafes) in the Municipality of Milan.

This project was developed for the Data and Information Quality (DIQ) course, focusing on transforming "dirty" administrative data into a high-quality dataset ready for reliable statistical analysis.

👥 Authors

Eric Piotti

Davide Rodler

Academic Year: 2025-2026

## 🛠️ Tech Stack & Libraries

The pipeline was implemented in Python using a specialized stack for data manipulation, profiling, and machine learning:

Pandas & NumPy: For core data manipulation, cleaning, and normalization.

Scikit-Learn: Specifically used for the KNNImputer to handle missing numerical values.

ydata-profiling (formerly Pandas Profiling): For generating comprehensive automated reports during the initial assessment and final validation phases.

Regex (re): For pattern matching and string extraction (e.g., house numbers).

Levenshtein / FuzzyWuzzy: For calculating string similarity during the deduplication phase.

## 📝 Project Overview
The objective was to address inherent noise and missingness in real-world open data, targeting two primary dimensions: Completeness and Consistency.

The Dataset

Source: Milan Open Data Portal

Initial Status: 6,904 records with significant encoding errors, ~49% missing values in business names, and inconsistencies between street addresses and administrative zones.

## 🔍 Pipeline Implementation
1. Profiling & Assessment

Used ydata-profiling to identify corrupted headers (encoding issues like þÿ) and map the distribution of missing values across the dataset.

## 2. Normalization & Standardization

Text Cleaning: Converted all strings to lowercase and removed leading/trailing whitespaces.

Encoding Fixes: Repaired character corruption across categorical columns.

Category Wrangling: Grouped complex business descriptions into macro-categories (e.g., "Bar", "Restaurant") for better analysis.

## 3. Error Detection & Correction

Logical Imputation: Extracted missing house numbers directly from street name strings using Regex.

KNN Imputation: Leveraged scikit-learn to estimate missing "Surface Area" values. The model identified the most similar establishments based on their geographic location and business type to fill the gaps.

Functional Dependencies: Verified that Zip Codes and Street Numbers correctly corresponded to the assigned administrative Zones.

## 4. Data Deduplication

To identify non-exact duplicates (e.g., "Pizzeria Da Mario" vs. "Pizz. Da Mario"):

Sorted Neighborhood Method (SNM): Used to optimize the comparison process by looking only at records within a specific "window."

Similarity Scoring: Applied string distance algorithms to flag potential duplicates.

Fusion: Merged records by prioritizing the one with the highest completeness score.
