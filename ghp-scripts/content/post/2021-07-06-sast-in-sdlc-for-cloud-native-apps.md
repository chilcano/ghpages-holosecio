---
title: SAST in SDLC for Cloud-Native Apps
date: 2021-07-06T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
url: /2021/07/06/sast-in-sdlc-for-cloud-native-apps
aliases: 
   - /post//2021/07/06/sast-in-sdlc-for-cloud-native-apps
---

[SAST](https://en.wikipedia.org/wiki/Static_application_security_testing) stands for "Static Application Security Testing" and it is used to identify vulnerabilities by reviewing the source code. The best point or place to implement this Security Testing, and according the Security Best Practices, is in early stages of your CI/CD Pipeline. But What about of SAST in Cloud Native Applications?. You will see in this post 😉 how to deal with that using only opensource.

[![](/assets/blog20210706_sast/20210706-sast-in-the-cloud-native-sdlc.png)](/assets/blog20210706_sast/20210706-sast-in-the-cloud-native-sdlc.png)
{{< rawhtml >}}
<i><center>Static Application Security Testing (SAST) in the Cloud Native SDLC</center></i>
{{</ rawhtml >}}

## SAST in Cloud-Native Applications

Implement SAST in old-school Monolith Application is/was easy, but how to do the same with Cloud Native Applications?. The answer is using as many SAST tools as different types of code and artifacts compose your stack.   
For example, a standard Cloud Native Application stack is composed of:
1. Microservices in different languages (Python, Golang, PHP, ...)
2. REST and GraphQL APIs
3. Docker containers (Dockerfile)
4. Infrastructure as Code (Terraform, CloudFormation, Kubernetes manifests, ...)
5. Configuration code (Chef, Bash, Ansible, ...)

Then, we are going to require 5 or less different SAST tools to review statically the code for each kind of code or artifact.

<!--more--> 

## Opensource SAST tools for Cloud-Native stacks

I'm going to list only the SAST tools, but if you want to browse the full list, look my post about [Security along the SDLC for Cloud-Native Apps](/2020/02/10/security-along-the-container-based-sdlc/#oss-sec-list).

| No. | SAST Tool                                              |                      | Vulnerability scanner for   |
|---  |---                                                     |---                   |---                          |
| 1.  | [Anchore Grype](https://github.com/anchore/grype)      | ![](/assets/blog20210706_sast/sast-anchore-grype.png)         | Containers and filesystems            |
| 2.  | [AquaSec Trivy](https://github.com/aquasecurity/trivy) | ![](/assets/blog20210706_sast/sast-aquasec-trivy.png)         | Containers and application dependencies (Bundler, Composer, npm, yarn, etc) |
| 3.  | [AWS Cfn-Lint](https://github.com/aws-cloudformation/cfn-lint)      | ![](/assets/blog20210706_sast/sast-cfn-lint.png) | CloudFormation (.json, .yaml). Rules in Python |
| 4.  | [AWS Serverless Rules](https://github.com/awslabs/serverless-rules) | ![]()                                            | Serverless Patterns in CloudFormation |
| 5.  | [Bandit](https://github.com/PyCQA/bandit)                   | ![](/assets/blog20210706_sast/sast-bandit.png)        | Python code |
| 6.  | [Checkmarx KICS](https://github.com/Checkmarx/kics)         | ![](/assets/blog20210706_sast/sast-checkmarx-kics.png)| Terraform (.tf, tfvars), CloudFormation (.json or .yaml), Ansible (.yaml), Dockerfile, K8s manifests, OpenAPI (.json or .yaml) |
| 7.  | [Clair](https://github.com/quay/clair)                      | ![](/assets/blog20210706_sast/sast-clair.png)         | Containers                            |
| 8.  | [Dagda](https://github.com/eliasgranderubio/dagda)          | ![]()                                                 | Containers and monitor Docker daemon  |
| 9.  | [Dockle](https://github.com/goodwithtech/dockle)            | ![](/assets/blog20210706_sast/sast-dockle.png)        | Containers and support CIS Benchmarks |
| 10. | [GolangCI-Lint](https://github.com/golangci/golangci-lint)  | ![](/assets/blog20210706_sast/sast-golangci-lint.png) | Golang code |
| 11. | [GoSec](https://github.com/securego/gosec)                  | ![](/assets/blog20210706_sast/sast-gosec.png)         | Golang code |
| 12. | [PHPStan](https://github.com/phpstan/phpstan)               | ![](/assets/blog20210706_sast/sast-phpstan.png)       | PHP code    |
| 13. | [Pylint](https://www.pylint.org)                            | ![](/assets/blog20210706_sast/sast-pylint.png)        | Python code |
| 14. | [Skyscanner CFrippe](https://github.com/Skyscanner/cfrippe) | ![](/assets/blog20210706_sast/sast-skyscanner-cfrippe.png) | CloudFormation (.json, .yaml). Rules in Python |
| 15. | [SonarQube CE](https://www.sonarqube.org)                   | ![](/assets/blog20210706_sast/sast-sonarqube.png)     | Platform and carry out analysis of over 20 programming languages |
| 16. | [Stelligent cfn_nag](https://github.com/stelligent/cfn_nag) | ![](/assets/blog20210706_sast/sast-stelligent-cfn_nag.png) | CloudFormation (.json, .yaml). Rules in Ruby   |
| 17. | [Terraform Linter](https://github.com/terraform-linters/tflint)  | ![]()                                            | Terraform (.tf, .tfvars) |
| -   |                                                                  |                                                  |                          |

## Designing the CI/CD Pipeline with SAST stages

I am going to pick up the next tools:

1. Jenkins as CI/CD Server
2. SonarQube as Platform with multiple default Linters (Python, Golang, etc)
3. Checkmarx KICS







## Conclusions

 1. ...



## References

1. [33(+) K8s Security Tools - Sysdig / Mateo Burillo / July 2019](https://sysdig.com/blog/33-kubernetes-security-tools).
2. [Kali Linux Tools Listing](https://tools.kali.org/tools-listing).
3. [Top 10 Open Source Security Testing Tools for Web Applications - Hackr.io / Youssef Nader / Last Updated 05 Feb, 2020](https://hackr.io/blog/top-10-open-source-security-testing-tools-for-web-applications).
4. [Awesome Penetration Testing / Nick Raienko](https://github.com/enaqx/awesome-pentest).


https://github.com/analysis-tools-dev/static-analysis#security

