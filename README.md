# Algotrading NLP on 10-K's
In this project, NLP Analysis was carried out on 10-k financial statements to generate an alpha factor. For the dataset, the end of day from Quotemedia and Loughran-McDonald sentiment word lists were used.

## Installation
Use `git clone` to get a copy of this repository.

```
$ git clone https://github.com/lucaskienast/algotrading_NLP_on_10Ks.git
$ cd algotrading_random_forest_enhanced_alpha
```

## Method
- define list of public companies and get their CIK's
- use `BeautifulSoup` to get XML files for each CIK
- download _complete submission text file_ for all CIK's with `sec_edgar_downloader`
- use `re` to get text content between `<DOCUMENT>` tags where `<TYPE>` is '10-k'
- use `BeautifulSoup` to remove `<HTML>` tags and convert to lower case
- lemmatize verbs using `nltk.stem.WordNetLemmatizer`
- remove stopwords using `nltk.corpus.stopwords`
- get _Loughran-McDonald_ sentiment word list and lemmatize it
- generate bag of words that counts number of sentiment words in each 10-K via `sklearn.feature_extraction.text.CountVectorizer`
- compute _Term Frequency Inverse Document Frequency_ (TFIDF) via `sklearn.feature_extraction.text.TfidfVectorizer`
- compute cosine similarity to evaluate change in TFIDF over time using `sklearn.metrics.pairwise.cosine_similarity`
- get stock data using `zipline`
- implement cosine similarities as alpha factors and analyse factor returns using `alphalens`
- compute Sharpe ratio for each sentiment factor

## Results
Alpha factors (negative, positive, uncertainty, litigous, constraining, and interesting) do not display monotonicity in quantiles of factor returns. The sentiment word _litigous_ achieved the highest Sharpe ratio at 2.23.
