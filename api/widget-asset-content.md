---
title: Top Content Widget
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /widget-asset-content/
---

This HTML widget contains most shared articles for a particular {identifier} or a list of comma-seperated {identifier}s, and will be automatically updated with new articles via javascript.

```
GET /top-content/{identifier}/
```

## Example Request

```
GET https://insights.knows.is/widgets/top-content/AAPL,TSLA/?css=https://www.client.com/style.css
Accept: text/html
```

```html
<div id="app-container">

    <div class="top-content-list">
        
        <article>
            <div class="tile" data-url-identifier="5755795537f91844a95254a7">
                <div style="background-image:url('https://insights.knows.is/external/image/?url=http://static2.businessinsider.com/image/5755795152bcd01d7b8c6cf9-1190-625/apple-is-the-top-tech-company-in-the-fortune-500.jpg');"></div>
            </div>

            <div class="text">
                <h4>Apple is No. 3 in Fortune 500 - Business Insider</h4>
                <small>businessinsider.com | 06 Jun, 2016</small>
                <p>Apple continues to leads the tech industry, at least when measuring by sales.</p>
            </div>

            <a class="component-link" href="http://www.businessinsider.com/apple-is-no-3-in-fortune-500-2016-6" target="_blank"><span></span></a>
        </article>

    </div>

</div>
```