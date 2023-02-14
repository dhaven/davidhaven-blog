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

| Type | Timespan | Programming Language | Main library used/ relied on | Concepts |
|------|----------|----------------------|------------------------------|----------|
| Browser extension | Feb, 2021 - June, 2021 |  Javascript | lit-element, videojs, nodejs | websockets, queues, oauth, video processing |


Clipshare is the first project that I ever took from an idea to a production ready app. Pundits and news commentators
on Twitter often use short video clips to provide context for their tweets. A typical workflow for producing
these video clips will involve the following steps:
1. Download the source video to computer.
2. Clip the video to only include what is relevant for the commentary.
3. Post tweet with video clip.

Clipshare simplifies this process by allowing the user to reach the same goal without leaving the browser.


## Architecture

![architecture](/img/arch-clipshare.png)

## What I got right

1. **Making a browser extension**. The idea of going for a browser extension was to limit the scope of the
app by the fact that the UI you can work with is quite limited. It's tempting to have grand plans for 
a revolutionary app then never get to the end because it is too much work. Here I wanted to make sure
that I would be able to complete the project
2. **An app that is an optimization**. Users are usually quite keen to find ways to do certain things faster.
3. **The app user flow**.

## What I got wrong

1. **Handling video data** : Video data is very expensive to manage in terms of storage and transfer costs.
There is also no economies of scale because the cost would increase linearly as the number of active users.
As a solo developer with little funding this was probably not a smart idea. There are some solutions to mitage this.
For example by not downloading the video source to the backend and instead streaming it directly to the frontend
I could reduce storage and transfer costs.  

2. **Self hosting the backend** : With my background in systems engineering I wanted to build the cloud infrastructure
from scratch using AWS. This included setting S3 buckets, dynamoDB tables, VPC, security groups, etc...
This was a poor choice for two reasons:
    -  **It takes time and it does not provide value for the customer**. The choice to self host was purely motivated 
    by an interest in building cloud infrastructure.
    - **It's more expensive**. The graph below shows the cost in dollars for hosting the infrastructure before the app was
    even released to the public. By June I started shutting down the infrastructure because it was not viable for me.
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

3. **Not using a frontend framework**: 
4. **Not knowing who my customers are**: I had no idea how to reach customers and let people know my app exists.
5. **Overengineering certain aspects**: Being able to distinguish between critical features and nice to haves is
very important if you want to be able to ship quickly. For example I wanted to make sure that if the user left the extension
while the flow was in progress he could resume where he had left off when he came back to the app. This required implementing various caching mechanisms and was certainly not a critical feature.
7. **Creating an "unfriendly" app from the point of vue of Youtube and Twitter**. Clipshare is both "youtube downloader" and "custom twitter client". Neither of these concepts are much appreciated by Youtube or Twitter.
This means that I'm playing a risky game where I could get cut off from the Twitter API.This observation also led me to 
develop the app for Firefox which means cutting myself off from most of my potential customers.

## Takeaways

Suprisingly, as I was working on my app Youtube was working on a similar feature called Youtube clips which was
released in July 14, 2021 [source](https://www.youtube.com/watch?v=A63imEmP_-I)

## Screenshots

![start_editing](/img/start_editing.png)
![finish_editing](/img/finish_editing.png)
![send_tweet](/img/send_tweet.png)
![tweet_send](/img/tweet_send.png)