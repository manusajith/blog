---
layout: post
title: DomainKeys Identified Mail
tags:
- codingarena
- forging
- gmail
- hacking
- internet
- Internet
- mail
- manu
- neo
- security
- Security
- spoofing
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  dsq_thread_id: ''
---
DomainKeys (DK) and DomainKeys Identified Mail (DKIM) are cryptographic email verification systems that can be utilized to prevent spoofing (forging another person's email address in order to pose as a different message sender). Additionally, because most junk email (spam) messages contain spoofed addresses, DK/DKIM can help greatly in the reduction of spam even though the specifications weren't specifically designed to be an anti-spam tool. DK/DKIM can also be used to ensure the integrity of incoming messages, or ensure that the message hasn't been tampered with between the time it left the signing mail server and arrived at yours. In other words, with DK/DKIM cryptographic verification the receiving server can be certain that the arriving message is from the server that signed it, and that no one changed that message in any way.

<!--more-->

In order to ensure the validity and integrity of messages, DK/DKIM uses a public and private key-pairs system. An encrypted public key is published to the sending server's DNS records and then each outgoing message is signed by the server using the corresponding encrypted private key. For incoming messages, when the receiving server sees that a message has been signed, it will retrieve the public key from the sending server's DNS records and then compare that key with the message's cryptographic signature to determine its validity. If the incoming message cannot be verified then the receiving server knows it contains a spoofed address or has been tampered with or changed. A failed message can then be rejected, or it can be accepted but have its spam score adjusted.

<a title="Manu" href="http://facebook.com/manusajith" target="_blank">Manu</a>

<a title="codingarena" href="http://codingarena.in" target="_blank">Codingarena</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
