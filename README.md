# New Deduplication

## Introduction
The goal of this project is to deduplicate and aggregate news articles on similar topics to present users with concise summaries, reducing redundancy and enhancing information relevance.
Articles on the same topic often contain repetitive information. This system clusters articles on similar themes and summarizes them to produce a digestible overview for users.

## Libraries
requests, beautifulsoup4, scikit-learn, and nltk are used for web scraping, data processing, clustering, and summarization.
NLTK Downloads: Additional NLTK data files, specifically punkt for sentence tokenization and stopwords for filtering common English words.

## System Workflow
The code follows a sequence of steps that build on each other to achieve the desired deduplication and summarization:
Fetching and storing article content.
Text preprocessing and vectorization.
Clustering similar articles.
Summarizing each cluster.

## Process Explanation
### Step 1: Data Collection - Fetching Articles
The function uses requests to retrieve HTML content from each article's URL.
BeautifulSoup parses the content to extract text within <p> tags, combining paragraphs into a single article string.
Articles are stored in a list for further preprocessing.
### Step 2: Preprocessing and Vectorization
Prepare the text data by removing common English stop words and transforming it into a format suitable for similarity comparison.
Preprocessing Method:
The function filters out stop words from each article, converts words to lowercase, and removes common filler words.
Vectorization Method:
The TfidfVectorizer from scikit-learn computes term frequency-inverse document frequency (TF-IDF) scores for each word.
The resulting TF-IDF matrix represents each article as a vector in multi-dimensional space, enabling similarity calculation.
### Step 3: Similarity Computation
The cosine_similarity function calculates the cosine similarity between articles, creating a similarity matrix. Cosine similarity is effective for text comparison as it measures the angle between two vectors, indicating how closely related they are in content.
### Step 4: Clustering Articles
Using K-means clustering, the articles are grouped based on their vector representations. The number of clusters (num_clusters) is set to 3 but can be adjusted based on the dataset.
Each article is assigned a cluster label based on its similarity to other articles within the same group.
### Step 5: Summarization of Articles within Each Cluster
Sentence Tokenization: Split the text of each cluster into individual sentences.
Frequency Distribution: Compute word frequencies to identify key terms within the cluster text.
Sentence Ranking: Rank sentences based on the cumulative frequency of words they contain.
Summary Creation: Select the top-ranked sentences (three in this case) to form a concise summary of each cluster.
### Step 6: Displaying Clustered Summaries
Present the final summaries for each topic cluster.

## Conclusion
This deduplication and summarization system effectively groups articles on similar topics and generates summaries for each group.
### Limitations:
The fixed number of clusters may not dynamically adapt to varied topic distributions.
Summarization relies on frequency-based ranking, which may overlook less frequent but significant information.
### Future Improvements:
Implement dynamic topic modeling to adjust cluster numbers.
Use advanced summarization techniques like transformer-based models for better context retention.
