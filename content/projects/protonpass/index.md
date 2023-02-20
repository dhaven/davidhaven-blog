---
title: "Protonpass"
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

programming language: C#
main library used: N/A
type: desktop app
technologies: cryptography


ProtonPass is an plugin for the password manager Keepass. As part of Keepass's design the user is responsible for managing
the encrypted password database. A common pattern is to store the database in the Cloud. For example using Dropbox. I wanted
to take things further and store my database in ProtonDrive, the Cloud storage solution from Proton. This service is end-to-end
encrypted and therefore offers and extra layer of security out-of-the-box.

Things noteworthy.
=> Challenges with interacting with the API: Proton doesn't have a straighforward API with wich you can interact with simple
GET and POST request in order to store or retrieve data like you would with most other Cloud services. This is because of Proton's
promise of offering end-to-end ecrypted services which means a great deal of engineering goes in client side processing. Most
notably everything the client receives is encrypted and everything the client sends is encrypted. Because there is not much public
knowledge about this process I had to spend a great deal of time reading the source code of the Proton services in order to
understand everything that into the encryption/decyption process.

Authenticating the user also presented itself with it's own set of challenges. Indeed it doesn't follow a typical authentication 
process where you would simply send the credentials to the backend. Instead it implements the SRP protocol to authenticate users.
This is an extra secure protocol in which the credentials are never send to the server.

Finally building an plugin for a windows app written in C# is also something brand new to me. I had to familiarize myself with the
VisualStudio IDE, the C# programming language, the various libraries that I would need to use to build out my functionalities.

This is the project for which I had the least amount of knowledge going in and I wasn't sure if it was even doable.