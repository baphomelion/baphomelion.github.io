---
title: "리눅스 노트북 덮개를 닫아도 안 꺼지게 하는 방법"
categories:
  - Linux
toc: true
---

## 요약
GUI가 설치되지 않는 CLI 환경의 리눅스 노트북 덮개를 덮어도 안 꺼지고 계속 실행되도록 함

## 방법

### HandleLidSwitch ignore 처리
덮개를 닫아도 시스템에서 아무런 동작을 하지 않도록 수정

```
File : /etc/systemd/logind.conf

...
HandleLidSwitch=ignore

...
```
```
# systemctl restart systemd-logind
```

### 화면 끄기
HandleLidSwitch=ignore를 할 경우 덮개를 덮어도 화면이 계속 켜져있음

밝기를 0으로 변경하여 화면을 끄도록 함
```
# echo 0 >  /sys/class/backlight/intel_backlightlight/brightness
```