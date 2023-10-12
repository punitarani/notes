# Data Mining

KDD: Knowledge Discovery in Databases

- **Nominal**: Categorical, no order (ex: red, green, blue)
- **Ordinal**: Categorical, with order (ex: low, medium, high)
- **Interval**: Numerical, with order, no natural zero (ex: temperature)
- **Ratio**: Numerical, with order, with natural zero (ex: height)

## Preprocessing

- Quality
  - **Noise**: random errors or variance in a measured variable
  - **Outliers**: extreme values that deviate from the rest of the data
  - **Missing Values**: empty values in a dataset
  - **Duplicate Data**: identical records in a dataset
- Preprocessing
  - **Aggregation**: combining multiple features into one
  - **Discretization**: converting continuous features into categorical features
  - **Feature Selection**: selecting a subset of features
  - **Feature Extraction**: deriving new features from existing features
  - **Sampling**: selecting a subset of data 

### Vector Space Model

- **Document**: a collection of words
- Convert documents into vectors
- $d_i = (w_{i1}, w_{i2}, ..., w_{in})$ where $w_{ij}$ is the weight of word $j$ in document $i$

### Term Frequency-Inverse Document Frequency (TF-IDF)

- $w_{ij} = tf_{ij} \times idf_j$
  - $tf_{ij}$ is the frequency of word $j$ in document $i$
  - $idf_j = \log \frac{N}{df_j}$ where $N$ is the number of documents and $df_j$ is the number of documents containing word $j$

## Supervised Learning


### Classification


### K-Nearest Neighbors (KNN)


### Decision Trees

- **Entropy**: measure of impurity in a set of examples
  - $\text{entropy}(T) = -p_+ \log p_+ - p_- \log p_-$
    - $p_+$ and $p_-$ are the probabilities of positive and negative examples
  - $H(X) = -\sum_{i=1}^{n} p_i \log p_i$
  - $p_i$ is the probability of class $i$
  - $H(X) = 0$ if all examples are of the same class
  - $H(X) = 1$ if all examples are equally distributed among classes
- **Information Gain** (IG): measure of the difference in entropy before and after splitting a set of examples on an attribute
  - $IG(A, S) = H(S) - \sum_{v \in values(A)} \frac{|S_v|}{|S|} H(S_v)$
  - $IG = 0$ if the attribute does not split the examples, $IG = 1$ if the attribute perfectly splits the examples

### Naive Bayes Classifier

- **Bayes' Theorem**: $P(A|B) = \frac{P(B|A)P(A)}{P(B)}$
  - What is the probability of A given B if we know the probability of B given A and the probability of A and B?

#### Weighted Vote Relation Neighbor (wvRN)

$P(y_i = 1 | N(v_i)) = \frac{1}{|N{v_i}} \sum_{v_j \in N(v_i)} P(y_j = 1)$

The probability of a node being a positive example is the average of the probabilities of its neighbors being positive examples.

### Regression

$W = (X^T X)^{-1} X^T Y$

## Unsupervised Learning

### Similarity Measures

- **Euclidean Distance**: $\sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}$
  - Distance between two points in Euclidean space (n-dimensional space)
- **Cosine Similarity**: $\frac{X \cdot Y}{||X|| \times ||Y||}$
  - Similarity between two vectors
  - $X \cdot Y = \sum_{i=1}^{n} x_i y_i$
  - $||X|| = \sqrt{\sum_{i=1}^{n} x_i^2}$
- **Mahalanobis Distance**: $\sqrt{(X - Y)^T S^{-1} (X - Y)}$
  - $S$ is the covariance matrix
  - $S_{ij} = \frac{1}{n} \sum_{k=1}^{n} (x_{ki} - \bar{x_i})(x_{kj} - \bar{x_j})$
  - $\bar{x_i}$ is the mean of $x_i$
  - $S^{-1}$ is the inverse of $S$
- **Manhattan Distance**: $\sum_{i=1}^{n} |x_i - y_i|$
  - Distance between two points in Manhattan space (n-dimensional space)
- **$L_p Norm$**: $\sqrt[p]{\sum_{i=1}^{n} |x_i - y_i|^p}$
  - Generalization of Euclidean distance and Manhattan distance
  - $L_1$ is Manhattan distance
  - $L_2$ is Euclidean distance

### K-Means

- **K-Means Clustering**: partitioning a set of $n$ objects into $k$ clusters
  - **Cluster**: a collection of objects that are similar to each other and dissimilar to objects in other clusters
  - **Centroid**: the center of a cluster
  - **Cluster Assignment**: assigning each object to a cluster
  - **Cluster Update**: updating the centroid of each cluster

$J = \sum_{i=1}^{k} \sum_{x \in C_i} ||x - \mu_i||^2$

#### Cohesiveness

- How close the objects in a cluster are to each other and the centroid (small std dev)
- $\text{cohesiveness}(C_i) = \sum_{i=1}^{k} \sum_{j=1}^{n(i)} \text{dist}(x_j^i, c_i)^2$

#### Seperateness

- How far the objects in a cluster are from objects in other clusters (large distance between centroids)
- $\text{seperateness}(C_i, C_j) = \text{dist}(c_i, c_j)^2$

#### Silhouette Index

- How similar an object is to its own cluster compared to other clusters
- $s(x) = \frac{b(x) - a(x)}{\max\{a(x), b(x)\}}$
  - $a(x)$ is the average distance between $x$ and all other objects in the same cluster
  - $b(x)$ is the average distance between $x$ and all other objects in the nearest cluster


## Evaluation

- **Accuracy**: $\frac{\text{number of correct predictions}}{\text{number of predictions}}$
  - How many predictions are correct?
- **Precision**: $\frac{\text{number of true positives}}{\text{number of predicted positives}}$
  - How many of the predicted positives are actually positive?
- **Recall**: $\frac{\text{number of true positives}}{\text{number of actual positives}}$
  - How many of the actual positives are predicted as positive?
- **F1 Score**: $2 \times \frac{\text{precision} \times \text{recall}}{\text{precision} + \text{recall}}$
  - Harmonic mean of precision and recall
