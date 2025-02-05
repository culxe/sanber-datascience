# Data Science Bootcamp Sanbercode

Final Project Report - [Home Purchase Recommendations](https://github.com/culxe/sanber-datascience/blob/main/final%20project/Laporan%20Final%20Project%20Data%20Science.pdf)
---

## House Purchase Recommendation

### Project Objectives

- Provide optimal house recommendations based on price, location, facilities, and other preferences.

- Identify factors influencing house prices.

- Analyze relationships between house attributes to understand trends and patterns.

## Data and Analysis

### Data Understanding

The dataset includes various house attributes such as price, living area (sqft_living), number of bedrooms and bathrooms, year built, and location.

Initial analysis was performed to understand data distribution and patterns.
![image](https://github.com/user-attachments/assets/56a5249b-24ff-42b9-9dca-0e569d49502d)


### Data Preparation

- There is no missing values and duplicate data.

- Handling outliers in key features such as price, sqft_living, bathrooms, and sqft_basement.

![image](https://github.com/user-attachments/assets/34a9dbab-8426-4fd5-be1a-9b1605cf21bf)

```python
df_cleaned = df[
    (df['price'] <= 7000000) &
    (df['price'] > 0) &
    (df['sqft_living'] <= 12000) &
    (df['sqft_above'] <= 9000) &
    (df['bathrooms'] <= 7) &
    (df['sqft_lot'] <= 800000) &
    (df['sqft_basement'] <= 4000)
]
```


### Exploratory Data Analysis (EDA)

Correlation between key features:

- Year built vs house condition → Older houses tend to be in worse condition.

- Living area (sqft_living) strongly correlates with house prices (correlation ≈ 0.9).

- Price per square foot (price_per_sqft) ratio is used to evaluate property pricing.

![image](https://github.com/user-attachments/assets/0d63199e-5324-42b5-b280-9a3a2f4ecd86)


### Model Implementation

- Selecting key features such as sqft_living, bedrooms, bathrooms, year_built, and year_renovated.

- Filtering houses based on year_built (minimum 1990) or renovations.

- Recommendations are made based on price_per_sqft calculations.

```
built_after_1990 = df_cleaned[df_cleaned['yr_built'] >= 1990]
renovated_after_2000 = df_cleaned[(df_cleaned['yr_built'] < 1990) & (df_cleaned['yr_renovated'] > 2000)]
filtered_houses = pd.concat([built_after_1990, renovated_after_2000])
filtered_houses['price_per_sqft'] = filtered_houses['price'] / filtered_houses['sqft_living']
recommended_houses = filtered_houses.sort_values(by=['price', 'price_per_sqft']).head(10)

```


### Results & Output

The model successfully identified houses with a more efficient price per square foot ratio.

Key visualizations:

- Price correlation with main house features.

- Distribution of price per square foot to determine reasonably priced houses.

![image](https://github.com/user-attachments/assets/f571bd40-3c29-4d35-8744-c5d8dc4d2463)



📁 Dataset & Code: Available in the notebook finalproject_report.ipynb.
