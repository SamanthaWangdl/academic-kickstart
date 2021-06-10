+++
# Project title.
title = "Coronavirus Drug Prediction based on Machine Learning and Graph Neural Network"

# Date this page was created.
date = 2020-07-09T00:00:00

# Project summary to display on homepage.
summary = "Our group participated MIT AIcure Drug Prediction Competition. We achieved 88% of auc-roc results and solved the problem of data imbalance."

# Tags: can be used for filtering projects.
# Example: `tags = ["economic-impact", "r-package"]`
tags = ["Deep Learning"]

# Optional external URL for project (replaces project detail page).
# external_link = "https://runwang.xyz/page1/landing_page/"

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Links (optional).
url_pdf = ""
url_slides = ""
url_video = ""
url_code = "https://github.com/SamanthaWangdl/PRMLfinalpj"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
#url_custom = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/antaldaniel"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  # caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"

+++
## Summary
Our group tried all the methods of drug molecule representation learning under this task. We not only achieved **88%** of auc-roc results, but also tried all the drug molecule processing methods seen in the paper, and tried to solve the problem of data imbalance. First of all, a variety of classical classification methods are performed on  three types of manually extracted chemical features. Secondly, four recurrent neural network structures were tried on the smiles string, and the highest roc was 0.64; Finally, the graph network which inculdes mpnn and gcn got 0.88 and 0.87 roc respectively. In addition, various sampling methods have been tried to solve the problem of data imbalance.

## Classic Methods
### Classification method based on molecular descriptor

Molecular descriptor is an important tool of chemometrics, which refers to the measurement of a certain aspect of a molecule, which can be the physical and chemical properties of the molecule. Molecular descriptor can also be a numerical index derived through various algorithms based on the molecular structure. It includes various theories or experiments spectral data (such as ultraviolet spectrum), molecular composition (such as hydrogen bond donor number, chemical bond number), physical and chemical properties (such as ester water distribution coefficient) description characters, molecular field descriptors, and molecular shape descriptors. Molecular descriptors can be the most important and effective feature of this question. Compared with the complex network structure, we found that using better molecules descriptor features can bring greater growth to the results.
The special python package Rdkit provides convenient functions for processing Smiles strings and extracting molecular descriptors.
Conveniently,  you can extract 299 molecular descriptor features of smiles strings.

```python
def get_fps(mol):
calc=MoleculeDescriptors.MolecularDescriptorCalculator([x[0] for x in
Descriptors._descList])
ds = np.asarray(calc.CalcDescriptors(mol))
arr=Fingerprinter.FingerprintMol(mol)[0]
return np.append(arr,ds)
```
After extracting features, random forest and multilayer perceptron classifiers are used to perform the task of E. coli drug resistance rate predication. The multilayer perceptron is an artificial neural network with a forward structure. Use Relu as the activation layer, Adam optimization method, two-layer hidden layer network structure. The number of hidden layer units is defined as 100 and 10. 
In this task, the effect of random forest is almost the same as that of multilayer perceptron, but the training time of random forest is much shorter than that of multilayer perceptron.

|                   | Random forest                  |  Multilayer perceptron|
| ------------------| ------------------------------ |-----------------------|
| roc               | 81%                            |      79%              |
| prc               | 45%                            |       44%             |

### Classification method based on molecular fingerprint

Chemical fingerprinting is a method of converting drawn molecules into streams of 0 and 1 bits. Morgan fingerprints are more common, which is a round fingerprint, encode all possible atoms within a given atomic radius in the target molecule and their connection form, and get 0, 1 digital stream.
At present, ECFP4 fingerprint, ECFP6 fingerprint and RDKFP fingerprint are popularly used in chemoinformatics. 
The getmorganfingerprint module can easily generate the fingerprints.
```python
data['fingerprint']=data['mol'].apply(lambda m:
AllChem.GetMorganFingerprintAsBitVect(m, radius=2, nBits=2048))
```

### Classification Method Based on Mol2vec

In the previous section, we talked about the problem of excessively high latitude of molecular fingerprints, analogous to the relationship between words and sentences in natural language processing, in molecular representation, we consider the fingerprint of the molecule as a vocabulary, and the molecule as a sentence, then the word2vec method in natural language processing can be used.

{{< figure library="true" src="drug1.jpg" title="mol2vec" style="zoom: 40%;" >}}

In the article Mol2vec: Unsupervised Machine Learning Approach with Chemical Intuition, by using the word2vec algorithm on the molecule, the high-dimensional molecular fingerprint can be reduced to a 300-dimensional word embedding vector. 
We use the mol2vec method here to treat each molecule in the smiles formula as a sentence, and each molecular fingerprint (fingerprints can be regarded as molecular substructure) as words. After mol2vec, we get the word vector representation of each word, and we think that each molecule is its the sum of substructure word vectors, so the vector of all substructures of each molecule represents the representation of both molecules.
Each molecule is represented as a 300-dimensional vector, and we use the random forest and multilayer perceptron used in the previous sections to perform the task of E. coli and get the average roc and prc on the 10-fold.

|      | Random Forest | Multilayer Perceptron |
| ---- | ------------- | --------------------- |
| roc  | 82.3%         | 71.4%                 |
| prc  | 45.6%         | 37.2%                 |

### Molecular Descriptor, Mol2vec, Molecular Fingerprint Feature Hybrid

In order to make the representation of feature engineering cover as much information as possible, I tried to splice the above three features to effectively improve the results of roc.

|      | Random Forest |
| ---- | ------------- |
| roc  | 85%           |
| prc  | 44%           |

## Recurrent Neural Nework

Referring to the practice in the article SMILES2Vec: An Interpretable General-Purpose Deep Neural Network for Predicting Chemical Properties, it is believed that the method of converting the string smiles into a vector can be regarded as a method of predicting its physical and chemical properties. As for the method of processing strings, we can try the method of recurrent neural network.

In fact, before the graph network was applied to the problem of chemical molecules, both the cv and NLP methods were used to predict the properties of chemical molecules. The cv method was used to process molecular graphs, and the nlp method was used to process smiles. We can see that the advantage of the neural network here compared to the classical method is that it no longer requires expert experience, and results can be produced solely by relying on the network.

But the main question here is whether the Amiles string can express all the characteristics of the molecule? We know that for a cyclic molecule with a complex structure, different expressions of smiles can be formed by breaking the chain from different positions, but in fact these molecules are a substance, but the expression of smiles has undergone a huge transformation. This problem leads to multiple expressions of smiles in a molecule. At the same time, the molecular data in our data is too small, in fact, training rnn is not sufficient.

In trying to use the cyclic network method, I tried four network structures. The overall result is not as good as the classic method. The overall network framework follows the seq2seq framework, adjusted to use no rnn layer, and also tried to add a one-dimensional convolutional layer.

{{< figure library="true" src="drug2.jpg" title="rnn structure" style="zoom: 60%;" >}}

The following table shows the results of the recurrent network. You can see from the results that the level of aucroc actually fluctuates around 0.6-0.7, even if it is good, it is only 0.71, and at the same time prc is low, as we used in the previous feature extraction and classical methods. The results cannot be compared. However, the cyclic network does not require humans to manually extract features, which is its advantage, but the ability to extract features is far from the graph network.

|               | aucprc | aucroc |
| ------------- | ------ | ------ |
| bigru+bigru   | 0.11   | 0.73   |
| bilstm+bilstm | 0.08   | 0.60   |
| cnn+gru       | 0.11   | 0.71   |
| cnn           | 0.12   | 0.65   |



## Graph Neural Network

### Data Prepossessing

In the graph neural network, in addition to the network structure which has a great impact on the effectiveness of the model, the node and edge information of the graph is also important as input. Here, we mainly discuss the feature extraction of edges and nodes in data preprocessing.

The open source architecture **Deepchem** provides us with an effective method to extract atoms and edge features from molecules:

```python
node_feature = dc.feat.graph_features.atom_features()
bond_feature = dc.feat.graph_features.bond_features()
```

In the article *Analyzing Learned Molecular Representations for Property Prediction*, the author used the following features as the atomic and chemical bond features.

{{< figure library="true" src="drug3.jpg" title="Node&Edge" style="zoom: 60%;" >}}

Similarly, using deepchem's feature extraction function, we can get:

| Property            | Length |
| ------------------- | ------ |
| Symbol              | 44     |
| Degree              | 10     |
| Valence             | 6      |
| Formal Charge       | 5      |
| Radical Electronics | 4      |
| Hybridization       | 5      |
| Aromaticity         | 1      |

The above features use one-hot encoding, and the total length of the encoded features is 75. In order to further enhance the capabilities of the network model, we consider adding new features.

### Graph Neural Network

Message Passing Neural Networks (MPNN) is a general framework of graph neural networks proposed by Google. Empirically, it has an excellent performance in predicting the properties of chemical molecules. Therefore, in the method of using graph networks, we prefer to use MPNN to achieve the task of molecular performance prediction.
$$
m_{v}^{t + 1} = \sum_{w\in N(v)}M_t(h_v^t, h_w^t, e_{vw})\\h_v^{t+1} = U_t(h_v^t, m_v^{t+1})\\y = R({h_v^T|v\in G})
$$

| Layer | Input                                             | Output            |
| ----- | ------------------------------------------------- | ----------------- |
| Lin0  | n_feature_dim                                     | n_h_feature_dim_1 |
| Lin1  | e_feature_dim                                     | e_h_feature_dim   |
| Lin2  | n_h_feature_dim + n_feature_dim + e_h_feature_dim | n_feature_dim     |
| Lin3  | 2 * n_feature_dim                                 | n_h_feature_dim_2 |
| Lin4  | n_h_feature_dim_2                                 | 1                 |

 

```python
self.lin0 = {0: nn.Linear(self.n_feature_dim, self.n_h_feature_dim), 
        1: nn.Linear(self.n_feature_dim, self.n_h_feature_dim), 
        2: nn.Linear(self.n_feature_dim, self.n_h_feature_dim)}
self.lin1 = nn.Linear(self.e_feature_dim, self.e_h_feature_dim)
self.lin2 = {
  			0: nn.Linear(self.n_h_feature_dim + self.n_feature_dim + self.e_h_feature_dim, self.e_h_feature_dim),
        1: nn.Linear(self.n_h_feature_dim + self.n_feature_dim + self.e_h_feature_dim, self.e_h_feature_dim), 
        2: nn.Linear(self.n_h_feature_dim + self.n_feature_dim + self.e_h_feature_dim, self.e_h_feature_dim)}
self.lin3 = nn.Linear(2 * self.n_feature_dim, self.n_out_dim)
self.lin4 = nn.Linear(self.n_out_dim, 1)
```

MPNN has achieved good results on the roc value, and has strong generalization ability. It can get an average of 0.8838 `roc_auc` on the test set, but the performance of `prc` is not satisfactory. We know that the roc curve remains unchanged when the distribution of positive and negative samples changes. And prc can show the ability to model on tilted data sets. Since in this data set, the positive samples are much smaller than the negative samples, the low roc reflects that the classifier misjudges a large number of negative examples as positive examples. It can be seen from the training process that after multiple iterations, both the values of `roc_auc` and `prc_auc` can reach values close to 1 in the training data. Therefore, the model may have over-fitting behavior and poor generalization ability.

#### ROC

{{< figure library="true" src="drug4.jpg" title="Roc Curve" style="zoom: 40%;" >}}

The figure above shows the change of ROC curve during fold `5,6,7` training. The first column of data is the ROC curve of the first iteration, the middle column is the result of the 100th iteration, and the third column Is the result of the last iteration. In the experiment, as the number of epochs increases, the loss decreases, and the roc value tends to increase. But it is not always on an upward trend. It can be seen that there are three folds in the figure, and the roc in the third column of data is slightly inferior to the middle column.

### GCN

Graph Convolutional Neural Network (GCN) is also a commonly used graph network structure. We also want to know whether MPNN has better capabilities in molecular performance prediction tasks than GCN. In the experiment, the GCN structure we tried is as follows: `1 layer embedding layer + n layer convolution layer + 1 layer fully connected layer`.

| Layer         | input            | Output           |
| ------------- | ---------------- | ---------------- |
| **Embedding** | node_input_dim   | node_feature_dim |
| **Conv**      | node_feature_dim | node_feature_dim |
| **Fc**        | node_feature_dim | 1                |

|            | ROC_AUC | PRC_AUC |
| ---------- | ------- | ------- |
| **fold 0** | 0.9367  | 0.7106  |
| **fold 1** | 0.9035  | 0.5185  |
| **fold 2** | 0.8718  | 0.5914  |
| **fold 3** | 0.5644  | 0.0282  |
| **fold 4** | 0.9308  | 0.8439  |
| **fold 5** | 0.6869  | 0.4133  |
| **fold 6** | 0.8502  | 0.0156  |
| **fold 7** | 0.9810  | 0.7269  |
| **fold 8** | 0.9531  | 0.1251  |
| **fold 9** | 0.9429  | 0.8149  |
| **mean**   | 0.8754  | 0.4788  |

It can be seen that in GCN training, although `roc` can achieve good performance in most compromises, there are still relatively poor data (such as fold3). And there is an experimental process to know that in relatively large data, such as fold3, fold5, there are still very impressive results (>0.9) on the training set, which is caused by the poor generalization ability of the model. Although GCN's `roc` performance is slightly inferior to MPNN-1, it has a stronger performance on `prc`, which shows that the GCN model has a stronger ability to deal with our skewed data set

There is no chemical bond characteristic information, just using a simple network structure, you can still get good results. This may be due to the limited contribution of chemical bond information to the prediction of chemical properties, or the complex network is not effective enough to express information.

## Conclusion

In the drug prediction task, we tried classical methods, recurrent network methods and graph network methods, and optimized sampling and integration in the imbalance problem, achieving most of the existing solutions to the drug prediction problem.

The classical method mainly relies on feature engineering, because chemical molecular science has already precipitated very mature molecular features. The extraction of molecular descriptors and molecular fingerprints can achieve a roc of 0.80 or more even with a simple classifier.

The use of recurrent networks, although it was our first thought when we saw smiles strings, did not work well, and the training time was too long, so a simple recurrent network may not be suitable for drug prediction tasks.

In the task of predicting drug properties, both the graph neural network MPNN and GCN show certain predictive capabilities. Among them, the roc of GCN can reach 0.8754, and the prc can reach 0.4788. MPNN performs better on roc, reaching 0.8838, but the prc value is not good, only 0.2383. Although the effect of graph neural network is considerable, the training time is long, and due to the small amount of data, the data distribution is skewed, the model may have overfitting problems, and the generalization ability still needs to be strengthened.