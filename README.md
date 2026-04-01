# 📊 Demographic Data Analyzer

A Python data analysis project that extracts demographic insights from 1994 US Census data using **pandas**.

> Part of the **freeCodeCamp – Data Analysis with Python** certification — Project 2.

---

## 📁 Project Files

| File | Purpose |
|------|---------|
| `demographic_data_analyzer.py` | Main script — all analysis logic |
| `adult.data.csv` | Dataset — 1994 US Census income data |
| `main.py` | Development runner and test file |
| `test_module.py` | Unit tests provided by freeCodeCamp |

---

## 📋 Dataset

Each row represents one person. Key columns used:

| Column | Description |
|--------|-------------|
| `age` | Age in years |
| `education` | Highest education level |
| `sex` | Male / Female |
| `race` | Race category |
| `hours-per-week` | Hours worked per week |
| `native-country` | Country of origin |
| `salary` | `<=50K` or `>50K` |

---

## ❓ Questions Answered

| Question | Method Used |
|----------|-------------|
| How many of each race are in the dataset? | `.value_counts()` |
| Average age of men? | Boolean filter + `.mean()` |
| % with Bachelor's degree? | `.sum()` / `len(df)` × 100 |
| % with higher education earning >50K? | `.isin()` filter + ratio |
| % without higher education earning >50K? | `~` (NOT) operator filter + ratio |
| Minimum hours worked per week? | `.min()` |
| % of minimum-hour workers earning >50K? | Filter + ratio |
| Country with highest % of rich people? | `.value_counts()` ratio per country |
| Top occupation for >50K earners in India? | Double filter + `.value_counts().idxmax()` |

---

## 💡 Code Explained Line by Line

### Race count
```python
race_count = pd.Series(df['race'].value_counts())
```
`.value_counts()` counts how many times each race appears and sorts by frequency.

---

### Average age of men
```python
average_age_men = df[df['sex'] == 'Male']['age'].mean()
```
`df[df['sex'] == 'Male']` filters rows where sex is Male, then `.mean()` averages their ages.

---

### Bachelor's degree percentage
```python
percentage_bachelors = (df['education'] == 'Bachelors').sum() / len(df) * 100
```
`(df['education'] == 'Bachelors')` returns True/False per row. `.sum()` counts the True values (Bachelors holders). Dividing by `len(df)` gives the proportion, ×100 makes it a percentage.

---

### Higher vs lower education earners
```python
higher_education = df[df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
lower_education  = df[~df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
```
`.isin([...])` returns True if value is in the list.
`~` is the NOT operator — flips True/False to get everyone else.

```python
higher_education_rich = len(higher_education[higher_education['salary'] == '>50K']) / len(higher_education) * 100
```
Filters the higher-educated group further to only those earning >50K, then calculates the ratio.

---

### Minimum hours workers
```python
num_min_workers = df[df['hours-per-week'] == min_work_hours]
rich_percentage = len(num_min_workers[num_min_workers['salary'] == '>50K']) / len(num_min_workers) * 100
```
First gets all people who work the minimum hours, then checks what % of them earn >50K.

---

### Country with highest % of rich people
```python
rich_per_country   = df[df['salary'] == '>50K']['native-country'].value_counts()
total_per_country  = df['native-country'].value_counts()
country_percentages = (rich_per_country / total_per_country) * 100
highest_earning_country = country_percentages.idxmax()
```
Dividing rich count per country by total count per country gives the percentage.
`.idxmax()` returns the index label (country name) of the highest value.

---

### Top occupation in India for >50K earners
```python
india_high_earners = df[(df['native-country'] == 'India') & (df['salary'] == '>50K')]
top_IN_occupation  = india_high_earners['occupation'].value_counts().idxmax()
```
`&` combines two conditions (must both be True).
`.idxmax()` returns the most frequent occupation name.

---

## 🧠 Key Concepts (Quick Revision)

| Concept | Explanation |
|---------|-------------|
| `df[condition]` | Filter rows where condition is True |
| `.isin([...])` | True if value matches any item in the list |
| `~` operator | Flips boolean — NOT filter |
| `&` operator | AND — both conditions must be True |
| `.value_counts()` | Counts frequency of each unique value |
| `.idxmax()` | Returns the label/index of the maximum value |
| `.mean()` | Average of a numeric column |
| `.min()` | Minimum value in a column |
| `len(df)` | Total number of rows in DataFrame |

---

## ▶️ How to Run

```bash
python main.py
```

---

## ✅ Tests

All unit tests pass (`test_module.py` provided by freeCodeCamp).

---

## 🏅 Certification

[freeCodeCamp – Data Analysis with Python](https://www.freecodecamp.org/learn/data-analysis-with-python/)
