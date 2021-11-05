---
title: 'Secrets Management in the last mile'
date: 2021-10-12T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
url: /2021/11/12/secrets-management-in-the-last-mile
---

"Securing secrets once they have been delivered" is the responsibility of Container-app (secret consumer). I call it "Secret Management in the Last Mile" and it is the weakest link in all Secret Management Solutions. However, this risk can be minimized by taking a SPIFFE-based approach (Zero Trust, Attestation) to trusting the way the secret is accessed from the container application. 
AWS has a service for this called Nitro Enclaves. Although, in my opinion, this is like "using a sidge-hammer to break a nut". 
Here a Twitter discussion I had: 

https://mobile.twitter.com/lizrice/status/1116293199499337728

{{< image-resize "/assets/blog20210904_sast_2/20210904-sast-in-your-cicd-pipeline-full-stack-apps.png" 710x >}}
{{< rawhtml >}}
<i><center>A SAST Jenkins Pipeline for a Full Stack Cloud Native Application</center></i>
{{</ rawhtml >}}

<!--more--> 

## Conclusions

1. xxxx

## References

1. [Security along the SDLC for Cloud-Native Apps](/2020/02/10/security-along-the-container-based-sdlc/#oss-sec-list) - Posted on 2020/02/10
2. [SAST in your SDLC for Cloud-Native Apps - Part 1](/2021/07/06/sast-in-sdlc-for-cloud-native-apps/)
