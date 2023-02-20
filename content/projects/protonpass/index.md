---
title: "ProtonPass"
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

<table class="p-4 rounded-md drop-shadow-md dark:bg-blue-900 bg-blue-100">
  <thead>
    <tr>
      <th class="px-4">Type</th>
      <th>Duration</th>
      <th>Programming Language</th>
      <th>Libraries</th>
      <th>Concepts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="p-4">desktop app</td>
      <td>Dec, 2022 - Now</td>
      <td>C#, Javascript, Python</td>
      <td>N/A</td>
      <td>pgp, public/private cryptography</td>
    </tr>
  </tbody>
</table>


ProtonPass is an plugin for the password manager KeePass. When using KeePass the user needs to decide where the encrypted file
that contains all of his password is going to be stored. Because most users want to file to be accessible on multiple devices,
a common pattern is to store the database in the Cloud. For example using Dropbox. I wanted
to take things further and store my database in ProtonDrive, the Cloud storage solution from Proton.
ProtonDrive is end-to-end encrypted and therefore offers and extra layer of security out-of-the-box.

## Key feature

The user should be able to login to his Proton account from a KeePass menu and select the KeePass file that he wants to open.
When saving a modified file. The file in the drive should also be updated.

## Development challenges

When I started this project it wasn't even clear if it was feasible. And while progressing through the project it was
hard to figure out the "how". I.e. how to perform certain actions with respect to the ProtonDrive app. This is certainly the
project for which I was most in the dark when starting.

### Understanding the encryption/decryption flow

Because of Proton's promise of end-to-end encryption, a great deal of engineering goes into client side processing of data. Most
notably everything the client receives from the server is encrypted and everything the client sends is encrypted. Because there
isn't a lot of online documentation about this process I had to spend time reading the source code of the Proton services in order to
understand everything that goes into the encryption/decyption process.

### Authenticating the user
Authenticating the user also presented itself with it's own set of challenges. Indeed it doesn't follow a typical authentication 
process where you would simply send the credentials to the backend. Instead it implements the SRP protocol to authenticate users.
This is an extra secure protocol in which the credentials are never send to the server.

### Building a desktop app extension
Finally building an plugin for a windows app written in C# is also something brand new to me. I had to familiarize myself with the
VisualStudio IDE, the C# programming language, the various libraries that I would need to use to build out my functionalities.