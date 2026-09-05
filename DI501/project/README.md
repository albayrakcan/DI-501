# Music Popularity Prediction using Lyrical Features

## Project Overview
This project investigates whether the artist popularity significantly associated with track popularity and asks the question of how well audio features can predict track popularity.

## Project Structure

- `spotify_artists.csv`  
  Contains information about the artists.

- `spotify_tracks.csv`  
  Contains information about the tracks

- `e2161503_interim_notebook.ipynb` 
  Performs data preprocessing and cleaning, exploratory analysis, data visualization, naive baseline evaluation using performance metrics.

- `e216150_final.ipynb`  
  Continues from the interim notebook. Applies feature selection and generation, hypothesis testing, hyperparameter tuning, model comparison, significance testing, and interpretability analysis.

- `e216150_final_report.docx`  
  Final paper in IEEE conference format. Covers the full analysis from preprocessing through conclusions, including all results, tables, and figures.

## Workflow

1. **Data Loading and Inspection**
   - All datasets are loaded
   - Columns and observations are inspected.

2. **Preprocessing**
   - Column names are standardized.
   - Only relevant datasets are retained.
   - Missing Value and Unique Value Analysis is conducted.
   - Tracks with multiple artists were re-arranged to have only a single artist with the highest popularity.
   - Datasets are merged.

3. **Preliminary Analysis**
   - Descriptive statistics and distributions are examined.
   - A filtering threshold is determined to remove non-musical records.
   - Histograms and boxplots are generated.
   - Skewness and outliers are analyzed using IQR-based methods.

4. **Baseline Evaluation**
   - A naive baseline is defined using the global mean popularity.
   - Performance is evaluated using:
     - Mean Absolute Error (MAE)
     - Coefficient of Determination (R²)

5. **Feature Selection and Generation**
   - Spearman correlation is computed between each predictor and the target.
   - A Random Forest importance screen is applied to rank feature usefulness.
   - A Pearson correlation heatmap is produced to identify redundant predictor pairs.
   - Two new features are generated (log_duration, mood_index) and their added predictive value is evaluated; neither is retained as the improvement is negligible.
   - Scale-sensitive models use a StandardScaler fitted inside a pipeline; the tree-based model uses raw features.

6. **Hypothesis Testing**
   - RQ1: Is artist popularity significantly associated with track popularity?
   - H₀: population correlation = 0; H₁: correlation ≠ 0; α = 0.05.
   - Both Pearson (r = 0.683) and Spearman (ρ = 0.665) correlations are computed; H₀ is rejected (p < 0.001).

7. **Modelling and Hyperparameter Tuning**
   - Data split into training (60%), validation (20%), and test (20%) sets.
   - Models trained: Naive baseline, Linear Regression (OLS), Ridge (regularisation strength tuned over {0.01, …, 1000}), and Random Forest (n_estimators, max_depth, min_samples_split, min_samples_leaf tuned on the validation set).
   - Best Random Forest configuration: 120 trees, max_depth 16, min_samples_split 10, min_samples_leaf 10.

8. **Model Comparison**
   - All models evaluated on the held-out test set using MAE, RMSE, and R².
   - Results: Naive MAE 12.567 / R² 0.000; Linear MAE 8.912 / R² 0.477; Random Forest (tuned) MAE 8.491 / R² 0.520.
   - Paired Wilcoxon signed-rank tests confirm all improvements are statistically significant except Ridge vs. OLS (p = 0.53).

9. **Interpretability Analysis**
   - Impurity-based feature importance: artist_popularity accounts for ~75% of total importance; all audio features together account for ~25%.
   - Permutation importance on the test set: shuffling artist_popularity drops R² by ~0.94; shuffling any single audio feature changes R² by less than 0.04.

## Results Summary

- Artist popularity is strongly and significantly associated with track popularity (Pearson r = 0.68, p < 0.001).
- The tuned Random Forest predicts track popularity substantially better than the naive baseline (R² = 0.52 vs. 0.00, MAE = 8.49 vs. 12.57).
- Predictive power comes almost entirely from artist popularity; high-level audio features contribute little once artist popularity is included.

## Future Work

- Incorporate cleaned genre, release date, or playlist metadata.
- Engineer low-level or typicality-based audio features (e.g., optimal-differentiation measure).
- Test gradient-boosted or neural models.
- Examine how the artist-vs-audio importance balance varies across genres, markets, and time periods.
