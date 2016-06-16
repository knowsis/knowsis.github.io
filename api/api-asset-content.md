---
title: Asset Content
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-asset-content/
---

The Asset Content endpoint returns a list of the most shared content from across the internet. The default view is the last 24 hours of content.

For API consumers that have licensed our historical asset content data there are optional parameters to get content for a specified date range:


| Parameter         | Format   | Description                                                   |
|-------------------|----------|---------------------------------------------------------------|
| startdate         | datetime | the start of the requested range                              |
| enddate           | datetime | the end of the requested range                                |



```
GET /assets/{identifier}/content/
```

## Example request/response

```
GET https://api.knows.is/assets/ADM.L/content
Accept: application/json, text/javascript
```

```

{
    "content": [
        {
          "url": "http://www.tickerreport.com/banking-finance/1858357/admiral-group-unsp-adr-each-repr-1-amigy-stock-rating-upgraded-by-berenberg-bank/",
          "article": {
            "author": "@RatingsNetwork",
            "image": "http://www.tickerreport.com/logos/generic-stocks4.jpg",
            "title": "ADMIRAL GROUP UNSP ADR EACH REPR 1 (AMIGY) Stock Rating Upgraded by Berenberg Bank - Ticker Report",
            "lead_text": "ADMIRAL GROUP UNSP ADR EACH REPR 1 (OTC:AMIGY) was upgraded by equities researchers at Berenberg Bank from a “sell” rating to a “hold” rating in a report released on Thursday, StockTargetPrices.com reports. ADMIRAL GROUP UNSP ADR EACH REPR 1 (OTC:AMIGY) opened at 27.63 on Thursday. The company has a market capitalization of $7.37 billion and […]",
            "published_date": "2016-06-13 05:07:04+00:00",
            "icon": "http://www.tickerreport.com/favicon.ico"
          },
          "domain": "www.tickerreport.com",
          "share_count": 2
        },
        {
          "url": "http://sleekmoney.com/berenberg-bank-reiterates-hold-rating-for-admiral-group-unsp-adr-each-repr-1-amigy/1284096/",
          "article": {
            "author": "@RatingsNetwork",
            "image": "http://sleekmoney.com/logos/admiral-group-plc-logo.jpg",
            "title": "Berenberg Bank Reiterates “Hold” Rating for ADMIRAL GROUP UNSP ADR EACH REPR 1 (AMIGY) – sleekmoney",
            "lead_text": "ADMIRAL GROUP UNSP ADR EACH REPR 1 (OTCMKTS:AMIGY)‘s stock had its “hold” rating reiterated by Berenberg Bank in a research note issued to investors on Thursday. A number of other equities analysts have also recently commented on the company. Nomura raised ADMIRAL GROUP UNSP ADR EACH REPR 1 from a “neutral” rating to a “buy” […]",
            "published_date": "2016-06-13 09:04:58+00:00",
            "icon": "http://sleekmoney.com/wp-content/themes/newsplus/images/favicon.ico"
          },
          "domain": "sleekmoney.com",
          "share_count": 1
        },
    ],
    "startdate": "2016-06-14T00:00:00",
    "identifier": "ADM.L",
    "enddate": "2016-06-13T00:00:00",
    "name": "Admiral Group PLC"
}

```