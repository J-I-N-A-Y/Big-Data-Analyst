# Big-Data-Analyst
*COMPANY*: CODTECH IT SOLUTIONS

*NAME*:JINAY SHAH

*INTERN ID*:CT04DL198

*DOMAIN*:DATA ANALYTICS

*DURATION*:4 WEEKS

*MENTOR*:NEELA SANTHOSH

## DESCRIPTION

This Python script simulates a large user activity log dataset and analyzes it using Dask, a parallel computing library built to scale data processing tasks efficiently. The script comprises data generation, transformation into a Dask DataFrame, and multiple analytics operations to gain insights into user behavior and page interactions.

### **Data Simulation**

The script begins by importing necessary libraries: `pandas`, `dask.dataframe`, `numpy`, and datetime utilities. It sets a random seed for reproducibility and defines `n_rows = 1_000_000` to simulate one million rows of data. The dataset emulates logs of user activity on a website with 100 unique users (`user_1` to `user_100`) and six types of pages: `'home'`, `'products'`, `'cart'`, `'checkout'`, `'profile'`, and `'support'`.

Three main features are generated for each log entry:

* `user_id`: randomly selected from the list of users.
* `page`: randomly chosen from the list of page types.
* `duration_seconds`: modeled using an exponential distribution to simulate session duration, with an average of 60 seconds.
* `timestamp`: randomly generated as an offset from a fixed `start_time` (January 1, 2024), providing a realistic time component.

These data points are assembled into a Pandas DataFrame (`df`), which provides an in-memory tabular structure for easy data manipulation.

### **Conversion to Dask DataFrame**

The script then converts the Pandas DataFrame into a Dask DataFrame (`ddf`) using `dd.from_pandas(df, npartitions=10)`. This step splits the dataset into 10 partitions, enabling parallel processing and out-of-core computation. Dask is particularly useful when dealing with data that doesn't fit into memory or requires efficient distributed computation.

### **Analytical Operations**

Three main analytics operations are performed:

1. **Total Time Spent per Page**:
   The script groups the data by the `page` column and calculates the total session duration using `.sum()`. The results are sorted in descending order to identify which pages consumed the most user time.

2. **Average Session Duration per User**:
   It groups by `user_id` and calculates the mean session duration, providing insight into which users spend the most time per session on average. The results are sorted to highlight the most engaged users.

3. **Most Visited Pages**:
   It computes the frequency of visits per page using `.value_counts()`, showing which pages are most frequently accessed across the dataset.

All these computations are lazily evaluated and only executed when `.compute()` is called. This is a key feature of Dask, which builds a task graph and optimizes execution only when results are needed.

### **Output Storage**

Finally, the script saves the computed results to CSV files. It exports `total_time_per_page` and `avg_duration_per_user` to separate CSVs. This allows for easy sharing, visualization, or further downstream processing.

## OUTPUT

Total Time Spent per Page:

 page
support     1.001063e+07
profile     9.996564e+06
cart        9.993494e+06
products    9.991177e+06
checkout    9.980149e+06
home        9.965842e+06
Name: duration_seconds, dtype: float64

Average Session Duration per User:
user_id
user_31    61.079454
user_41    61.024913
user_29    60.967548
user_62    60.938977
user_9     60.821070
user_90    60.781809
user_80    60.706773
user_13    60.689942
user_19    60.642238
user_81    60.637110
Name: duration_seconds, dtype: float64

Most Visited Pages:
...
checkout    166527
products    167199
home        166241
Name: count, dtype: int64[pyarrow]
Output is truncated. View as a scrollable element or open in a text editor. Adjust cell output settings...
