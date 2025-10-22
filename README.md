
# IBM Watson Studio Community - Recommendation System

A comprehensive recommendation system built for the IBM Watson Studio platform, implementing multiple recommendation techniques including Rank-Based, User-User Collaborative Filtering, Content-Based Filtering, and Matrix Factorization (SVD).

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Methodology](#methodology)
- [Results](#results)
- [Technologies Used](#technologies-used)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This project analyzes user-article interactions on the IBM Watson Studio platform to build a sophisticated recommendation system. The system can recommend articles to users based on their reading history and preferences using multiple recommendation strategies.

### Key Objectives

- Analyze 45,993 user-article interactions across 5,149 users and 714 articles
- Implement multiple recommendation algorithms for different use cases
- Handle cold-start problems for new users
- Provide personalized recommendations based on user behavior and content similarity

## ✨ Features

### 1. **Exploratory Data Analysis (EDA)**
- Comprehensive statistical analysis of user-article interactions
- Visualization of interaction distributions
- Identification of popular articles and power users
- Missing data handling and preprocessing

### 2. **Rank-Based Recommendations**
- Recommend most popular articles globally
- Ideal for new users with no interaction history
- Simple but effective cold-start solution

### 3. **User-User Collaborative Filtering**
- Find similar users based on interaction patterns
- Recommend articles that similar users have engaged with
- Cosine similarity-based user matching
- Ranked recommendations by popularity

### 4. **Content-Based Recommendations**
- TF-IDF vectorization of article titles
- K-Means clustering (50 clusters) of similar articles
- LSA (Latent Semantic Analysis) for dimensionality reduction
- Recommend articles within the same content cluster

### 5. **Matrix Factorization (SVD)**
- Singular Value Decomposition for latent feature extraction
- Article similarity based on latent representations
- Optimized with 200 latent features
- High precision in article recommendations

## 📁 Project Structure

```
recommendation-system/
│
├── data/
│   └── user-item-interactions.csv          # Raw interaction data
│
├── Recommendations_with_IBM.ipynb          # Main Jupyter notebook
├── project_tests.py                        # Test suite for validation
│
├── top_5.p                                 # Cached top 5 articles
├── top_10.p                                # Cached top 10 articles
├── top_20.p                                # Cached top 20 articles
│
└── README.md                               # This file
```

## 🚀 Installation

### Prerequisites

- Python 3.8+
- Jupyter Notebook
- Git

### Step 1: Clone the Repository

```bash
git clone https://github.com/iimaha-AI/recommendation-system.git
cd ibm-recommendation-system/recommendation-system
```

### Step 2: Install Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

### Step 3: Launch Jupyter Notebook

```bash
jupyter notebook Recommendations_with_IBM.ipynb
```

## 💻 Usage

### Running the Complete Analysis

Open `Recommendations_with_IBM.ipynb` and run all cells sequentially. The notebook is organized into five main parts:

1. **Part I: Exploratory Data Analysis**
2. **Part II: Rank-Based Recommendations**
3. **Part III: User-User Collaborative Filtering**
4. **Part IV: Content-Based Recommendations**
5. **Part V: Matrix Factorization (SVD)**

### Example: Get Top 10 Recommendations for a User

```python
# For an existing user (User ID 20)
rec_ids, rec_names = user_user_recs_part2(20, 10)
print("Top 10 recommendations:")
print(rec_names)

# For a new user (no history)
new_user_recs = get_top_article_ids(10)
print("Top 10 popular articles:")
print(get_article_names(new_user_recs))
```

### Example: Content-Based Recommendations

```python
# Get 10 similar articles to article ID 25
rec_ids, rec_names = make_content_recs(25, 10)
print("Similar articles:")
print(rec_names)
```

### Example: SVD-Based Recommendations

```python
# Get 10 similar articles using SVD (article ID 4)
k = 200  # Number of latent features
vt_new = v[:k, :]
rec_articles = get_svd_similar_article_ids(4, vt_new)[:10]
print("SVD-based recommendations:")
print(get_article_names(rec_articles))
```

## 🔬 Methodology

### 1. Data Preprocessing

- Loaded 45,993 user-article interactions
- Handled 17 missing email values (assigned to "unknown_user")
- Mapped user emails to numeric IDs
- Created binary user-item matrix (5,149 × 714)

### 2. Rank-Based Approach

**Algorithm:**
- Count total interactions per article
- Sort articles by interaction count (descending)
- Return top N articles

**Use Case:** New users, cold-start problem

### 3. User-User Collaborative Filtering

**Algorithm:**
1. Compute cosine similarity between all users
2. Find K most similar users to target user
3. Collect articles interacted with by similar users
4. Filter out articles already seen by target user
5. Rank by popularity among similar users

**Improvements:**
- Sort similar users by similarity score and total interactions
- Rank recommended articles by unique user interactions

### 4. Content-Based Filtering

**Algorithm:**
1. Extract article titles as text features
2. Apply TF-IDF vectorization (max 200 features)
3. Perform LSA with 50 components (45% variance explained)
4. Apply K-Means clustering (50 clusters)
5. Recommend articles from the same cluster

**Parameters:**
- `max_df=0.75`, `min_df=5`
- Stop words removed
- Normalized vectors

### 5. Matrix Factorization (SVD)

**Algorithm:**
1. Decompose user-item matrix: `U × Σ × V^T`
2. Reduce to K latent features (K=200)
3. Compute cosine similarity in latent space
4. Recommend most similar articles

**Performance Metrics:**
- Accuracy, Precision, and Recall evaluated
- Optimal performance at 200 latent features

## 📊 Results

### Dataset Statistics

| Metric | Value |
|--------|-------|
| Total Interactions | 45,993 |
| Unique Users | 5,149 |
| Unique Articles | 714 |
| Median Interactions/User | 3 |
| Max Interactions (User) | 364 |
| Most Viewed Article ID | "1429" |
| Most Viewed Article Views | 937 |

### Model Performance

✅ **All Tests Passed Successfully**

- Part I (EDA): ✅ All metrics verified
- Part II (Rank-Based): ✅ Top articles correct
- Part III (Collaborative): ✅ Similar users identified
- Part IV (Content-Based): ✅ Clusters formed correctly
- Part V (SVD): ✅ Similar articles retrieved

### Key Findings

1. **User Behavior:**
   - Distribution highly skewed (50% of users interact with ≤3 articles)
   - Few power users with hundreds of interactions

2. **Article Popularity:**
   - Small number of articles drive most interactions
   - Long-tail distribution of article views

3. **Recommendation Quality:**
   - User-User filtering works best for active users
   - Content-based effective for article discovery
   - SVD captures latent patterns effectively

## 🛠️ Technologies Used

- **Python 3.11**: Core programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Matplotlib**: Data visualization
- **Scikit-learn**: Machine learning algorithms
  - `TfidfVectorizer`: Text vectorization
  - `KMeans`: Clustering
  - `TruncatedSVD`: Matrix factorization
  - `cosine_similarity`: Similarity computation
- **Jupyter Notebook**: Interactive development environment

## 📚 Documentation

Detailed documentation is available in the following files:

- **[COMPLETE_PROJECT_DOCUMENTATION.md](COMPLETE_PROJECT_DOCUMENTATION.md)**: Complete step-by-step technical documentation
- **[IMPLEMENTATION_DOCUMENTATION.md](IMPLEMENTATION_DOCUMENTATION.md)**: Implementation details in Arabic
- **[RESULTS_VERIFICATION.md](RESULTS_VERIFICATION.md)**: Test results and verification
- **[FIX_SUMMARY.md](FIX_SUMMARY.md)**: Bug fixes and troubleshooting

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is part of the Udacity Data Science Nanodegree program. Feel free to use and modify the code for educational purposes.

## 🙏 Acknowledgments

- **IBM Watson Studio** for providing the dataset
- **Udacity** for the project framework and guidance
- The Data Science community for inspiration and best practices

## 📧 Contact

For questions or feedback, please open an issue in the repository.

---

**Note:** This project was developed as part of the Udacity Data Science Nanodegree program's Recommendation Systems module.
