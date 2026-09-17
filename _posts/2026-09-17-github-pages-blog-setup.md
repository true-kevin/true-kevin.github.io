---
title: "GitHub 계정 생성하고 무료로 지킬 블로그 만들기 (feat. Chirpy 테마)"
date: 2026-09-17 10:00:00 +0900
categories: [Jekyll, 개발환경]
tags: [jekyll, github pages, chirpy, github actions]
description: "GitHub 계정을 만드는 것부터 Chirpy 테마 템플릿으로 리포지토리를 생성하고, GitHub Actions로 자동 배포되어 실제 사이트가 뜨기까지의 전 과정을 정리했습니다."
published: false
---

## GitHub Pages로 무료로 블로그 만들기

티스토리는 제한이 많고, 워드프레스는 서버 비용 때문에 무료 운영이 어렵습니다. GitHub Pages는 GitHub이 제공하는 무료 정적 사이트 호스팅 서비스입니다. 지킬(Jekyll)은 정적 사이트를 만드는 도구입니다. GitHub Pages와 지킬을 함께 사용하면 비용 없이 블로그를 만들고 운영할 수 있습니다.

순서는 이렇습니다.

- GitHub 계정 생성
- Chirpy Starter 템플릿으로 리포지토리 만들기
- GitHub Pages 배포 소스 설정 및 자동 빌드 확인
- 실제 배포된 사이트 접속해서 확인하기

---

## 1. GitHub 계정 만들기

[github.com](https://github.com)에 접속하고 오른쪽 위 **Sign up** 버튼을 클릭합니다.

![GitHub 랜딩 페이지](/assets/img/posts/github-pages-setup/01_github_landing.png)
_GitHub 첫 화면_

가입 폼에 이메일, 비밀번호, 사용자명(Username)을 입력합니다.

![회원가입 폼](/assets/img/posts/github-pages-setup/02_signup_form.png)
_GitHub 회원가입 폼_

> 입력한 Username이 블로그 주소(`username.github.io`)가 됩니다. Username은 한 번 정하면 바꾸기 어렵습니다. 신중히 입력하세요.
{: .prompt-warning }

가입이 끝나면 로그인된 상태에서 대시보드 홈 화면이 표시됩니다.

![가입 후 대시보드](/assets/img/posts/github-pages-setup/03_dashboard_home.png)
_가입 직후 대시보드 홈 화면_

---

## 어떤 테마를 쓸까?

Jekyll 테마는 [jamstackthemes.dev](https://jamstackthemes.dev/ssg/jekyll/)에서 300개 이상 확인해 볼 수 있는데요. 다양한 스타일을 선택할 수 있습니다.

![Jekyll 테마 목록](/assets/img/posts/github-pages-setup/00_jekyll_themes_list.png)  
_jamstackthemes.dev의 Jekyll 테마 목록_

이 포스트에서는 **Chirpy** 테마를 선택해서 진행하겠습니다. Chirpy 테마는 사이드바 레이아웃 형태인데요. 기본적으로 카테고리, 태그, 검색, 다크모드 같은 기능들이 들어 있습니다. 보통 개발자 블로그나 기술 블로그에서 많이 쓰이지만 일상적인 블로그에도 잘 어울리는 테마입니다.

---

## 2. Chirpy Starter 템플릿으로 리포지토리 생성

Create repository 버튼을 바로 누르지 말고, Chirpy 테마가 적용된 템플릿을 복사합니다.

[github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter) 페이지로 이동합니다.

![chirpy-starter 리포지토리 페이지](/assets/img/posts/github-pages-setup/04_chirpy_starter_repo.png)
_cotes2020/chirpy-starter 페이지_

오른쪽 위 초록색 **Use this template** 버튼을 클릭하고 **Create a new repository**를 선택합니다.

![Use this template 드롭다운](/assets/img/posts/github-pages-setup/05_use_this_template_menu.png)
_Use this template 드롭다운 메뉴_

새 리포지토리 생성 폼이 나타납니다. **Repository name**에 반드시 **`본인 사용자명.github.io`** 형식으로 정확히 입력합니다.

![새 리포지토리 생성 폼](/assets/img/posts/github-pages-setup/06_create_new_repository_form.png)
_리포지토리 이름 입력 — 초록색 "available" 체크 확인_

> 이름이 GitHub 사용자명과 정확히 일치하지 않으면 GitHub Pages가 자동으로 동작하지 않습니다. 입력창 아래 초록색 체크에 "OO.github.io is available."가 표시되는지 확인합니다.
{: .prompt-warning }

**Visibility**는 Public으로 두고 **Create repository** 버튼을 클릭합니다.

---

## 3. 생성된 리포지토리 확인

리포지토리를 만들면 Chirpy 테마의 기본 파일 구조가 그대로 들어 있습니다. 예를 들어 `_posts`, `_tabs`, `_data`, `.github/workflows` 등이 보입니다.

![생성된 리포지토리 파일 구조](/assets/img/posts/github-pages-setup/07_created_repository.png)
_Initial commit으로 만든 리포지토리_

자주 쓰게 될 폴더는 다음과 같습니다.

- **`_posts`** — 블로그 글을 저장하는 폴더
- **`_tabs`** — About, Archives 같은 상단 탭 페이지
- **`.github/workflows`** — 커밋할 때마다 사이트를 빌드하고 배포하는 GitHub Actions 설정

---

## 4. GitHub Pages 배포 소스 설정

리포지토리 상단의 **Settings** 탭을 엽니다.

![Settings General 페이지](/assets/img/posts/github-pages-setup/08_settings_general.png)
_Settings 메뉴 화면_

왼쪽 메뉴에서 **Pages**를 클릭합니다. **Source** 드롭다운을 열면 **GitHub Actions**와 **Deploy from a branch** 두 옵션이 보입니다. **GitHub Actions**를 선택합니다.

![Pages Source 드롭다운](/assets/img/posts/github-pages-setup/09_pages_source_dropdown.png)
_Source를 GitHub Actions로 변경_

저장하면 "GitHub Pages source saved."라는 안내와 함께 "Your site is live at https://username.github.io/"라는 문구가 나타납니다. 이 주소가 블로그 홈 주소가 됩니다.

![Source 저장 완료 화면](/assets/img/posts/github-pages-setup/10_pages_source_saved.png)
_배포 소스 저장 완료 — 사이트가 이미 살아있는 상태_

---

## 5. Actions 탭에서 자동 빌드 확인

리포지토리를 만들면 chirpy-starter에 포함된 워크플로우가 자동으로 실행됩니다. 상단 **Actions** 탭에 들어가면 확인할 수 있습니다.

![Actions 탭 워크플로우 실행 결과](/assets/img/posts/github-pages-setup/11_actions_workflow_runs.png)
_Build and Deploy → pages build and deployment, 두 단계 모두 초록색 체크 표시로 성공_

- **Build and Deploy**: Jekyll 소스를 정적 사이트로 빌드하는 단계
- **pages build and deployment**: 빌드된 결과물을 GitHub Pages 서버에 배포하는 단계

두 단계가 순서대로 성공하면 배포가 끝난 것입니다.

---

## 6. 실제 사이트 접속해서 확인

`https://username.github.io` 주소로 접속하면 Chirpy 기본 테마가 적용된 사이트를 볼 수 있습니다.

![실제 배포된 사이트 화면](/assets/img/posts/github-pages-setup/12_site_live.png)
_실제로 뜬 Chirpy 기본 테마 블로그_

아직 글이 없으니 본문은 비어 있지만, chirpy-starter는 샘플 포스트가 없는 빈 템플릿이기 때문에 정상입니다. 왼쪽 사이드바 메뉴는 이미 작동합니다.

---

## 빌드가 실패했다면

이번 편은 운 좋게 한 번에 성공했지만, Actions 탭에서 빨간 X를 마주치는 경우도 흔합니다. 대부분 아래 두 가지 중 하나가 원인입니다.

- 리포지토리 이름이 `username.github.io` 형식과 정확히 일치하지 않는 경우
- Settings → Pages의 Source가 GitHub Actions로 제대로 저장되지 않은 경우

Actions 탭에서 실패한 워크플로우를 클릭하면 실제 에러 로그를 확인할 수 있습니다. 로그 메시지를 보면 원인을 좁히기가 훨씬 수월합니다.

---

## 자주 묻는 질문

**GitHub Pages는 정말 완전 무료인가요?**

네 개인 블로그를 호스팅하는 것은 완전히 무료입니다. 다만 나중에 블로그에 GitHub Pages 주소가 아니라 커스텀 도메인을 연결하려면 도메인 구매 비용은 별도로 듭니다.(이건 선택 사항입니다.)

**리포지토리 이름을 잘못 지으면 어떻게 되나요?**

`username.github.io` 형식이 아니면 GitHub Pages가 자동으로 활성화되지 않습니다. 이 경우 리포지토리를 삭제하고 새로 만드는 걸 추천드립니다.

**나중에 다른 테마로 바꿀 수 있나요?**

가능은 하지만 테마마다 `_config.yml` 구조와 필요한 폴더가 구성이 달라서 상당히 까다로울 수 있습니다. 그래서 처음부터 확실하게 테마를 정하고 가시는 게 좋습니다.

---

## 마무리

계정을 만든 지 몇 분 만에 GitHub Pages와 Jekyll로 블로그를 만들었습니다. 아직 수정할 부분이 남아 있긴 한데요.

다음 편에 이어서 `_config.yml`, `_tabs/about.md`, `_data/contact.yml` 파일을 고쳐서 블로그 기본 정보를 설정해보겠습니다. 사이트 제목, 설명, About 페이지 소개글등을 넣는 방법을 알아 볼겁니다.