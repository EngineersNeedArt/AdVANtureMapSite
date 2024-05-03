# AdVANtureMapSite
Web page using Leaflet to display markers for a YouTuber's travels with links to videos.

<p align="center">
<img src="https://github.com/EngineersNeedArt/AdVANtureMapSite/blob/b4bc2316736c1402a006d2e2b6f45f26f301154b/screenshot.png">
<a href="https://engineersneedart.com/OneAdvanture/index.html" target="_blank">The current place</a> I am hosting the site.
</p>

### Site

A husband and wife have travelled the country in their self-converted van-to-RV for over five years. They have a YouTube site with hundreds of videos now showing us the various places they have travelled, the places they have found to camp for free (or nearly free). I created this site to gather the locations from their videos and display them on a map with markers. Markers, when clicked on, display popups with links to the relevant videos for that location.

A "Latest" button at the top of the map will take you to the marker representing the location of their most recent video.

### Motivation

I am a fan of their YouTube "adVANtures" and also an RV traveller of the U.S. myself. I have always wished for something like this site in order to find their relevant videos when I am on the road.

I am only reluctantly a "Web designer" and so leaned on A.I. to help me put the pieces together for this page. Claude and ChatGPT helped me get me the plumbing in place. I have always been interested in mapping web pages and also saw this as an opportunity to dip my toe into it.

I then went off and spent four days or so working through the YouTube video collection on their channel — pulling out latitude and longitude data as well as the date the video was uploaded, URL for the video.

I created an SVG icon for the map marker as a very stylized representation of their RV and did an SVG approximation of their logo (because I am an SVG snob).

### Details

Leaflet.js and their OpenStreetMap tile data are used for the map itself. Additionally, the MarkerCluster plug-in for Leaflet is used for, of course, the clustering.

A popup is bound to each marker. The popup contains a title for the location and the date the corresponding video was uploaded. The date also acts as a link (anchor tag) to the relevant YouTube video. Since the YouTube couple would sometimes re-visit a location, some popups have two or three dates/links that will each take you to a different YouTube video (the one corresponding to the date and location or course).

The data "backend" is as simple as can be: inline JSON within the HTML document itself. The data itself is about 50K in bytes representing a little over 300 markers. The JSON represents an array of objects (dictionaries) that contain keys for "title", "lat", "lon", "url" and "date". The keys are probably self-explanatory. For re-visited locations I (hackishly) added optional "url2" and "url3" keys (and corresponding "date2" and "date3" keys). At this point there are not any specific locations they have re-visited four or more times.

The array is ordered more or less from the most recent location visited to the oldest location visited. Given that, new locations as they show up on YouTube will be added at the start of the array.

The "Latest" button always pulls the latitude and longitude from the zero-th ([0]) element of the JSON data and passes that to the "flyto" function on the Leaflet map.

### AI

Rolling my own HTML/CSS in the past has consisted of a lot of web searching/browsing just to move incrementally along. Each search session generally results in only a small step forward — and then some new hurdle arises and a new search session begins.

From my first interaction with Claude (claude.ai) where I described a map view of the U.S. with markers representing locations I was presented with a number of options for the mapping library with descriptions of each. Claude also presented boilerplate HTML for a simple map web page showing both New York and L.A. marked up. I have no doubt that had I searched the web manually as I had done in the past I might well have ended up with the same boilerplate code but it's hard to know how many dead-end alleys I would have had to first abandon.

A few more prompts asking for richer marker popups and Claude I had some popup CSS and HTML code to play with.

We went round and round where I drilled Claude on padding and line spacing until I had a popup layout I liked.

At one point, I had used all my free queries of Claude for the morning and had to resort to my old web searches for answers about padding, margins and spans and I was once again thrust into plowing through SEO-driven results that wanted me to accept cookies, sign up for notifications, etc. The internet is littered with cess-pools and search engines direct us there.

Ocassionally, Claude's suggestions would lead to incorrect results and I would call him (?) out on it:

_Me: I'm not seeing the span and anchor on the same line. Do I need to wrap the anchor in a span as well?_

_Claude: You're right, wrapping both the span and anchor in a parent inline element like a `<div>` or another `<span>` should make them appear on the same line. Here's how you can modify the HTML and CSS:_

Even with a barebones site up and running I still had to manually scrape hundreds of YouTube videos to build up my web data, but the HTML and CSS went together fairly easily with help from Claude and ChatGPT. I more or less knew the right questions to ask. Like when the number of markers climbed past 100 or so I asked about marker clustering — Claude quickly pointed me to the MarkerCluster plugin for Leaflet.js. 

### Ideally

Preferably the marker data would live external to the web page. Because of cross-origin issues I opted for simplicity. To make the data more easily editable in the future though it should be served up by the backend. Ideal would be a login-secured front-end so that a user could edit the marker data without needing sophisticated database knowledge or direct access. This is beyond my means for a "hobby project". Additionally, that would require extra steps in hosting — what I have now is certainly easily portable.
