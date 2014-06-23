---
title: June Tech Session
layout: post
---
Every so often we hold [ArcLabs Tech Sessions](https://plus.google.com/communities/102861833796677820528) on our campus. These events are open to all to sign up and attend. The idea is that we pick a conference. Everyone picks different videos or audio + slides to watch. We all summarise what we saw and present in a few minutes at the end of the session. This allows people to potentially see presentation they might not normally see but also the engage with colleagues or neighbours to find out about something that might interest them. Here are my brief notes from the most recent tech session based on the [2014 TNC](https://tnc2014.terena.org/). 

### Simplifying Federation Deployment

[Based on the video archives](https://tnc2014.terena.org/web/media/archive/2B)

#### Presentation by GARR
  - IdP federation in the cloud
    - virtual appliance
    - IdM tools
      - Automated installation - 17 mins vs. 2.5 hours with a skilled sysadmin manually setting up
      - also lets them update with patches

### Lightning Talks

#### Stefan Winter - Heartbleed and what it means to Eduroam
  - not just webservers - imaps, smtps, etc.
  - lots of protocols on eduroam with packet encapsulation (with TLS)
  - is eduroam vulnerable to heartbleed?
    - yes - can become an evil twin
  - initially 20% of servers vuln. now about 1.9%

#### Sustainability of Opensource Projects
  - initially they had to make another DNS server other than Bind
  - genetic diversity - NSD
  - OpenNetlabs - company for sustaining the foundation (http://www.opennetlabs.com/site/)
  - changing landscape 
    - scalability
    - security
    - crime
  - looking for collaboration

#### Log Analysis as a Service
  - Logging
  - [LogStash](http://logstash.net/) - logging swiss army knife
  - [ElasticSearch](http://www.elasticsearch.org/) - free text analysis
  - [Kibana](http://www.elasticsearch.org/overview/kibana/) - 
  - Commodity PCs
  - Important to spread jobs over many machines so you get many disks to get IO reads
  - made dependable by replication over many hosts

#### eduRoam UK Monitoring Probes - Scott Armitage
  - based on TP-Link MR3020
  - OpenWRT Barrier Breaker
  - [wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/)
  - scripts in Bash
  - [code on Githuab](https://github.com/jimdigriz/monitorProbe)
  - probes report home over HTTPS (will always work at every site)

#### Reflow - Martijn Hoogesteger
  - based on an internet 2 project
  - gathering data from several networks on properties of network flows
  - generate reports with several statistics
  - [See it here](http://stats.simpleweb.org/statistics.php)


