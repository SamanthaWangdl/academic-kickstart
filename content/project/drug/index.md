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
Our group tried all the methods of drug molecule representation learning under this task. We not only achieved **88%** of auc-roc results, but also tried all the drug molecule processing methods seen in the paper, and tried to solve the problem of data imbalance. First of all, a variety of classical classification methods are performed on  three types of manually extracted chemical features. Secondly, four recurrent neural network structures were tried on the smiles string, and the highest roc was 0.64; Finally, the graph network which inculdes mpnn and gcn got 0.88 and 0.87 roc respectively. In addition, various sampling methods have been tried to solve the problem of data imbalance

## Classic Methods
### Classification method based on molecular descriptor

Molecular descriptor is an important tool of chemometrics, which refers to the measurement of a certain aspect of a molecule, which can be the physical and chemical properties of the molecule. Molecular descriptor can also be a numerical index derived through various algorithms based on the molecular structure. It includes various theories or experiments spectral data (such as ultraviolet spectrum), molecular composition (such as hydrogen bond donor number, chemical bond number), physical and chemical properties (such as ester water distribution coefficient) description characters, molecular field descriptors, and molecular shape descriptors. Molecular descriptors can be the most important and effective feature of this question. Compared with the complex network structure, we found that using better molecules descriptor features can bring greater growth to the results.
The special python package Rdkit provides convenient functions for processing Smiles strings and extracting molecular descriptors.
Conveniently, you can extract 299 molecular descriptor features of smiles strings.
```python
def get_fps(mol):
calc=MoleculeDescriptors.MolecularDescriptorCalculator([x[0] for x in
Descriptors._descList])
ds = np.asarray(calc.CalcDescriptors(mol))
arr=Fingerprinter.FingerprintMol(mol)[0]
return np.append(arr,ds)
```
After extracting features, random forest and multilayer perceptron classifiers are used to perform the task of E. coli drug resistance rate predication. The multilayer perceptron is an artificial neural network with a forward structure. Use relu as the activation layer, adam optimization method, two-layer hidden layer network structure.The number of hidden layer units is defined as 100 and 10. 
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


### Classification method based on mol2vec