---
title: "VS Code에서 지킬 포스팅할 때 이미지 쉽게 넣는 방법"
date: 2026-09-25 10:00:00 +0900
categories: [Jekyll, 개발환경]
tags: [jekyll, vscode, markdown, chirpy]
description: "확장 설치 없이 VS Code 기본 기능만으로, 이미지를 복사해서 붙여넣으면 지정한 폴더에 자동 저장되고 링크까지 삽입되도록 설정하는 방법을 정리했습니다."
image:
  path: /assets/img/posts/vscode-image-paste/15_local_result_top.webp
  alt: 붙여넣은 이미지가 로컬 서버에서 표시된 모습
published: true
---

## 이번 포스트에서 해볼 것

[지난 포스트](/posts/vscode-posting-workflow/)에서는 포스트에 이미지를 삽입할 때 `assets/img/posts/폴더명/`에 직접 이미지를 넣은 후 포스트에 이미지 경로를 직접 입력해서 넣었었는데요. 이렇게 번거롭지 않게 쉽게 이미지를 삽입하는 방법을 알아보겠습니다.

따로 VS Code 확장 설치 없이 기본 기능만으로, **이미지를 복사해서 붙여넣으면 지정한 폴더에 자동으로 저장되고 링크까지 삽입되도록** 설정해 보겠습니다.

---

## 1. 저작권 걱정 없는 무료 이미지 사이트

블로그 글에 넣는 이미지는 저작권 문제가 없는 이미지일 수록 좋습니다. 대표적인 저작권 없이 무료로 사용할 수 있는 이미지 제공 사이트 3곳을 소개합니다.

- **Unsplash** — [unsplash.com](https://unsplash.com){:target="_blank" rel="noopener"}
- **Pixabay** — [pixabay.com](https://pixabay.com){:target="_blank" rel="noopener"}
- **Pexels** — [pexels.com](https://www.pexels.com){:target="_blank" rel="noopener"}

> 세 사이트 모두 무료로 쓸 수 있는 이미지를 제공하지만, 사이트마다 라이선스 조건이 조금씩 다릅니다. 사용 전에 각 사이트의 라이선스 페이지를 한 번 확인해 두세요.
{: .prompt-info }

이 글에서는 Unsplash 사이트의 이미지를 사용해보겠습니다.

![Unsplash 메인 화면](/assets/img/posts/vscode-image-paste/01_unsplash_main.webp)
_Unsplash 메인 화면_

마음에 드는 이미지를 클릭해 상세 화면을 연 뒤, 이미지 위에서 우클릭 → **이미지 복사**를 선택합니다.

![이미지 우클릭 후 이미지 복사](/assets/img/posts/vscode-image-paste/02_unsplash_copy_image.webp)
_이미지 우클릭 → 이미지 복사_

---

## 2. 설정 없이 붙여넣으면?

먼저 아무 설정 없이, md 파일 본문에서 `Ctrl+V`로 붙여넣어 보겠습니다.

![기본 설정으로 붙여넣은 결과](/assets/img/posts/vscode-image-paste/03_default_paste.png)
_링크는 자동으로 들어가지만, 이미지가 _posts 폴더에 저장됨_

`![alt text](image.png)` 형태의 링크가 자동으로 삽입되고, 이미지 파일도 저장됩니다. 그런데 이미지가 저장되는 위치가 `_posts` 폴더 안, 포스팅하는 md 파일과 같은 경로에 `image.png`로 저장되었습니다.

이대로 쓰면 포스트 파일과 이미지 파일이 한 폴더에 뒤섞여서 관리하기 어려워집니다. 이미지를 `assets/img/posts/` 아래에 모아두는 방식으로 저장 위치 설정을 바꿔보겠습니다.

---

## 3. 이미지 저장 위치 설정하기

`Ctrl+,`(컨트롤 + 쉼표)를 눌러 설정 화면을 엽니다. 상단의 **User / Workspace** 중 **Workspace** 탭을 선택하고, 검색창에 아래 내용을 입력합니다.

```
markdown.copyFiles.destination
```

> **Workspace** 탭에서 설정하면 지금 열려 있는 블로그 폴더에만 적용됩니다. 다른 프로젝트에는 영향을 주지 않습니다.
{: .prompt-tip }

설명 아래로 조금 내려가면 **Add Item** 버튼이 보입니다.

![설정 검색 결과](/assets/img/posts/vscode-image-paste/04_settings_search.png)
_markdown.copyFiles.destination 검색 결과_

**Add Item**을 누르면 Item과 Value 입력칸이 나타납니다. 아래처럼 입력합니다.

![Item과 Value 입력](/assets/img/posts/vscode-image-paste/05_settings_add_item.png)
_Item과 Value 입력_

Item은 **어떤 md 파일에 적용할지**를 정하는 칸입니다. `_posts` 폴더 안의 md 파일에 적용하도록 입력합니다.

```
**/_posts/*.md
```

Value는 **이미지를 어디에 저장할지**를 정하는 칸입니다.

```
/assets/img/posts/${documentBaseName}/
```

- 맨 앞의 `/`는 컴퓨터의 최상위 경로가 아니라 **블로그 폴더 기준**이라는 뜻입니다.
- `${documentBaseName}`은 md 파일명에서 `.md`를 뺀 이름으로 바뀝니다. 예를 들어 `2026-09-25-image-paste-test.md`라면 `assets/img/posts/2026-09-25-image-paste-test/` 폴더에 저장됩니다. 이렇게 하면 포스트마다 이미지 폴더가 자동으로 따로 만들어지게 되어 이미지들을 깔끔하게 관리하기 편해집니다.

**OK**를 누르면 바로 적용됩니다.

![설정이 추가된 화면](/assets/img/posts/vscode-image-paste/06_settings_item_added.png)
_설정 추가 완료_

이 설정은 블로그 폴더의 `.vscode/settings.json` 파일에 자동으로 기록됩니다. Chirpy 테마는 이 파일을 기본으로 포함하고 있어서, 기존 내용 맨 아래에 방금 입력한 설정이 추가된 것을 확인할 수 있습니다.

![settings.json에 기록된 설정](/assets/img/posts/vscode-image-paste/07_settings_json.png)
_.vscode/settings.json에 자동으로 기록된 설정_

---

## 4. 다시 붙여넣기

앞에서 생긴 `_posts/image.png`와 링크는 지우고, 다시 이미지를 복사해서 `Ctrl+V`로 붙여넣습니다.

![설정 후 붙여넣은 결과](/assets/img/posts/vscode-image-paste/08_paste_after_setting.png)
_assets/img/posts/파일명/ 폴더에 이미지가 저장됨_

이번에는 `assets/img/posts/2026-09-25-image-paste-test/` 폴더가 자동으로 만들어지고, 그 안에 `image.png`가 저장되었습니다. 링크 경로도 저장 위치에 맞게 자동으로 들어갑니다.

### 여러 장을 붙여넣으면?

이미지를 계속 붙여넣으면 같은 이름이 겹치지 않도록 `image-1.png`, `image-2.png`처럼 숫자가 자동으로 붙습니다.

![여러 장 붙여넣었을 때](/assets/img/posts/vscode-image-paste/09_multiple_paste_numbering.png)
_파일명 뒤에 숫자가 자동으로 붙음_

이렇게만 해도 이름이 겹칠 일은 없지만 가능하면 파일명도 이미지에 맞게 바꾸는 게 좋을 겁니다. 이 방법은 6번에서 설명하겠습니다.

---

## 5. 내 컴퓨터의 이미지 파일 넣기

로컬에 있는 이미지 파일을 넣을 때는 파일 탐색기에서 이미지 파일을 VS Code 편집 화면으로 끌어다 놓으면 됩니다.

> 그냥 끌어다 놓으면 VS Code가 이미지를 새 탭으로 열어버립니다. **`Shift` 키를 누른 채로** 편집 화면에 놓아야 링크로 삽입됩니다.
{: .prompt-tip }

![파일 탐색기에서 이미지 드래그](/assets/img/posts/vscode-image-paste/10_local_file_drag.webp)
_파일 탐색기에서 VS Code 편집 화면으로 이미지 끌어오기_

복사해서 넣은 이미지와는 다르게 `image.png` 대신 **원래 파일명이** 입력됩니다.

![로컬 이미지 붙여넣은 결과](/assets/img/posts/vscode-image-paste/11_local_file_paste.png)
_원래 파일명 그대로 복사됨_

파일명에 공백이 있으면 경로가 `<...>`로 감싸져서 들어갑니다. 동작에는 문제가 없지만, 보기에도 깔끔하지 않으니 다음 단계에서 이름을 바꿔주는 게 좋습니다.

> 아이폰으로 찍은 사진은 HEIC 형식인 경우가 많은데, 대부분의 브라우저에서 HEIC 이미지는 표시되지 않습니다. JPG나 PNG로 변환한 뒤 넣어주세요.
{: .prompt-warning }

---

## 6. 이미지 파일명 바꾸기

파일명은 링크 안의 파일명(예: `image.png`) 부분에 커서를 두고 `F2`를 누르면 이름 바꾸기 입력창이 뜹니다. 입력창에는 경로 전체가 표시되는데, 앞쪽 경로는 그대로 두고 **맨 끝의 파일명만** 바꾼 뒤 Enter를 누릅니다.

![F2 이름 바꾸기 입력창](/assets/img/posts/vscode-image-paste/12_rename_input.png)
_F2를 누르면 뜨는 이름 바꾸기 입력창_

Enter를 누르면 **링크와 실제 이미지 파일명이 함께** 바뀝니다.

![파일명 변경 결과](/assets/img/posts/vscode-image-paste/13_rename_file.png)
_링크와 탐색기의 실제 파일명이 함께 변경됨_

> 파일명은 영문 소문자, 숫자, 하이픈(`-`)이나 언더바(`_`) 조합으로 짓는 것을 추천합니다. 공백이나 특수문자가 들어가면 경로가 복잡해지고, 나중에 다른 환경에서 문제가 생길 수 있습니다.
{: .prompt-tip }

---

## 7. alt text 채우기

붙여넣은 링크의 `[alt text]` 부분은 비워두지 말고 이미지 설명으로 바꿔주는 게 좋습니다.

![alt text 입력](/assets/img/posts/vscode-image-paste/14_alt_text.png)
_alt text 자리에 이미지 설명 입력_

alt text는 이런 역할을 합니다.

- 이미지가 로드되지 않을 때 이미지 대신 표시됩니다.
- 화면 리더기를 쓰는 사용자에게 이미지 내용을 전달합니다.
- 검색엔진이 이미지 내용을 이해하는 데 사용됩니다.

특히 검색 노출을 신경 쓰는 블로그라면 꼭 채워두는 습관을 들이는 게 좋습니다.

---

## 8. 로컬 서버에서 확인

터미널에서 로컬 서버를 실행하고 `http://127.0.0.1:4000`으로 접속해 포스트를 확인합니다.

```powershell
bundle exec jekyll serve --livereload --unpublished
```

![로컬 서버에서 확인한 포스트](/assets/img/posts/vscode-image-paste/15_local_result_top.webp)
_웹에서 복사해 붙여넣은 이미지_

![로컬 이미지 확인](/assets/img/posts/vscode-image-paste/16_local_result_local_image.webp)
_내 컴퓨터에서 복사해 넣은 이미지_

이미지들이 모두 정상적으로 표시되는 것을 확인할 수 있습니다.

---

## 마무리

이 글을 따라 이미지 저장 경로를 설정해 두면, 이후에는 이미지를 넣는 과정이 편해질 거예요.

- 이미지 복사 → md 파일에 `Ctrl+V` → `F2`로 파일명 정리 → alt text 입력

그럼 다음 포스팅으로 돌아오겠습니다.
