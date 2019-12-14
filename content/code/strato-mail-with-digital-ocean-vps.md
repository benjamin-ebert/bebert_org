---
title: "Strato Mail With Digital Ocean Vps"
date: 2019-12-14T11:59:44+01:00
draft: true
tags: [""] 
---

- setup Digital Ocean droplet via Forge as usual
- purchase domain and email package from strato (Mail Basic)
- in digital ocean add domain
- optional:
	- in the digital ocean dns records for the domain, delete all ns records
	- set three A records:
		- domain.com
		- www.domain.com
		- staging.domain.com
- in Strato, manage domain
- setup subdomain if neede (staging.domain.com)
- for domain and subdomain, set an A record pointing to the ip of the Digital
  Ocean droplet
- if you wish, setup the corresponding AAAA record too (for usage of ipv6
  adress)
- don't touch the nameserver settings / NS records
- don't touch the MX records
- that way, your domain will still be at home at strato, using your strato mail
  package just as if nothing had changed
- when calling your website, you'll now get the answer from the Digital Ocean
  droplet
