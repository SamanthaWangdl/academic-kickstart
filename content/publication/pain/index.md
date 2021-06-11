---
title: "Hybrid  RNN-ANN  Based  Deep  Physiological  Network  for  PainRecognition"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- admin


date: "2021-05-15T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2020-07-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: IEEE EMBC 2020
publication_short: In *ICW*

abstract: Quantitative  assessment  of  pain  is  vital  progressin treatment choosing and distress relief for patients. However,previous approaches based on self-report fail to provide objec-tive and accurate assessments. For impartial pain classificationbased on physiological signals, a number of methods have beenintroduced using elaborately designed handcrafted features. Inthis  study,  we  enriched  the  methods  of  physiological-signal-based pain classification by introducing deep Recurrent NeuralNetwork (RNN) based hybrid classifiers which combines auto-extracted features with human-experience enabled handcraftedfeatures.  A  bidirectional  Long  Short-Term  Memory  network(biLSTM)  was  applied  on  time  series  of  pre-processed  signalsto  automatically  learn  temporal  dynamic  characteristics  fromthem.  The  handcrafted  features  were  extracted  to  fuse  withRNN-generated features. Finely selected features from biLSTMlayer  output  and  handcrafted  features  trained  an  ArtificialNeural Network (ANN) to classify the pain intensity. The hand-crafted  features  enhance  the  RNN  classification  performanceby complementing RNN-generated features. With our accuracyreaching  83.3%,  comparison  results  on  an  open  dataset  withother  methods  show  that  the  proposed  algorithm  outperformsall of the previous researches with higher classification accuracy.Therefore, this research is a good demonstration of introducinghybrid  features  for  pain  assessment.

# Summary. An optional shortened abstract.
summary: Quantitative  assessment  of  pain  is  vital  progressin treatment choosing and distress relief for patients. However,previous approaches based on self-report fail to provide objec-tive and accurate assessments. In this  study,  we  enriched  the  methods  of  physiological-signal-based pain classification by introducing deep Recurrent NeuralNetwork (RNN) based hybrid classifiers which combines auto-extracted features with human-experience enabled handcrafted features.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: ''
url_code: ''
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
