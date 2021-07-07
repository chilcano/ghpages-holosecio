---
title: SAST in Cloud based SDLC
date: 2021-07-06T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
---

[SAST](https://en.wikipedia.org/wiki/Static_application_security_testing) stands for "Static Application Security Testing" and it is used to identify vulnerabilities by reviewing the source code. The best point or place to implement this Security Testing, and according the Security Best Practices, is in early stages of your CI/CD Pipeline. But What about of SAST in Cloud Native Applications?. You will see in this post 😉 how to deal with that using only opensource.

[![](/assets/img/20210706-sast-in-the-cloud-native-sdlc.png)](/assets/img/20210706-sast-in-the-cloud-native-sdlc.png)
{{< rawhtml >}}
<i><center>Static Application Security Testing (SAST) in the Cloud Native SDLC</center></i>
{{</ rawhtml >}}

## SAST in Cloud Native Applications

Implement SAST in old-school Monolith Application is/was easy, but how to do the same with Cloud Native Applications?. The answer is using as many SAST tools as different types of code and artifacts compose your stack.   
For example, a standard Cloud Native Application stack is composed of:
1. Microservices in different languages (Python, Golang, ...)
2. REST and GraphQL APIs
3. Docker containers (Dockerfile and Images)
4. Infrastructure as Code (Terraform or CloudFormation)
5. Configuration code (Chef, Bash, Ansible, ...)

Then, we are going to require at least 5 different SAST tools to review statically the code for each kind of code or artifact.

<!--more--> 

## Opensource SAST tools for Cloud Native stacks

1. 



[](#)

{{< rawhtml >}}
<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRTLn8bLX-Sp6JEbKcJIludCb6wJbTM-5xV5te94srdYnmLYutCu9vcgmiWcc2taioH5cJcj2xXH_Ba/pubhtml?widget=true&amp;headers=false" width="800" height="800"></iframe>
{{</ rawhtml >}}

[Click here to download the list in PDF format](/assets/pages/2020-02-10-security-along-the-container-based-sdlc-oss-tools-list.pdf).  
If don't see a open source security product in the document that is worth being reviewed, please, drop me an email and I'll add to document and review it.

## Conclusions

 1. ...



## References

1. [33(+) K8s Security Tools - Sysdig / Mateo Burillo / July 2019](https://sysdig.com/blog/33-kubernetes-security-tools).
2. [Kali Linux Tools Listing](https://tools.kali.org/tools-listing).
3. [Top 10 Open Source Security Testing Tools for Web Applications - Hackr.io / Youssef Nader / Last Updated 05 Feb, 2020](https://hackr.io/blog/top-10-open-source-security-testing-tools-for-web-applications).
4. [Awesome Penetration Testing / Nick Raienko](https://github.com/enaqx/awesome-pentest).


https://github.com/analysis-tools-dev/static-analysis#security

