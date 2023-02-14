---
title: "SR-stats"
draft: true

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
| Web app | Feb, 2022 - Now |  Javascript | NextJS, Antlr4, MongoDB, graph.js | Tree parsing, grammar |


## What is Star Realms?
Star Realms is a fast-paced 2 player card game in which you construct a fleet of dangerous interstallar ships that you
use to inflict damage on your oponent and reduce his life to 0 before he does the same to you. It's available on steam
and as a mobile app.
The Star Realms app doesn't provide any statistics once you have finished a game nor does it provide a history
of the game you've played.
SR-stats attempts to fill this gap by providing a web app where players can upload games they have played and
then view details statistics.

## Architecture
Once the user has finished a game of Star Realms he should copy the game data from the options menu and paste it
into the SR-stats app. So far this is the only way to transfer a game between the 2 apps. 
SR-stats is as simple web app built using NextJS (a React framework). It relies on a parser to build the AST representation
of the game data and a visitor then traverses to tree a constructs a json representation of the game which is
then stored on the MongoDB cloud.

![architecture](/img/arch-srstats.png)

## What I got right

A lot of the things I got right came from mistakes I made building my first app Clipshare. You can learn more about this here.

1. **Focus on core features and have a POC out quickly**. 
2. **Keep it simple and cheap**
3. **Build for well-known customers**

## Tradeoffs I had to make

1. **The friction that comes from asking the users to upload each game manually**.
2. **Relying too much on a third-party**.
3. **Underestimating the difficulty of UI and UX**

These are tradeoffs I was aware of when I started working on the project and I decided to proceed regardless because
I thought value could still be delivered.

## Screenshots

Phase 2: Web app UI design

For this I decided to use Next.js and vercel for the deployment. I knew I was going to use React because I had some experience
with it but I also wanted something else on top of it to make it easier to setup a website. I found that Next.js had everything
I needed and the platform Vercel could handle deployments of the app.
Sometime I realised at this step is that making a website that looks and feels good is really hard. You sort of know what
are the features that you want the user to be able to interact with but how you structure them, what hierarchie what UI 
components to use. That part is really hard. To help me with this process I used figma for designing the UI and wrote all 
the features on some cards grouping them based on their relationship and putting them on a scale from least important to
more important. My first UI looked like this.

Phase 3: showing the app to users and gathering feedback

[add screenshots of the evolution of the UI]

Challenges
Promoting the app is hard