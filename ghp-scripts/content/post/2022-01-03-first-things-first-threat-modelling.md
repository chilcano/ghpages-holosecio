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

![](/media/assets/blog20220103_threat_model/20220103_threat_model_and_devsecops.png)
{{< rawhtml >}}
<i><center>Threat Model and DevSecOps</center></i>
{{</ rawhtml >}}

Well, in this post I'll try to help you do it well from the Tooling point of view.

<!--more--> 

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

Before, this was the domain of the Security Consultant aided by some commercial tool. Not now, there are very good opensource tools of all kinds, they are able to be integrated into CI/CD Processes, 
even they have semi-automated functionalities: templates and examples already pre-loaded, database of common threats by type of application already defined, etc.  
There is not excuse now. Here all opensource tools I've found and tested:

| 1. [Cairis](https://cairis.org) |
|--- |
| * Apache Software License.  |
| * Live demo: https://demo.cairis.org  |
| * It is a Web Application and can be shared as part of your Toolchain. |
| * Features exposed as RERTful API and can be integrated into your ecosystem. |
| * Focused on specification of requirements, modelling threats and managing risks. |
| * Manages the security, usability, and design artifacts in one place. |
| * We can visualise the design from different perspectives. |
| * Leverages attack and architectural patterns. |
| * Show all security, usability and design elements associated with your product's risks. |
| * Quickly validate even the most basic design for known security design and privacy problems. |
| * Generate documentation from Volere compliant requirement specification to GDPR DPIA docs. |
|--- |

| 2. [OWASP pytm](https://github.com/izar/pytm) |
|--- |
| * xxxx |
|--- |

| 3. [OWASP Threat Dragon](https://threatdragon.org)
|--- |
| * xxxx |
|--- |

| 4. [Threagile](https://threagile.io) |
|--- |
| * xxxx |
|--- |

| 5. [ThreatSpec](https://github.com/threatspec/threatspec) |
|--- |
| * xxxx |
|--- |

| 6. [Microsoft Threat Modeling Tool](https://docs.microsoft.com/en-us/azure/security/develop/threat-modeling-tool) |
|--- |
| * xxxx |
|--- |

| 7. [Threats Manager Suite (TMS)](https://threatsmanager.com) |
|--- |
| * xxxx |
|--- |

by Simone Curzi


## References

1. https://shostack.org/resources/tm-in-2021.html
2. https://www.threatmodelingmanifesto.org/
3. Raising resilience against advanced cyber attacks through threat modeling: https://www.unifiedkillchain.com/
4. Minimum Viable Secure Product: https://mvsp.dev/mvsp.en/index.html
5. More OSS security tools (~102) to use in the SDLC: https://holisticsecurity.io/2020/02/10/security-along-the-sdlc-for-cloud-native-apps/