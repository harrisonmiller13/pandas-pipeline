# pandas-pipeline
pandas pipelining testing
Pandas is an amazing library in the Python ecosystem for data analytics and machine learning. They form the perfect bridge between the data world, where Excel/CSV files and SQL tables live, and the modeling world where Scikit-learn or TensorFlow perform their magic.
A data science flow is most often a sequence of steps — datasets must be cleaned, scaled, and validated before they can be ready to be used by that powerful machine learning algorithm.
These tasks can, of course, be done with many single-step functions/methods that are offered by packages like Pandas but a more elegant way is to use a pipeline. In almost all cases, a pipeline reduces the chance of error and saves time by automating repetitive tasks.
Pandas also offer a .pipe method which can be used for similar purposes with user-defined functions. However, in this article, we are going to discuss a wonderful little library called pdpipe, which specifically addresses this pipelining issue with Pandas DataFrame.


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