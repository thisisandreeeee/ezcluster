# ezcluster
Ezcluster implements simple ways of finding the optimal number of clusters for various unsupervised learning methods, such as [K-Means](http://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html). Determining the best number of clusters is a tricky task, which ezcluster aims to simplify through use of criterions such as the gap statistic, as proposed in the paper from [Data Science Lab](https://datasciencelab.wordpress.com/2013/12/27/finding-the-k-in-k-means-clustering/).

Install ezcluster from pypi:
```
pip install ezcluster
```

## Plots
![alt text](https://github.com/thisisandreeeee/ezcluster/blob/master/gaps_with_error.png "Optimal K")

The optimal number of K can be found in the above plot where the y-axis first becomes positive, as indicated in the above paper.

## Example
```python
import pandas as pd
import ezcluster

# load the iris dataset
import pandas as pd
import ezcluster

iris = pd.read_csv('https://raw.githubusercontent.com/thisisandreeeee/ezcluster/master/iris.csv')
species = iris['species']
iris.drop('species', axis = 1, inplace = True)

# initialize the kmeans class with a pandas dataframe, and indicate the categorical or id columns
ezc = ezcluster.Kmeans(iris, categorical_cols = None, id_col = None)

# find the optimal number of clusters by indicating the range of K to try
num_of_clusters = ezc.optimal_k(min_k=1, max_k=10, num_iters=100)

# plot the gap statistic plots
ezc.plot()

# return a model with optimal number of clusters
model = ezc.fit(n_clusters = num_of_clusters)

# save instance
ezc.save_model()

# save labeled dataset to csv
ezc.write_csv()
```
