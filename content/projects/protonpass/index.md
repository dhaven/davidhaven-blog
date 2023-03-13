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


[ProtonPass](https://github.com/dhaven/protonPass) is an plugin for the password manager [KeePass](https://keepass.info/index.html). 
When using KeePass the user needs to decide where the encrypted file
that contains all of his passwords is going to be stored. Because most users want the file to be accessible on multiple devices,
a common pattern is to store the database in the Cloud. For example using Dropbox. Solutions like this compromise security
because they rely on the storage provider privacy and security practices. As an alternative, [ProtonDrive](https://proton.me/drive) 
the cloud storage solution from Proton is an end-to-end encrypted storage solutions which relies on user-provided keys for encrypting the data at-rest.
I decided to build my own KeePass extension for storing my database file on ProtonDrive.

Because this is an ongoing project, this page will change as I make progress.

## Key feature
The user should be able to use a KeePass database file stored in ProtonDrive and open the file inside KeePass on his device.
When saving a modified file. The file in the drive should also be updated.

## Development challenges

When I started this project there were a lot of unknowns. The main difficulty is that I am trying to do something new that hasn't been
done before. Therefore there aren't any existing examples that I can base my work on. This can be explained by the fact that Proton
services are quite unique in their design.

### Understanding the encryption/decryption flow

Because of Proton's promise of end-to-end encryption, a great deal of engineering goes into client side processing of data. Most
notably everything the client receives from the server is encrypted and everything the client sends is encrypted. Because there
isn't a lot of online documentation about this process I had to spend time reading the source code of the Proton services in order to
understand everything that goes into the encryption/decryption process.

### Authenticating the user
Authenticating the user also presented itself with it's own set of challenges. Indeed it doesn't follow a typical authentication 
process where you would simply send the credentials to the backend. Instead it implements the [SRP](https://en.wikipedia.org/wiki/Secure_Remote_Password_protocol) protocol to authenticate users. Understanding this protocol and how to generate
all the cryptographic material was challenging.

### Building a desktop app extension
Finally building an plugin for a Windows app written in C# is also something brand new to me. I had to familiarize myself with the
VisualStudio IDE, the C# programming language and the various libraries that I would need to use to build out my functionalities.