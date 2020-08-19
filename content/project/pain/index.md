+++
# Project title.
title = "Hybrid RNN-ANN Based Deep Physiological Network for Pain Recognition"

# Date this page was created.
date = 2020-07-27T00:00:00

# Project summary to display on homepage.
summary = "In this study, we enriched the methods of physiological-signal- based pain classification by introducing deep Recurrent Neural Network (RNN) based hybrid classifier."

# Tags: can be used for filtering projects.
# Example: `tags = ["economic-impact", "r-package"]`
tags = ["Pain Monitoring with Physiological Signal"]

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
url_code = "https://github.com/SamanthaWangdl/painrnn"

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

Quantitative assessment of pain is vital progress in treatment choosing and distress relief for patients. However, previous approaches based on self-report fail to provide objec- tive and accurate assessments. For impartial pain classification based on physiological signals, a number of methods have been introduced using elaborately designed handcrafted features. In this study, we enriched the methods of physiological-signal- based pain classification by introducing deep Recurrent Neural Network (RNN) based hybrid classifiers which combines auto- extracted features with human-experience enabled handcrafted features. A bidirectional Long Short-Term Memory network (biLSTM) was applied on time series of pre-processed signals to automatically learn temporal dynamic characteristics from them. The handcrafted features were extracted to fuse with RNN-generated features. Finely selected features from biLSTM layer output and handcrafted features trained an Artificial Neural Network (ANN) to classify the pain intensity. The hand- crafted features enhance the RNN classification performance by complementing RNN-generated features. With our accuracy reaching 83.3%, comparison results on an open dataset with other methods show that the proposed algorithm outperforms all of the previous researches with higher classification accuracy. Therefore, this research is a good demonstration of introducing hybrid features for pain assessment.

{{< figure library="true" src="pain2.jpg" title="Nerwork Structure" >}}

{{< figure library="true" src="pain1.jpg" title="Result" >}}