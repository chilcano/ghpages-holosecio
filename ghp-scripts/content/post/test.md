---
title: Test
date: 2021-09-14T10:00:10+02:00
draft: true
type: post
layout: single_simple
categories: [Cloud, SDLC, DevSecOps, Holism]
tags: [SAST]
---

## Issue with Image Resize for longer filename

{{< image-resize "/assets/blog20210904_sast_2/20210904-sast-in-your-cicd-pipeline-full-stack-apps.png" 710x >}}

{{< image-resize "/assets/blog20210904_sast_2/123456789-123456789-123456789-123456789-123456789-pqr" 410x >}} 

### 54 chars (img resized is created: <filename>_huxxxxx_size_box_3.png)
{{< image-resize "/assets/blog20210904_sast_2/123456789-123456789-123456789-123456789-123456789-abcd" 510x >}} 

### 54 chars + (img resized is created _huxxxxxxxxxx.png) 
{{< image-resize "/assets/blog20210904_sast_2/20210904-sast-in-your-cicd-pipeline-full-stack-2-aggregate-reports" 610x >}} 

