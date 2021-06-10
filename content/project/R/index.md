+++
# Project title.
title = "Maximizing the Smallest Eigenvalue of Grounded
Laplacian Matrix by Node Selection"

# Date this page was created.
date = 2017-11-29T00:00:00

# Project summary to display on homepage.
summary = "The smallest eigenvalue of a grounded Laplacian matrix plays a pivotal role in complex networks, such as system control, convergence rate and the robustness of a system. In this paper, we focus on the node selection problem of maximizing the smallest eigenvalue of the grounded Laplacian matrix for a graph."

# Tags: can be used for filtering projects.
# Example: `tags = ["economic-impact", "r-package"]`
# tags = ["R"]

# Optional external URL for project (replaces project detail page).
external_link = "http://iotables.ceemid.eu/"

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
url_code = "https://github.com/rOpenGov/iotables/"

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

Grounded Laplacian matrix, a principal submatrix of the Laplacian matrix, functions as a significant model in network control study. Due to the impossibility of controlling all nodes in the network, steering a fraction of nodes is a significant al- ternative, which relates to grounded Laplacian matrix closely. Both pinning control and leader selection problem employ grounded Laplacian matrix as their model, and the eigenvalue of the grounded Laplacian matrix performs as efficient metrics in diverse control systems.

Our work is a comprehensive study of the SMALLEST EIGENVALUE OPTIMIZATION problem. We prove the NP - hardness and non-submodularity of this combinatorial optimization problem. Then we propose a nearly linear time heuristic algorithm. It capitalizes on two analysis methods: network derivative mining, and matrix disturbance theory, to evaluate the eigen-gap for node selection. The consistency between these two methods justifies the reliability of our analysis. Sufficient experiments and excellent results warrant the performance of our algorithm.



Based on tedious analysis, the optimization of extreme eigenvalue is reduced to the computation of the corresponding eigenvector u and the core of our algorithm is shown as follows.

{{< figure library="true" src="sourcecode.png" title="The core of the optimization algorithm" >}}