# Course Recommender System - Viva / Q&A Preparation

## Project Explanation

This project builds a recommender system for online courses. The goal is to suggest courses that a learner has not taken yet but is likely to find useful. The project starts with exploratory data analysis, then builds content-based recommenders, and finally compares collaborative-filtering models.

## Dataset

The notebooks use the IBM Skills Network course recommender datasets stored in the local `datasets` folder:

- `ratings.csv`: user-course interaction records with ratings 2.0 or 3.0.
- `course_genre.csv`: course IDs, titles, and 14 genre indicators.
- `user_profile.csv`: user preference vectors over the 14 genres.
- `rs_content_test.csv`: test interactions for recommendation evaluation.
- `course_processed.csv`: cleaned course title and description text.
- `courses_bows.csv`: bag-of-words course features.
- `sim.csv`: precomputed course-course similarity matrix.

## Short Answer: What Did You Build?

I built and compared multiple course recommender systems. First, I explored the course and enrollment data. Then I implemented content-based recommenders using genre profiles, course similarity, and user clustering. Finally, I implemented collaborative-filtering models using KNN, NMF, and neural-network embeddings. The final recommendation is to use a hybrid system: content-based methods for cold-start users and neural collaborative filtering for users with enough history.

## Key Results to Remember

| Area | Result |
|---|---|
| EDA | Top 20 courses account for about 63.3% of enrollments |
| User profile + genres | Score threshold 10.0; broadest recommendation coverage |
| Course similarity | Similarity threshold 0.6; conservative, high-precision recommendations |
| Clustering | PCA keeps more than 90% variance, then KMeans groups similar users |
| KNN | Presentation RMSE: 0.2063 |
| NMF | Presentation RMSE: 0.2048 |
| Neural network | Presentation RMSE: 0.1534, best model |

## Likely Viva Questions

### 1. Why did you start with EDA?

EDA helps understand what courses exist, which genres dominate, how users interact with courses, and whether the data is sparse. This guides the choice of recommender algorithms.

### 2. What is the difference between content-based filtering and collaborative filtering?

Content-based filtering recommends items similar to a user's known interests, using course genres or text. Collaborative filtering recommends based on patterns in user-course interactions, even if course content is not directly analyzed.

### 3. Why use course genres?

Genres are interpretable features. They allow us to represent both users and courses in the same feature space, so we can calculate how well a course matches a user's interests.

### 4. What does the dot product mean in the user-profile recommender?

The dot product measures alignment between a user's genre interests and a course's genre labels. A higher score means the course matches the user's profile more strongly.

### 5. Why use cosine similarity for course similarity?

Cosine similarity measures how close two course text vectors are in direction, which is useful for comparing text-based features regardless of document length.

### 6. Why use PCA before clustering?

PCA reduces dimensionality while preserving most of the information. This can make clustering faster and reduce noise in the feature space.

### 7. Why use KMeans?

KMeans groups users with similar genre-interest profiles. Once users are grouped, we can recommend popular courses from the same cluster.

### 8. What is RMSE?

RMSE stands for Root Mean Squared Error. It measures how far predicted ratings are from actual ratings. Lower RMSE means better prediction accuracy.

### 9. Why did the neural-network model perform best?

The neural model learns dense embeddings for users and courses. These embeddings capture hidden preference patterns and non-linear relationships better than simpler neighborhood or matrix-factorization methods.

### 10. Which model would you deploy?

I would deploy a hybrid recommender. For new users or users with little history, I would use content-based recommendations. For users with enough rating history, I would use the neural-network collaborative-filtering model because it has the best RMSE in the comparison.

### 11. What are the limitations?

The data is sparse, the ratings are limited to two values, and offline RMSE does not fully measure real user satisfaction. A production system should also use ranking metrics and live feedback.

### 12. What future improvements would you suggest?

I would tune hyperparameters more systematically, use Precision@K and Recall@K, add course difficulty or skill-level metadata, and test recommendations with real users.
