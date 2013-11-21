---
layout: post
title: DNS Zone & DNS Records Explained
tags:
- a record
- cname
- codingarena
- dns
- dns records
- internet
- Internet
- mail
- manu
- mx record
- nameserver
- server
- site
- web
- Website
- website
- zone
- zone records
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

##WHAT IS THE DNS ZONE ? ##

In short, a zone is only a portion of a domain in that sense that it doesnt go outside the server that the root domain is on. If that summation is confusing then read on.

Every domain name, which is a part of the DNS system, has several DNS settings, also known as DNS records. In order for these DNS records to be kept in order, the DNS zone was created. The total of all DNS zones, which are organized in a hierarchical tree-like order of cascading lower-level domains, form the DNS namespace.

Domain name servers store information about part of the domain name space called a zone. The name server is authoritative for a particular zone. A single name server can be authoritative for many zones.

Understanding the difference between a zone and a domain is sometimes confusing. A zone is simply a portion of a domain. For example, the Domain codingarena.in may contain all of the data for codingarena.in, blog.codingarena.in and sandbox.codingarena.in. However, the zone codingarena.in contains only information for codingarena.in and references to the authoritative name servers for the subdomains.

The zone codingarena.in can contain the data for subdomains of codingarena.in if they have not been delegated to another server. For example, blog.codingarena.in may manage its own delegated zone. sandbox.codingarena.in may be managed by the parent, codingarena.in.
If there are no subdomains, then the zone and domain are essentially the same. In this case the zone contains all data for the domain.

##Understanding zones ##

DNS data is divided into manageable sets of data called zones. Zones contain name and IP address information about one or more parts of a DNS domain. A server that contains all of the information for a zone is the authoritative server for the domain. Sometimes it may make sense to delegate the authority for answering DNS queries for a particular subdomain to another DNS server. In this case, the DNS server for the domain can be configured to refer the subdomain queries to the appropriate server.

For backup and redundancy, zone data is often stored on servers other than the authoritative DNS server. These other servers are called secondary servers, which load zone data from the authoritative server. Configuring secondary servers allows you to balance the demand on servers and also provides a backup in case the primary server goes down. Secondary servers obtain zone data by doing zone transfers from the authoritative server. When a secondary server is initialized, it loads a complete copy of the zone data from the primary server. The secondary server also reloads zone data from the primary server or from other secondaries for that domain when zone data changes.

WHAT RECORDS MAKE UP THE DNS ZONE? HERE ARE SOME
* NS  specifies which are the DNS servers for your domain. For example the DNS servers at lethost host are waiting for requests that are a DNS/Domain pair that it will redirect to its correct IP
* A - specifies IP addresses corresponding to your domain and its subdomains. So we can presum that the A-record is always set in the background when using a shared hosting package. So when a website request for mysite.ie arrives at letshosts name servers then they check the DNS zone for that domain, see the correct a-records (their IP for the domin), then hey-presto.
* MX  specifies where the emails for your domain should be delivered. Again I presume this is set automatically in the background. OR maybe the same mailserver is set for the entire DNS server (a default) rather than for each domain. Hmm I wonder.
* CNAME - The history of the term CNAME is this. A canonical name is the properly denoted host name of a computer or network server. Canonical means according to the rules. A CNAME specifies an alias or nickname for a canonical host name record.

A computer hosting a Web site must have an IP address in order to be connected to the World Wide Web. The DNS resolves the computer??s domain name to its IP address, but sometimes more than one domain name resolves to the same IP address, and this is where the CNAME is useful. A machine can have an unlimited number of CNAME aliases, but a separate CNAME record must be in the database for each alias.


<a title="Neo" href="http://facebook.com/manusajith" target="_blank">Manu</a>

<a title="Codingarena.in" href="http://codingarena.in" target="_blank">http://codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
