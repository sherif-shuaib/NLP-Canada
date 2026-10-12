# Analyzing Reddit and Facebook Social Media Content on Canadian Fishers' and Fishing Communities' Attitudes Toward Species Range Shifts: 
#A Sentiment and Topic Modeling Study

## Overview

This repository contains code used to analyze social media discussions concerning Canadian fishers' and fishing communities' attitudes toward species range shifts. The uploaded notebook documents the Reddit analysis, including text preprocessing, topic modelling, sentiment and emotion analysis, statistical comparisons among topics, and temporal trend analysis.

The workflow combines natural language processing, Latent Dirichlet Allocation (LDA), PySentimiento-based sentiment analysis, and statistical tests to characterize patterns in social media discourse.

## Repository Contents

- `Reddit_Topic Modeling.ipynb` — Jupyter notebook containing the Reddit text-processing, topic-modelling, sentiment, emotion, and temporal-trend analyses.

> Note: This README is based on the uploaded Reddit notebook. Facebook analysis also follows a similar pattern.

## Analysis Workflow

The notebook performs the following main steps:

### 1. Data Import and Preparation

The Reddit dataset is imported from a CSV file and processed using the `CleanedText` field. Missing text records are removed and the dataframe index is reset.

### 2. Text Preprocessing

Text preprocessing includes:

- emoji removal;
- English stop-word removal;
- punctuation removal;
- lemmatization using spaCy;
- retention of nouns, adjectives, and verbs during lemmatization;
- tokenization with NLTK; and
- removal of short tokens.

### 3. TF-IDF Representation

The processed text is transformed using `TfidfVectorizer`. The notebook specifies:

- English stop words;
- `max_df = 0.75`;
- `min_df = 50`;
- `use_idf = True`; and
- `norm = None`.

The fitted vectorizer and TF-IDF matrix can be saved for reuse.

### 4. Topic-Number Evaluation

Candidate LDA solutions are evaluated across a range of topic numbers using measures that include:

- perplexity;
- topic coherence (`c_v`); and
- topic similarity/separation measures.

### 5. Latent Dirichlet Allocation Topic Modelling

The main Reddit topic model is fitted using scikit-learn's `LatentDirichletAllocation` with:

- 18 topics;
- online learning;
- `learning_offset = 50`;
- `random_state = 111`; and
- parallel processing with `n_jobs = -1`.

The notebook extracts the most important terms for each topic and assigns each record to its dominant topic based on the highest topic probability.

The retained Reddit topics used in later analyses are:

- Topic 1 — Overfishing & Climate
- Topic 3 — Habitat & Regulations
- Topic 4 — Climate Futility
- Topic 8 — Pollution Concern
- Topic 9 — Advocacy Critique
- Topic 10 — Governance Failure
- Topic 11 — Carbon Tax Debate

### 6. Topic Visualization and Inspection

The notebook includes:

- interactive LDA visualization using `pyLDAvis`;
- inspection of high-confidence records within topics;
- word clouds for retained topics; and
- manual examination of representative text.

### 7. Sentiment Analysis

Sentiment analysis is performed using the English PySentimiento sentiment model.

For each record, the notebook obtains probabilities for:

- Positive (`POS`);
- Neutral (`NEU`); and
- Negative (`NEG`).

The dominant sentiment is assigned from the highest of the three probabilities.

### 8. Emotion Analysis

Emotion scores are used to identify the dominant emotion for each record from:

- Other;
- Anger;
- Disgust;
- Fear;
- Sadness;
- Joy; and
- Surprise.

These emotions are also collapsed into broader categories:

- **Positive** — Joy
- **Negative** — Anger, Disgust, Fear, Sadness
- **Neutral** — Other, Surprise

### 9. Topic–Sentiment and Topic–Emotion Comparisons

The notebook constructs contingency tables to compare sentiment and emotion distributions among topics. Analyses include:

- chi-square tests of independence;
- standardized residuals;
- one-way ANOVA;
- Kruskal–Wallis tests; and
- post-hoc comparisons using `scikit-posthocs`.

### 10. Temporal Trend Analysis

Sentiment is aggregated over time and examined using several approaches, including:

- Mann–Kendall trend tests;
- Seasonal Mann–Kendall tests;
- trend slopes;
- Spearman rank correlations; and
- Augmented Dickey–Fuller tests for stationarity.

The notebook also produces time-series visualizations of negative sentiment and other sentiment measures by topic.

## Software and Main Dependencies

The notebook uses Python and the following main packages:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scipy`
- `scikit-learn`
- `nltk`
- `spacy`
- `en_core_web_md`
- `gensim`
- `tmtoolkit`
- `pyLDAvis`
- `pysentimiento`
- `wordcloud`
- `emoji`
- `tqdm`
- `pymannkendall`
- `scikit-posthocs`
- `statsmodels`

The notebook output records Python **3.12.4** and pandas **1.5.3** for the environment in which those version checks were run.

## Installation

A typical environment can be prepared with:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn nltk spacy gensim tmtoolkit pyLDAvis pysentimiento wordcloud emoji tqdm pymannkendall scikit-posthocs statsmodels
python -m spacy download en_core_web_md
```

Some package versions may need to be adjusted to reproduce the original environment exactly.

## Data Requirements

The notebook expects a Reddit CSV dataset containing, at minimum, a cleaned-text field named:

```text
CleanedText
```

Several later analyses also use variables such as:

```text
Date
created_utc
id
Positive
Neutral
Negative
Other
Anger
Disgust
Fear
Sadness
Joy
Surprise
```

The exact columns required depend on which sections of the notebook are executed.

## File Paths

The notebook contains local file paths from the original analysis environment, including paths for:

- the Reddit CSV dataset;
- the saved TF-IDF vectorizer;
- the saved TF-IDF sparse matrix; and
- the saved LDA model.

These paths must be changed to match the directory structure on the user's computer or repository before the notebook can be run elsewhere.

## Reproducibility

Random seeds are specified for major topic-modelling steps, including:

```python
random_state=111
```

and, in an additional Gensim LDA workflow:

```python
random_state=42
```

For reproducible results, users should also record the exact package versions used in the final analysis environment.

## Outputs

The notebook generates outputs including:

- candidate topic-model evaluation statistics;
- topic-term lists;
- dominant-topic assignments;
- topic-confidence scores;
- sentiment probabilities and labels;
- emotion classifications;
- topic-by-sentiment and topic-by-emotion contingency tables;
- chi-square statistics and standardized residuals;
- non-parametric and parametric topic comparisons;
- temporal trend-test results;
- topic word clouds; and
- sentiment and emotion visualizations.

## Citation

If this repository is used in association with the manuscript, please cite:

**Shuaib, S. E., et al.** *Analyzing Reddit and Facebook Social Media Content on Canadian Fishers' and Fishing Communities' Attitudes Toward Species Range Shifts: A Sentiment and Topic Modeling Study.*



## Contact

For questions concerning the analysis or code, please contact the corresponding author through the contact information provided in the associated manuscript.
