---
title: 'Applying Minimum Viable Security to APIs'
date: 2024-04-24T12:00:00+02:00
draft: true
type: post
layout: single_simple
categories: [SDLC, DevSecOps, Holism]
tags: [Pareto, Shift-Left, SAST, SCA, DAST, API]
url: /2024/04/24/minimum-viable-security-to-apis
---

From Security standpoint, exposing Application functionalities as APIs means increasing the attack surface. The APIs are like to adding windows to a house, we know the doors usually are secure and being monitored in houses, however new windows might not be built with security in mind. Well, in this post I'll explain how to check the security of your APIs and make it more secure according [The Minimum Viable Security, following Pareto Principle and Shift-Left Testing](https://holisticsecurity.io/2020/03/08/minimum-viable-security-for-a-k8s-webapp-tls-everywhere-part1/) approaches.

Some time ago I had the chance to speak (in Spanish) about [Securing API lifecycle through the CI/CD](https://holisticsecurity.io/2021/12/29/seguridad-en-el-ci-cd-de-las-apis/), with that experience, I'm going to share the technical details on how to apply Minimum Viable Security to Application's RESTful APIs, specifically how to implement SAST, SCA & DAST using opensource tools. To do that, I'll use [MAC Address Manufacturer Lookup](https://github.com/chilcano/mac-address-manuf-lookup) python service.

![](/media/assets/blog20240424_api_mvs/20240424_secure_apis_01_sdlc_in_api.png)
{{< rawhtml >}}
<i><center>SDLC and APIs</center></i>
{{</ rawhtml >}}


<!--more-->

## Security along the APIs lifecycle

Software Development Life Cycle (SDLC) is an interable process with a sequence of stages that Engineers follow to gather requirements, plan, design and build Systems, Applications and/or Software. From Security point of view, we, the Security Specialsts, use different Security best practices and tools in each stage to make the end product (software) more robust, secure and reduce its defects and security issues.

The SDLC is more or less used to build any kind of software, on cloud, client/server, docker-based, blockchain-based, etc. That said, exposing a set of Application functionalities as RESTful APIs mean extending its features only, and doing that doesn't require a new SDLC, because the process stages will not change. The only thing we will need is extending our CI/CD pipelines by adding the right approach to check the security of newly RESTful API artifacts added to our Application stack.

> From Security standpoint, exposing functionalities as APIs only requires extending CI/CD pipelines and adding security checks in SDLC key stages.

## Using the Pareto Principle and Shift-Left Testing

I’ve borrowed both approaches to outline what I want for Minimum viable Security, while Pareto Principle helps to focus on what to test and what testing technology will be used on specific software artifacts, the Shift-Left Testing recommends where those tests in SDLC stages will be implemented, considering limited resources, budget, time and maximizing the security outcome. 
With that, the SDLC stages and Security Controls are:


![](/media/assets/blog20240424_api_mvs/20240424_secure_apis_02_mvs_in_sdlc.png)
{{< rawhtml >}}
<i><center>Implementing Minimum Viable Security in APIs Projects</center></i>
{{</ rawhtml >}}



| SDLC Stage    | Security Control   | Tool options  
|---            |---                 |---
| 02. CODE      | SAST, Config Drift | SonarQube, Bandit (Python), Spectral (OpenAPI spec).
| 03. BUILD     | SCA                | Trivy, OWASP Dependency-Check.
| 04. TEST      | DAST               | OWASP ZAP.
| 07. OPERATE   | WAF                | [Apache APISIX](https://api7.ai/apisix) with [Coraza WAF](https://coraza.io) or [Chaitin SafeLine](https://github.com/chaitin/SafeLine).
| 08. MONITOR   | Logging            | APISIX with ELK, Loki, Prometheus, Grafana, etc.


With this and considering the [MAC Address Manufacturer Lookup](https://github.com/chilcano/mac-address-manuf-lookup) python service, we could reduce the above list and have this:

__1. SAST for Application__

The Service is implemented in Python, using a [SonarCloud](https://sonarcloud.io/) free account is enough to scan statically the Python code in entire repository.
You can run scan for vulnerabilities in your code easily with SonarCloud by integrating it with your Github repository. 
* You can get a report every time you make changes in your code, in my case, you can see the report for the MAC Address Manufacturer Lookup repository here: https://sonarcloud.io/summary/overall?id=chilcano_mac-address-manuf-lookup

__2. SAST for APIs__

The Service is exposed as RESTful API, we are using the [APIFlask Python library](https://apiflask.com) to generate the OpenAPI specification and documentation. I'll use the [Spectral CLI](https://stoplight.io/open-source/spectral) as an API style guide enforcer and linter. It will require a set of rules to enforce the security, in this case the [OWASP API Security Top 10 (2023)](https://owasp.org/www-project-api-security) and the [Spectral OWASP API Security Ruleset](https://github.com/stoplightio/spectral-owasp-ruleset) are suitable to check of security of these APIs.
* You can see the report generated by Spectral and imported to Github Security - Code scanning here: https://github.com/chilcano/mac-address-manuf-lookup/security/code-scanning
* If you are interested on how to trigger Spectral CLI to check OWASP API Security ruleset from your Github repository, you can use this Github workflow: https://github.com/chilcano/mac-address-manuf-lookup/blob/main/.github/workflows/02-sast-api-sec-spectral-owasp.yaml

__3. SCA__

The MAC Address Manufacturer Lookup service uses Python libraries, a Dockerfile to build the application, a Docker Image based on Linux Alpine with a pre-installed Python environment to ship the application and its configuration, and since all source code, configuration files, Dockerfile, etc. are included in a single [public Github repository](https://github.com/chilcano/mac-address-manuf-lookup) I will use only a single tool to take care of everything in one single shot. The right tool to do everything is [Trivy](https://trivy.dev/).
* Although Trivy CLI can be executed from a local terminal, I've implemented a Github workflow that is triggered by events in the repository, it generates different kind of reports and are published as Github artifacts, although the report in Sarif format would be imported to Github Security - Code scanning Dahboard as well. This Github workflow is available here: https://github.com/chilcano/mac-address-manuf-lookup/actions/workflows/01-sca-app-deps-sec-trivy.yaml


__4. DAST__

Conduct Dynamic Application Security Testing (DAST) requires the application is up and running, and an appropiate tool to scanner all web interfaces exposed for this application. The recommended tool to do this is [OWASP ZAP](https://www.zaproxy.org). It works as a web proxy where we can automate the execution of many different tactics to find gaps and bugs in the applications. ZAP provides extensions and scripts to scan the security of APIs. The next guides explain how to do that:
* How can you use ZAP to scan APIs?: https://www.zaproxy.org/faq/how-can-you-use-zap-to-scan-apis/
* Scanning APIs with ZAP: https://www.zaproxy.org/blog/2017-06-19-scanning-apis-with-zap/
* ZAP - API Scan: https://www.zaproxy.org/docs/docker/api-scan/


![](/media/assets/blog20240424_api_mvs/20240424_secure_apis_03_sast_sca_dast.png)
{{< rawhtml >}}
<i><center>SAST, SCA and DAST for APIs</center></i>
{{</ rawhtml >}}


__5. Web Application Firewall (WAF)__

Once the Application has been deployed, an way to protect it when it is up and running is using a WAF. You can install and configure a WAF to catch the incoming traffic before hitting the application, however this requires re-configure the application and re-route the traffic through the WAF.

To make easier everything and since our Application exposes APIs, to do everything in the API Gateway side. With that, changes in the Application side and re-route the traffic will not needed. Generally, the API Gateway supports making these changes and configurations.

The combination recommended for that is APISIX as API Gateway and Coraza as WAF. Next guides explain very well how to accomplish that:
* Protecting Your APIs in the Wild - A Deep Dive into WAF and API Gateway Integration: https://api7.ai/blog/waf-and-api-gateway-integration
* Integrate APISIX with Coraza - https://docs.api7.ai/apisix/how-to-guide/security/waf/integrate-with-coraza

![](/media/assets/blog20240424_api_mvs/20240424_secure_apis_04_gateway_and_waf.png)
{{< rawhtml >}}
<i><center>APISIX and Coraza WAF</center></i>
{{</ rawhtml >}}


__6. Observability__

Observability is important in Security. If we don't know what is happening with my application, we can not make decisions to enhance the security and the health of my application.
As stated before, an API Gateway makes easier manipulate the traffic and integrate with 3rd party services. If we want to monitor the activity and performance of my running application and its APIs, then we need collect all log events and analyze that activity.

That's why I've fallen in love with APISIX. It provides easier mechanisms to integrate monitoring services such Log Indexers, Log SaaS, Tracing, Metrics Monitoring, etc. Next guides to implement observability (security monitoring):
* Observe APIs with APISIX - https://apisix.apache.org/docs/apisix/tutorials/observe-your-api/
* API Observability with APISIX Plugins - https://apisix.apache.org/blog/2022/04/17/api-observability/


![](/media/assets/blog20240424_api_mvs/20240424_secure_apis_05_observability.png)
{{< rawhtml >}}
<i><center>API Observability with APISIX</center></i>
{{</ rawhtml >}}


## Conclusions

* Adopt API First approach, it allows you be aware what functionalities and services are being exposed and should be protected and monitored. Using an OpenAPI spec file you can automate the security checking from your CI/CD pipeline. This is the first thing you should deal when implementing APIs.
* Consider an API Gateway as part of your Application stack. The API Gateway will make easier the thing about security be implemented, specifically advanced security cotrols like Runtime Protection through WAF and Security Observability.
* There are many things to secure when building Applications and APIs, but if you have release faster with a good level of security, then embrace the Minimum Viable Security approach and implement it using opensource tools. For more security tools, I've created this list for you: https://holisticsecurity.io/sec-sdlc-oss-tool-list/

