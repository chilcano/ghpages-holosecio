---
title: "Hands on with TLS Authentication for Microservices"
date: 2021-06-22T10:00:10+02:00
draft: false
type: post
layout: single_simple
categories: [Security, Talk]
tags: [Docker, TLS, Sidecar, Caddy, Proxy]
---

On March 25th I had the opportunity to collaborate with a workshop at [The DevOps Playground](https://www.meetup.com/DevOpsPlayground/) Meetup about How to use TLS to authenticate and authorize communications between and to Microservices. 

![](/assets/img/20210622-devops-playground-mtls-authn-for-microservices.png)

This event was very special for me because it was my second event in English after many years. There are many things to improve, but that does not discourage me from following this path, in fact I am already preparing the next workshop.
From here I thank [The DevOps Playground](https://www.meetup.com/DevOpsPlayground/) and [ECS](https://ecs.co.uk) for supporting me before, during and after the event, I also thank everyone who attended the playground, and if you want read the presentation, go through the code or watch the playground session again, below you will find the details:

<!--more-->

### Abstract:

While Transport Layer Security (TLS) protects communications between two parties for confidentiality and integrity, the Public Key Certificates (x.509) and the Certificate Authority (CA) will allow users to set a cryptographic identity and build a trust relationship between these parties.

With all these concepts, we will be able to secure (encrypt) data in transit and authenticate the parties in scenarios such as Client-Server or Service-Service.

During this Playground you will learn:
- What One-Way TLS, Two-Way TLS or Mutual TLS (mTLS) are,
- How to use Public Key Certificates,
- How to use Mutual TLS together for securing communications among Microservices,
- How to automate everything.

### Resources

* [Presentation](https://github.com/chilcano/mtls-apps-examples/blob/main/slides/DevOpsPlayground-MTLSAuthnforMicroservices.pdf)
* [Source code](https://github.com/chilcano/mtls-apps-examples)
* [YouTube](https://youtu.be/aMD7vq1EWnA)
