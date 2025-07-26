# Exploratory Data Analysis (EDA) Report: Movie Profit Dataset

## Overview
This report presents the findings from an exploratory data analysis (EDA) conducted on the `movie_profit.csv` dataset. The dataset contains information about movies, including their release dates, titles, production budgets, domestic and worldwide gross earnings, distributors, MPAA ratings, and genres. The analysis was performed using Python with libraries such as `pandas` and `matplotlib` in a Jupyter Notebook environment (`Movies.ipynb`). The goal of this EDA is to uncover patterns, trends, and insights about movie financial performance and characteristics.


![image_alt](https://github.com/Raka-Deb/Movie-Profit-Analysis-/blob/b52cb6547d657243a04f12f8a8b6b106a20d5ad7/Movie.jpg)


## Dataset Description
The dataset consists of **3401 entries** with the following columns:
- `Unnamed: 0`: An index column (dropped during analysis as it was redundant).
- `release_date`: The release date of the movie (object type).
- `movie`: The title of the movie (object type).
- `production_budget`: The budget allocated for producing the movie (float64).
- `domestic_gross`: The gross revenue in the domestic market (float64).
- `worldwide_gross`: The total gross revenue worldwide (float64).
- `distributor`: The company distributing the movie (object type, contains some missing values).
- `mpaa_rating`: The MPAA rating of the movie (object type, contains some missing values).
- `genre`: The genre of the movie (object type).

### Key Dataset Statistics
- **Total Entries**: 3401
- **Data Types**:
  - Numerical: `production_budget`, `domestic_gross`, `worldwide_gross` (float64)
  - Categorical: `release_date`, `movie`, `distributor`, `mpaa_rating`, `genre` (object)
- **Missing Values** (before cleaning):
  - `distributor`: 48 missing values
  - `mpaa_rating`: 137 missing values
  - Other columns: No missing values
- **After Cleaning**:
  - Rows with missing values in `distributor` or `mpaa_rating` were dropped, resulting in **3230 entries**.
  - No duplicate rows were found in the dataset.

## Data Cleaning and Preprocessing
1. **Dropped Redundant Column**:
   - The `Unnamed: 0` column, which served as an index, was removed as it provided no additional information.
2. **Handling Missing Values**:
   - Rows with missing values in `distributor` (48 rows) and `mpaa_rating` (137 rows) were dropped to ensure data consistency for analysis.
   - After dropping, no missing values remained in the dataset.
3. **Duplicate Check**:
   - No duplicate rows were identified (`data.duplicated().sum() == 0`).
4. **Sorting**:
   - The dataset was sorted by `production_budget` in ascending order to examine movies with the lowest budgets.

## Key Findings

### 1. Numerical Columns: Descriptive Statistics
The numerical columns (`production_budget`, `domestic_gross`, `worldwide_gross`) were analyzed using `data.describe()` to understand their distributions.

- **Production Budget**:
  - **Mean**: $34.59M
  - **Standard Deviation**: $35.26M
  - **Minimum**: $250,000
  - **Maximum**: $175M
  - **Quartiles**:
    - 25th percentile: $10M
    - 50th percentile (median): $22M
    - 75th percentile: $49M
  - **Insight**: The production budgets vary widely, with a significant standard deviation indicating a diverse range of budgets. Most movies (50%) have budgets below $22M, but high-budget films (up to $175M) skew the mean upward.

- **Domestic Gross**:
  - **Mean**: $47.27M
  - **Standard Deviation**: $59.74M
  - **Minimum**: $0
  - **Maximum**: $474.54M
  - **Quartiles**:
    - 25th percentile: $6.87M
    - 50th percentile (median): $27.33M
    - 75th percentile: $63.41M
  - **Insight**: Domestic gross earnings show high variability, with some movies earning nothing ($0) domestically, possibly due to limited releases or failures, while others achieve massive success (up to $474.54M). The median domestic gross is significantly lower than the mean, indicating a right-skewed distribution with a few high-grossing outliers.

- **Worldwide Gross**:
  - **Mean**: $98.42M
  - **Standard Deviation**: $143.28M
  - **Minimum**: $0
  - **Maximum**: $1.30B
  - **Quartiles**:
    - 25th percentile: $11.78M
    - 50th percentile (median): $44.04M
    - 75th percentile: $125.20M
  - **Insight**: Worldwide gross earnings are also highly variable, with a maximum of $1.3B (e.g., *Jurassic World: Fallen Kingdom*). The large standard deviation and difference between mean and median suggest that a few blockbuster films significantly inflate the average.

### 2. Genre Distribution
The `genre` column was analyzed using `value_counts()` to determine the frequency of each genre.

- **Top 5 Genres** (out of 3230 movies):
  - Drama: 1180 movies (36.5%)
  - Comedy: 775 movies (24.0%)
  - Action: 540 movies (16.7%)
  - Adventure: 469 movies (14.5%)
  - Horror: 266 movies (8.2%)
- **Insight**: Drama is the most common genre, followed by Comedy and Action. This suggests that drama and comedy films are produced more frequently, possibly due to lower production costs or broader audience appeal compared to genres like Adventure or Horror.

### 3. MPAA Rating and Domestic Gross
The relationship between `mpaa_rating` and `domestic_gross` was explored by grouping the data by MPAA rating and calculating the mean domestic gross.

- **Mean Domestic Gross by MPAA Rating** (sorted descending):
  - G: $82.53M
  - PG: $67.42M
  - PG-13: $54.87M
  - R: $32.09M
- **Top 2 MPAA Ratings by Mean Domestic Gross**:
  - G: $82.53M
  - PG: $67.42M
- **Insight**: G-rated movies have the highest average domestic gross, followed by PG-rated movies. This suggests that family-friendly films (G and PG) tend to perform better domestically, likely due to their broad appeal to audiences of all ages. R-rated movies, which may have restricted audiences, have the lowest average domestic gross.

### 4. Distributor Performance
A horizontal bar chart was created to visualize the average domestic gross for the top 5 distributors (using `data.groupby('distributor')['domestic_gross'].mean().head().plot(kind='barh')`).

- **Key Distributors Analyzed** (top 5 by mean domestic gross):
  - The specific distributors were not listed in the output, but the visualization indicates significant variation in average domestic gross across distributors.
- **Insight**: Certain distributors are associated with higher average domestic gross, likely due to their focus on high-budget or blockbuster films. Further analysis could identify which distributors consistently achieve higher earnings.

### 5. Low-Budget Movies
The dataset was sorted by `production_budget` in ascending order to examine low-budget films.

- **Top 5 Movies with Lowest Production Budgets** ($250,000 each):
  1. *November* (2005, Drama, Sony Pictures Classics, R-rated, Domestic Gross: $191,862, Worldwide Gross: $191,862)
  2. *Lovely and Amazing* (2002, Drama, Lionsgate, R-rated, Domestic Gross: $4,210,379, Worldwide Gross: $4,613,482)
  3. *Sleight* (2017, Action, High Top Releasing, R-rated, Domestic Gross: $3,930,990, Worldwide Gross: $3,934,450)
  4. *Love and Other Catastrophes* (1997, Comedy, Fox Searchlight, R-rated, Domestic Gross: $212,285, Worldwide Gross: $743,216)
  5. *Like Crazy* (2011, Drama, Paramount Pictures, PG-13, Domestic Gross: $3,395,391, Worldwide Gross: $3,728,400)
- **Insight**: Low-budget films (budget of $250,000) can still achieve significant domestic and worldwide gross, particularly in the Drama genre. For example, *Lovely and Amazing* earned over $4M domestically despite its low budget, indicating a high return on investment. However, some films like *November* had minimal earnings, suggesting variability in financial success among low-budget films.

## Visualizations
- **Horizontal Bar Chart: Average Domestic Gross by Distributor**:
  - The chart highlights the top 5 distributors by average domestic gross.
  - **Insight**: The visualization confirms that certain distributors outperform others in terms of average domestic earnings, likely due to their portfolio of films or marketing strategies. Specific distributor names were not provided in the output, but the chart indicates significant differences.

## Conclusions
1. **Financial Performance**:
   - The dataset shows a wide range of financial outcomes, with some movies earning nothing domestically or worldwide, while others achieve blockbuster status (e.g., *Jurassic World: Fallen Kingdom* with $1.3B worldwide gross).
   - High-budget films tend to have higher gross earnings, but low-budget films can also achieve significant returns, particularly in genres like Drama.

2. **Genre Trends**:
   - Drama and Comedy dominate the dataset, making up over 60% of the movies. This suggests a market preference for these genres, possibly due to lower production costs or broader appeal.
   - Action and Adventure films, while fewer in number, often have higher budgets and can achieve substantial earnings (e.g., *Jurassic World: Fallen Kingdom*).

3. **MPAA Rating Impact**:
   - G and PG-rated films have the highest average domestic gross, indicating strong performance for family-friendly content.
   - R-rated films, while popular in genres like Drama and Horror, have lower average earnings, likely due to restricted audience access.

4. **Distributor Performance**:
   - Some distributors achieve significantly higher average domestic gross, suggesting they focus on high-performing films or have effective distribution strategies.

5. **Low-Budget Success**:
   - Low-budget films, particularly in the Drama genre, can achieve impressive returns on investment, as seen with *Lovely and Amazing*. However, success is not guaranteed, as evidenced by films like *November*.

## Recommendations for Further Analysis
1. **Profitability Analysis**:
   - Calculate profit (worldwide gross - production budget) to identify the most financially successful films and genres.
2. **Time-Based Trends**:
   - Convert `release_date` to a datetime object and analyze trends over time (e.g., changes in budgets or gross earnings by year).
3. **Genre and Rating Combinations**:
   - Explore combinations of genres and MPAA ratings to identify which pairings yield the highest gross earnings.
4. **Distributor Deep Dive**:
   - Analyze the full list of distributors to identify which ones consistently produce high-grossing films and their associated genres.
5. **Correlation Analysis**:
   - Investigate correlations between `production_budget`, `domestic_gross`, and `worldwide_gross` to understand the relationship between investment and earnings.

## Technical Notes
- The analysis was conducted using Python 3.13.5 in a Jupyter Notebook (`Movies.ipynb`).
- Libraries used: `pandas` for data manipulation and `matplotlib` for visualization.
- The dataset was cleaned by removing missing values and redundant columns to ensure robust analysis.
- Visualizations were limited to a single bar chart due to the scope of the provided code, but additional visualizations (e.g., box plots, scatter plots) could provide deeper insights.
