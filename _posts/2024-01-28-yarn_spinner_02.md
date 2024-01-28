---
layout: single
title:  "[YarnSpinner] #02 Yarn Files "
categories: Study
tag: [YarnSpinner]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---
# [YarnSpinner] #01 Yarn Fiels
## Yarn Proejct
Yarn 스크립트를 함께 연결하는 파일

![img](https://307131674-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MUzduXovTOfMmBpZ0Wi%2Fuploads%2Fgit-blob-5d3ace6ce661f4b86c3e2ce02840b9dfef042680%2Fyarn-project-inspector.png?alt=media)

Asset menu -> Yarn Spinner -> Yarn Project 로 생성



### Yarn Project에 Yarn Script를 추가하는 방법

Yarn Project에는 프로젝트가 Source Files 디렉토리에서 찾은 모든 Yarn Scripts를 포함

기본적으로 Yarn Project와 동일한 디렉토리에 있는 Yarn Scripts들은 자동으로 포함 

|Pattern|Description|Examples|
|---|----|-----|
|```*```|임의의 파일명|```*.yarn```은 test1.yarn 과 test2.yarn을 찾음 |
|```**/*```|서브디렉토리를 포함한 임의의 경로|```**/*.yarn```은 test1.yarn과 Subfolder/test2.yarn을 찾음|
|..|상위폴더|```../*.yarn```은 상위 폴더에서 "test1.yarn"을 찾음|

Source Files 필드에 원하는 만큼 항목을 추가 가능
파일이 여러 패턴으로 일치하는 경우 한 번만 포함 



### Yarn Script에서 Yan Project 생성 가능
원하는 Yarn Script를 선택 -> Inspector 에서 Create New Yarn Project 클릭해서 생성

위와 같은 방식으로 생성할 경우 Yarn Script 옆에 Yarn Project가 생성되며, Yarn Script를 Yan Project에 포함



### Managing Localisations and Assets
다른 것으로 변경하지 않는 한 기본 언어를 컴퓨터의 현재 로케일로 설정

![img](https://307131674-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MUzduXovTOfMmBpZ0Wi%2Fuploads%2Fgit-blob-909d5d0f204159e08d1cec08a47062844722d413%2Fdefault-language.png?alt=media&token=489ea7ca-bc41-4e22-b956-e07080f21ea0)

Base Language를 변경해서 Yarn Project의 기본 언어를 설정 가능

스크립트를 다른 언어로 번역하거나  각 행을 오디오 클립의 음성과 연결하려면 새 Localisation을 생성 해야 함 

추가 방법은 [Adding Localizations and Assets to Projects](https://docs.yarnspinner.dev/using-yarnspinner-with-unity/assets-and-localization) 을 참조 



### Using Yarn Projects with Dialogue Runners

Yarn Project는 Dialogue Runner에서 사용

Dialouge Runner가 대화를 시작하라는 명령을 받으면 제공된 Yarn Project에서 읽음



### Inspector
|Property|Description|
|---|---|
|Source Files|Yarn Project에서 Yarn Scripts를 찾는 장소 목록|
|Base Language|Yarn Scripts가 작성되는 언어|
|Use Addressable Assets|체크한 경우, Addressable Assets system을 사용하여 오디오 파일과 같은 자산을 가져와야 한다고 알려주도록 설정|
|Export Strings as CSV|버튼 클릭 시, Yarn Scripts에서 이 프로젝트가 사용하는 모든 행이 ```.csv```파일로 기록되며, 이 파일은 다른 언어로 번역될 수 있음|
|Add Line Tags to Scripts|버튼 클릭 시,소스 스크립트 목록에 line 태그가 없는 대화행이 하나 추가.|




## Yarn Script
Yarn Script는 대화 내용이 들어 있는 텍스트 파일

Yarn Script는 게임에 사용하려면 Yarn Project의 일부여야 함

### Creating a New File
Asset Menu -> Yarn Spinner -> Yarn Script 로 생성
새로 만든 파일에는 파일과 같은 이름의 단일 노드가 포함 됨

### Editing Yarn Scripts
Yarn script 파일을 두 번 클릭 하면 VS Code를 통해 편집 가능
