# Brighton, A Memorable City!

## Brief
The competition is a binary classification problem (label1 for memorable and label 0 for not memorable). You are provided with 24 7 labelled training data (209 memorable scenes and 38 not memorable scenes), and 11874 test data, which are not labelled. The task is to develop a binary-classclassifier that predicts the labels for the test data. Each data instance is represented by a 4608-dimensional feature vector. This vector is a concatenation of 4096-dimensional deep Convolutional Neural Networks (CNNs) features extracted from the fc 7 activation layer of CaffeNet 1and 512-dimensional GIST2 features (this representation is given therefore you do not have to perform any feature extraction on images!). The training data were collected in Brighton, while test data were collected in London. We therefore have a domain adaptation problem! And, of course (!), we also know that there are many more memorable sceneries in Brighton than in London.

## Approach
Here we employ a three stage pre-processing technique
for analysing the data. Firstly the input data is standardised.
Instead of feature selection, principal component analysis
is used to extract optimum features from the data. The final
stage of pre-processing, is the use of a clustering algorithm.
This is to account for observed differences between training
and testing data sets, so the clusters can be used to construct
a composite data set with a shape that more closely resembles
the testing data. A small subsection of the training data
is then taken aside for model validation after the classifier
has been trained.
After the clustering, the pre-processing of the information
is complete and the training of a classifier can begin. In
this analysis, the choice of classifier is a multi-layer perceptron
(MLP), this MLP has a five layer structure such that an
arbitrary decision boundary can be formed such that there
is a high limit to the complexity of the decision boundary
formed.
The principal component analysis process involves finding
the set of eigenvectors, resulting in as set of composite
features for the training data. Organising these features
by those with the highest combined variance allows us to
reduce the dimensionality by minimising information loss.
When dimensionality needs to be reduced as in our case,
the eigenvectors with the lowest variance are dropped leaving
only the composite PCA features that carry the most
information.
The k-means algorithm used is as a means of clustering
the testing data, this is an algorithm that does not rely on any
external training samples [2]. A set number of centres is assigned
a random location in feature space, and a decision
boundary drawn linearly between them. The centre of each
cluster is then moved to the mean location of the data contained
within the cluster. This process is iterated until the
centres converge to the optimum location in feature space.
The MLP classifier used here has it’s prediction power
rooted in linear algebra where each layer acts as a matrix
transformation on the layer before it, this reduces a trained
MLP model down to a specific linear equation, making it
trivial to implement once trained. To train an MLP there
are two distinct phases, the forward pass and the backward
pass[3]. In the forward pass we supply the MLP with a sample
or a batch of the training data and perform the linear algebra
to find out the model’s predictions for the data. Subsequently,
the predictions are compared to the target label and
the difference between the two values is quantified in a loss
statistic. After this step comes the backward pass, where the
parameters within the model are progressively tweaked and
back-propagated through the entire structure of the MLP to
reduce the loss of the sample[3]. Upon iteration of this, on a
large data set the MLP will generalise to any sample resembling
the training data and produce accurate predictions.
