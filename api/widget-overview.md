---
title: Widgets Overview
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /widget-overview/
---


Access to HTML widgets is via the same oAuth credentials as the Knowsis data API above. These widgets are useful for light touch integration of visual elements.

## General

The returned widgets are `html` pages, which include `css` and `js` files where necessary.

## Requests

The Insights Widgets API is available at https://insights.knows.is/widgets/, e.g.:


```
GET https://insights.knows.is/widgets/tweets/$ARM/?css=https://www.client.com/style.css
Accept: text/html
```

The following are optional query string parameters 

|Field|Type|Description|
|-----|----|-----------|
|css|encoded url|the https url to a stylesheet which will replace the widget's default theme stylesheet|

## Markup

All widgets share the following base markup:

```html
<!DOCTYPE html>
<html>
<head></head>
    <body>
        <div id="app-container">
            <!-- widget content goes here -->
        </div>
        <div id="powered-by-knowsis">
            Powered by <a href="http://knowsis.com" target="_blank" title="Knowsis | Actionable Web Intelligence">Knowsis</a>
        </div>
    </body>
</html>
```

## Styling

Each widget uses three stylesheets:

1. `skeleton.css`, which provides a basic layout.
2. `theme.css`, which provides the default theme (colours, typography) for the widget.
3. `powered-by-knowsis.css`, which styles the bottom *Powered by Knowsis* footer.

The *Powered By Knowsis* footer must not be styled, moved or hidden without prior agreement.

## Custom Themes

You can provide your own theme stylesheet, which will replace the widget's default theme.
This allows you to style widgets according to your brand guidelines.