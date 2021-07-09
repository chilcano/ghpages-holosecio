---
title: SAST in your SDLC for Cloud-Native Apps
date: 2021-07-06T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
url: /2021/07/06/sast-in-sdlc-for-cloud-native-apps
aliases: 
   - /post/2021/07/06/sast-in-sdlc-for-cloud-native-apps
---

[SAST](https://en.wikipedia.org/wiki/Static_application_security_testing) stands for "Static Application Security Testing" and it is used to identify vulnerabilities 
by reviewing the source code. The best point or place to implement this Security Testing, and according the Security Best Practices, is in early stages of your 
CI/CD Pipeline. But What about of SAST in Cloud Native Applications?. You will see in this post 😉 how to deal with that using only opensource.

[![](/assets/blog20210706_sast/20210706-sast-in-your-sdlc-for-cloud-native-apps.png)](/assets/blog20210706_sast/20210706-sast-in-your-sdlc-for-cloud-native-apps.png)
{{< rawhtml >}}
<i><center>Static Application Security Testing (SAST) in the Cloud Native SDLC</center></i>
{{</ rawhtml >}}

<!--more--> 

## SAST in Cloud-Native Applications

Implement SAST in old-school or traditional Application is/was easy because you have to deal with a big block or a monolithic stack, but how to do the same with Cloud 
Native Applications?. The answer is using as many SAST tools as different types of code, artifacts or building blocks compose your stack.   
For example, a standard Cloud Native Application stack is composed of:
1. Microservices in different languages (Python, Golang, PHP, ...)
2. REST and GraphQL APIs
3. Docker containers (Dockerfile)
4. Infrastructure as Code (Terraform, CloudFormation, Kubernetes manifests, ...)
5. Configuration code (Chef, Bash, Ansible, ...)

Then, we are going to require 5 or less different SAST tools to review statically the code for each kind of code or artifact. Below I show a SAST tool list where you can pickup any tool for convenience or requirements.

### Opensource SAST tools for Cloud-Native stacks

I'm going to list only a few SAST tools, but if you want to browse the full list, even DAST, IAST or RASP tools, look my post about [Security along the SDLC for Cloud-Native Apps](/2020/02/10/security-along-the-container-based-sdlc/#oss-sec-list).

| No. | SAST Tool                                                   |                                                               | Vulnerability scanner for   |
|---  |---                                                          |---                                                            |---                          |
| 1.  | [Anchore Grype](https://github.com/anchore/grype)           | ![](/assets/blog20210706_sast/sast-anchore-grype.png)         | Containers and filesystems            |
| 2.  | [AquaSec Trivy](https://github.com/aquasecurity/trivy)      | ![](/assets/blog20210706_sast/sast-aquasec-trivy.png)         | Containers and application dependencies (Bundler, Composer, npm, yarn, etc) |
| 3.  | [AWS Cfn-Lint](https://github.com/aws-cloudformation/cfn-lint)      | ![](/assets/blog20210706_sast/sast-cfn-lint.png)      | CloudFormation (.json, .yaml). Rules in Python |
| 4.  | [AWS Serverless Rules](https://github.com/awslabs/serverless-rules) | ![]()                                                 | Serverless Patterns in CloudFormation |
| 5.  | [Bandit](https://github.com/PyCQA/bandit)                   | ![](/assets/blog20210706_sast/sast-bandit.png)             | Python code |
| 6.  | [Checkmarx KICS](https://github.com/Checkmarx/kics)         | ![](/assets/blog20210706_sast/sast-checkmarx-kics.png)     | Terraform (.tf, tfvars), CloudFormation (.json or .yaml), Ansible (.yaml), Dockerfile, K8s manifests, OpenAPI (.json or .yaml) |
| 7.  | [Clair](https://github.com/quay/clair)                      | ![](/assets/blog20210706_sast/sast-clair.png)              | Containers                            |
| 8.  | [Dagda](https://github.com/eliasgranderubio/dagda)          | ![]()                                                      | Containers and monitor Docker daemon  |
| 9.  | [Dockle](https://github.com/goodwithtech/dockle)            | ![](/assets/blog20210706_sast/sast-dockle.png)             | Containers and support CIS Benchmarks |
| 10. | [GolangCI-Lint](https://github.com/golangci/golangci-lint)  | ![](/assets/blog20210706_sast/sast-golangci-lint.png)      | Golang code |
| 11. | [GoSec](https://github.com/securego/gosec)                  | ![](/assets/blog20210706_sast/sast-gosec.png)              | Golang code |
| 12. | [PHPStan](https://github.com/phpstan/phpstan)               | ![](/assets/blog20210706_sast/sast-phpstan.png)            | PHP code    |
| 13. | [Pylint](https://www.pylint.org)                            | ![](/assets/blog20210706_sast/sast-pylint.png)             | Python code |
| 14. | [Skyscanner CFrippe](https://github.com/Skyscanner/cfrippe) | ![](/assets/blog20210706_sast/sast-skyscanner-cfrippe.png) | CloudFormation (.json, .yaml). Rules in Python |
| 15. | [SonarQube CE](https://www.sonarqube.org)                   | ![](/assets/blog20210706_sast/sast-sonarqube.png)          | Platform and carry out analysis of over 20 programming languages |
| 16. | [Stelligent cfn_nag](https://github.com/stelligent/cfn_nag) | ![](/assets/blog20210706_sast/sast-stelligent-cfn_nag.png) | CloudFormation (.json, .yaml). Rules in Ruby   |
| 17. | [Terraform Linter](https://github.com/terraform-linters/tflint)  | ![]()                                                 | Terraform (.tf, .tfvars) |
|-    |                                                                  |                                                       |                          |

## Designing the CI/CD Pipeline with a SAST stages

[![](/assets/blog20210706_sast/20210706-sast-in-your-cicd-pipeline.png)](/assets/blog20210706_sast/20210706-sast-in-your-cicd-pipeline.png)
{{< rawhtml >}}
<i><center>SAST stage in CI/CD Pipeline</center></i>
{{</ rawhtml >}}

I am going to pick up the next tools to implement my CI/CD Pipeline with SAST stages:

1. Jenkins
  * It will be our CI/CD Server and will orchestrate our CI/CD workflow.
2. SonarQube
  * It will work as our Platform to consolidate all our outcomes, it has multiple default Linters (Python, Golang, etc) that will be used as a SAST tool according the source code in our project.
3. Checkmarx KICS
  * It will allow us scan for vulnerabilities in our IaC (Terraform, Ansible, CloudFormation, Docker, Kubernetes, etc.) used in our project.

### Why Checkmarx KICS

Although I could use AWS Cfn-Lint or AquaSec Trivy, I choose KICKS because It integrates multiple IaC Linters in one.

## Implementing the CI/CD Pipeline with a SAST stages

* I'm going to use AWS EC2 to deploy everything.
* Everything will be Dockerized.
* The Project I'm going to use as example will be [Weaveworks Sock Shop](https://microservices-demo.github.io), specifically the version for AWS ECS which contains CloudFormation Templates. 
In fact, you could use any kind of Cloud-Native Project, the only thing you need is the GitHub Repository URL.


### Steps

#### 1. Deploy your DevOps Infraestructure and Tooling

```sh
xyz
```

#### 2. Implement your CI/CD Pipeline with SAST stages

```sh
xyz
```

#### 3. Run Jenkins Pipeline againts your Cloud-Native Project

```sh
xyz
```

## Conclusions

 Since that a Cloud-Native App stack is composed of multiple building blocks, artifacts and different programming languages, you will need SAST Tools for each of them, although that is not a problem, 
 the hard part will be consolidate all outcomes comming from multiple SAST Tools in a single point, and then to make the right decisions during CI/CD-runtime (Jenkins runtime). Said that, SonarQube CE covers this part while you don't have any approach in place yet.
 

## References

1. [Awesome Open Source / The Top 254 Static Analysis Open Source Projects](https://awesomeopensource.com/projects/static-analysis)
2. [analysis-tools-dev / static-analysis](https://github.com/analysis-tools-dev/static-analysis)
