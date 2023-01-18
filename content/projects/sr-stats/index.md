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

programming language: javascript
main library used: NextJS, Antlr4, MongoDB, graph.js
type: Web App
technologies: N/A

->how the project came to be (why)

-> initial setup (how)

-> Challenges

-> what I learned so far

I discovered Star Realms in 2020 (date more precise). At that time I was looking for a new board game that wouldn't take up
too much space so that it would be easy to travel with it. I also wanted to find something fresh and different. I 
settled with the game called Star Realms. A type of "deck building" game which I had heard of but never actually played.
After playing a few games. Winning some and losing some. I decided to try the digital version of the game available on
mobile and desktop. After playing a few games online on thing became clear: I wasn't exactly sure why I was winning or losing. 
The most important decision making of the game is deciding which card to buy from the trade row. 
One thing I found was missing from the app is being able to review your game and have some statistics about the game you just played. One thing the game did give you access to is the log data from the whole game. So I thought, why not parse the logfile 
and generate some stats and graphs? From this simple observation started the SR stats journey.

Phase 1: Grammars and parsers

Based on my prior knowledge of AST and compilers I decided that the best approach to parsing the log file would be the
define a grammar for the data and use that to generate an AST representation of the data which would then be much easier
to parse in a systematic way. I found the library Antr4 which had what I need so I started writing the grammar.

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