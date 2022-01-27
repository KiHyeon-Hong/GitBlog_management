---
title: Windows 환경에서 Ubuntu 설치하기
date: 2022-01-27 17:46:24
tags:
  - Windows
  - Ubuntu
categories:
  - Windows
  - Ubuntu
---

## 설치 전 참고 사항

### WSL 간편 설정

- WSL 설치 및 세팅은 Docker를 설치한 후 실행하면 편하다.
- WSL2 업데이트가 나오는데, 커널 업데이트를 미리 실행할 것
- https://www.docker.com/products/docker-desktop
- https://docs.microsoft.com/ko-kr/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package
- x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지 다운 후 설치

### Windows Terminal 설치

- Windows Terminal을 chock 또는 microsoft store에서 설치를 할 것

## Ubuntu 설치

- Microsoft store에서 Ubuntu 18.0.4 LTS를 다운로드 한다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl1.jpg"></p>

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl2.jpg"></p>

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl3.jpg"></p>

- 처음 실행하면, username과 passowrd를 설정한다.
- sudo 명령어를 사용할 때, 해당 password를 이용하기 때문에 반드시 기억해야 한다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl4.jpg"></p>

- Windows Terminal을 보면 Ubuntu를 볼 수가 있는데, 이는 리눅스 환경에서 동작한다.

### WSL2 설치 확인

- WSL2로 업데이트 및 확인을 위해 해당 명령어를 Ubuntu 콘솔에 작성한다.
- 만약 Docker를 설치하고, 커널 업데이트를 완료 했다면 다음과 같은 화면이 출력될 것이다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl5.jpg"></p>

## Windows Terminal 설정

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl6.jpg"></p>

- Windows Terminal의 설정을 들어가면 Json 파일 열기가 있다.
- 이를 선택한다.
- Windows Terminal 선택 시 기본으로 열리는 콘솔을 Ubuntu로 하기 위해 settings.json의 "defaultProfile"을 수정한다.
- "Profiles"의 "list"를 보면 선택 가능한 콘솔이 있으며, "Ubuntu-18.04"의 "guid"를 복사해서 "defaultProfile"에 붙여넣는다.

```json
{
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "defaultProfile": "{c6eaf9f4-32a7-5fdc-b5cf-066e8a4b1e40}",
  ...
  "profiles": {
    "list": [
      ...
      {
        "guid": "{c6eaf9f4-32a7-5fdc-b5cf-066e8a4b1e40}",
        "name": "Ubuntu-18.04",
        "source": "Windows.Terminal.Wsl"
      }
    ]
  },
  ...
}
```

- 재시작 하면 기본적으로 Ubuntu 환경으로 들어온다.

## Oh my zsh

- https://github.com/ohmyzsh/ohmyzsh
- zsh의 설정 관리를 위한 프레임워크인 oh-my-zsh를 설치한다.
- 이를 위해 먼저 zsh를 설치한다.

```bash
sudo apt install zsh
```

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl7.jpg"></p>

- Oh my zsh를 설치한다.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl8.jpg"></p>

- 콘솔이 바뀐 것을 확인할 수 있다.

## Powerlevel10k

- https://github.com/romkatv/powerlevel10k
- powerlevel10k는 zsh의 테마를 변경할 수 있다.

```bash
sudo git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

- .zshrc 파일을 수정한다.
- 이를 위해 .zshrc 파일을 열어야 한다.
  만약 code ~/.zshrc가 동작하지 않는다면 vi를 이용한다.

```bash
code ~/.zshrc
vi ~/.zshrc
```

- ZSH_THEME를 수정한다.

```rc
ZSH_THEME="robbyrussell" -> ZSH_THEME="powerlevel10k/powerlevel10k"
```

- :wq를 이용해 수정하고, 터미널을 재시작하면 다음과 같은 화면이 뜬다.
- 이는 powerlevel10k의 기본 설정이며, 처음 실행에서 나타난다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl9.jpg"></p>

- 이를 보면 사각형이 잘 나오지 않는 것을 볼 수가 있는데, 이는 폰트의 문제이다.
- powerlevel10k의 사이트에 들어가면 4개의 폰트가 있는데, 해당 4개 모두 다운로드 후 설치한다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl10.jpg"></p>

### Windows Terminal의 setting.json

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl11.jpg"></p>

- setting.json의 "defaults"에서 "FontFace"를 "MesloLGS NF"로 수정한다.

```json
"profiles": {
    "defaults": {
      // Put settings here that you want to apply to all profiles.
      "fontFace": "MesloLGS NF"
    },
    "list": [
      {
        // Make changes here to the powershell.exe profile.
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "Windows PowerShell",
        "commandline": "powershell.exe",
        "hidden": false
      },
```

### Visual studio code 설정

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl12.jpg"></p>

- File -> Preferences -> Settings
- 검색창에 integrated를 검색하면 Font Family가 있다
- 이를 "MesloLGS NF"로 수정한다.

### 콘솔 재시작

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl13.jpg"></p>

- 콘솔을 재시작하면 다음과 같이 정상적으로 나오는 것을 볼 수 있다.
- 원하는대로 설정을 모두 마치고 나면 다음과 같은 화면이 출력된다.

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl14.jpg"></p>

### ls color 변경

- code ~/.zshrc 파일 맨 마지막 줄에 다음을 추가한다.

```rc
LS_COLORS="ow=01;36;40" && export LS_COLOR
```

### powerlevel10k 재설정

```bash
p10k configure
```

## Windows에서 설치한 Ubuntu 상세 구조 분석

<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl15.jpg"></p>
<p align="center"><img src="/images/Windows/Ubuntu/Install/wsl16.jpg"></p>

- 실제로 구현되는 구조는 아니라 가상화로 구현되는 구조이다.
- cmd, powershell, 그리고 Windows Terminal과 같은 window 환경에서 동작하는 터미널의 경우 C 드라이브가 루트이며, 이 이상으로 올라갈 수 없다.
- 그러나 가상화로 구현된 Ubuntu, 그리고 Ubuntu 위에서 동작하는 zsh 터미널은 루트 디렉터리까지 올라갈 수 있으며, Windows 환경은 mnt 디렉터리를 통해 들어간다.
- home 디렉터리의 user는 Ubuntu에서 생성한 사용자이며, 이는 user 사용자의 환경이다.
