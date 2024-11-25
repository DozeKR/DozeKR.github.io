---
layout: single
title:  "[YarnSpinner] #01 Setup "
categories: Study
tag: [YarnSpinner]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [YarnSpinner] #01 Setup

## VS Code Setup

Extensions -> Yarn Spinner 검색 -> Yarn Spinner 선택  -> Install

![YarnSpinnerExtensions]({{site.ur}}/images/2024-01-28-yarn_spinner_setup/YarnSpinnerExtensions.png?raw=true)



## Unity Setup

### Setting Up the OpenUPM Registry in Your Project

Editor -> Project Settings -> Package Manager

![ProjectSettings]({{site.ur}}/images/2024-01-28-yarn_spinner_setup/ProjectSettings.png?raw=true)

1. Name field 에  ```OpenUPM``` 입력
2. URL field 에 ```https://package.openupm.com``` 입력
3. Scopes field 에 ```dev.yarnspinner``` 입력
4. Save 클릭

### Installing the Yarn Spinner package

Window -> Package Manager



![PackageManager]({{site.ur}}/images/2024-01-28-yarn_spinner_setup/PackageManager.png?raw=true)

1. 상단 메뉴에서 Packages 를 클릭해서 My Registires 선택
2. Yarn Spinner 선택 후, Inastall 클릭
3. Project의 Package 폴더에 Yarn Spinner가 설치 되었는지 확인

