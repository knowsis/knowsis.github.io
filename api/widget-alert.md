---
title: Alert Widget
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /widget-alert/
---

This HTML widget contains the the content for a particular {alert_identifier}.


```
GET /widgets/alerts/{alert_identifier}/
```


## Example Request

```
GET https://insights.knows.is/widgets/alerts/575ac51af3d4f7468291fd45/?css=https://www.client.com/style.css
Accept: text/html
```

```html
<div id="app-container">
    <header class="m-and-a">
        <h1><strong>M&amp;A alert</strong> <small class="date">2016-06-12
        17:03:31</small></h1><span class="credibility high">high
        credibility</span>
    </header>
    <main>
        <h1>Communications</h1>
        <p class="mentioned-actors">mentioned 
          <span class="m-and-a-actor">Microsoft Corporation</span>
          <span class="m-and-a-actor">LinkedIn Corporation</span>
        </p>
        <span class="retweeted-by">Retweeted by 
            <a href="https://twitter.com/intent/user?screen_name=KnowsisTechnolo" target="_blank">Knowsis Technology</a>
        </span>
        <p class="alert-content">Microsoft to buy LinkedIn</p>
        <div class="tweet-media">
            <a href="https://twitter.com/Knowsis/status/586443087565586432" target="_blank">
                <img class="img-responsive" src="https://insights.knows.is/external/image/?url=https://pbs.twimg.com/media/CCN24R7UgAE18g0.png"
                    alt="Image attached to this tweet">
            </a>
        </div>
    </main>
    <footer>
        <div class="col">
            <div class="avatar-and-name">
                <a class="avatar" href="https://twitter.com/intent/user?screen_name=Knowsis" target="_blank">
                    <img src="https://pbs.twimg.com/profile_images/1734171568/Screen_shot_2012-01-04_at_14.48.16_normal.png">
                </a>
                <div class="name">
                    <h1><a href=
                    "https://twitter.com/intent/user?screen_name=Knowsis"
                    target="_blank">Knowsis</a></h1>
                    <h2><a href=
                    "https://twitter.com/intent/user?screen_name=Knowsis"
                    target="_blank">@Knowsis</a></h2>
                </div>
            </div>
            <div class="stats">
                <span class="followers">followers <strong>421</strong></span>
                <span class="following">following <strong>639</strong></span>
            </div>
        </div>
        <div class="col">
            <p class="bio">Social Intelligence for the Capital Markets (TWEETS NOT ADVICE)</p>
            <p class="location" title="London, UK">London, UK</p>
            <p class="home-url"><a href="http://knowsis.com" target="_blank">knowsis.com</a>
        </div>
    </footer>
</div>
```

## Images

By default images attached to an alert are shown and links to these images are hidden.

If you want to hide images and display links instead, add the following css to your stylesheet:

```css
.media-url {
    display: inline;
}

.tweet-media {
    display: none;
}
```
