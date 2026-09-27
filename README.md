# 고세종T 테스트 성적 관리 시스템

학원 테스트 성적을 관리하는 웹앱입니다. 반/학생 관리, 답안 입력·자동 채점, 통계, 성적표 이미지 출력을 지원합니다.

- 파일은 `index.html` 하나뿐입니다. 빌드 과정이 없으니 수정하고 커밋하면 바로 반영됩니다.
- 데이터는 Firebase Firestore(`sejong-tds` 프로젝트)에 저장되고, 로그인은 Firebase 이메일/비밀번호 계정으로 합니다.

## 배포 (GitHub Pages)

1. 저장소 **Settings → Pages**
2. Source: **Deploy from a branch**, Branch: **main / (root)** → Save
3. 1~2분 뒤 `https://<계정명>.github.io/<저장소명>/` 에서 접속할 수 있습니다.

## 처음 한 번 해야 할 Firebase 설정

[Firebase 콘솔](https://console.firebase.google.com/) → `sejong-tds` 프로젝트에서:

- **Authentication → Settings → 승인된 도메인**에 `<계정명>.github.io`를 추가합니다. 추가하지 않으면 Pages 주소에서 로그인이 되지 않습니다.
- **Authentication → Users**에서 로그인할 계정을 추가하거나 관리합니다.
- **Firestore → 규칙**이 로그인한 사용자만 읽고 쓰도록 되어 있는지 확인합니다. 예:
  ```
  rules_version = '2';
  service cloud.firestore {
    match /databases/{database}/documents {
      match /{document=**} {
        allow read, write: if request.auth != null;
      }
    }
  }
  ```

> `index.html` 안의 Firebase `apiKey`는 공개돼도 되는 값입니다. 보안은 위의 로그인과 Firestore 규칙이 담당합니다.

## 백업

앱의 **기타** 탭에서 전체 데이터를 JSON으로 내보내거나 가져올 수 있습니다. 가끔 내보내서 보관해 두세요.
