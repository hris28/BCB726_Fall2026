
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

