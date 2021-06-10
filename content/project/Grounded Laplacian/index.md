+++
# Project title.
title = "Maximizing the Smallest Eigenvalue of Grounded
Laplacian Matrix by Node Selection"

# Date this page was created.
date = 2021-06-09 T00:00:00

# Project summary to display on homepage.
summary = "The smallest eigenvalue of a grounded Laplacian matrix plays a pivotal role in complex networks, such as system control, convergence rate and the robustness of a system. In this paper, we focus on the node selection problem of maximizing the smallest eigenvalue of the grounded Laplacian matrix for a graph with n nodes and m edges, under an upper bound constraint k ≪ n."

# Tags: can be used for filtering projects.
# Example: `tags = ["economic-impact", "r-package"]`
tags = ["Complex network"]

# Optional external URL for project (replaces project detail page).


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
url_code = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
url_custom = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/antaldaniel"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Screenshot of the package website"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++

Spectral theory has already a long history and widespread usage in different scenarios. The eigensystem of adjacency matrix can evaluate network topology for immunization and infrastructure study. Besides, the eigensystem of Laplacian matrix can measure the network’s connectivity. Our study focuses on a variant of Laplacian matrix, grounded Laplacian matrix, whose smallest eigenvalue matters broadly.

Grounded Laplacian matrix, a principal submatrix of the Laplacian matrix, functions as a significant model in network control study. Due to the impossibility of controlling all nodes in the network, steering a fraction of nodes is a significant al- ternative, which relates to grounded Laplacian matrix closely. Both pinning control and leader selection problem employ grounded Laplacian matrix as their model, and the eigenvalue of the grounded Laplacian matrix performs as efficient metrics in diverse control systems.

Specifically, the smallest eigenvalue of grounded Laplacian matrix can not only quantify node-selection scheme for pin- ning control strategy but also evaluate convergence rate and the system H∞ norm in consensus dynamics. Then a spontaneous question arises as what nodes should be controlled with respect to the smallest eigenvalue of grounded Laplacian matrix. Nevertheless, prior researches remain elusive on scalable node- selection strategy for the smallest eigenvalue of grounded Laplacian matrix.

The SMALLEST EIGENVALUE OPTIMIZATION problem is inevitable and difficult. Preceding study on its inverse pro- portion with network size implies the necessity of the re- fined node-selection scheme on a large network. However, the fundamental properties of the problem resist advances. Firstly, its combinatorial nature leads to exponential compu- tation complexity so that the brute-force algorithm fails even in medium-sized networks. Secondly, without submodularity, greedy algorithms, as the conventional resort for NP-hard problems, lose their approximation guarantee. To our best knowledge, the computation techniques for this problem are either empirical or exclusive for small networks.
Our work is a comprehensive study of the SMALLEST EIGENVALUE OPTIMIZATION problem. We prove the NP- hardness and non-submodularity of this combinatorial op- timization problem. Then we propose a nearly linear time heuristic algorithm. It capitalizes on two analysis methods: network derivative mining, and matrix disturbance theory, to evaluate the eigen-gap for node selection. The consistency between these two methods justifies the reliability of our analysis. Sufficient experiments and excellent results warrant the performance of our algorithm.

