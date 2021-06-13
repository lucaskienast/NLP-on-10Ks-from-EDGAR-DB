# Algotrading NLP on 10-K's
This is an algotrading sentiment trading strategy, written in Python, and applying NLP on 10-K's from the SEC EDGAR database. It works in the follwing way:
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
