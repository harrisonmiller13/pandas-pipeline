# pandas-pipeline
pandas pipelining testing
Pandas is an amazing library in the Python ecosystem for data analytics and machine learning. They form the perfect bridge between the data world, where Excel/CSV files and SQL tables live, and the modeling world where Scikit-learn or TensorFlow perform their magic.
A data science flow is most often a sequence of steps — datasets must be cleaned, scaled, and validated before they can be ready to be used by that powerful machine learning algorithm.

Pandas also offer a .pipe method which can be used for similar purposes with user-defined functions. However, we are going to use a library called pdpipe, which specifically addresses this pipelining issue with Pandas DataFrame.

First to have a look at our data, we used pandas profiling to generate an EDA report
Pandas profiling generates profile reports from a pandas DataFrame. The pandas df.describe() function is great but a little basic for serious exploratory data analysis. pandas_profiling extends the pandas DataFrame with df.profile_report() for quick data analysis.
For each column the following statistics - if relevant for the column type - are presented in an interactive HTML report:

Essentials: type, unique values, missing values
Quantile statistics like minimum value, Q1, median, Q3, maximum, range, interquartile range
Descriptive statistics like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
Most frequent values
Histogram
Correlations highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices
Missing values matrix, count, heatmap and dendrogram of missing values

Next we begin to make the pipeline


At this point, we can look back and see what our pipeline does to the DataFrame right from the beginning,
-drops a specific column
-one-hot-encodes a categorical data column for modeling
-tags data based on a user-defined function
-drops rows based on the tag
-drops the temporary tagging column
All of this — using the following five lines of code,
pipeline = pdp.ColDrop('Avg. Area House Age')
pipeline+= pdp.OneHotEncode('House_size')
pipeline+=pdp.ApplyByCols('Price',price_tag,'Price_tag',drop=False)
pipeline+=pdp.ValDrop(['drop'],'Price_tag')
pipeline+= pdp.ColDrop('Price_tag')
df5 = pipeline(df)

NLTK was then used to tokenize the address field
After tokenizing the address field, we are able to extract the state and create a column for it using the pipeline

Using pandas pipline, one can easily and quickly put together a pipline for incoming new data with very few lines of code.
These tasks can, of course, be done with many single-step functions/methods that are offered by packages like Pandas but a more elegant way is to use a pipeline. In almost all cases, a pipeline reduces the chance of error and saves time by automating repetitive tasks.
