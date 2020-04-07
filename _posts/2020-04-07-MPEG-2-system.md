---
layout: post
title: ISO/IEC 13818-1(MPEG-2 시스템)이란?     # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [study,MPEG,방송솔루션]
excerpt_separator: <!--more-->
---

## MPEG 시스템 표준이란 <br>
      
  - 압축 부호화된 비디오,오디오,데이터 등 비트 스트림의 `다중화` 및 `동기화`를 규정 
    여러 압축된 다중의 채널 서비스를 다중화,동기화 등을 통해 단일의 비트열로 전달 
    전세계 디지털 방송/멀티미디어 TS(Transport Stream) 전달의 사실상의 표준 
  
  - 관련 표준                                                          
     - ISO/IEC 11171-1 (MPEG-1 시스템) 
     - ISO/IEC 13818-1 (MPEG-2 시스템: MPEG-1 시스템을 포괄함)  

<!--more-->

### MPEG 종류

      

 `※ MPEG-1,2,4는 주로 압축 부호화 관련 표준이고, MPEG-7,21은 압축 부호화와 관련 없음`

  4. MPEG-7  (1999~, ISO/IEC 15938)
     - 멀티미디어 컨텐츠의 검색/저장을 위한 표현형식(메타데이터)의 정의 표준
        . 내용기반 비디오 서술자, 오디오 서술자, 멀티미디어 서술구조, 메타데이터 압축
          방식 등

  5. MPEG-21  (2000.5~, ISO/IEC 21000)
     - 멀티미디어 컨텐츠의 생성,관리,유통에 이르는 전자상거래에 대한 프레임워크


<br><br><br>
### MPEG 시스템 계층구조
![Image Alt 텍스트](http://www.ktword.co.kr/img_data/3682_1.JPG)
      
      
### MPEG 시스템 다중화 및 동기화

  1. MPEG 다중화
     - 복수의 비디오,오디오,데이터 스트림(ES) 또는 프로그램(PS)을 하나의 데이터 스트림(PES)으로 다중화      
         ![Image Alt 텍스트](http://www.ktword.co.kr/img_data/3682_2.JPG)

        . 비디오,오디오,데이터 등의 각각의 기본 스트림(ES)을 PES 패킷화시켜,
        . 하나의 전송 스트림(TS)으로 다중화하거나, 
        . 하나 이상의 전송 스트림(TS)를 다시 하나의 전송 스트림(TS)으로 재 다중화
        . [참고] ES → PES 패킷 → PES 패킷 스트림 → TS 패킷 → TS 스트림

  2. MPEG 동기화
     - 비디오 및 오디오 미디어 간, 엔코더 및 디코더 간의 동기화
       ![Image Alt 텍스트](http://www.ktword.co.kr/img_data/3682_3.JPG)


### MPEG 비트 스트림 구분

  1. 기본 비트 스트림    
     - 기본 스트림 (ES,Elementary Stream)      
        . 비디오,오디오,데이터가 각각 압축된 미디어 비트 스트림  

  2. 다중화된 비트 스트림  
     - 기초패킷스트림 (PES,Packetized Elementary Stream)     
        . PS 및 TS를 만들기위한 전 단계
     - 프로그램스트림 (PS,Program Stream)  
        . CD-ROM 저장 처럼 단일 프로그램을 대상으로 규격화된 스트림
     - 수송스트림 (TS,Transport Stream)  
        . 전송 오류가 있는 전송채널을 통해 전달되도록 규격화된 스트림


<hr/>  
<br><br><br>

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
[정보통신기술용어해설]http://www.ktword.co.kr/abbr_view.php?nav=2&id=54
