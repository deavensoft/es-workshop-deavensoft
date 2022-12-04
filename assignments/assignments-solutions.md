# Assignments Solutions

## Assignment 2
```
#  2-1
GET /drinks/_search?q=name:Cosmopolitan

#  2-2
GET /drinks/_search?q=ingredients:tequila

#  2-3
GET /drinks/_search?q=ingredients:(orange cranberry)

#  2-4
GET /drinks/_search?q=ingredients:(+vodka -cranberry)

#  2-5
GET /drinks/_search?q=ingredients:(+vodka -cranberry lemonade)

#  2-6
GET /drinks/_search?q=%2Bingredients:whiskey %2Bgarnish:cherry

#  2-7
POST /drinks/_doc
{
  "name": "Gree Beast",
  "ingredients": "absinthe, lime juice, syrup, water",
  "glass": "regular",
  "strength": "medium",
  "garnish" : "cucumber"
}
```

## Assignment 3

```
#  3-1
DELETE blog

PUT blog
{
  "settings": {
    "analysis": {
      "analyzer": {
        "comma-delimited-analyzer": {
          "tokenizer": "my_tokenizer"
        }
      },
      "tokenizer": {
        "my_tokenizer": {
          "type": "pattern",
          "pattern": ","
        }
      }
    }
  }
}


#  3-2
PUT blog/_mapping
{
  "properties" : {
	"title" : {
	  "type" :    "text",
	  "analyzer": "english"
	},
	"article_text" : {
	  "type" :    "text",
	  "analyzer": "english"
	},
	"author_email" : {
	  "type" :   "keyword"
	},
	"publish_date" : {
	  "type" :   "date"
	},
	"article_id" : {
	  "type" :   "long"
	},
          "tags" : {
              "type" : "text",
	  "analyzer" : "comma-delimited-analyzer"
          }
  }
}

GET blog/_mapping
```

## Assignment 4
```
#  4-1
GET tweets/_search
{
  "query": {
    "match": {
      "author": "@venkat_s"
    }
  }
}


#  4-2
GET tweets/_search
{
  "query": {
    "match": {
      "tweet_text": "java website"
    }
  }
}


#  4-3
GET tweets/_search
{
  "query": {
    "bool": {
      "must": { "match" : {"tweet_text":"java"}},
      "must_not": { "match" : {"tweet_text":"arduino"}}
    }
  }
}


#  4-4
GET tweets/_search
{
  "query": {
    "range": {
      "tweet_date": {
        "gte": "2017-12-01",
        "lte" : "2017-12-31"
      }
    }
  }
}


#  4-5
GET tweets/_search
{
  "query": {
    "match_all": {}
  },
  "size": 2
}


#  4-6
GET tweets/_search
{
  "query": {
    "bool": {
      "must": { "match" : {"tweet_text":"thing"}},
      "filter" : {"range": {
        "tweet_date": {
          "gte" : "2016-01-01",
          "lte" : "2016-12-31"
        }
      }}
    }
  }
}
```

## Assignment 5

```
# 5-1
GET shop/_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "category": "shoes"
        }
      },
      "should": [
        {
          "match": {
            "brand": {
              "query": "Nike",
              "boost": 2
            }
          }
        }
      ]
    }
  }
}


#  5-2
GET shop/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      },
      "should": {
        "range" : {
          "inventory_amount" : {
            "gte" : 30,
            "boost" : 2
          }
        }
      }
    }
  }
}
```

# Assignment 6

```
#  6-1
GET future-bank/_search?size=0
{
    "aggs" : {
        "age_ranges" : {
            "range" : {
                "field" : "age",
                "ranges" : [
                    { "to" : 30 },
                    { "from" : 30, "to" : 40 },
                    { "from" : 40, "to" : 50 },
                    { "from" : 50 }
                ]
            }
        }
    }
}


#  6-2
GET future-bank/_search
{
   "size" : 0,
    "aggs" : {
        "age_ranges" : {
            "range" : {
                "field" : "age",
                "ranges" : [
                    { "to" : 30 },
                    { "from" : 30, "to" : 40 },
                    { "from" : 40, "to" : 50 },
                    { "from" : 50 }
                ]
            },
            "aggs" : {
              "avg_balance" : {
                "avg" : {
                  "field": "balance"
                }
              }
            }
        }
        
    }
}
```
