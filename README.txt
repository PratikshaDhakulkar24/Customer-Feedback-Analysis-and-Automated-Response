Customer Feedback Analysis and Automated Response

## Project Overview

This project analyzes customer reviews from the Women's E-Commerce Clothing Reviews dataset.

The main goals of the project are:

- Clean and prepare customer review data.
- Identify critical customer reviews using a simple rule-based approach.
- Find common complaint keywords.
- Select the 3 most detailed critical reviews.
- Generate personalized apology emails using Gemini Generative AI.

---

## Tools and Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Requests
- Google Gemini API
- Jupyter Notebook

---

## Dataset

The project uses the:

**Women's E-Commerce Clothing Reviews Dataset**

The main columns used in this project are:

- `Title`
- `Review Text`
- `Rating`
- `Recommended IND`

Only these columns are selected for the analysis.

---

## 1. Data Cleaning Approach

The following steps were used to clean the data.

### Select Required Columns

Only the required columns were kept:

```python
df = df[["Title", "Review Text", "Rating", "Recommended IND"]].copy()
```

### Handle Missing Values

Missing values in `Title` and `Review Text` were replaced with empty strings.

Reviews with an empty `Review Text` were removed because review text is required for the analysis.

```python
df["Title"] = df["Title"].fillna("")
df["Review Text"] = df["Review Text"].fillna("")

df = df[df["Review Text"] != ""].copy()
```

### Clean Review Text

The review text was cleaned by:

- Converting text to lowercase.
- Replacing punctuation with spaces.
- Removing extra spaces.
- Removing leading and trailing spaces.

This makes keyword searching easier and more consistent.

---

## 2. Rule-Based Logic

No machine learning model was used to identify critical reviews.

A simple rule-based approach was used.

### Identifying Critical Reviews

Reviews with a rating of **1 or 2 stars** were considered critical reviews.

```python
critical_reviews = df[df["Rating"].isin([1, 2])].copy()
```

This rule helps focus the analysis on customers who gave low ratings.

### Complaint Keywords

A predefined list of complaint-related keywords was used to identify common customer complaints.

The cleaned review text was searched for these keywords, and their occurrences in critical reviews were counted.

---

## 3. Selecting the Most Critical Reviews

After identifying the 1-star and 2-star reviews, the review length was calculated.

The 3 longest critical reviews were selected for the Generative AI response step.

```python
critical_reviews["Review Length"] = critical_reviews["Clean Review"].str.len()

top_3_reviews = critical_reviews.sort_values(
    "Review Length",
    ascending=False
).head(3).copy()
```

These reviews were selected because they contain more detailed customer feedback that can provide more information for generating personalized responses.

---

## 4. Generative AI Response

Gemini Generative AI is used to create personalized apology emails for the selected reviews.

The review text and rating are provided to the Gemini API.

The prompt asks the AI to:

- Start with a suitable subject line.
- Apologize for the customer's experience.
- Mention the main complaint.
- Show empathy.
- Keep the response professional and simple.
- Avoid inventing refunds or replacements.
- End with a polite customer-support closing.

The project uses the Gemini model:

```text
gemini-3.5-flash-lite
```

---

## 5. How to Run the Project

### Step 1: Install Required Libraries

Open Jupyter Notebook and install `requests` if it is not already installed:

```python
!pip install requests
```

The other libraries used in the project are:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Step 2: Keep the Dataset in the Same Folder

Place the following file in the same folder as the Jupyter Notebook:

```text
Womens Clothing E-Commerce Reviews.csv
```

The notebook loads the dataset using:

```python
file_name = "Womens Clothing E-Commerce Reviews.csv"
df = pd.read_csv(file_name)
```

### Step 3: Run the Notebook

Run the notebook cells from top to bottom.

The notebook will:

1. Load the dataset.
2. Understand the data.
3. Select required columns.
4. Handle missing values.
5. Clean review text.
6. Identify critical reviews.
7. Analyze rating distribution.
8. Find complaint keywords.
9. Select the 3 most detailed critical reviews.
10. Generate AI-based apology emails.

---

## 6. Gemini API Key Setup

A Gemini API key is required for the Generative AI section.

### Get the API Key

Create an API key from Google AI Studio:

https://aistudio.google.com/app/apikey

### Enter the API Key

The notebook asks for the API key using:

```python
from getpass import getpass

api_key = getpass("Enter your Gemini API key: ")
```

The key is entered directly in the Jupyter Notebook and is not written in the source code.

**Do not share the API key publicly or upload it to GitHub.**

After entering the key, the notebook uses it to send requests to the Gemini API.

---

## 7. Project Output

The project produces:

- Customer rating distribution.
- Number of critical reviews.
- Common complaint keywords.
- Complaint keyword visualization.
- The 3 selected critical reviews.
- 3 AI-generated personalized apology emails.

---

## 8. Final Insights

The analysis helped identify critical customer reviews using low ratings, especially 1-star and 2-star reviews.

Common complaint keywords were identified to understand the main issues mentioned by customers.

The most detailed critical reviews were selected for further analysis.

Gemini AI was then used to generate personalized apology emails based on the customer's review and rating.

Overall, the project demonstrates how Python and Generative AI can be used together to analyze customer feedback and automate customer-support responses.

---

## Conclusion

This project shows how customer reviews can be analyzed using Python to identify critical feedback and common complaints. Generative AI can then be used to create personalized responses, helping make the customer feedback analysis and response process more efficient.

