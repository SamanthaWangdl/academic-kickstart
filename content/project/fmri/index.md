+++
# Project title.
title = "Maximizing the Smallest Eigenvalue of Grounded
Laplacian Matrix by Node Selection"

# Date this page was created.
date = 2021-06-09T00:00:00

# Project summary to display on homepage.
summary = "The smallest eigenvalue of a grounded Laplacian matrix plays a pivotal role in complex networks, such as system control, convergence rate and the robustness of a system. In this paper, we focus on the node selection problem of maximizing the smallest eigenvalue of the grounded Laplacian matrix for a graph with n nodes and m edges, under an upper bound constraint k ≪ n."

# Tags: can be used for filtering projects.
# Example: `tags = ["economic-impact", "r-package"]`
# tags = ["complex network"]

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

The symmetric input-output tables (SIOTs) are complex statistical products that present inter-related statistics in a predefined structure. They are often found in spreadsheets that follow this structure, or in the case Eurostat in a data repository. In both cases they in reproducible research must be downloaded and restructured to programmatically accessible form. Often these highly structured statistics need to be analyzed together with other data, for example, when employment effects and multipliers are calculated. In this case processing the employment data to SIOT conforming format is a significant preprocessing challenge.

The iotables are exactly designed for these tasks. Currently the package downloads and processes standardized European SIOTs conforming to the latest statistical regulations, i.e. SIOTs starting from the year 2010.

In order to test the analytical functions of the package and to have a manageable sized example data set, we use the real-life data from the Eurostat manual. The calculation of induced effects (Type-II multipliers) are following the Input-Output Multipliers Specification Sheet and Supporting Material, Spicosa Project Report. The analytical functions are tested against this example, too.
