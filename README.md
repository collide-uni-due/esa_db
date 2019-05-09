# esa_db

This is a SQLite database containing an index that can be used for explicit semantic analysis [https://en.wikipedia.org/wiki/Explicit_semantic_analysis]. The index was generated from a Wikipedia dump in April 2019.

The database dump can be downloaded at: [https://uni-duisburg-essen.sciebo.de/s/kYNVLdrE7KycpSJ]

## DB structure

![database schema][db_schema.png]

**terms** contains all the terms and their corresponding indexes. **Note** Terms are stemmed using Porter stemming.
**articles** contains all Wikipedia articles and ids.
**term_article_score** gives for each term-article pair the corresponding tf_idf score of the term for that article.

**Querying the ESA vectors for single (stemmed) term**

```SQL
SELECT t.term, a.article, s.tf_idf
  FROM terms t, term_article_score s, articles a
  WHERE t.term like 'physic' 
  AND t.id = s.term_id AND a.id = s.article_id
  ORDER BY s.tf_idf DESC;
```


## How to use it
Queries 

### From command line
1. Download the appropriate prebuild binary sqlite-tools-... for your platform.
2. Unzip everything into a new folder, e.g. sqlite
3. Open a console and navigate to the folder. You start the command line tool by typing sqlite3

### From R
Install the lates RSQLite package (if not already installed). 
```R
install.packages("RSQLite")
```



### From python
