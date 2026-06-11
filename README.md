# dask-lsh-recommender

A university data mining project for **DATA301** exploring whether **Locality Sensitive Hashing (LSH)** can be used to speed up item-based collaborative filtering for movie and TV recommendations.

This project compares an **LSH-accelerated collaborative filtering pipeline** against a **brute-force collaborative filtering baseline** using the Amazon Movies and TV Reviews dataset. The main focus of the project was to evaluate the trade-off between recommendation accuracy and computational runtime.

## Project Context

This repository contains the code, project proposal, progress update and final report for a university project completed for **DATA301**.

The research question was:

> What is the difference in movie and TV recommendation accuracy and computational runtime between Locality Sensitive Hashing accelerated collaborative filtering and brute-force collaborative filtering when applied to the Amazon Movies and Television Reviews dataset?

The project was implemented as a single Jupyter notebook and accompanied by a written report.

## Overview

Recommender systems often rely on comparing items to find similar movies or products. However, brute-force pairwise similarity comparison becomes expensive as the number of items grows.

This project uses **MinHash** and **Locality Sensitive Hashing** to reduce the number of item comparisons needed before applying collaborative filtering. Instead of comparing every item against every other item, LSH identifies candidate similar item pairs first, making the recommendation pipeline much faster.

## Dataset

The project uses the **Amazon Movies and TV Reviews 5-core dataset** from the UC San Diego McAuley Lab dataset collection.

Each record includes:

- User ID
- Item ID
- Rating from 1 to 5

The dataset is not included in this repository due to its size and licensing. The notebook assumes the dataset is downloaded separately.

## Methods

The pipeline follows these main stages:

1. Load and preprocess the Amazon Movies and TV review data using Dask
2. Split the data into training and test sets
3. Build item-to-user sets from positive ratings
4. Generate MinHash signatures for each item
5. Apply LSH banding to identify candidate similar item pairs
6. Compute cosine similarity for candidate pairs
7. Generate top-10 item recommendations using item-based collaborative filtering
8. Evaluate recommendation accuracy and runtime
9. Compare LSH-accelerated collaborative filtering with a brute-force baseline

## Technologies Used

- Python
- Dask
- NumPy
- Pandas
- Matplotlib
- Google Cloud Dataproc

## Key Results

The LSH-based approach significantly reduced computational runtime compared with brute-force collaborative filtering.

Key findings included:

- LSH reduced the number of item-pair comparisons substantially.
- The fastest LSH configuration completed the full pipeline in seconds rather than hours.
- The LSH approach preserved recommendation quality while greatly improving runtime.
- Absolute Precision@10 values were low, largely due to dataset sparsity and the long-tail distribution of ratings.
- Weak scalability testing showed that the LSH banding step became a bottleneck, limiting parallel efficiency.

Overall, the project showed that LSH can make collaborative filtering much more scalable, especially for large and sparse recommendation datasets.

## Repository Structure

```text
dask-lsh-recommender/
│
├── README.md
├── data301-project-samladbrook.ipynb
├── DATA301 Project Submission - Sam Ladbrook.pdf
├── DATA301 Project Progress Report - Sam Ladbrook.pdf
├── DATA301 Project Project Proposal - Sam Ladbrook.pdf
├── requirements.txt
└── .gitignore
```

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/dask-lsh-recommender.git
cd dask-lsh-recommender
```

2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

3. Download the Amazon Movies and TV Reviews 5-core dataset separately.

4. Open the notebook:

```bash
jupyter notebook data301-project-samladbrook.ipynb
```

## Notes

This project was completed as part of a university course and is intended to demonstrate data mining, scalable processing, and recommendation system concepts. It is not intended to be a production-ready recommender system.

The original dataset is not included in this repository.
