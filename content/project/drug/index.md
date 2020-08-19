+++
# Project title.
title = "Coronavirus Drug Prediction based on Machine Learning and Graph Neural Network"

# Date this page was created.
date = 2020-07-09T00:00:00

# Project summary to display on homepage.
summary = "Our group tried all the methods of drug molecule representation learning under the MIT Drug Prediction Competition. We not only achieved 88% of auc-roc results, but also implemented all the drug molecule processing methods and solved the problem of data imbalance."

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



