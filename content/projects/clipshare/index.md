---
title: "Clipshare"
draft: false

showDate : false
showDateUpdated : false
showHeadingAnchors : false
showPagination : false
showReadingTime : false
showTableOfContents : true
showTaxonomies : false 
showWordCount : false
showSummary : false
sharingLinks : false
showEdit: false
showViews: true
showLikes: true
layoutBackgroundHeaderSpace: false

#groupByYear : false

---


a project overview IDcard
programming language: javascript
main library used/ relied on: lit-element, videojs, nodejs
type: Browser extension
technologies: websockets, queues, authentication

This can be my considered to be the first project that I ever took from an idea to a releasable app.
The idea behind this project is that twitter users who listen to podcast might want to provide some
"hot takes" about certain parts of the podcast. If they want to do so, they would first need to 
download the video. Then use a video editor to trim to video to the desired content. Then share it on
Twitter.
With this project was to provide an optimization to this process where you would be able to do everything
right from your browser.

## Architecture

![architecture](/img/arch-clipshare.png)

The things I got right
1. Making a browser extension: The idea of going for a browser extension was to limit the scope of the
app by the fact that the UI you can work with is quite limited. It's tempting to have grand plans for 
a revolutionary app then never get to the end because it is too much work. Here I wanted to make sure
that I would get to the end
2. An app that is an optimization: 

The mistakes I made
1. Handling video data : Video data is very costly to store and transfer.

{{< chart >}}
type: 'bar',
data: {
  labels: ['February', 'March', 'April', 'Mai', 'June', 'July'],
  datasets: [{
    label: 'AWS hosting cost',
    data: [9.26, 77.78, 70.64, 91.70, 65.13, 9.88],
  }]
}
{{< /chart >}}

2. Self hosting the backend : 
3. Not using a frontend framework
4. Not knowing who my customers are
5. Overengineering certain aspects
6. Not implementing the app for chromium
7. Creating an unfriendly app from the point of vue of youtube (youtube downloader) and twitter (alternative client for tweeting)

Youtube implemented my app right into their app

Getting the details wrong
The app was really slow and it wasn't easy to be precise with the trim bars