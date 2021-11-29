---
title: Raspbian OS BackUp 하기
date: 2021-11-29 22:59:47
tags:
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## 준비물

- 현재 시스템이 돌아가고 있는 Micro SD card
- BackUp을 위한 포맷이 완료된 Micro SD card

## BackUp

1. 새로운 SD card를 SD card 리더기에 연결한 후 현재 사용중인 Raspberry Pi의 USB 포트에 연결한다.
2. SD Card Copier에 접속
   1. 시작 메뉴
   2. Accessories
   3. SD Card Copier
3. SD Card Copier 설정
   1. 윗 부분(현재 시스템이 돌아가고 있는 SD card): SC16G(/dev/mmcblk0)
   2. 아래 부분(BackUp을 실행할 SD card): Generic Mass-Storage(/dev/sda)
4. Start

- BackUp 완료

## 주의 사항

- cloud not set flag 에러: 사용 중인 공간과 빈 공간을 그대로 가져오므로 현재 시스템이 돌아가고 있는 SD card와 동일, 또는 그 이상 크기의 SD card로 수행하여야 한다.
