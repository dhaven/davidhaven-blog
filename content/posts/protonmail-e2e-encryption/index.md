---
title: "End-to-end encryption with Proton Mail"
date: 2023-08-22
draft: false

showDate : true
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
showViews: false
showLikes: false
layoutBackgroundHeaderSpace: false

---

{{< lead >}}
<em>In this article I describe the conceptual building blocks that make up an end-to-end
encrypted (E2EE) channel. Using email communication as the backdrop I examine the cryptographic 
primitives that comprise an end-to-end encrypted  channel. I conclude with a description of
how Proton has implemented these concepts to provide the E2EE email service Proton Mail.</em>
{{< /lead >}}

## What is end-to-end encryption?

If Amy wants to send an email to Brian the email will transit by the email provider you are using.
This can for instance be Gmail or Outlook. The email provider is responsible for relaying the email 
to its destination. 

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/simple-email-sending.png" />
  <figcaption class="mx-2">
    <em>When you send an email from you Gmail account. It will first reach Google’s servers before being 
forwarded to the recipient of the email.</em>
  </figcaption>
</figure>

Broadly speaking there are 2 ways your email could be accessed by unwanted third-parties:
1. **When the email is in transit from your laptop to the email provider**. However, HTTPS ensures
a secure communication between your laptop and the email provider's servers.
It guaranties that nobody can impersonate the email provider and provides a secure communication 
channel between yourself and the servers.
2. **When the email is stored on the provider’s servers (at rest)**. The provider will store your emails 
on it’s server. This allows you
to see the email on your mobile after sending it from your laptop. To prevent unwanted third-parties 
from accessing your emails, the provider will encrypt the email when it is stored.

![Email attack vectors](/posts/protonmail-e2e-encryption/images/email-attack-vectors.png)

<p>
Notice how the email is sometimes in <b>plaintext</b> format (
<span class="inline-flex align-middle">
    <img src="/posts/protonmail-e2e-encryption/images/plaintext.png" alt="" class="w-8 h-8 rounded-full m-0" />
</span> )
and sometimes in <b>encrypted</b> format (
<span class="inline-flex align-middle">
    <img src="/posts/protonmail-e2e-encryption/images/encrypted.png" alt="" class="w-8 h-7 rounded-full m-0" />
</span> ).
If your email is encrypted it means that it has been transformed 
into a scrambled format which is unreadable. In order to recover the original information 
you need a <b>key</b> which can decrypt the data. The next illustration highlights who has access 
to the keys required for encrypting and decrypting the information.
</p>

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/email-sending-with-keys.png" />
  <figcaption class="mx-2">
    <em>Amy, Brian and the email provider all have access to the keys required to decrypt the email message.</em>
  </figcaption>
</figure>

{{< alert icon="circle-info">}}
*One reason an email provider wants access to your emails is to improve it’s products. For example 
if you book a flight and receive a confirmation email, Gmail will automatically suggest the creation of an 
event in your calendar by using the reservation information in your email. At the same time, email content 
helps Google build an accurate representation of who you are and uses this to better sell targeted ads.*
{{< /alert >}}

Encryption is a useful tool for preventing unwanted parties from accessing data.
If we want to exclude the email provider from accessing the data we can encrypt the email using a key only 
Brian and Amy have access to (
<span class="inline-flex align-middle">
    <img src="/posts/protonmail-e2e-encryption/images/green-key.png" alt="" class="w-8 h-6 rounded-full m-0" />
</span> ).

Such a communication channel is called **end-to-end encrypted** because it guarantees that only the 2 ends 
of the communication channel (Amy and Brian) have access to the decrypted content.

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/simple-e2e-encryption.png" />
  <figcaption class="mx-2">
    <em>Amy first encrypts
    her email content before sending it to Brian. She does so using a key only herself and Brian have knowledge of. 
    When the email arrives at the email provider it is unreadable because it has been encrypted using a key the email 
    provider does not know. When the email finally arrives to Brian he can decrypt it using the same key Amy used for 
    encryption.</em>
  </figcaption>
</figure>

Amy and Brian are both using the same key for encryption and decryption. This is known
as **symmetric encryption**. The tricky part with symmetric encryption is that the key needs to be shared between
Amy and Brian without anyone else getting their hands on it.

## Implementing end-to-end encryption

This concept of ensuring privacy between the 2 ends of the communication was implemented in 1991 by Phil Zimmerman 
who wrote a program called [PGP](https://www.philzimmermann.com/EN/essays/WhyIWrotePGP/) which stands for Pretty Good Privacy. 
You can use PGP to encrypt your email message before sending it to it's destination and the recipient also uses
PGP to recover the message once he receives the email.

While diving into the details of PGP goes beyond the scope of this post, one important concept used by PGP is 
the concept of **public key cryptography**. With public key cryptography you generate 2 keys: the **public key** 
which can only be used to encrypt data and the **private 
key** (or secret key) used to decrypt the data encrypted by the public key.

![Asymmetric cryptography](/posts/protonmail-e2e-encryption/images/asymmetric-encryption.png)


In this scenario, only the public key needs to be shared between parties that want to communicate. 
Amy will share her public key with Brian and Brian will share his public key with Amy. Furthermore, the public
key can only be used for encryption so even if it is intercepted by someone else this does not represent a risk
because they will not be able to decrypt any message.

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/public-key-sharing.png" />
  <figcaption class="mx-2">
    <em>Amy and Brian share their public key</em>
  </figcaption>
</figure>

Now if Amy wants to send a message to Brian she can encrypt the message using Brian’s public key. Only Brian 
can decrypt the message because only he has access to the associated private key. Likewise, if Brian want’s to 
send a response message to Amy he can use Amy’s public key to encrypt the message.

PGP depends on this key exchange to guaranty a secure communication between Amy and Brian.
The following illustration shows a simplified view of how email communication works when using PGP.

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/pgp-email.png" />
  <figcaption class="mx-2">
    <em>Amy encrypts her message using PGP before sending it to Brian. Once Brian receives
    the email he can decrypt the content using PGP.</em>
  </figcaption>
</figure>

{{< alert icon="circle-info" >}}
*To be more precise PGP uses a combination of public key cryptography and symmetric cryptography.
The message is encrypted with a symmetric key which is then itself encrypted with a public key. 
The encrypted message and encrypted key are sent together.*
{{< /alert >}}

As a software, PGP never gained widespread adoption. For a start it is very technical to use so
difficult for those who are not tech-savvy. The security of PGP also depends on how well you can keep your private 
key secure which even for tech-savvy people can be [too much to manage](https://arstechnica.com/information-technology/2016/12/op-ed-im-giving-up-on-pgp/).  

The team behind Proton Mail realized that to make encrypted email more widespread, the user 
experience should be closer to that of other providers such as Gmail or Outlook. The user should 
only have to login to his account, write his email and send it to the recipient without having to worry 
about encryption keys. While PGP provides a good cryptographic foundation for security,
 it’s main pain points had to be solved.

## Proton Mail's solution

Here are the 3 requirements that ProtonMail had to reconcile:

1. **PGP should be used to guarantee E2E encryption of email content.**
2. **End users should not be required to manage their private keys or be in any way involved in the encryption process.**
3. **It should be impossible for Proton Mail to access the email content (i.e. Proton Mail should never 
have access to the user’s private key)**

To solve **2.** Proton needs to store your private key on its servers. When you access your emails either 
from your desktop or mobile the client app will ask Proton’s server for your private key which will then be 
sent over to you. To make sure that this approach does not conflict with **3.**, Proton only stores on its 
servers a key which is **locked with a passphrase** (
<span class="inline-flex align-middle">
    <img src="/posts/protonmail-e2e-encryption/images/locked-key.png" alt="" class="w-8 h-7 rounded-full m-0" />
</span> ). 
A passphrase is to a key what a password is to 
your account. The locked key is sent to the client where it is unlocked and then used to decrypt your 
emails.

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/protonmail-e2e-encryption/images/private-key-storage.png" />
  <figcaption class="mx-2">
    <em>Proton only stores a locked version of your private key which guaranties that it can never read your email content</em>
  </figcaption>
</figure>

The last question then is what is the passphrase used to lock your private key? Proton cannot 
keep this passphrase on it’s servers as that would defeat the purpose of locking the key in the first place. 
This means the passphrase should be accessible from any device when you connect to your Proton account but 
never stored by Proton. 
**The only piece of information that fits this requirement is your password**. Every time you connect to 
your Proton account you use your password to login. This password is then used by Proton's web or  mobile apps
to unlock the private key sent to you by Proton servers.

{{< alert icon="circle-info" >}}
*Proton actually uses a passphrase which is based on your password but transformed in a 
way that makes it harder to guess. [[source]](https://proton.me/support/how-is-the-private-key-stored)*
{{< /alert >}}

If we combine this with what we know about secure email sending using PGP we get the following picture 
which is in a nutshell how ProtonMail works.

![Proton PGP](/posts/protonmail-e2e-encryption/images/proton-pgp.png)

## One key to rule them all

If you go to **Setting → Encryption and Keys** when logged in to your Proton account you will find that 
you actually have more than one private key. There is the “Email encryption key” (also referred to 
as the address key) and the "Account key" (also referred to as the user key) each having their own responsibility.

→ The **account key** is used to encrypt account wide information such as 
your contact list and is also used to recover your account in case you forget your password.

→ **Address keys** are used to encrypt and decrypt the content of emails being sent. For each email address you 
have there is one address key.

Your password is only used to unlock your account key. Each address key is locked by a passphrase which 
is randomly generated. Each passphrase is itself encrypted using your account key.

![Proton key decryption](/posts/protonmail-e2e-encryption/images/proton-key-decryption.png)

With this architecture we have access to multiple private keys all locked with different passphrases 
but there is only one piece of information that we need to remember which is our password.

The implications of this architecture is that your password isn't just used for accessing your account
but is also the foundation of how your email contents is encrypted. This means that if you lose
your password you might be able to regain access to your account by means of recovery but your emails
will no longer be readable because the keys used to encrypt their content can no longer be unlocked.

You can learn more about account recovery by reading the official documentation [here](https://proton.me/support/set-account-recovery-methods).

## Wrap up

By building on top of a proven technology and by using strong cryptography concepts Proton has managed to make
end-to-end encryption available to a broad public. While the experience provided by Proton has abstracted away
the underling encryption concepts some basic understanding of the primitives being used can help to better harness
the privacy tools out there and be less reliant on simply "trusting" the service. 

Proton decided to build on top of PGP but it is not the
only way to ensure privacy of communications. For example [Signal](https://signal.org/) developed it's own Protocol 
called the signal protocol and which is also [in use by Whatsapp](https://scontent-cdg4-3.xx.fbcdn.net/v/t39.8562-6/328495424_498532869106467_756303412205949548_n.pdf?_nc_cat=104&ccb=1-7&_nc_sid=ad8a9d&_nc_ohc=DG1P4TyHCd4AX_vaZQ5&_nc_ht=scontent-cdg4-3.xx&oh=00_AfDWXF6kQWMkTosoxb2yfWBYaQUEdP0JawkeYKJX6Pcanw&oe=64E74FFC) to support end-to-end encryption.