

# Auto Machine Learning

## Papers
<details>
<summary>
 <a href="https://ml.informatik.uni-freiburg.de/papers/15-AUTOML-AutoML.pdf">Methods for Improving Bayesian Optimization for AutoML
(AutoSklearn paper)
</a> 
</summary>
This is the paper that introduces AutoSklearn.
This paper compares the performance of AutoSklearn with AutoWEKA(which is an AutoML package that combines WEKA with Bayesian optimization).
This paper (AutoSklearn) approaches AutoML in three main steps:
<ol>
<li> Meta-learning to find good instantiations of machine learning frameworks: 
140 datasets from OpenML are considered and a set of meta-features are evaluated for each of these datasets. Each of these datasets is characterized by 38 meta-features including simple, information-theoretic and statistical meta-features.
Further, a Random-forest Bayesian optimization method SMAC (Sequential model-based algorithmic configuration) is applied for 24 hours with 10-fold CV on 2/3rd dataset with 1/3rd dataset as CV set. Given a new dataset, the above mentioned meta-features are extracted and the L1 distance between this meta-feature space is compared with the meta-feature spaces of the 140 datasets to find the k-nearest datasets. The results from the closest datasets are extracted from the meta-knowledge database to warm start SMAC.
</li>

<li>
Bayesian optimization to navigate through search space: 
Search space has only 132 hyperparameters. 
The models considered within the search space include:
 <ul>
  <li> General Linear models(3 algorithms)</li>
  <li> Support vector machines (2)</li>
  <li> Discriminant analysis (2)</li>
  <li> Nearest neighbors (1)</li>
  <li> Naive Bayes (3)</li>
  <li> Decision Trees (1)</li>
  <li> Ensemble methods (4)</li>
 </ul>
 </li>
 Preprocessing:<br>
Data preprocessing: Scaling inputs, imputation of missing values and balancing target classes.<br>
Feature preprocessing: 11 possible methods which include Feature Selection (2), Kernel approximation (2), matrix decomposition (3), Embeddings (3), feature clustering (1), methods using classifier for feature selection (2).
<li> Automated construction of ensembles of Models evaluated during optimization:
The idea behind the construction of Ensembles is that ensembles perform well if the models are individually strong and make uncorrelated errors. Ensemble selection method is outlined in Caruana et al. (2004).
</li>
 </ol>
 The benefit of AutoSkleran over AutoWEKA comes from meta-learning and ensemble construction. The version of AutoSklern without the above two is called vanilla AutoSklearn. Experiments are performed to see how the above mentioned techniques can benefit performance. The following are observed from the experiments:<br>
 <ol>
 <li> Meta-learning yields drastic improvements from the first configuration till the end of experiments.</li>
 <li> Although Vanilla AutoSklearn and AutoSklearn (with meta-learning) both show improved performance with ensembles, ensembles with meta-learning yields performance gains faster than Vanilla AutoSklearn. </li>
 </ol>
</details>

<details>
<summary>
 <a href="https://link-springer-com.ezproxy.lib.uh.edu/content/pdf/10.1007%2F978-3-540-73263-1.pdf">Metalearning: Applications to Data Mining (Book on Meta learning)
</a> 
</summary>
 <b>This is a book on metalearning. Each chapter will be summarized. <br>
Work in progress!</b>

<ol>
<li>
<h3>Metalearning: Concepts and Systems
</h3>
<b>Base learning</b> is the successive application of a learner on the same data. No knowledge is extracted over domains.
With <b> Meta learning</b> the focus is on accumulating experience from previous tasks and applying them to a learning system.<br>
Metalearning covers both declarative and procedural bias. The following is ideally performed in order:
<ol>
<li> Obtain dataset.</li>
<li> Extract meta-features</li>
<li>From the <b>meta knowledge database</b> containing the ML/DL algos (initial bias), Datasets along with their respective meta-features and their performance, the matching and search is performed with the new dataset</li>
<li> The smaller search space is obtained with the new bias</li>
<li> Evaluation and selection of the search space is performed with a suitable evaluation strategy</li>
<li> Best algorithm is chosen</li>
</ol> 
Effectiveness of search space depends on the quality of the available meta-knowledge.
 <p><b>Generation of meta-features</b></p>
Three main classes of meta-features have been proposed:
<ul>
<li> Statistical and information-theoretic characterization: Number of classes, number of features, Ratio of examples to features, degree of correlation between features and target, Average class entropy.</li>
<li> Exploit properties of some induced hypothesis: For example, construct decision trees on each dataset and get it’s properties to form meta features.</li>
<li> Use many simple and fast learners on the datasets and use the accuracy of these “landmarks” to characterize the datasets. Example, k-NN has been used at the meta level to identify most similar datasets for a given input dataset.</li>
</ul>
</p>


</ol>

 
 
 </details>


## Papers (NAS)

<!-- Making NAS more efficient -->
<details>
<summary>
 <a href="https://arxiv.org/abs/1807.11626">MnasNet: Platform-Aware Neural Architecture Search for Mobile
</a> 
</summary>
 <b> Focus on making NAS more efficient</b><br>
 This paper discusses modifies existing NAS algorithms in two ways:
<ol>

<li> Multi-objective Reward:<br>

Unlike previous work where the common method is to treat T as a hard constraint and maximize accuracy under this constraint:<br>

maximize ACC(m) wrt m subject to LAT(m)≤T                <br>                               
    

where Acc(m) is the accuracy of the model and LAT(m) is the inference latency of the model. LAT(m) is therefore treated as the hard constraint and accuracy is maximized under this constraint.
But, the problem with this approach is that it maximizes a single metric (ACC) and does not provide multiple Pareto optimal solutions (state of allocation of resources from which it is impossible to reallocate so as to make any one individual or preference criterion better off without making at least one individual or preference criterion worse off). <br>
The problem now now be re-framed as finding multiple Pareto-optimal solutions within a single architecture search.
[K. Deb. Multi-objective optimization. Search methodologies, pages 403–449, 2014.] provides multiple methods to solve this type of problem, but the one chosen by this paper is <br>




maximize ACC(m)×[LAT(m)/T]^w wrt m                  <br> 				
      

where w is the weight factor defined as:

w= α,if LAT(m)≤T<br>
&nbsp;&nbsp;&nbsp;   β,otherwise <br>

where α and β are picked according to the trade-off between accuracy and inference latency.  As a hard constraint (not allowing the latency to increase beyond the constraint, severely penalizing if it does so) α= 0, β=−1 may be chosen. But, this paper uses α= -0.07, β=−0.07 as the constraint (soft constraint) in order to smoothly adjust the constraints.
</li>

<li> Factorized hierarchical search space: <br>

Past work search for a complex cell(s) and replicate them to form full architectures. This work focuses on dividing the architectures into blocks and searching for operations and connections within these blocks separately with the intention that given the input and output shape of a block, we want to get the best accuracy-latency tradeoff.<br>

Within each block, the following are searched:
<ul>

<li>Convolutional ops ConvOp: regular conv (conv), depthwiseconv (dconv), and mobile inverted bottleneck conv </li>
<li>Convolutional kernel sizeKernelSize: 3x3, 5x5.</li>
 <li>Squeeze-and-excitation [for more information on this technique refer reference 13 of this paper] ratioSERatio: 0, 0.25.</li>
<li>Skip ops SkipOp: pooling, identity residual, or no skip </li>
<li>Output filter size Fi.</li>
<li>Number of layers per block Ni</li>
</ul>

</ol>
Reinforcement learning (with an RNN agent) approach is adopted for navigating through search space. (Paper says that RL is easy to use but other techniques like evolution also will work). Similar work as is references [35, 36, 25, 20] of this paper.<br>

Training is performed on the ImageNet and the COCO detection datasets and reported accuracies of the best performing models are 75.6% and 66% respectively versus state-of-the-art accuracies of 72% and 60.3% of MobileNetV2.

 
 
 
</details>

## Plan 
