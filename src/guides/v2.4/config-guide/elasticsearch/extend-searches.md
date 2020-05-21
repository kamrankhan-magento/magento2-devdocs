---
group: configuration-guide
title: Extend partial searches in Elasticsearch
functional_areas:
  - Configuration
  - Search
  - System
  - Setup
---

Shoppers can perform quick searches using partial words
With the 2.4.0 release, the Quick Search in Magento will have the ability to perform partial searches via elastic search. This will enable shoppers to search for partial words and get relevant results so that they can find the products they're looking for on storefront and drive more sales.

The partial search is enabled by default on 2 attributes - name and sku. It leverages "match_phrase_prefix" from elastic to perform prefix matches on the last terms of the text.  It is still possible to add attributes in search_request.xml with a matchCondition "match_phrase_prefix" in order to make them to be considered by partial search.

Some Examples:

Searching for "Hood" will return products with name "Hooded Fleece", "Pullover Hoodie",..
Searching for "Run" will return products with sku "RUNSH-01", "M-RUNNING-SHOE",..

This feature is also enabled for GraphQL while searching for products with the Products query.

The keywords used on the "search" attribute will be considered for partial search.