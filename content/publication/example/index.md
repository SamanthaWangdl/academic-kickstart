---
title: "Maximizing the Smallest Eigenvalue of Grounded
Laplacian Matrix by Node Selection"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- admin


date: "2021-05-15T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: ""

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: IEEE Transaction on Cybernetics(Under Review)
publication_short: In *ICW*

abstract: The smallest eigenvalue of a grounded Laplacian matrix plays a pivotal role in complex networks, such as system control, convergence rate and the robustness of a system. In this paper, we focus on the node selection problem of maximizing the smallest eigenvalue of the grounded Laplacian matrix for a graph with n nodes and m edges, under an upper bound constraint k ≪ n. We show this combinatorial optimization problem is NP-hard and the objective function is monotone but non-submodular. Since the optimal solution cannot be calculated directly, we adopt a greedy strategy to solve this problem by selecting one node at a time. Specifically, we employ derivatives and matrix perturbations to make our algorithm efficient with a time complexity of O ̃(km), where O ̃(·) notation suppresses the poly(log n) factors, and also applicable to large-scale networks. We conduct numerous experiments on different networks of various sizes to demonstrate the superiority of our algorithm in terms of efficiency and effectiveness compared to other methods.

# Summary. An optional shortened abstract.
summary: We show this combinatorial optimization problem is NP-hard and the objective function is monotone but non-submodular.Specifically, we employ derivatives and matrix perturbations to make our algorithm efficient with a nearly-linear time complexity.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: ''
url_code: 'https://github.com/SamanthaWangdl/grounded_laplacian_eigenvalue'
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- 'GR'

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.

---
