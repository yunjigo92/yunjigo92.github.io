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


<br><br><br>
### MPEG 시스템 계층구조
![Image Alt 텍스트](http://www.ktword.co.kr/img_data/3682_1.JPG)
      
여기서 추가로, MUX / DEMUX란 ? 
      
- 멀티플렉서 (Multiplexer)
![Image Alt 멀티플렉서](http://postfiles11.naver.net/20160522_202/lagrange0115_1463894040126oH6zm_PNG/%B1%D7%B8%B21.png?type=w773)
멀티플렉서는 MUX, MPX라고 줄여 부르기도 하며, 여러 개의 입력 중 하나를 선택해 출력으로 내보내는 논리 회로를 말합니다. 멀티플렉서는 그림 1과 같이 입력 단과 출력단 이외에 어떠한 입력단을 출력으로 내보낼지 결정해주는 control input 핀이 따로 있습니다. Control input 핀에 원하는 신호를 내보내면 원하는 입력이 출력으로 내보내지는 논리 회로입니다.     
      
- 디멀티플렉서 (Demultiplexer)      
![Image Alt 멀티플렉서](http://postfiles4.naver.net/MjAxOTA1MjhfMjk0/MDAxNTU5MDQxMzI4Mjkz.rJJSdyRZtSP2cqv9iu0RElJzLjlKqQtseF2kt-3URGkg.ErFcceZk0lUuVjItkgPThusAOMLg6xrM39QhGfVOuxQg.PNG.lagrange0115/%EA%B7%B8%EB%A6%BC2.png?type=w773)
디멀티플렉서는 DEMUX라고 줄여 부르기도 하며, 한 개의 입력을 어느 출력단에 내보낼지 선택할 수 있는 기능을 가진 논리 회로를 말합니다. 디멀티플렉서는 멀티플렉서와 마찬가지로 그림 6과 같이 입력단과 출력단 이외에 어떠한 출력단으로 내보낼지 결정해주는 control input 핀이 따로 있습니다. Control input 핀에 원하는 신호를 내보내면 원하는 출력핀으로 내보내지는 논리 회로입니다.    
      
      
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

각 비트스트림에 대해서는 상세하게 또 포스팅을 하도록 하겠다.


<br><br><br>

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
[정보통신기술용어해설]http://www.ktword.co.kr/abbr_view.php?nav=2&id=54     
멀티플렉서 (Multiplexer), 디멀티플렉서 (Demultiplexer)|작성자 엠에스리http://blog.naver.com/PostView.nhn?blogId=lagrange0115&logNo=220716574603&parentCategoryNo=&categoryNo=13&viewDate=&isShowPopularPosts=false&from=postView 
