---
title: SAST in your SDLC for Cloud-Native Apps
date: 2021-07-06T10:00:10+02:00
draft: false
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

Then, we are going to require 5 or less different SAST tools to review statically the code for each kind of code or artifact. Below I show a SAST tool list where you can pickup any tool for convenience or based on your requirements.

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
| 7.  | [Checkov](https://github.com/bridgecrewio/checkov)          | ![](/assets/blog20210706_sast/sast-checkov.png)            | Terraform, CloudFormation, Kubernetes, Dockerfile, ARM Templates. |
| 8.  | [Clair](https://github.com/quay/clair)                      | ![](/assets/blog20210706_sast/sast-clair.png)              | Containers                            |
| 9.  | [Dagda](https://github.com/eliasgranderubio/dagda)          | ![]()                                                      | Containers and monitor Docker daemon  |
| 10. | [Dockle](https://github.com/goodwithtech/dockle)            | ![](/assets/blog20210706_sast/sast-dockle.png)             | Containers and support CIS Benchmarks |
| 11. | [GolangCI-Lint](https://github.com/golangci/golangci-lint)  | ![](/assets/blog20210706_sast/sast-golangci-lint.png)      | Golang code |
| 12. | [GoSec](https://github.com/securego/gosec)                  | ![](/assets/blog20210706_sast/sast-gosec.png)              | Golang code |
| 13. | [huskyCI](https://github.com/globocom/huskyCI)              | ![](/assets/blog20210706_sast/sast-huskyci.png)            | Orchestrate security test (Python, JS, Ruby, Tf, Golang, Java, ...) and centralizes all results |
| 14. | [PHPStan](https://github.com/phpstan/phpstan)               | ![](/assets/blog20210706_sast/sast-phpstan.png)            | PHP code    |
| 15. | [Pylint](https://www.pylint.org)                            | ![](/assets/blog20210706_sast/sast-pylint.png)             | Python code |
| 16. | [Semgrep](https://semgrep.dev/) | ![](/assets/blog20210706_sast/sast-semgrep.png) | Works on 17+ languages. Write rules that look like your code. |
| 17. | [Skyscanner CFrippe](https://github.com/Skyscanner/cfrippe) | ![](/assets/blog20210706_sast/sast-skyscanner-cfrippe.png) | CloudFormation (.json, .yaml). Rules in Python |
| 18. | [SonarQube CE](https://www.sonarqube.org)                   | ![](/assets/blog20210706_sast/sast-sonarqube.png)          | Platform and carry out analysis of over 20 programming languages |
| 19. | [SpotBugs](https://github.com/spotbugs/spotbugs)            | ![](/assets/blog20210706_sast/sast-spotbugs.png)           | Java. SpotBugs is the spiritual successor of FindBugs.   |
| 20. | [Stelligent cfn_nag](https://github.com/stelligent/cfn_nag) | ![](/assets/blog20210706_sast/sast-stelligent-cfn_nag.png) | CloudFormation (.json, .yaml). Rules in Ruby   |
| 21. | [Terraform Linter](https://github.com/terraform-linters/tflint)  | ![]()                                                 | Terraform (.tf, .tfvars) |
| 22. | [tfsec](https://github.com/aquasecurity/tfsec)      | ![](/assets/blog20210706_sast/sast-tfsec.png)              | Terraform templates and support Terraform CDK. |
|-    |                                                                  |                                                       |                          |

## The CI/CD Tooling and the Pipeline with SAST 

In order to embed the SAST process in our CI/CD pipeline, we will need at least 3 things:

1. The CI/CD server
  * It will orchestrate the multiple tasks (stages) defined in our CI/CD workflow.
  * A CI/CD workflow or pipeline is a sequence of tasks or stages. In this post, I'm going to use Jenkins with a pipeline with 4 stages: clone the GIT repository, run the SAST tools, get the report or outcomes and promote the code if the code is free of bugs.
2. The SAST tool(s)
  * It will allow us to scan for vulnerabilities in our IaC (Terraform, Ansible, CloudFormation, Docker, Kubernetes, etc.) used in the project.
  * As above, there are many SAST tool, each one is for each type of code. That means we will need one or more SAST tool. Although I could use AWS Cfn-Lint or AquaSec Trivy, I choose KICKS because It integrates multiple IaC Linters in one. 
3. The CI/CD portal server
  * It will work as our web portal to consolidate all our outcomes in a single point. 
  * Initially, I wanted to use SonarQube, but unfortunatelly it has limitations to [import third party generated reports](https://docs.sonarqube.org/latest/analysis/external-issues/), although It can be used as SAST tool as well, in this post I'm going to use Jenkins and HTML reports.

[![](/assets/blog20210706_sast/20210706-sast-in-your-cicd-pipeline.png)](/assets/blog20210706_sast/20210706-sast-in-your-cicd-pipeline.png)
{{< rawhtml >}}
<i><center>SAST stage in CI/CD Pipeline</center></i>
{{</ rawhtml >}}


## Implementing the CI/CD Pipeline with a SAST stage

* I'm going to use AWS EC2 to deploy everything.
* Everything will be Dockerized.
* The Project I'm going to use as example will be [Weaveworks Sock Shop](https://microservices-demo.github.io), specifically the version for AWS ECS which contains CloudFormation Templates. 
In fact, you could use any kind of Cloud-Native Project, the only thing you need is the GitHub Repository URL. The Jenkins Pipeline I've created uses by default [TerraGoat](https://github.com/bridgecrewio/terragoat.git).


### Steps

I've created a Github repository with a CDK Project that automate the creation of AWS EC2 instance, with bash scripts to automate the installation of Jenkins and default plugins and a [Jenkins Pipeline](https://github.com/chilcano/aws-cdk-examples/blob/main/simple-ec2/_scripts/sast-pipeline-kics.groovy) that includes SAST stages in the CI/CD process.

```sh
git clone https://github.com/chilcano/aws-cdk-examples.git

cd aws-cdk-examples/simple-ec2/

npm install @aws-cdk/aws-ec2 @aws-cdk/aws-iam dotenv

cdk deploy --profile es --require-approval never --outputs-file output.json
```

Further details can be found in the *[Chilcano/AWS-CDK-Examples](https://github.com/chilcano/aws-cdk-examples/tree/main/simple-ec2)* GitHub repository.


## Conclusions

1. Since that a Cloud-Native App stack is composed of multiple building blocks, artifacts and different programming languages, you will need SAST Tools for each of them, although that is not a problem, the hard part will be consolidate all outcomes comming from multiple SAST Tools in a single point, and then to make the right decisions during CI/CD-runtime (Jenkins runtime). Said that, SonarQube CE covers this part while you don't have any approach in place yet, however importing third party reports into SonarQube is difficult.

2. Kics is a good SAST tool for Infrastructure as Code, It integrates multiple IaC Linters in one, but what if your project includes Golang code, Python code or Java code?. You will need to use other SAST Tools like GoSec, PyLint or Bandit, add a few stages to your Jenkins Pipeline and finally import all different reports generated for all SAST tools, even the Kics' report, in a single point, correlate and track all vulnerabilities using a common criteria, etc, being that a real headache. At this point, [Jenkins and Warnings-NG Plugin](https://plugins.jenkins.io/warnings-ng/) help a lot. In a next post I will explain how to do that.


## References

1. [Awesome Open Source / The Top 254 Static Analysis Open Source Projects](https://awesomeopensource.com/projects/static-analysis)
2. [Analysis-Tools-Dev / Static-Analysis](https://github.com/analysis-tools-dev/static-analysis)
