
---
10/19/26

Ideally, we want to tain models of disease states based on samples from donors in a training or *discovery cohort* and evaluate the model on a completelu independent validation (v) cohort. A model that does well on a ___ ...

A trained model can be used to evaluate how cell-type specific contributions to a donor's phenotype. 
This example is related to aging and therefore highlights cell-types that are likely to have a pro-aging effect.


Data matrix ($X$) is an array comprised of $N$ data instances x $d$ features measured about these data instances. We often say this matrix, $X e R^Nxd$.

1. Scientific Question & ___
2. Data Preparation & Exploration
3. Modeling
4. Validation
5. Communication

Parameters: This is the collection of learnable values that help to translate the *input features* to the target variable.
- Example: regression coefficients (B), which provide a weight for each input feature. When you fit a regression model, you are trying to learn an appropariate ___ ...

Hyperparameters: additional parameters 

Training

Prediction

### Types of learning

Supervised: Leverage labels of data instances to learn parameters. We are training by showing several instances of a predicted data input and what the output label is.
- disgn

Unsupervised: Looking for patterns across data instances based on features. Usually involves clustering or ___ ....
- ...

==🟡ex)== Unsupervised learning
**Dimensionality reduction** refers to the fact that cells here, which were originally in a ~20K dimensional space are represented in two-dimensions.
**Clustering** refers to the computationally-determined ___ ...
==🟡ex)== Supervised learning: **Regression** 
Models of age were trained with supervision (e.g. ) ___ ...

**Feature engineering**: We define or measure features about each data instance that we suspect are important for differentiating classes in the data
- Canonical example: omics features measured for each data instance.
- Summaries of the data: for example, counts across cell-types.
**Feature learning**: Learning representations of the data.
- Here, features represent mathematically abstract dimensions that were trained to be helpful for some task, such as, classification.

The simplest way to label data: $k$-nearest neighbors classification
If we have an unlabeled point, $x$, ___ ...

Advantages and disadvantages of this simple approach
- If the data are well separated, then a kNN classifier ___ ...

Mapping data input to label
- Classifiers and regression models specify a set of rules of take input data and map it to a label
- Consider a simple linear classifier, $f$ as, $f(x, W) = Wx + b$
	- $x$ is the data instance
	- $w$ is the weights on the map ___

**Overfitting** is when a complex models with many parameters effectively memorizes the data.
Usually happens if we train and test the mdoel on the same data, as the model would effectively memorize the data, but not generalize.

In an ideal setting with enough data points, we would like to divide the data into three disjoint components:
- **Training**: A set of data points that will be used to learn model parameters
- **Validation**: A subset of the training set that can be used to select hyperparameters
- Testing: A never before seen ___ ...

Different train/test splits can cause variability in the trained models and lead to varying test-set accuracies. Hence, good to *bootstrap* and compute a mean or median across train/test splits or cross validation folds.

Cross validation - common for ___ ...

Leave-one-out cross validation (LOOCV)
aka. N-folds cross validation
- Realistically in biology, we often have super small datasets (<30 data points)
- We can make as many folds as there are datapoints. So, for $N$ datapoints, we would essentially be doing $N$ fold cross validation.
- For data point, $i$, train the model with all $n$ datapoints, *except $i$*. Test the model on datapoint $i$.

**Loss function**: A quantity that we defines, which reflects how well the current model explains the labels (either discrete or continuous) on our training data.
- The loss function implements 'book-keeping' for quantifying how much that predictions of training impages violate their true labels.

Loss function notation
- Consider your dataset of data points and labels ${(xi, yi)}N i=1$
	- $xi$ is the ___
- ...

==🟡ex)== Since this is classification, ...

**Hinge loss**
- Consider our example of the 3 images
we can define this piecewise loss...

Finding the best model parameters via the loss function
- Let $E(w)$ be the error function evaluated for a particular set of parameters, $w$,
- Ideally, we want to walk in a productive direction so that $upsidedowndelta E(w) = 0$. So, we ___ ...

Overall Workflow for Data-Driven Discovery via Unsupervised Learning


---
10/21/26

---
10/26/26

Discriminative Model
- 
Generative Model
- joint distribution between our class labels and ___ data

Loss function
- we can use it to optimize the parameters of our model (via gradient descent)
- a way to tabulate, under a current set of parameters, how wrong are our predictions.
- will use this information to adjust our parameters and ensure more data instances are predicted accurately.

Need to calculate the probability that $y^i$ = 1 and 0.

z = interproduct between out weight product (w) and ($x^i$).

$\hat{y^i}$

Stoachastic gradient descent
- sampling random data points from the training set to update model parameters.
- alternative to using the entire dataset, when having large datasets

We often enforce regularization on ___

Might have 50 samples with 20,000 things we're measuring from them...far too many features.
So many features measured about your training data enables more memorization of the training set and thus higher likelihood of overfitting. That kind of model would not generalize well to new data instances.

There are approaches that penalize you for adding coefficients ___...
- The simplest way to avoid this is to minimize the amount of features. A common solution is to regularize the loss function with a penalty term, which forces many coefficients to be 0.
- Lasso looks at the correlation structure among the features (if i know feature 1, i can easily predict feature 4 or 5)
- The way that the penalty if 
- Lasso if you want smallest number of features
	- very harsh and sparse
	- there are multiple variants (e.g., group lasso, ___ lasso)
- Ridge if you want larger number of features
- Elastic net if you want somewhere in the middle number of features


### Overview of a generative classifier: naive bayes

Let's say our
- x's are actually just discrete values
- input features are binary, so they're either zero or one

So first, we would like to model the joint probability of all of our observed data instances, so $x_1$ through $x_n$, given our label $y$. 
- Another nice property of this is something called conditional independence. So this says that we can measure the joint probability of all these variables conditioned on a class label as just the product of the probability of every observed feature conditioned on our class label y.
So basically, this is called like a factorization, and it's a very nice property. Again, that people doing like theoretical work have come up with that you can approximate this joint distribution by just doing like a factorized approach.

Feature selection
- can help prune down

Important to determine what are the features that affect the outcome...

Data Leakage
- a little bit of test data that was accidentally seen in model training, which may inflate the numbers slightly.

---

10/28/2026

Clustering Algorithms (k-means, hierarchical clustering, and spectral clustering)


k-means repeats two steps until it settles
Step 1: Pick k starting centers. 
Step 2: Assign every point to its nearest center.
Step 3: Move each center to the mean of its points.
Step 4: Repeat 2 and 3 until no point changes cluster.
The goal: k centers with the smallest total squared distance from each point to its center.

What k-means assumes
1. Users choose k. The algorithm returns exactly k clusters, whether or not the data has k groups.
2. Group are round/spherical. Every point joins its nearest center, so the boundaries between clusters are straight lines. Stretched, curved or nested groups get cut apart.
3. The start matters. Different starting centers can end in different answers.

Hierarchical clustering builds a tress
1. Start with every point as its own cluster.
2. Merge the two closest clusters.
3. Repeat until one cluster is left.
4. Cut the tree at a height to get k clusters.
The linkage decides what "closest" means: single (), ()

One tree holds every k
Cutting high gives two clusters. Cutting lower splits each of them again.

Linkage defines the distances between clusters
1. Single linkage: minimal distance between clusters. Can isolate outliers.
2. Complete linkage: maximal distance between clusters
3. Average linkage:
4. Ward linkage: 

Spectral clustering uses a neighbor graph
Step 1: Connect each point to its 10 nearest neighbors.
Step 2: Take the eigenvectors of L with the smallest eigenvalues.
Step 3: Run k-means on the new coordinates
- Researcher Funeuxenbourg (2010) wrote a paper on spectral clustering.

Choosing settings without labels (hyperparameters, the numebr of clusters, validity indices)

3 central choices
Preprocessing: Normalization, the number of principal components, ...\

Clustering has no good way to validate. Supervised learning uses cross-validation. But with clustering, there are no labels to hold out.

Stability and Generalizability
- Checking a clustering by resampling the data

Stability: If we cluster a different random subsample of the cells, do we get the same clusters? ()
Generalizability: If we train a classified on the clusters, can it predict the clusters of cells it has not seen? (Dudoit & Fridlyand 2002; Tibshirani ....)

The Adjusted Rand Index (ARI) measures agreement
- comparing two clusters
- the ARI compares two clusterings of the same points. It checks every pair of points: are the two togetehr in both clusterings, or apart in both?