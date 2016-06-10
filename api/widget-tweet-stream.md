---
title: Tweet Stream Widget
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /widget-tweet-stream/
---

This HTML widget contains the most recent tweets for a particular {identifier} or a list of comma-seperated {identifier}s, and will be automatically updated with any new tweets via javascript.

```
GET /tweets/{identifier}/
```


## Example request

```
GET https://insights.knows.is/widgets/tweets/$ARM,$TSLA/?css=https://www.client.com/style.css
Accept: text/html
```

```html
<div id="app-container">
    <ul id="ARMH" class="tweets-list">
        <li class="tweet-container">
            <div class="tweet-title-container">
                <a href="https://twitter.com/intent/user?screen_name=HalftimeReport">
                    <div class="tweet-profile-icon"><img
                            src="https://testinsights.knows.is/external/twitter_profile/?url=https://pbs.twimg.com/profile_images/590580807753986049/fhYEXRiC_normal.png"
                            width="15px" height="15px" alt="User Image"></div>
                    <div class="tweet-profile">CNBC Halftime Report</div>
                    <div class="tweet-username">@HalftimeReport</div>
                </a>
                <a class="tweet-date-link" href="https://twitter.com/HalftimeReport/status/738400580079517697"
                   target="_blank">
                    <div class="tweet-date" data-created="2016-06-02T16:03:11"
                         title="Thu, 2 Jun 2016 16:03:11 +0100">2 minutes
                    </div>
                </a>
            </div>
            <div class="tweet-content">
                Best days behind for Apple? $AAPL
                <a href="http://twitter.com/HalftimeReport/status/738400580079517697/photo/1"
                   class="link-primary media-url" target="_blank">pic.twitter.com/7a00FrhTaK</a>

                <div class="tweet-media">
                    <a href="http://twitter.com/HalftimeReport/status/738400580079517697/photo/1"
                       target="_blank">
                        <img class="img-responsive"
                             src="https://testinsights.knows.is/external/image/?url=https://pbs.twimg.com/media/Cj9TaZsWgAAKCIM.jpg"
                             alt="Image attached to this tweet">
                    </a>
                </div>
            </div>
        </li>
    </ul>
</div>
```

## Images

By default images attached to a tweet are shown and links to these images are hidden.

If you want to hide images and display links instead, add the following css to your stylesheet:

```css
.media-url {
    display: inline;
}

.tweet-media {
    display: none;
}
```