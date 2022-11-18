---
weight: 1
title: "Git 설치하기 - MAC"
---

# Git 설치하기 (MAC)

---

## Homebrew 설치하기

맥을 사용해 개발하는 사람이라면, Homebrew 의 존재를 모르는 사람은 드물 것이다. Git 역시 Homebrew 를 통해 Git 을 설치하고 관리할 수 있다.

### Homebrew 란?

Homebrew 는 Mac 용 패키지 관리자 프로그램으로 제공하는 이점은 크게 2가지가 있다.

-   Homebrew 에 등록된 프로그램들을 단순한 명령어를 통해 쉽게 설치할 수 있다.
-   설치한 프로그램들을 Homebrew 가 관리하는 디렉토리 내에서 쉽게 관리할 수 있다.

Mac 을 통해 개발하는 사람들에게 필수적인 프로그램이라고 할 수 있다.

### Homebrew 설치 명령어

터미널을 열고 아래 명령어를 작성하면 Homebrew 프로그램을 바로 설치할 수 있다.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

(Homebrew 에 대한 좀 더 자세한 내용은 [Homebrew 홈페이지](https://brew.sh/index_ko) 홈페이지에서 살펴보도록 하자.)

---

## Git 설치하기

터미널을 통해 아래 명령어를 사용하면 git 을 설치할 수 있다.

```bash
brew install git
```

정상적으로 설치가 완료됐다면, 아래 명령어를 입력할 경우 설치된 git 버전을 확인할 수 있다.

```bash
git --version       // git version 2.xx.x
```
