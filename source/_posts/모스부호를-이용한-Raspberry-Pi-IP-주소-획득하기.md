---
title: 모스부호를 이용한 Raspberry Pi IP 주소 획득하기
date: 2022-02-12 11:43:59
tags:
  - Morse code
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## 모스부호를 이용하여 Raspberry Pi의 IP 주소 획득하기

- Raspberry Pi의 IP 주소를 획득하거나, Wifi 설정을 위해 SSH 접속을 시도하려고 하여도, 결국 IP 주소가 필요하다.
- 또한, 유동 IP의 경우 라즈베리 파이의 부팅마다 IP 주소가 달라지므로, 모니터와 같이 IP 주소를 확인할 수 있는 추가적인 수단이 필요하다.
- 이를 해결하기 위해 gpio pin을 이용하여 모스부호를 반환해주는 프로그램을 작성한다.

### 모스부호 설명

- 모스부호는 짧은 발신 전류(.)와 간 발신 전류(-)를 조합하여 알파벳과 숫자를 표기한 것이다.
- IP 주소는 숫자와 '.'으로 이루어져 있으며, 이에 해당하는 모스부호는 다음과 같다.

<p align="center"><img src="/images/RaspberryPi/MorseCode/Morsecode1.jpg"></p>
<p align="center"><img src="/images/RaspberryPi/MorseCode/Morsecode2.jpg"></p>

### 소스 코드

- IP 주소를 모스부호로 변환해주는 프로그램은 미리 작성하였다.
- https://github.com/KiHyeon-Hong/Convert_IP_address_to_morse_code_cjs.git

```bash
git clone https://github.com/KiHyeon-Hong/Convert_IP_address_to_morse_code_cjs.git
cd Convert_IP_address_to_morse_code_cjs
npm i
```

- index.js에는 사용 예시 코드가 있으며, 공인 IP와 사설 IP를 모스부호로 반환해주는 메소드 2개를 사용하였다.

### Raspberry Pi에 연동

- gpio pin을 이용해 센서 및 액츄에이터를 조작하는 방법은 아래 링크에서 참고할 수 있다.
- https://kihyeon-hong.github.io/2021/11/15/Raspberry-Pi-4-gpio-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0/
- 아래 소스 코드는 gpio 29번 핀을 사용하였으며, 소스 코드를 변경하여 원하는 방식으로 수정 가능하다.

```javascript
const gpio = require('node-wiring-pi');
const morse = require(__dirname + '/src/toMorseCode');

const MORSE = 29;

gpio.setup('wpi');
gpio.pinMode(MORSE, gpio.OUTPUT);

const stop100ms = () => {
  gpio.digitalWrite(MORSE, 0);
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, 100);
  });
};

const stop500ms = () => {
  gpio.digitalWrite(MORSE, 0);
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, 500);
  });
};

const short = () => {
  gpio.digitalWrite(MORSE, 1);
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, 100);
  });
};

const long = () => {
  gpio.digitalWrite(MORSE, 1);
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, 500);
  });
};

async function main() {
  let priIP = await morse.priToMorseCode();
  priIP = priIP.split('');

  for (let i = 0; i < priIP.length; i++) {
    if (priIP[i] === '.') {
      await short();
      await stop100ms();
    } else if (priIP[i] === '-') {
      await long();
      await stop100ms();
    } else {
      await stop500ms();
    }
  }
}

main();
```

- '.': 100ms 1 신호를 주며, 100ms 0 신호를 준다.
- '-': 500ms 1 신호를 주며, 100ms 0 신호를 준다.
- ' ': 각 모스 부호 사이의 간격은 500ms이며, 500ms 동안 0 신호를 준다.

### Raspberry Pi 부팅 시 프로그램 자동 수행

- 해당 프로그램을 라즈베리 파이가 부팅이 될때 실행하도록 하여야 한다.
- 이는 다음 링크를 참조한다.
- https://kihyeon-hong.github.io/2021/11/24/Raspberry-Pi-%EB%B6%80%ED%8C%85-%EC%8B%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%9E%90%EB%8F%99-%EC%88%98%ED%96%89/
