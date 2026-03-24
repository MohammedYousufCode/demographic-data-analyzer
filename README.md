# Demographic Data Analyzer

A Python-based data analysis tool using **Pandas** to explore and extract insights from the 1994 Census database. This project identifies relationships between education, work hours, and income levels across different demographics.

## 📋 Features

This script calculates the following demographic metrics:
*   **Race Distribution**: Counts of each race represented in the dataset.
*   **Average Age**: Specifically calculating the mean age for men.
*   **Education Analysis**: Percentage of the population with a Bachelor's degree.
*   **Income vs. Education**: Percentage of people with and without advanced education (`Bachelors`, `Masters`, or `Doctorate`) earning >50K.
*   **Work Hours**: Minimum work hours per week and the percentage of those workers earning >50K.
*   **Global Trends**: Identifies the country with the highest percentage of high earners.
*   **Regional Occupation**: The most popular job for high earners in India.

## 🛠️ Tech Stack

*   **Python 3.x**
*   **Pandas**: For data manipulation and analysis.

## 🚀 Usage

1.  **Prepare the Data**: Ensure `adult.data.csv` is in the root directory.
2.  **Run the Function**:
    ```python
    import pandas as pd
    from demographic_data_analyzer import calculate_demographic_data

    # Execute the analysis
    results = calculate_demographic_data()
    ```

## 📊 Methodology

The analysis utilizes several key Pandas operations:
*   **Boolean Indexing**: Filtering subsets of data (e.g., `df[df['salary'] == '>50K']`).
*   **Method Chaining**: Combining `.value_counts()` and `.idxmax()` to find top categories.
*   **Vectorized Math**: Calculating percentages across Series efficiently.
*   **Tilde Operator (`~`)**: Used for "NOT" logic when filtering for lower education.

## 📝 Example Output

```text
Number of each race:
 White                 27816
 Black                  3124
 ...
Average age of men: 39
Percentage with Bachelors degrees: 16.45%
Percentage with higher education that earn >50K: 46.54%
Highest percentage of rich people in country: 41.9%
Top occupations in India: Prof-specialty
