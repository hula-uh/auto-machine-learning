

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

## Plan 
