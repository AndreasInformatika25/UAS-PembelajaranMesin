# Integration of Topic Modeling, Social Network Analysis, and NER on Online Loan (Pinjol) Victim Cases

## 📌 Project Description
This repository contains the documentation and implementation code for the Final Semester Examination (UAS) in the Machine Learning course. The project focuses on integrating three distinct text analysis approaches: *Topic Modeling*, *Social Network Analysis* (SNA), and *Named Entity Recognition* (NER) to comprehensively dissect public opinion surrounding the core theme of "Korban Pinjol" (Online Loan Victims).

## 🛠️ Data Collection (Crawling)
Data was systematically scraped from Twitter (X), yielding a total of 1,538 raw tweets/data entries stored in Excel format.

The data retrieval process was conducted using a specific set of target keywords:
* gagal bayar pinjol (online loan default)
* pinjol galbay (loan default)
* dc lapangan pinjol (loan field debt collectors)
* sebar data pinjol (loan data shaming/breach)
* korban pinjol (online loan victims)

## 🧹 Data Preprocessing
To ensure the data was fully prepared for model injection, a systematic preprocessing pipeline was implemented:
1. **Duplicate Removal:** Eliminating redundant and identical tweets.
2. **Case Folding:** Standardizing all text characters into lowercase.
3. **Data Cleaning:** Stripping out RT tags, URLs/hyperlinks, user mentions, special characters, emojis, and excess whitespaces.
4. **Attribute Extraction:** Isolating handles into the *author* column and extracting specific *mentions* required to construct the SNA network graph.
5. **Tokenization:** Splitting continuous text into individual word tokens using the NLTK library.
6. **Normalization:** Correcting slang and non-standard words using a combination of an external mapping dictionary (CSV) and manual overrides.
7. **Stop Word Removal:** Filtering out conjunctions and meaningless words using NLTK, a custom CSV list, and a domain-specific filter refined for online loan contexts.
8. **Stemming:** Reducing words to their morphological base form using the Sastrawi library.

## ⚙️ Methodology & Results
### 1. Topic Modeling
This project evaluates and compares the performance of two text clustering algorithms:
* **Frequent Term-Based Text Clustering (FTC):** Utilizes frequent termsets extraction and *Entropy Overlap* calculation using the formula $EO(C_{i})=\sum_{D_{j}\in C_{i}}\frac{-1}{f_{j}}.Ln(\frac{1}{f_{j}})$ to evaluate final cluster quality. The model was executed with a *minimum support* (`minsup`) parameter of 0.05.
* **Latent Dirichlet Allocation (LDA):** A probabilistic generative model evaluated via the *Elbow Perplexity* metric. Based on the generated perplexity curve, an optimal value of K=3 was discovered:
  * **Topic 1:** Debt Collector Terror & Online Loan Victims
  * **Topic 2:** Debt, Credit & Economic Hardships
  * **Topic 3:** Reporting Illegal Loans & Wider Social Impacts

### 2. Social Network Analysis (SNA)
Implemented to map out and analyze the interaction dynamics (mentions) between distinct user accounts interacting within the online loan topic.
* **Visualization & Tools:** Processed data was exported into structured `edge_list.csv` and `node_list.csv` files to be visualized in Gephi, and rendered interactively using the PyVis library.
* **Centrality Metrics:**
  * Top Most Mentioned Accounts (*Indegree*): `@ojkindonesia` (0.0187) and `@prabowo` (0.0156).
  * Top Most Active Mentioning Accounts (*Outdegree*): `@belengbeleng687` (0.0374) and `@divhumas_polri` (0.0234).
* The graph analysis within Gephi successfully achieved a *Community Detection* modularity score of 0.929.

### 3. Named Entity Recognition (NER)
Extracts key domain entities using two parallel methods for a robust comparative assessment:
* **NER SpaCy Indonesian:** Utilizes the pre-trained `id_ner_spacy_indonesian` model pipeline to extract entities based on ORG, GPE, PERSON, NOR, and LOC labels.
* **NER Rule-Based:** Relies on tailored Regex regular expressions combined with a *Custom Dictionary* targeting key terms (e.g., 'ojk', 'polisi', 'bpjs', etc.).
* **NER Conclusion:** The *Rule-Based* approach demonstrated a significantly higher and more contextually accurate entity extraction count (capturing entities such as "Indonesia", "Bpjs", and "Ojk") compared to the generic SpaCy pipeline.

## 🧑‍💻 Author
* **Name / NIM:** Andreas / 2411500750
