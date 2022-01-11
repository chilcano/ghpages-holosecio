---
title: 'First things first: Threat Modelling'
date: 2022-01-03T10:00:10+02:00
draft: false
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

## Why is it the first thing to do in Cybersecurity ?

Because:
* It makes sense:
  - Minimum Viable Secure. 
  - Shift-Left Testing. 
  - Pareto Principle.
  - Holistic Security.
* It is cheaper.
* No security skills are required when modelling.

## Why now ? Mature Threat Modelling Tools

Before, this was the domain of the Security Consultant aided by some commercial tools. Not now, because there are very good opensource tools of all kinds, many of them are integrable into CI/CD Pipelines, 
even they have functionalities that help to be productive such as templates and examples already pre-loaded, database of common threats by type of application already defined, etc.  
> There is not excuse now. We have good mature opensource Threat Modelling Tools.  

Here all opensource tools I've found and reviewed:


| 1. [Cairis](https://cairis.org) | {{< image-resize "/assets/blog20220103_threat_model/logo-cairis.jpg" 60x >}} | 
|--- | --- |
| * Apache Software License.  |
| * Live demo: https://demo.cairis.org  |
| * It's a Web Application and can be shared as part of your Toolchain. |
| * Features exposed as RERTful API and can be integrated into your ecosystem. |
| * Focused on specification of requirements, modelling threats and managing risks. |
| * Manages the security, usability, and design artifacts in one place. |
| * We can visualise the design from different perspectives. |
| * Leverages attack and architectural patterns. |
| * Show all security, usability and design elements associated with your product's risks. |
| * Quickly validate even the most basic design for known security design and privacy problems. |
| * Generate documentation from Volere compliant requirement specification to GDPR DPIA docs. |
|--- | 

| 2. [OWASP pytm](https://github.com/izar/pytm) | {{< image-resize "/assets/blog20220103_threat_model/logo-owasp-pytm" 120x >}} |
|--- | --- |
| * MIT License. |
| * pytm: A Pythonic framework for threat modeling |
| * The goal of pytm is to shift threat modeling to the left, making threat modeling more automated and developer-centric. |
| * Based on your input and definition of the architectural design, pytm can automatically generate Data Flow Diagram (DFD), Sequence Diagram and Relevant threats to your system |
| * Provides a Threats database. It can be extended. |
|--- |

| 3. [OWASP Threat Dragon](https://threatdragon.org) | {{< image-resize "/assets/blog20220103_threat_model/logo-owasp-threat-dragon.png" 200x >}} |
|--- | --- |
| * Apache Software License. |
| * It can be used as a standalone desktop app for Windows and MacOS (Linux coming soon) or as a web application.  |
| * Live demo: https://threatdragon.org/login |
| * It is cross-platform threat modelling application including system diagramming and a threat rule engine to auto-generate threats/mitigations. |
| * The focus of the project is on great UX, a powerful rule engine and integration with other development lifecycle tools. |
| * Threat Dragon provides [STRIDE per Element](https://www.microsoft.com/security/blog/2007/10/29/the-stride-per-element-chart/) rules to generate the suggested threats for an element on the diagram - except for trust boundaries. The suggested threats can be individually accepted or ignored, and other threats added manually. |
|--- |

| 4. [Threagile - Agile Threat Modeling Toolkit](https://threagile.io) | {{< image-resize "/assets/blog20220103_threat_model/logo-threagile.png" 420x >}} |
|--- | --- |
| * MIT License. |
| * Live demo: https://run.threagile.io |
| * It allows to model an architecture with its assets in an agile fashion as a YAML file directly inside the IDE. |
| * Threagile toolkit checks a set of risk-rules execute security against the architecture model and create a report with potential risk and migitation advice. |
| * Generates automatically data-flow diagrams as well as other output formats (Excel and JSON). |
| * The risk tracking can also happen inside the Threagile YAML model file, so that the current state of risk mitigation is reported as well. |
| * It can either be run via the CLI or started as a REST server allowing easy integration into CI/CD Pipelines. |
|--- |

| 5. [ThreatSpec](https://github.com/threatspec/threatspec) | {{< image-resize "/assets/blog20220103_threat_model/logo-threatspec.png" 500x >}} |
|--- | --- |
| * MIT License. |
| * Threatspec is an open source project that aims to close the gap between development and security by bringing the threat modelling process further into the development process. |
| * This allows the developers and security engineers write threat specifications alongside code, then dynamically generating reports and data-flow diagrams from the code. |
| * This allows engineers to capture the security context of the code they write, as they write it by using `annotations`. |
| * How does it work?: Annotating your code. And supported language are: C, C++, C#, Golang, HTML, Java, Javascript, Shell and XML. |
|--- |

| 6. [Microsoft Threat Modeling Tool](https://docs.microsoft.com/en-us/azure/security/develop/threat-modeling-tool) |
|--- |
| * This tool is free to download and use.  |
| * Windows Desktop Application. |
| * It applies STRIDE threat classification scheme to the identified threats. |
| * It was designed with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models. |
| * It suggests and manages mitigations for security issues. |
| * It uses [STRIDE per Element](https://www.microsoft.com/security/blog/2007/10/29/the-stride-per-element-chart/) : Guided analysis of threats and mitigations. |
| * Designed for Developers and Centered on Software and focused on Design Analysis. |
|--- |

| 7. [Threats Manager Suite (TMS)](https://threatsmanager.com) |
|--- |
| * This tool is free to download and use. 
| * Created by [Simone Curzi](https://simoneonsecurity.com), Senior Consultant at Microsoft Global CyberSecurity Practice (GCP). |
| * Windows Desktop Application. |
| * TMS is based on a solid Open Source foundation called [Threats Manager Platform](https://github.com/simonec73/threatsmanager), which is under the MIT license. |
| * TMS has been designed to fulfill the needs of many different personas, from the super-Expert to the novice, including Project Managers, Product Owners, and Business Stakeholders. |
|--- |


## Other complementary Tools

Attack Maps, Assessment Methodologies, Frameworks to automate and integrate the Threat Intelligence process into CI/CD Pipelines, etc:

| 1. [The Raindance Project](https://github.com/devsecops/raindance) |
| --- |
| * Apache Software License. |
| * Project intended to make Attack Maps part of software development by reducing the time it takes to complete them. |
| * The attack map process helps identifying target surface and adversary attack strategies that lead to exploit and compromise. This project is extensive with a goal of creating re-usable and inheritable attack maps. |
| --- |


| 2. [Mozilla Rapid Risk Assessment (RRA)](https://infosec.mozilla.org/guidelines/risk/rapid_risk_assessment.html) |
| --- |
| * Mozilla License. |
| * The Rapid Risk Assessment or Rapid Risk Analysis (RRA) methodology helps formalize this type of decision making and ensures that the process is reproducible, consistent and the results are easy to communicate.. |
| --- |


| 3. [ThreatPlaybook](https://threatplaybook.io) |
| --- |
| * No mentioned. |
| * A unified DevSecOps Framework that allows you to go from iterative, collaborative Threat Modeling to Application Security Test Orchestration. |
| * ThreatPlaybook be used in CI/CD environments. It uses the Robot Framework. |
| * Here is a working example of Threat Models and Security Automation with ThreatPlaybook: https://github.com/we45/ThreatPlaybook-Example |
| --- |



## References

1. ["Threat Modeling in 2021" - By Adam Shostack](https://shostack.org/resources/tm-in-2021.html)
2. [The Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org)
3. [Raising resilience against advanced cyber attacks through threat modeling](https://www.unifiedkillchain.com)
4. [Minimum Viable Secure Product](https://mvsp.dev/mvsp.en/index.html)
5. [Why Threat Intelligence Is Like Teenage Sex - Dark Reading, 2014](https://www.darkreading.com/threat-intelligence/why-threat-intelligence-is-like-teenage-sex)
6. [More OSS security tools (~102) to use in the SDLC](https://holisticsecurity.io/2020/02/10/security-along-the-sdlc-for-cloud-native-apps/)