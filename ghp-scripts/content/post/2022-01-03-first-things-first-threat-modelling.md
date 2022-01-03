---
title: 'First things first: Threat Modelling'
date: 2022-01-03T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
url: /2022/01/03/first-things-first-threat-modelling
aliases: 
   - /post/2022/01/03/first-things-first-threat-modelling
---

On 2014 RSA Conference (archive not available), Eric Olson of Cyveillance said a good and real simil about Threat Modelling: "It is a lot like teenage sex: Everyone is talking about it, 
everyone thinks everyone else is doing it, and most of the few people who are actually doing it aren't doing it all that well".

Well, in this post I'll try to help you do it well from the Tooling point of view.

## What is Threat Modelling

From [Wikipedia](https://en.wikipedia.org/wiki/Threat_model):
> Threat modeling is a process by which potential threats, such as structural vulnerabilities or the absence of appropriate safeguards, can be identified, enumerated, and mitigations can be prioritized.

In other words, using Threat Modelling we will be able to identify potential threats along your process (Software Development Life Cycle) and anticipate before happening.

## Why it is first thing to do in Cybersecurity

Because:
* It makes sense:
  - Minimum Viable Secure. 
  - Shift-Left Testing. 
  - Pareto Principle.
  - Holistic Security.
* It is cheaper.
* No security skills are required when modelling.

## Why now 



{{< image-resize "/assets/blog20210904_sast_2/20210904-sast-in-your-cicd-pipeline-full-stack-apps.png" 710x >}}
{{< rawhtml >}}
<i><center>A SAST Jenkins Pipeline for a Full Stack Cloud Native Application</center></i>
{{</ rawhtml >}}


"Security is a process, not a product" (Bruce Schneier, April 2000). Get started with #Threat #Modelling. Here are some open source tools to accomplish that:

1) Cairis: https://cairis.org
2) Microsoft Threat Modeling Tool: https://docs.microsoft.com/en-us/azure/security/develop/threat-modeling-tool
3) OWASP pytm: https://github.com/izar/pytm
4) OWASP Threat Dragon: https://threatdragon.org
5) Threagile: https://threagile.io
6) Threats Manager Suite (TMS): https://threatsmanager.com by Simone Curzi
7) ThreatSpec https://github.com/threatspec/threatspec

Here more #security tools (~102) to use in the #SDLC: https://holisticsecurity.io/2020/02/10/security-along-the-sdlc-for-cloud-native-apps/

<!--more--> 

## References

1. https://shostack.org/resources/tm-in-2021.html
2. https://www.threatmodelingmanifesto.org/
3. Raising resilience against advanced cyber attacks through threat modeling: https://www.unifiedkillchain.com/
4. Minimum Viable Secure Product: https://mvsp.dev/mvsp.en/index.html