---
title: 'Blockchain-based Application Threat Modeling'
date: 2024-06-26T12:00:00+02:00
draft: false
type: post
layout: single_simple
categories: [Threat Modeling]
tags: [Blockchain, Web3, dApp, DeFi]
url: /2024/06/26/blockchain-based-application-threat-modeling
aliases: 
    - /2024/06/26/web3-threat-modeling
---

Using Blockchain Technology does not make your application secure. The Blockchain-based Applications are as vulnerable, or more, than traditional applications for many reasons. For example, the Blockchain-based Application, called Web3 Application or Decentralised Application (dApp) have defects like traditional applications because they are software as well. Both Blockchain and traditional applications are created by humans to be used by humans, and both types of applications make the same mistakes and face the same threats. Other reasons are the Smart Contracts included in Blockchain-based Applications increase the attack surface, the Wallet adds a new attack vector and the very tenet of Decentralisation in Blockchain-based applications also becomes its Achilles' heel. In simple words, every revolution and innovation in the IT space comes with its own set of challenges and vulnerabilities, and all this is happening to Web3 Applications.

![](/media/assets/blog20240626_web3_tm/01-web3-tm-architecture-ini.png)
{{< rawhtml >}}
<i><center>Blockchain-based Application Architecture & Security</center></i>
{{</ rawhtml >}}

<!--more-->

Starting from the assumption that Blockchain Networks are a managed secure service. I’m going to run the first iteration of Threat Modeling only for a typical Blockchain-based, or Web3, Application, without considering the Blockchain Network. Threat Modeling will allow us to bring security into system trade-offs, identify blind spots or architectural and design security gaps, to be able to communicate and understand threats and define corresponding mitigation strategies.


## Web3 Security Incidents: facts

According to the SlowMist Monthly Security Report.

> In April 2024, there were a total of 37 security incidents, resulting in approximately $90.81 million in losses. Based on the data from the [SlowMist Blockchain Security Incident Database](https://hacked.slowmist.io/statistics/?c=all&d=all), these incidents were caused by contract vulnerabilities, third-party vulnerabilities, exit scams, and hacked accounts.

And

> Of the 37 reported security incidents this month, 15 were due to exit scams by project teams, accounting for 40.54% of the total incidents. These exit scam incidents resulted in losses of approximately $37.57 million, representing 41.4% of the total stolen amount this month. 

And

> This month, 10 incidents of contract vulnerability exploitation resulted in losses of approximately $46.93 million, accounting for 51.7% of the total stolen amount this month.

In brief, incidents come from the exploitation of vulnerabilities available throughout the application attack surface, including many incidents come from the exploitation of the human factor and the other large part of incidents come from the exploitation of vulnerabilities in the Smart Contracts because that is a new attack vector in Web3 Applications. That is because “[security is only as strong as the weakest link](https://www.schneier.com/blog/archives/2005/12/weakest_link_se.html)” and malicious people put focus and use all their resources to take advantage of weakest links.


{{< image-resize "assets/blog20240626_web3_tm/02-web3-tm-slowmist-hacked-db-top-10.png" 710x >}}
{{< rawhtml >}}
<i><center>SlowMist Report about security in Blockchain space</center></i>
{{</ rawhtml >}}


## Continuous Threat Modeling

Since “[Security is a process](https://www.schneier.com/essays/archives/2000/04/the_process_of_secur.html)”, Threat Modeling is best applied continuously along Software Development Life Cycle (SDLC), in this article I’ll not be able to repeat this activity more than once. This article is only the first iteration but I think it will help us to highlight in an iterable way the most important threats that blockchain-based applications are facing. 

Another recommendation is to try to introduce this practice as part of technical design and analysis of requirements meetings, independently of the kind of application you want to build. This will help to gain security awareness among your team.


## Bringing problems, not solutions

I’ve heard many times “The application is secure because is using Blockchain”, “My applications is a front-end that call to Smart Contracts and It has not any secret or sensitive information to protect” or “The application is secure because all Smart Contracts are been peer-reviewed and audited”. As I stated before, the technology Blockchain is only a part of the application, and as each part they contribute a little bit more in increasing the attack surface and if that security risk is not managed, then early or late, that will impact your business. 

That is the reason why conducting Threat Modeling sessions among our Teams will allow us to detect threats, raise them and implement countermeasures before adversaries take advantage of those gaps. Threat Modeling doesn’t solve the problems, it only helps us identify and raise them. But doing that solves a huge part of the problem. As you know “out of sight, out of mind” or if a threat has not been identified, it can not be mitigated.

## Getting started the Threat Modeling Process

We are going to follow [The Ultimate Beginner's Guide to Threat Modeling](https://shostack.org/resources/threat-modeling) (by Shostack & Associates), specifically we will follow The Shostack’s Four Question Framework:


{{< image-resize "assets/blog20240626_web3_tm/03-web3-tm-four-question-framework.png" 710x >}}
{{< rawhtml >}}
<i><center>The Shostack’s Four Question Framework</center></i>
{{</ rawhtml >}}

And for the 2nd question “What can go wrong”, we will use the lovely whitepaper [Fast, Cheap and Good](https://shostack.org/files/papers/Fast-Cheap-and-Good.pdf), that will allow us to contextualise and run a first iteration for our scenario. This whitepaper introduces some techniques and tools to ease this 2nd phase.

The findings will be complemented with information from articles about Web3 Architecture, Blockchain’s Promises and Principles, Web3 Products and Services and Incident and Vulnerabilities Databases in Web3. 

### Question #1. What are we working on?

We have to define or clarify what we are working on. In this case, we want to build a simple Web3 Application, which is depicted in the next diagram. 

#### Model the System

We should review the requirements, existing design documents and have many technical and business interviews in order to have a full understanding of what we are doing and what we want to do. Since we would like to ease the introduction of TM to the Web3 world, well, using a high level architecture diagram rather than a data flow diagram (DFD) will be easier to understand. Then let’s start with these coarse grained requirements: “We want to create a decentralised Web Application on the Ethereum Blockchain. It should consist of a user interface that interacts with deployed Solidity-based Smart Contracts”. 

The components and services are:
* Web Client: Chrome, Firefox or Brave.
* Wallet: Metamask
* Package Manager: NPMJS
* Source Code Repository service: Two public repositories in Github, one for application source code and second one for Smart Contracts Solidity code.
* IPFS: IPFS Network for storage of metadata, IPFS Gateway to retrieve content and Fleek to manage the deployment of static websites.
* RPC and Subgraph Service Providers: Alchemy, Satsuma and Infura.
* Smart Contracts: Solidity
* L1 & L2 Blockchains: Ethereum and Polygon.

{{< image-resize "assets/blog20240626_web3_tm/04-web3-tm-architecture-flows.png" 710x >}}
{{< rawhtml >}}
<i><center>High Level Web3 Application Architecture</center></i>
{{</ rawhtml >}}

#### High Level Architecture Diagram with Data and Process Flows

Next table lists all data and process flows identified when the Web3 Application is being implemented (sysops) and when it is on running time. We did this separation because it allows us to raise threats that affect specifically during build time and others that affect in run time.

They are:

{{< image-resize "assets/blog20240626_web3_tm/05-web3-tm-build-time-flows.png" 710x >}}
{{< rawhtml >}}
<i><center>05-web3-tm-build-time-flows.png</center></i>
{{</ rawhtml >}}

The next table shows all data and process flows identified during the execution of Web3 Application. The flows are:


{{< image-resize "assets/blog20240626_web3_tm/06-web3-tm-run-time-flows.png" 710x >}}
{{< rawhtml >}}
<i><center>06-web3-tm-run-time-flows.png</center></i>
{{</ rawhtml >}}

### Question #2. What can go wrong?

Once we have the architecture and defined the context of the application, outlined all data and process flows, we are ready to enumerate the threats that we can identify. 
Remember, you can use any tool you feel comfortable with, in my case, we do an “evil brainstorming” with colleagues that are working in the Blockchain space and combine it with the outcome from [techniques recommended by Adam Shostack](https://shostack.org/files/papers/Fast-Cheap-and-Good.pdf). 

#### Threats Enumeration

{{< image-resize "assets/blog20240626_web3_tm/07-web3-tm-build-time-threats.png" 710x >}}
{{< rawhtml >}}
<i><center>07-web3-tm-build-time-threats</center></i>
{{</ rawhtml >}}

{{< image-resize "assets/blog20240626_web3_tm/08-web3-tm-run-time-threats.png" 710x >}}
{{< rawhtml >}}
<i><center>08-web3-tm-run-time-threats</center></i>
{{</ rawhtml >}}

### Question #3. What are we going to do about it?

As I stated before, this is not an in-depth threat modeling process, this only attempts to begin quickly, explore what we are doing and raise and highlight gaps and potential problems. However, while we were doing threat enumeration, many solutions came to our minds, that is why We’ve added the next section about Countermeasures where We outlined some suggestions.

#### Countermeasures & Mitigation

{{< image-resize "assets/blog20240626_web3_tm/09-web3-tm-build-time-countermeasures.png" 710x >}}
{{< rawhtml >}}
<i><center>09-web3-tm-build-time-countermeasures</center></i>
{{</ rawhtml >}}

{{< image-resize "assets/blog20240626_web3_tm/10-web3-tm-run-time-countermeasures.png" 710x >}}
{{< rawhtml >}}
<i><center>10-web3-tm-run-time-countermeasures</center></i>
{{</ rawhtml >}}

## Conclusions

1. Threat Modeling is about contextualising and understanding what, how and why we are building an application. These sessions should be integrated to technical, design, analysis or retrospective meetings in a continuous way, independently of the kind of application you want to build. This will help to gain security awareness and familiarise in countermeasure plans among your team.
2. We can confirm that in Web3 Applications can be identified more threats than in the Web2 world. That is because Web3 is a specialisation of Web2 Application with a set of constraints and new attack vectors such as: Decentralisation, Wallets and Smart Contracts.
3. Many of the detailed countermeasures make reference to Web2 technical approaches or patterns, even the Smart Contracts require, from a security point of view, SAST (Static Application Security Testing) and DAST (Dynamic Application Security Testing) tools to identify vulnerabilities. While that other countermeasures require reconsider or redefine the concept of “Decentralisation” in our Web3 Application. Is “Decentralisation” a “buzzword” or a mandatory requirement?. 
4. The implementation of “Decentralisation” impacts the architecture of the application. It forces building a static and monolith web application to be served from IPFS Network and using IPFS to persist its metadata rather than using DB. Another consequence of this is leaking secrets in the front-end and trust in an external addon or plugin or application only to deal with key material such as wallet address, private keys, etc. To sort those threats, the listed countermeasures suggest embracing Multilayered Architecture (add a backend and/or API Gateway), introduce a Secrets Management Tool, implement a Monitoring Framework, etc.

## Resources

* Threat Modeling in Web3: A Guide to DeFi Security by John Amatulli, August 31, 2023 - https://www.linkedin.com/pulse/threat-modeling-web3-guide-defi-security-john-amatulli/ 
* Ethereum: Introduction to dApps - https://ethereum.org/en/developers/docs/dapps/ 
* Mitre ATT&CK - https://attack.mitre.org 
* SlowMist Blockchain Security Incident Database - https://hacked.slowmist.io 
* Immunefi Top 10 Bugs - https://immunefi.com/immunefi-top-10/ 
* DefiLlama Hacks - https://defillama.com/hacks 
* CryptoScamDB - https://cryptoscamdb.org/scams 
* Top 5 Web3 security breaches: A deep dive into DApp frontend and API vulnerabilities - https://escape.tech/blog/top-5-web3-security-breaches/ 

## Acknowledgement

Thanks to Guido Portalanza & Gustavo Vazquez Amado, for their unconditional collaboration during the writing of this article.
