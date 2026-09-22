---
title: "VS Code로 지킬 블로그 포스트 작성하고 GitHub Pages에 배포하기"
date: 2026-09-22 10:00:00 +0900
categories: [Jekyll, 개발환경]
tags: [jekyll, vscode, github pages, github actions]
description: "VS Code로 새 포스트 파일을 만들고, 로컬 미리보기로 확인한 뒤 GitHub Pages에 실제로 배포하기까지의 과정을 정리했습니다."
image:
  path: /assets/img/posts/vscode-posting-workflow/27_live_post_detail.png
  alt: 지킬에 포스팅 후 페이지 확인
published: false
---

## 이번 편에서 할 일

이번 편에서는 VS Code에서 실제로 **포스트를 작성**하고, 로컬에서 확인한 뒤, **GitHub Pages에 배포**하는 과정을 진행합니다.

---

## 1. 새 포스트 파일 만들기

VS Code 상단 메뉴에서 **File > Open Folder**로 블로그 리포지토리 폴더를 엽니다.

![File 메뉴에서 Open Folder 선택](/assets/img/posts/vscode-posting-workflow/01_file_open_folder.png)
_File > Open Folder_

리포지토리 폴더(`morotamia.github.io`)를 선택합니다.

![폴더 선택 창](/assets/img/posts/vscode-posting-workflow/02_select_folder_dialog.png)
_리포지토리 폴더 선택_

폴더가 열리면 왼쪽 탐색기에 `_posts`, `_tabs`, `assets` 등 리포지토리 구조가 나타납니다.

![탐색기에 열린 리포지토리 구조](/assets/img/posts/vscode-posting-workflow/03_explorer_structure.png)
_탐색기에 열린 리포지토리 폴더 구조_

`_posts` 폴더에서 마우스 오른쪽 클릭 후 **New File**을 선택합니다.

![_posts 폴더 우클릭 메뉴](/assets/img/posts/vscode-posting-workflow/04_new_file_menu.png)
*`_posts` 폴더에서 새 파일 생성*

파일명은 `YYYY-MM-DD-제목.md` 형식으로 입력합니다. 파일이 생성되면 빈 편집 화면이 열립니다.

![새로 생성된 빈 파일](/assets/img/posts/vscode-posting-workflow/05_new_empty_file.png)
_새로 생성된 파일 (빈 상태)_

---

## 2. Front Matter 작성

파일 맨 위에 title, date, categories, tags, published 등 기본 정보를 입력합니다. 작성 중에는 `published: false`로 두어 실수로 사이트에 바로 노출되지 않도록 합니다.

![Front matter 입력 화면](/assets/img/posts/vscode-posting-workflow/06_front_matter.png)
_Front matter 작성 (published: false)_

---

## 3. 본문 작성 및 이미지 삽입

본문을 작성하고, 이미지는 `assets/img/posts/포스트폴더명/` 경로에 넣은 뒤 아래와 같은 형식으로 참조합니다.

```markdown
![이미지 설명](/assets/img/posts/포스트폴더명/파일명.png)
_캡션 텍스트_
```

본문과 이미지 참조까지 작성된 화면은 아래와 같습니다.

![본문 작성 완료 화면](/assets/img/posts/vscode-posting-workflow/07_body_written.png)
_본문 작성 완료 (이미지 경로 포함)_

이미지 파일은 참조 경로와 동일한 위치에 넣어둡니다.

![이미지 파일이 들어간 폴더](/assets/img/posts/vscode-posting-workflow/08_image_folder.png)
_이미지 파일을 넣어둔 폴더_

`Ctrl+Shift+V`로 마크다운 미리보기를 열면 아래처럼 front matter가 표 형태로, 본문이 렌더링된 형태로 보입니다.

![마크다운 미리보기 - 상단부](/assets/img/posts/vscode-posting-workflow/09_preview_top.png)
_마크다운 미리보기 상단부 (front matter + 본문 텍스트)_

아래로 스크롤하면 이미지도 정상적으로 렌더링된 것을 확인할 수 있습니다.

![마크다운 미리보기 - 이미지 렌더링](/assets/img/posts/vscode-posting-workflow/10_preview_image.png)
_마크다운 미리보기에서 이미지가 렌더링된 모습_

---

## 4. 로컬 서버로 확인

**View > Terminal** 메뉴로 통합 터미널을 엽니다.

![View 메뉴에서 Terminal 선택](/assets/img/posts/vscode-posting-workflow/11_view_terminal_menu.png)
_View > Terminal_

아래 명령어로 로컬 서버를 실행합니다.

```powershell
bundle exec jekyll serve --livereload --unpublished
```

`--unpublished` 옵션 덕분에 `published: false`인 글도 로컬에서 바로 확인할 수 있습니다.

![jekyll serve 실행 로그](/assets/img/posts/vscode-posting-workflow/12_jekyll_serve_log.png)
_서버가 정상적으로 실행된 상태_

브라우저에서 `http://127.0.0.1:4000`으로 접속하면 홈 화면에 작성한 포스트가 보입니다.

![로컬 사이트 홈 화면](/assets/img/posts/vscode-posting-workflow/13_local_home.png)
_로컬 서버에서 확인한 홈 화면_

포스트를 클릭하면 상세 페이지에서 본문과 이미지가 실제로 어떻게 보일지 확인할 수 있습니다.

![로컬 사이트 포스트 상세 페이지](/assets/img/posts/vscode-posting-workflow/14_local_post_detail.png)
_로컬 서버에서 확인한 포스트 상세 페이지_

---

## 5. 게시 처리 및 Git 커밋

내용 확인이 끝나면 front matter의 `published` 값을 `true`로 바꿉니다.

![published: true로 변경](/assets/img/posts/vscode-posting-workflow/15_published_true.png)
_published: true로 변경_

왼쪽 **Source Control** 아이콘을 클릭하면 변경된 파일 목록이 보입니다. 파일을 우클릭하면 **Stage Changes** 메뉴로 개별 스테이징도 가능합니다.

![Stage Changes 메뉴](/assets/img/posts/vscode-posting-workflow/16_stage_changes_menu.png)
_변경 파일 우클릭 → Stage Changes_

스테이징이 끝나면 **Staged Changes** 항목에 파일들이 이동합니다.

![Staged Changes 상태](/assets/img/posts/vscode-posting-workflow/17_staged_changes.png)
_스테이징 완료 상태_

**Commit** 버튼을 눌렀을 때, git에 사용자 정보가 설정되어 있지 않으면 아래와 같은 안내가 뜹니다.

![user.name, user.email 설정 안내](/assets/img/posts/vscode-posting-workflow/18_git_config_warning.png)
_git 사용자 정보 설정 안내_

터미널에서 아래 명령어로 사용자 정보를 설정합니다. 한 번 설정해두면 이후 커밋부터는 다시 나타나지 않습니다.

```powershell
git config --global user.name "이름"
git config --global user.email "이메일"
```

![터미널에서 git config 실행](/assets/img/posts/vscode-posting-workflow/19_git_config_terminal.png)
_git config 명령어로 사용자 정보 설정_

다시 커밋을 진행하면 커밋 메시지 입력 화면이 열립니다. 첫 줄에 메시지를 입력하고 저장하면 커밋이 완료됩니다.

![커밋 메시지 입력 화면](/assets/img/posts/vscode-posting-workflow/20_commit_message.png)
_커밋 메시지 입력_

---

## 6. GitHub에 Push 및 배포 확인

커밋이 완료되면 **Commit** 버튼이 **Sync Changes 1↑**로 바뀝니다. 이 버튼을 누르면 로컬 커밋을 GitHub로 전송합니다.

![Sync Changes 버튼](/assets/img/posts/vscode-posting-workflow/21_sync_changes_button.png)
_Sync Changes 1↑ 버튼_

버튼을 누르면 원격 저장소와 pull/push를 진행한다는 안내가 뜹니다. **OK**를 누르면 진행됩니다.

![pull/push 확인 안내](/assets/img/posts/vscode-posting-workflow/22_pull_push_confirm.png)
_pull/push 진행 확인_

이 리포지토리에 처음 push하는 경우, GitHub 로그인 창이 뜹니다. **Sign in with your browser**를 눌러 로그인을 완료합니다.

![GitHub 로그인 창](/assets/img/posts/vscode-posting-workflow/23_github_signin.png)
_GitHub 로그인 창_

push가 끝나면 Graph 패널에서 로컬 커밋과 `origin/main`이 같은 위치에 놓인 것을 확인할 수 있습니다.

![push 완료 후 그래프](/assets/img/posts/vscode-posting-workflow/24_push_complete_graph.png)
_push 완료 후 커밋 그래프_

---

## 7. GitHub Actions 배포 확인 및 실제 사이트 확인

GitHub 리포지토리의 **Actions** 탭에서 방금 push한 커밋에 대한 워크플로우가 실행되고, 완료되면 초록색 체크로 표시됩니다.

![Actions 탭 워크플로우 완료](/assets/img/posts/vscode-posting-workflow/25_actions_success.png)
_워크플로우 실행 완료_

실제 도메인으로 접속하면 홈 화면에 새 글이 반영된 것을 확인할 수 있습니다.

![실제 사이트 홈 화면](/assets/img/posts/vscode-posting-workflow/26_live_home.png)
_실제 사이트에 반영된 홈 화면_

포스트 상세 페이지에 들어가면 로컬에서 확인했던 내용과 이미지가 그대로 반영되어 있습니다.

![실제 사이트 포스트 상세 페이지](/assets/img/posts/vscode-posting-workflow/27_live_post_detail.png)
_실제 사이트에서 확인한 포스트 상세 페이지_

---

## 마무리

이번 포스팅에서는 VS Code에서 새 포스트 파일을 만들고, 로컬에서 확인한 뒤, GitHub에 커밋과 push로 배포하는 흐름을 한 번 따라가 봤습니다.

- 요약하면 새글 작성시에는 `_posts`에 새 파일 → `published: false`로 작성한 뒤 로컬에서 확인 → `true`로 전환 → commit → push

그럼 다음 포스팅으로 돌아오겠습니다.