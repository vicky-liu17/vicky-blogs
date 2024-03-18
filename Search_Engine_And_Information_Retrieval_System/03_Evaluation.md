# Evaluation

### Evaluation in Information Retrieval
- How do we know if our search engine is any good?
    - Benchmarks
    - Precision and recall
    - Various measures based on precision and recall

### Measures for a search engine
- How fast does it index
    - Number of documents/hour
    - (Average document size)
- How fast does it search
    - Latency as a function of index size
- Expressiveness of query language
    - ability to express complex information needs
    - Speed on complex queries
- Uncluttered UI整洁的用户界面
- Is it free? Is it open sourse?

### What really matters
- All of the preceding criteria are measurable: we can quantify speed/size
    - we can make expressiveness precise
- The key measure: **user happiness**
    - What is this?
    - Speed of response/size of index are factors
    - But blinding fast useless answers won't make a user happy 盲目迅速的无用答案不会让用户满意
- Need a way of quantifying user happiness

### User happiness
- Web engine:
    - User finds what s/he wants and returns to the engine
        - Can measure rate of return users
    - User completes task – search as a means, not end 让用户去完成一些需要通过搜索来完成的任务，看用户是否能够达到目的
- eCommerce site: user finds what s/he wants and buys
    - Is it the end-user, or the eCommerce site, whose happiness we measure?
    - Measure time to purchase, or fraction of searchers who become buyers?
- Enterprise (company/govt/academic): Care about “user productivity”
    - How much time do my users save when looking for information?我的用户在查找信息时节省了多少时间？
    - Many other criteria having to do with breadth of access, secure access, etc 许多其他与访问范围、安全访问等有关的标准

### Happiness: difficult to measure
- Most common proxy: relevance of search results
- But how do you measure relevance?
- Relevance measurement requires 3 elements:
    1. A benchmark document collection
    2. A benchmark suite of queries
    3. A (usually binary) assessment of either Relevant or Nonrelevant for each query and each document… or a score 0-3 representing degree of relevance

