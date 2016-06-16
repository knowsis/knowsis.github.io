---
title: Overview
tags: [overview]
sidebar: api_sidebar
type: homepage
permalink: /
---


The Knowsis API allows developers to add Knowsis analytics to their website and applications. Knowsis sentiment data is derived from 1000s of online sources and is generated through our own proprietary machine learning algorithms. 

We make the sentiment of 100s of publicly traded assets (equities, commodities, indices, forex pairs) and non tradable assets (macro drivers, pre IPO companies etc) available.

## Technical Overview

Our API is accessible via HTTPS, is RESTful, and offers JSON response formats (find the schema below). All data responses are UTF-8 encoded.

We presently offer sentiment data for the current day.

Times and dates are provided in UTC timezone and are in ISO 8601 format.



## Authentication
We use OAuth for authentication. As all resources are protected, you must sign every request you make using your API consumer key and secret, as per the OAuth Consumer Request 1.0 Draft 1 specification. We strongly recommend using an existing OAuth library. The [oauth.net](http://www.oauth.net/code) website lists suggested libraries by language.

The following parameters MUST appear in every request:

+ **oauth_consumer_key** - The consumer key provided to you by Knowsis
+ **oauth_nonce** - A random string of characters that differs from call to call (this helps to prevent replay attacks) be sure to make these characters legal (percent-encoded)
+ **oauth_timestamp** - The number of seconds elapsed since midnight, 1 January 1970. Be sure this is within ten minutes of the real time
+ **oauth_signature_method** - The method used to generate the signature. We currently only support HMAC-SHA1
+ **oauth_signature** - You generate the signature by passing into a cryptographic function your consumer key, your shared secret, and an encoded version of the "base string"


The oauth_version parameter is optional; the value will be assumed to be 1.0 if it is not provided.

## Response Format

We render all responses as JSON. 
