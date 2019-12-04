---
title: "Netcup Digital Ocean Forge DNS Configuration"
date: 2019-11-19T11:47:24+01:00
draft: true
tags: ["Hosting"] 
---
Title ideas:
	- Offer hassle free hosting for your client's Laravel site
	- This is how you want to host your client's Laravel site
	- How to be a one-off hosting solution for your client

Goals:
	- Your future deployment workflow consists of not more than a push to github
	- You can test your changes on a staging environment
	- You don't have to deal with server configuration
	- You become a on-off solution: Domain, Subdomains, Email, VPS, Media Storage,
	  Backups, SSL
	- You don't have to worry about unpredictable costs based on server usage
	- Everything is ultra reliable and high-speed
	- You can keep it affordable for your client (or add a nice margin for yourself)
	- You can offer different hosting packages with different ressources

To host a complete Project for a client, you'll need 
- domain and email server (Netcup)
- applicaiton server (Digital Ocean)
- server configuration automation (Forge)

We want to:
- Purchase a domain and email server from Netcup
- Tell Digital Ocean to handle the requests coming from the Netcup domain
- Tell Netcup to use Digital Oceans nameservers
- Tell Digital Ocean to still let Netcup handle all the email traffic
- Create a site and deploy it on Digital Ocean via Forge

First thing you need is a domain, purchased from a domain registrar like Netcup.
You also need to buy a hosting package from them in order to have a working mail
server.

After doing this, login to Digital Ocean, go to Networking > Domains and enter
the Domain you purchased from Netcup and click "Add Domain". 

Click the domain name and create the following DNS records:
- A record: enter @ in the first field and choose your droplet from the second field,
  click "Create Record. This will point the domain to your droplets server and
  configure the nameservers.
- A record: enter www in the first field and choose your droplet from the second
  field, click "Create Record". This will make your site available under
  www.yourdomain.com and (aside from yourdomain.com) and will the default SSL
  installation configuration in forge prevent from failing, as we will see later
  on.
- A record: enter "mail" in the first field and paste your mailservers IP in the second field.
  This is the server from your Netcup hosting package, which will serve as a
  mailserver. Can be found in Netcup CCP under Products > your hosting package >
  Overview > Global Administration and Configuration > SMTP- / IMAP- /
  POP3-Server > IP-Address (In the middle of the third line)
- MX record: enter @ in the first field and enter the mailserver address in the
  second field. Can be found beside the IP in the Netcup CCP. Set the priority
  to 50.
- MX record: enter @ in the first field and enter mail.yourdomain.com in the
  second field, set the priority to 10. This points to the A record you created
  in the second step.

If you're not sure about the last three bullets, which will setup you email,
head over to Netcup and copy those three DNS record (one A, two MX) from Domains
> Your Domain > DNS.

Next you login to your Netcup CCP, head over to Domains > Your Domain > DNS
scroll down and choose "custom Nameserver". Two lines with three inputs each
will appear. First line, first input: ns1.digitalocean.com. Second line, second
input: ns2.digitalocean.com. Third line, third input: ns3.digitalocean.com. Hit
Save and confirm.

Your domain now points to the nameservers of Digital Ocean. All email traffic
will still go through your Netcup server, because of the DNS records we set up
in Digital Ocean.

Finally you set up your new site in Forge on your Digital Ocean droplet. Give it your
domain name. 

DNS needs a few hours to propagate, then your site will be available under your
domain.
