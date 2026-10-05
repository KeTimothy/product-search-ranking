# Product Search Ranking
A product search ranking system built on Home Depot product search dataset obtained from Kaggle. The project uses lexical retrieval, dense retrieval, hybrid retrieval, and Learning-to-Rank methods for improving search relevance.

## Overview
The system takes a query and return a ranking of items from the catalog based on the relevance to the query. 

The project explores several methods listed down.

- **BM25** for lexical retrieval
- **Dense retrieval** using Sentence-Transformers
- **Reciprocal Rank Fusion (RRF)** to combine BM25 and Dense into Hybrid
- **LambdaMART** for Learning-to-rank, with later additional features

## Dataset
The data is obtained from [Home Depot Product Search Relevance Kaggle competition](https://www.kaggle.com/competitions/home-depot-product-search-relevance/data). 

It contains:
- 86k+ product in product catalogs
- Product ID, title, description, attribute name and attribute value
- 11k+ unique queries
- For search term used, its paired with product ID and their corresponding relevance score, from 1.0 (irrelevant) to 3.0 (highly relevant) provided by human raters

## Models
### BM25
BM25 is the baseline for lexical retrieval. It basically tries to find token matches from the search term in product titles, description and attributes.

### Dense Retrieval
Dense retrieval utilize Sentence-Transformers to encode queries and product information into vector, then compute their cosine distance (similarity) to retrieve similar products.

### Hybrid Retrieval
Hybrid combines the BM25 and Dense by using Reciprocal Rank Fusion (RRF).

## Learning-to-Rank
In addition to hybrid retrieval, LambdaMART is also trained using BM25 and Dense scores.

Then additional features are generated to further improve the model. These features are:
- Token overlap
- Jaccard similarity
- Whether all query terms occur in the product title

## Result
|**Method**             |**NDCG@3**|**NDCG@5**|
|-------------------------|----------|----------|
|BM25                     |0.8821    |0.9110    |
|Dense                    |0.8813    |0.9105    |
|RRF                      |0.8813    |0.9105    |
|LambdaMART               |0.8809    |0.9089    |
|**LambdaMART + features**|**0.8990**|**0.9226**|