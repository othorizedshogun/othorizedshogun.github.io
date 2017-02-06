---
layout: post
title: "k-Nearest Neighbors"
date: 2017-02-09
category: notebook
comments: true
---

The basic idea for the k-Nearest Neighbors classifier is that we find the _k_ closest images in the dataset with
respect to our query _x_. Here, we will perform the following processes:

- [Load the CIFAR-10 dataset](#load-the-cifar-10-dataset)
- [Compute for the L2 (Euclidean) Distance](#compute-for-the-l2-distance)
    - [Two-Loop Implementation](#twoloop)
    - [One-Loop Implementation](#oneloop)
    - [No-Loop Implementation](#noloop)
- [Visualize the distances](#visualize-the-distances)
- [Perform cross-validation to find the best _k_](#crossval)

## Load the CIFAR-10 Dataset
CIFAR-10 is a labeled dataset that houses 80 million tiny images. It was created by Alex Krizhevsky, Vinod Nair, and Geoffrey Hinton. It contains 60,000 32x32 color images with 6,000 images per class.

We can visualize some examples in CIFAR-10, here we can see a sample of 10 classes with 7 examples each.  

![CIFAR Sample](/res/cs231n-knn/output_3_0.png){:width="560px"}  
__Figure 1:__ _Samples of the CIFAR-10 Dataset_
{: style="text-align: center;"}

As we can see, for each class, there are distinct images related to it. For example, the `car` class is represented of different car images, some of which have different orientation, or different color. These images then represent a certain "template" that can be used by the classifier in order to categorize a test image.

# Compute for the L2 Distance
Distance computation is a quantifiable means of comparing two images together. To compute for distance, pixel-wise differences are often implemented. In this method, distance is computed "pixel-by-pixel" and then the elements of the corresponding matrix is added together. Highly similar images will have lower values while different images will have higher values. Moreover, images that are exactly similar have a 0 distance. The choice of distance that was used in the assignment is the L2 distance:

$$
d_{2}(I_{1}, I_{2}) = \sqrt{\sum_{p}(I_{1}^{p} - I_{2}^{p})^{2}}
$$

Thus, for images $$I_{1}$$ and $$I_{2}$$, we perform a sum of squares pixel computation for each $$p$$ and then get the square root. The assignment requires us to implement the L2 distance in three different ways.

## <a name="twoloop"></a> Two-loop implementation
The two-loop computation uses a nested-loop in order to compute for the pixel-wise L2 Distance between the test and train images. This is one of the easiest methods to implement, but it takes a toll on speed because of the looping nature.

<?prettify?>
<pre class="prettyprint linenums">
num_test = X.shape[0]
num_train = self.X_train.shape[0]
dists = np.zeros((num_test, num_train))
for i in xrange(num_test):
  for j in xrange(num_train):
    dists[i,j] = np.linalg.norm(self.X_train[j,:]-X[i,:])
return dists
</pre>

Here, I am implementing the [`np.linalg.norm`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.norm.html) function to compute for the norm (which is, in a sense, equivalent to the L2 equation) of `X_train` and `X`. Furthermore, this can also be implemented by religiously following the equation above, and thus we can have something similar below:

<?prettify?>
<pre class="prettyprint linenums">
dists[i,j] = np.sqrt(np.sum(np.square(X[i,:]-self.X_train[j,:])))
</pre>

## <a name="oneloop"></a> One-loop implementation
For the one-loop implementation, what we do is that in our `dists` matrix, we compute for the distances _for each example in the test set_ `X` against the examples in the training set `X_train`. As we will see, instead of filling the `dists` matrix cell-by-cell (as we have done in the two-loop computation), we fill the `dists` matrix row-by-row, or in other words, by "test example by test example."

<?prettify?>
<pre class="prettyprint linenums">
num_test = X.shape[0]
num_train = self.X_train.shape[0]
dists = np.zeros((num_test, num_train))
for i in xrange(num_test):
  dists[i, :] = np.linalg.norm(self.X_train - X[i,:], axis = 1)
</pre>

This is intuitively faster than the previous implementation, because the distance computation against the training set is done in parallel. In the next implementation, we will implement a fully-vectorized computation that can further improve the speed of our computations.

## <a name="noloop"></a> No-loop implementation
The no-loop computation is a fully-vectorized implementation of the L2 distance. This eliminates the loops entirely, replacing a cell by cell (or row by row) implementation into a single matrix solution.  

My workaround for this is to implement another form of the L2 Distance, which can actually be derived from the equation above. In this case, for two vectors $$\mathbf{I}_{1}$$ and $$\mathbf{I}_{2}$$. We can also compute for the L2 Distance as:

$$
d_{2}(\mathbf{I}_{1}, \mathbf{I}_{2}) =  \left\lvert \left\lvert \mathbf{I}_{1} - \mathbf{I}_{2} \right\rvert \right\rvert  = \sqrt{\left\lvert \left\lvert\mathbf{I}_{1} \right\rvert \right\rvert^{2} +  \left\lvert \left\lvert \mathbf{I}_{2}\right\rvert \right\rvert^{2} - 2 \mathbf{I}_{1} \cdot \mathbf{I}_{2}}
$$

With this equation, we can easily compute for the `dists` matrix without using any loops, for this we implement the following:

<?prettify?>
<pre class="prettyprint linenums">
num_test = X.shape[0]
    num_train = self.X_train.shape[0]
    dists = np.zeros((num_test, num_train))
    test = np.reshape(np.sum(X*X, axis = 1),(-1,1))
    train = np.reshape(np.sum(self.X_train*self.X_train, axis = 1),(1,-1))
    temp = test + train - 2 * np.dot(X, np.transpose(self.X_train))
	  dists = np.sqrt(temp)
</pre>

The vectorized version can in fact provide a very fast performance compared to the looped implementations. Using my own
machine, I was able to obtain the following execution times:

```
Two loop version took 211.117404 seconds
One loop version took 135.111970 seconds
No loop version took 5.534445 seconds
```
We were then able to reduce the time it takes to compute for the L2 Distance in a large dataset from 3 minutes to just 5 seconds. Very impressive indeed!

## Visualize the distances
We can plot the `dists` matrix and visualize the distances of our test examples with respect to different training examples. Here, as you look down, we are looking at a representation of our test examples. As you look from left to right, we see the training examples. Thus we have over 500 test examples and over 5000 training examples. Darker regions represent areas of low distance (more similar images) while lighter regions represent areas of high distance (more different images).

![Plot distance](/res/cs231n-knn/output_9_0.png){:width="560px"}  
__Figure 2:__ _Visualization of the `dists` matrix_
{: style="text-align: center;"}

The distinctly visible rows (say, the dark rows in the 300 mark or the white rows in the 400 mark) represent test examples that are similar (or different) to most of the training examples. Let's focus on the dark rows in the 300 mark. The reason why distinct dark rows can be seen in it is because there could be many classes in the training set that was found to be similar to it. This can be attributed to similar backgrounds or hues that can confuse our classifier into thinking that it belongs to the same class.

On the other hand, the columns we see are in fact training examples that are not similar to any of the test examples. Perhaps a certain training example was found to have no any significant similarity to any of the test examples. This will then result to a high L2 distance, and consequently, generate a white column into our visualization.

## <a name="crossval"></a> Perform cross-validation to find the best k
One good method to know the best value of _k_, or the best number of neighbors that will do the "majority vote" to identify the class is through cross-validation. What we will do here is to split the training set into 5 folds, and compute the accuracies with respect to an array of k choices. From this we sort the accuracies and obtain the best value of k.  

Firt we split the training set `X_train`:

<?prettify?>
<pre class="prettyprint linenums">
num_folds = 5
k_choices = [1, 3, 5, 8, 10, 12, 15, 20, 50, 100]

X_train_folds = []
y_train_folds = []

X_train_folds = np.array_split(X_train, num_folds)
y_train_folds = np.array_split(y_train, num_folds)
</pre>

And then we perform cross-validation. Thus, for each k value, we will run the k-NN algorithm `num_folds` times. Here
we will use all but one folds as our training data, and the last one as our validation set. We then store the accuracies of each
fold and all values of k in the `k_to_accuracies` dictionary.

<?prettify?>
<pre class="prettyprint linenums">
for k in k_choices:
    k_to_accuracies[k] = []

for k in k_choices:
    print('k=%d' % k)
    for j in range(num_folds):
        # Use all but one folds as our crossval training set
        X_train_crossval = np.vstack(X_train_folds[0:j] + X_train_folds[j+1:])
        # Use the last fold as our crossval test set
        X_test_crossval = X_train_folds[j]

        y_train_crossval = np.hstack(y_train_folds[0:j]+y_train_folds[j+1:])
        y_test_crossval = y_train_folds[j]

        # Train the k-NN Classifier using the crossval training set
        classifier.train(X_train_crossval, y_train_crossval)

        # Use the trained classifer to compute the distance of our crossval test set
        dists_crossval = classifier.compute_distances_no_loops(X_test_crossval)

        y_test_pred = classifier.predict_labels(dists_crossval, k)
        num_correct = np.sum(y_test_pred == y_test_crossval)
        accuracy = float(num_correct) / num_test

        k_to_accuracies[k].append(accuracy)
</pre>

In order to see how the value of k changes with respect to our cross validation set, we can visualize them in terms
of line plot with error bars:

![Cross validation](/res/cs231n-knn/output_21_0.png){:width="560px"}  
__Figure 3:__ _Visualization of the cross-validation procedure with different k values_
{: style="text-align: center;"}

From now, we can choose a good k value. Let's take `k = 7`.

```
Got 141 / 500 correct => accuracy: 0.282000
```

And thus we were able to obtain an accuracy of 28.2%. It is not as good as state-of-the-art classifiers today (a Convolutional Neural Network solution in [Kaggle](https://www.kaggle.com/c/cifar-10/leaderboard) was able to reach a whopping 95%). But this is a good start to learn the image classification pipeline and the efficiency of the vectorization method.