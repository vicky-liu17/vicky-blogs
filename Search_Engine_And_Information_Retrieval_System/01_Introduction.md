# Introduction

### Information Retrieval(IR)

Finding relevant information
- in unstructured large sets of material (usually documents),
- satisfying an information need of the user.

### What IR is not
- An IR system is not a database system
- Databases
    - are structured
        - IR systems typically deal with unstructured or loosely structured data, such as text documents, web pages, or multimedia content. The focus is on understanding the meaning and context of the content.
        - Database systems handle structured data with predefined schemas, allowing for efficient storage, retrieval, and manipulation of data with well-defined relationships.
    - allow for exact search
        - IR systems often use relevance ranking algorithms to present search results in order of relevance to the user query. The goal is to provide the most relevant information, even if it doesn't exactly match the query.
        Database systems typically return exact matches to queries based on the structured data stored in the database.
- IR is inexact in several regards:
    - information need, search query, relevance

### Example IR Systems:
- in search engine
- in operating systems
- in e-mail programs

## Some Key Ideas

![](Pictures/introduction01.jpg)

![](Pictures/introduction02.jpg)

- Relevance measures how well the retrieved documents meet the information needs of the user. A document is considered relevant if it contains information that is pertinent and useful to the user's query.

- Recall, also known as sensitivity or true positive rate, measures the ability of the system to retrieve all relevant documents in the collection for a particular query.
    - It is calculated as the ratio of the number of relevant documents retrieved to the total number of relevant documents in the collection. The formula for recall is:  $\text{Recall} = \frac{\text{Number of Relevant Documents Retrieved}}{\text{Total Number of Relevant Documents}}$

- **Precision-Recall Trade-off:** Precision and recall are often considered together as part of the precision-recall trade-off. Precision focuses on the correctness of the retrieved documents, while recall emphasizes the completeness of the retrieval.

![](Pictures/introduction03.jpg)

- An inverted index is a data structure used in information retrieval systems to efficiently map terms (words or tokens) to the documents or records that contain them. It is a crucial component of search engines and other systems that need to quickly locate documents relevant to a user's query.




### Extensions
A search engine needs some extensions to be truly useful:
- Query completion
- Spell checking
- (Wildcard queries)
- NLP: treating synonyms, inflections, derivations, compound words, etc.
- Information extraction (for snippets)
- Clustering

![](Pictures/introduction04.jpg)

![](Pictures/introduction05.jpg)

### More extensions

- Nowadays, modern search engines also contain this:
    - Support for multiple languages and alphabets
    - Multimedia indexing (video, images, news, ... )
    - Direct question-answering
    - Personalized ranking function
    - Collaborative filtering and recommendation

- We will explore some of these ideas in the projects.

### An early search engine
- 早期：门户网站-雅虎 Portal
- An early search engine - AltaVista(Do not do ranking)