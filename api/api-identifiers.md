---
title: Identifiers
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-identifiers/
---


## Asset Identifiers

We support several publicly available identifiers for retrieving details of the assets that we track. A full list of available identifiers can be found using the /assets/ endpoint to fetch a list of all assets.

The following common ticker symbol formats are currently supported in requests for individual assets:

```
AAPL:US
AAPL.0
NASDAQ:AAPL
APPL
```

we also support the most common social media format, the Twitter cashtag:

```
$GOOG
```

and International Securities Identification Numbers (ISIN): 

```
US0378331005
```

Macro and asset driver topics do not have a ticker symbol or ISIN code so you will need to refer to these by the Knowsis proprietary identifiers which can be found by calling the `/assets/` endpoint. 



### Notes 

As some identifiers may contain reserved characters, you should ensure that the identifier has been url encoded before being sent to the API.