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

## Future Work

- Apply correlation analysis between artist and track popularity.
- Evaluate the track features in predicting song popularity.