# 오늘 운동 — v3.0 SEO 배포본

기존 v3.0 모바일 호환성 개선본을 바탕으로 검색엔진 최적화 파일만 추가했습니다. 운동 기록·휴식 타이머·JSON 백업·오프라인 저장 등 앱 기능의 JavaScript 코드는 변경하지 않았습니다.

## 포함 파일
- `index.html` : 기존 운동 앱 + SEO 메타태그, 공유 미리보기, 검색엔진이 JavaScript 없이도 읽을 수 있는 짧은 소개 문구, 구조화 데이터
- `robots.txt` : 모든 검색 로봇의 사이트 수집 허용 및 사이트맵 경로
- `sitemap.xml` : 메인 페이지 주소 1개 등록
- `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png` : 기존 PWA 구성 (서비스워커 캐시 버전만 변경)

## 중요: 기존 주소 유지하며 배포하기
대상 주소: https://workout-record-v30-mobile.vercel.app/
이 프로젝트는 기존 URL을 기준으로 canonical, Open Graph, 사이트맵을 생성했습니다. 새로운 Vercel 프로젝트/도메인으로 배포하는 경우, `index.html`, `robots.txt`, `sitemap.xml`의 URL을 새 주소로 바꿔야 합니다.

**기존 Vercel 프로젝트에 프로덕션 재배포**해야 같은 도메인과 브라우저 저장 기록을 유지할 수 있습니다. Vercel Drop에 새 프로젝트로 업로드하면 주소가 달라져 기록이 보이지 않을 수 있습니다.

### 같은 프로젝트에 CLI로 배포하는 예시
1. 이 ZIP을 압축 해제합니다 (파일들이 프로젝트 루트에 있도록).
2. Vercel 계정에 로그인한 PC에서 터미널을 엽니다.
3. 필요한 경우 `npm install -g vercel` 후 `vercel login`.
4. 압축 해제한 폴더에서 `vercel link`를 실행하고 **기존 `workout-record-v30-mobile` 프로젝트**를 선택합니다. 새로운 프로젝트를 만들지 마세요.
5. 연결된 프로젝트 이름을 확인하고 `vercel deploy --prod`로 배포합니다.
6. 배포 후 https://workout-record-v30-mobile.vercel.app/ 와 `/robots.txt`, `/sitemap.xml`이 열리는지 확인합니다.

Git 연결 프로젝트라면 Git 저장소에 이 파일들을 반영해 main 브랜치로 병합하는 방법이 더 편리합니다.

## 검색엔진 등록
### Google Search Console
1. https://search.google.com/search-console 에 로그인합니다.
2. URL 접두어 속성으로 `https://workout-record-v30-mobile.vercel.app/`를 등록합니다.
3. **HTML 태그 방식**을 선택하면 Google이 `google-site-verification` 메타태그를 발급합니다.
4. `index.html`의 `<head>`에 있는 인증 주석 근처에 실제 발급 태그를 그대로 넣고 **같은 프로젝트로 다시 배포**합니다. 또는 HTML 파일 업로드 방식으로 제공된 검증 파일을 루트에 넣어 재배포합니다.
5. 인증을 완료하고 `https://workout-record-v30-mobile.vercel.app/sitemap.xml`을 제출한 뒤 메인 URL의 색인 생성 요청을 진행합니다.

### 네이버 서치어드바이저
1. https://searchadvisor.naver.com/ 의 웹마스터 도구로 사이트를 등록합니다.
2. **HTML 태그 방식**으로 발급받은 `naver-site-verification` 메타태그를 `index.html`의 `<head>`에 추가해 같은 프로젝트에 재배포합니다. 또는 인증 HTML 파일을 루트에 넣어 배포합니다.
3. 사이트 소유 확인 후 사이트맵 경로 `https://workout-record-v30-mobile.vercel.app/sitemap.xml`을 제출하고 웹페이지 수집을 요청합니다.

**주의:** 실제 구글/네이버 소유권 확인 코드가 아직 없으므로 이번 ZIP에는 인증 태그가 없습니다. 배포만으로 자동 인증되는 것은 아닙니다. 검색엔진 수집·색인·순위는 보장되지 않습니다.

## 개인 운동 기록
운동 기록은 Vercel에 업로드되지 않고 각 기기의 브라우저 저장소에 남습니다. SEO는 공개 메인 페이지를 대상으로 하며 개인 세트·통증·메모를 검색엔진에 공개하지 않습니다. 기기를 바꾸거나 도메인을 변경할 때는 JSON 백업 및 가져오기를 이용하세요.
