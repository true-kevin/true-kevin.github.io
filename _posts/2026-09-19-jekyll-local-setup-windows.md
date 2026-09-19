---
title: "Windows에서 Jekyll 블로그 로컬에 설치하기"
date: 2026-09-19 09:00:00 +0900
categories: [Jekyll, 개발환경]
tags: [jekyll, ruby, github pages, windows, chirpy]
description: "Jekyll 블로그를 로컬에 설치하기 위해 Ruby와 Git을 설치하고 로컬 서버에서 블로그를 띄워 보는 방법을 알아봅니다."
image:
  path: /assets/img/posts/jekyll-local-setup/01_ruby_installer_home.png
  alt: Ruby 공식 사이트
published: true
---

## 지킬(jekyll) 로컬 환경의 필요성

GitHub pages에 바로 지킬(Jekyll) 포스트를 올리기 전에 **테스트해 볼 수 있는 환경**이 필요합니다.

그래서 이 글에서는 지킬(Jekyll)을 로컬 서버로 띄워서 테스트할 수 있는 환경을 만들어 볼 겁니다.

 Windows 기준으로, Ruby와 Git을 설치하고 실제로 로컬에 블로그를 띄워서 확인하는 과정까지 진행합니다.

---

## 1. Ruby 설치

Jekyll은 Ruby 기반으로 동작하기 때문에 Ruby부터 설치해야 합니다. [RubyInstaller](https://rubyinstaller.org/) 공식 사이트에서 다운로드합니다.

![RubyInstaller 홈페이지](/assets/img/posts/jekyll-local-setup/01_ruby_installer_home.png)
_RubyInstaller 공식 사이트_

**Download** 버튼을 눌러 다운로드 페이지로 이동합니다.

![RubyInstaller 다운로드 페이지](/assets/img/posts/jekyll-local-setup/02_ruby_downloads_page.png)
_다운로드 페이지_

> 다운로드 페이지에는 "WITH DEVKIT" 섹션에 여러 버전이 나열되어 있습니다. 반드시 **Devkit이 포함된 버전**을 받아야 합니다. Jekyll이 의존하는 일부 gem이 네이티브 확장을 컴파일해야 하는데, 이때 Devkit이 필요하기 때문입니다.
>
> 또한 사용하려는 Jekyll 테마의 요구 버전을 미리 확인하는 게 좋습니다. 예를 들어 이 블로그가 사용하는 **Chirpy 테마 7.x대는 Ruby 3.1 이상 4.0 미만**을 요구합니다. 무조건 최신 버전을 선택하기보다는 사용할 테마와 맞는 버전을 선택해야 합니다. 이 글에서는 **Ruby+Devkit 3.4.10 (x64)**를 기준으로 진행합니다.
{: .prompt-warning }

다운로드한 설치 파일을 실행하면 설치 모드를 선택하는 창이 뜹니다. 특별한 이유가 없다면 **'Install for me only'**를 선택합니다.

![설치 모드 선택](/assets/img/posts/jekyll-local-setup/03_install_mode.png)
_설치 모드 선택_

라이선스 동의 화면에서 **'I accept the License'**를 선택하고 Next를 누릅니다.

![라이선스 동의](/assets/img/posts/jekyll-local-setup/04_license_agreement.png)
_라이선스 동의_

설치 경로와 옵션을 선택하는 화면입니다. 기본 경로를 그대로 두고, **'Add Ruby executables to your PATH'**가 체크되어 있는지 확인합니다.

![설치 경로 및 옵션](/assets/img/posts/jekyll-local-setup/05_install_destination.png)
_설치 경로 및 옵션 설정_

설치할 구성요소를 선택하는 화면에서는 **'MSYS2 development toolchain'**이 체크되어 있는지 확인합니다.

![구성요소 선택](/assets/img/posts/jekyll-local-setup/06_select_components.png)
_설치할 구성요소 선택_

설치가 진행됩니다. 용량이 꽤 커서 시간이 좀 걸릴 수 있습니다.

![설치 진행](/assets/img/posts/jekyll-local-setup/07_installing_progress.png)
_설치 진행 화면_

설치가 끝나면 **'Run ridk install'** 항목이 체크된 상태로 완료 화면이 나옵니다. 이 체크박스를 그대로 두고 **Finish**를 누르면 이어서 MSYS2 개발 도구체인 설정이 자동으로 시작됩니다.

![설치 완료](/assets/img/posts/jekyll-local-setup/08_setup_complete.png)
_설치 완료 및 ridk install 실행_

---

## 2. MSYS2 개발 도구체인 설정 (ridk install)

Finish를 누르면 터미널 창이 자동으로 열리면서 어떤 구성요소를 설치할지 묻습니다. 특별한 이유가 없다면 기본값을 그대로 두고 Enter를 누릅니다.

![ridk install 옵션 선택](/assets/img/posts/jekyll-local-setup/09_ridk_install_prompt.png)
_ridk install 옵션 선택 화면_

MSYS2와 관련 도구들이 설치되는 과정이 진행됩니다. 이 단계는 시간이 걸리니 완료될 때까지 기다립니다.

![MSYS2 설치 진행](/assets/img/posts/jekyll-local-setup/10_ridk_install_progress.png)
_MSYS2 개발 도구체인 설치 진행_

**"Install MSYS2 and MINGW development toolchain succeeded"** 메시지가 뜨면 정상적으로 완료된 것입니다. 이후 다시 메뉴가 나오면 더 이상 설치할 게 없으니 그냥 Enter를 눌러 종료합니다.

![설치 성공](/assets/img/posts/jekyll-local-setup/11_ridk_install_success.png)
_MSYS2 설치 성공_

---

## 3. Ruby 설치 확인

새 PowerShell 창을 열어서(기존 창은 PATH가 갱신되지 않을 수 있으니 반드시 새 창) 버전을 확인합니다.

```powershell
ruby -v
gem -v
```

![Ruby, gem 버전 확인](/assets/img/posts/jekyll-local-setup/12_ruby_gem_version_check.png)
_Ruby와 RubyGems 버전 확인_

`ruby 3.4.10`, `gem 3.6.9` 같은 식으로 출력되면 정상적으로 설치된 것입니다.

---

## 4. Git 설치 & 리포지토리 클론

블로그 소스코드가 있는 GitHub 리포지토리를 로컬로 가져오려면 Git이 필요합니다. 먼저 Git이 이미 설치되어 있는지 확인합니다.

```powershell
git --version
```

설치되어 있지 않다면 아래처럼 명령어를 인식하지 못한다는 오류가 나옵니다.

![Git이 설치되지 않은 상태](/assets/img/posts/jekyll-local-setup/13_git_not_installed.png)
_설치 전에는 git 명령어를 인식하지 못합니다_

Windows 10/11이라면 아래 명령어로 간단히 설치할 수 있습니다.

```powershell
winget install --id Git.Git -e --source winget
```

![winget 설치 명령 입력](/assets/img/posts/jekyll-local-setup/14_winget_install_command.png)
_Git 설치 명령 입력_

Enter를 누르면 Git을 내려받고 설치가 시작됩니다. 중간에 관리자 권한을 요청하는 창이 뜨면 허용해 주면 되고, 이어서 아래와 같은 Git 설치 창이 나타납니다. 별도로 선택할 옵션은 없으니 끝날 때까지 기다리면 됩니다.

![Git 설치 진행 창](/assets/img/posts/jekyll-local-setup/15_git_setup_installing.png)
_Git 설치 진행 화면_

설치 창이 닫히고 터미널에 "설치 성공"이 표시되면 설치가 끝난 것입니다.

![Git 설치 성공](/assets/img/posts/jekyll-local-setup/16_winget_install_success.png)
_터미널에 설치 성공 메시지 확인_

설치가 끝나면 새 터미널에서 `git --version`으로 정상 설치 여부를 확인합니다.

![Git 버전 확인](/assets/img/posts/jekyll-local-setup/17_git_version_check.png)
_git version이 정상적으로 출력됩니다_

Git이 준비되면, 리포지토리를 원하는 폴더에 클론합니다.

```powershell
git clone https://github.com/사용자명/저장소명.git
```

![git clone 명령 입력](/assets/img/posts/jekyll-local-setup/18_git_clone_command.png)
_git clone 명령 입력_

리포지토리 파일들이 정상적으로 복사되면 완료입니다.

![git clone 완료](/assets/img/posts/jekyll-local-setup/19_git_clone_done.png)
_클론 완료_

---

## 5. Jekyll & Bundler 설치

클론이 끝났으면, 이제 Jekyll을 실행하는 데 필요한 gem들을 설치합니다.

```powershell
gem install jekyll bundler
```

![jekyll, bundler 설치 진행](/assets/img/posts/jekyll-local-setup/20_gem_install_jekyll_bundler.png)
_필요한 gem들이 순서대로 설치됩니다_

설치가 끝나면 여러 개의 gem이 설치되었다는 메시지가 뜹니다.

![jekyll, bundler 설치 완료](/assets/img/posts/jekyll-local-setup/21_gem_install_complete.png)
_설치 완료_

---

## 6. 프로젝트 의존성 설치 (bundle install)

클론해둔 리포지토리 폴더로 이동한 뒤, `Gemfile`에 명시된 정확한 버전의 gem들을 설치합니다.

```powershell
cd 저장소명
bundle install
```

![bundle install 명령 입력](/assets/img/posts/jekyll-local-setup/22_bundle_install_command.png)
_리포지토리 폴더로 이동 후 bundle install 실행_

의존성들이 순서대로 설치되는 과정이 나옵니다.

![bundle install 진행](/assets/img/posts/jekyll-local-setup/23_bundle_install_progress.png)
_gem들이 하나씩 설치되는 과정_

**"Bundle complete!"** 메시지와 함께 설치된 gem 개수가 표시되면 성공입니다. 여기서 Ruby 버전과 테마가 요구하는 버전이 맞지 않으면 에러가 날 수 있는데, 앞서 1단계에서 버전을 맞춰 설치했다면 문제없이 끝납니다.

![bundle install 완료](/assets/img/posts/jekyll-local-setup/24_bundle_install_complete.png)
_Bundle complete!_

---

## 7. 로컬 서버 실행

이제 실제로 로컬에서 사이트를 띄워볼 차례입니다.

```powershell
bundle exec jekyll serve --livereload
```

![jekyll serve 명령 입력](/assets/img/posts/jekyll-local-setup/25_jekyll_serve_command.png)
_로컬 서버 실행 명령_

빌드가 끝나면 아래처럼 서버 주소가 출력되고, **"Server running... press ctrl-c to stop."** 메시지가 뜨면 정상적으로 서버가 켜진 것입니다.

![jekyll serve 실행 성공](/assets/img/posts/jekyll-local-setup/26_jekyll_serve_running.png)
_로컬 서버 실행 성공_

---

## 8. 브라우저에서 확인

브라우저에서 아래 주소로 접속합니다.

```
http://127.0.0.1:4000
```

실제 블로그 화면이 그대로 보이면 성공입니다.

![브라우저에서 로컬 사이트 확인](/assets/img/posts/jekyll-local-setup/27_browser_localhost_check.png)
_로컬에서 정상적으로 뜬 사이트 화면_

---

## 마무리

`--livereload` 옵션을 붙여 서버를 띄우면 모든 내용 변화가 브라우저에 실시간으로 자동 반영됩니다. 실제 포스트를 작성할 때 어떻게 보일지 확인하며 작업할 수 있는 환경이 갖춰졌습니다.

- 서버를 끄려면 터미널에서 `Ctrl + C`를 누르면 됩니다.
- 포스트를 확인하고 싶을 때 파워쉘에서 지킬 프로젝트 폴더로 이동 후 `bundle exec jekyll serve --livereload`를 실행하고 실시간으로 확인하면 포스팅을 작성하시면 됩니다.
- `published: false` 비공개 처리해둔 글까지 확인하려면 `--unpublished` 옵션을 추가하시면 됩니다.

```powershell
bundle exec jekyll serve --livereload --unpublished
```

다음 포스팅에서는 실제로 로컬에서 포스트를 작성하고 GitHub pages에 올리는 실습을 해보겠습니다.