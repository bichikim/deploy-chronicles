---
theme: default
title: 배포 프로세스 개선
backgroundSize: right top
mdc: true
---

<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&display=swap');
  
  body {
    background-color: black;
    font-family: "Noto Sans KR", "Pretendard Variable", sans-serif;
  }
  li, span {
    --uno: 'dark:text-#f5f5f5';
    font-weight: 400;
  }
  .slidev-layout strong {
    font-weight: 700;
  }
  .slidev-layout h2 {
    line-height: 3.5rem;
  }
  .slidev-layout h3 {
    line-height: 3rem;
  }
  strong, h1, h2, h3, h4, h5 {
    --uno: 'dark:text-white';
  }
  .slidev-code-wrapper span {
    font-size: 1.3rem;
    line-height: 1.7rem;
  }
</style>

# 배포 프로세스 개선

업무를 잘하려다 보니...🤓

<div class="w-full flex justify-end items-end gap-5">
  <span class="font-size-6">이 프레젠테이션 문서 주소 --></span>
  <QrCode value="https://deploy-chronicles.vercel.app" size="240" />
</div>

---
layout: cover
image: /images/page-2-img.png
backgroundSize: contain
---

# 배포 프로세스 효율 문제

느리고 느린 배포 프로세스

---
layout: image-right
image: /images/page-2-img.png
backgroundSize: contain
---

# 배포 프로세스 효율 문제

## 🚀 배포 위험도 관리
- **QA vs Production** <br> 드물게 미묘한 환경 차이로 QA에서 발견 못한 이슈
- **전체 사용자 영향** <br> 이슈 발생 시 모든 고객에게 100% 적용
- **롤백 지연** <br> 더 빠른 롤백 시간으로 피해 최소화 필요

<span v-mark.underline.orange class="absolute bottom-400px right-250px">ㅤㅤㅤㅤ</span>
<span v-mark.underline.orange class="absolute bottom-190px right-180px">ㅤㅤㅤㅤ</span>

---
layout: image-right
image: ./images/page-3-img.png
backgroundSize: contain
---

# 배포 프로세스 효율 문제

## 🔧 디버깅 환경의 복잡성
- **디바이스별 다른 방법** <br> IVI, TV 디바이스마다 제조사/버전별 다른 디버깅
- **준비 시간 과다** <br> 디버깅 설정에 10-30분 소요
- **저사양 디바이스 한계** <br> 디버깅 중 속도저하 및 프리징 발생

<span v-mark.underline.orange class="absolute bottom-85px right-430px">ㅤㅤㅤㅤ</span>

---
layout: image-right
image: ./images/page-4-img.png
backgroundSize: contain
---

# 배포 프로세스 효율 문제

## 📝 코드 리뷰의 비효율성
- **리뷰 시간 과다**: GitLab MR 리뷰에 수십분 소요
- **누락 발생**: 리뷰에서 체크 못한 부분들 빈번
- **일관성 부족**: 리뷰어별 기준 차이

<span v-mark.underline.orange class="absolute bottom-57px right-270px">ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ</span>

---
layout: cover
image: ./images/page-5-img.png
backgroundSize: auto
---

# 무엇을 어떻게 개선?
- 배포 위험도 관리
- 디버깅 환경의 복잡성
- 코드 리뷰의 비효율성

---
layout: image-right
image: ./images/page-5-img.png
backgroundSize: auto
---

<style scoped>
  .slidev-page > div {
    overflow: visible;
    white-space: nowrap;
  }
</style>

# 무엇을 어떻게 개선?

## 🚀 AWS CloudFront 점진적 배포
- **빠른 롤백** 몇 초 내
- **이슈시 적은 영향** 트래픽 기반 / 헤더 기반
- 프로덕트 환경에서 최소 리스크로 테스트 가능

---
layout: image-right
image: ./images/page-6-img.png
backgroundSize: contain
---

# 무엇을 어떻게 개선?

## 🐛 Chii 원격 디버깅 툴
- **모든 디바이스** 에서 **같은 디버깅 방법**
- **모든 디바이스** 에서 브라우저 개발자 도구와 **같은 환경**
- **모든 디바이스** 에서 **최신 디버깅** 툴 유지

---
layout: image-right
image: ./images/page-7-img.png
backgroundSize: contain
---

# 무엇을 어떻게 개선?

<style scoped>
  .slidev-page > div {
    overflow: visible;
    white-space: nowrap;
  }
</style>

## 🤖 Cursor CLI x GitLab CI/CD
- dev 브랜치 MR 에 의한 **자동화된 코드 리뷰**
- AI 가 **요약을 MR 메세지로 작성**
- 개선이 필요한 **코드의 위치**를 표기하고 **개선점 작성**

<div class="absolute bottom-100px left-100px flex gap-4 items-center" v-motion
    :initial="{ opacity: 0, y: 100 }"
    :enter="{ opacity: 1, y: 0, scale: 1 }"
    :variants="{ custom: { scale: 2 } }"
    :hovered="{ scale: 1.2 }"
    :delay="200"
    :duration="1200"
 >
  <img src="/images/page-6-5-img.png" class="w-100px h-100px rd-7 rotate--5 shadow-xl">
  <span class="text-size-10">X</span>
  <img src="/images/page-6-6-img.png" class="w-100px h-100px rd-7 rotate-5 shadow-xl">
</div>

<span v-mark.underline.orange class="absolute bottom-165px left-550px">ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ</span>

---

# CloudFront 점진적 배포

## 🎯 장점

### 빠른 롤백 (몇 초 내)
- **기존**: 전체 배포 → 문제 발생 → 수동 롤백 (1-2분)
- **개선**: 점진적 배포 → 문제 감지 → 자동 롤백 (5초 이내)

### 이슈시 적은 영향
- **트래픽 분할**: 15% → 100%
- **문제 발생 시**: 해당 % 사용자만 영향
- **빠른 대응**: 즉시 배포 중단 가능

### 프로덕션 환경에서 최종 검토
- **특정 클라이언트** 만 **새로운 버전** 사용가능 <br> 헤더 기반으로 특정

---
---

# CloudFront 점진적 배포

## ⚠️ 우려 사항

### API 하위 호환성
- **기존 API 버전 정상 작동 유지** 필요

### 특정 % 접속 방법 제한
- **개발자 테스트** 어려움 <br> 헤더 기반으로 설정 변경해서 확인

### 세션 유지 길이
- 세션 만료로 오작동이 될 가능성 <br> % 기반 접속일 경우 세션 유지기간 최대(1시간인가??)

---
image: ./images/page-10-img1.png
---

# CloudFront 점진적 배포

#### 기존

<img src="/images/page-10-img1.png" class="h-80%" />

<!--
기존에는 GitLab 에서 버킷에 소스코드가 배보 (1) 되고 클라이언트가 CloudFront 를 통해 소스코드를 가져간다
-->

---
layout: default
---

# CloudFront 점진적 배포

#### 변경 후

<img src="/images/page-10-img2.png" class="h-85%" />

<!--
점진적 배포 적용 후 GitLab 에서 가중치 % 기반 또는 헤더 기반 새 소스를 올리는 (1) 버켓과 실 프로덕트 새 소스코드를 올리는 (3) 버켓이 있고  가중치 % 기반 또는 헤더 기반에 따라 클라이언트를 (2) 로 보내거나 (4) 로 보내서 점진적 배포가 적용된다
-->

---
layout: default
---

# CloudFront 점진적 배포

## 📊 적용 결론

| 항목 | 기존 | 개선 후
|------|------|---------|
| 롤백 시간 | 1-2분 | 5초 이내 |
| 이슈로 서비스 문제 범위 | 전체 사용자 | 일부 사용자 |
| 안전한 프로덕션 Live 검증 | 불가능 | 가능 |

<!--
트레픽 제어로 수 초내 롤백이 가능하고 

헤더 기반으로는 특정 테스터 클라이언트만 가중치 % 기반으로는 가중치 만큼만 이슈가 있을 경우 그 이슈에 노출되게 된다

헤더 기반으로 트레픽 제어할 경우 프로덕션 환경에서 이팩트 없는 live 검증을 할 수 있다
-->

---
layout: default
---

# Chii 원격 디버깅 툴

## 🚀 주요 기능

- **웹 기반 인터페이스**: 브라우저에서 디바이스 목록 페이지에서 <span v-mark.underline.orange>바로 접속 </span>
- **원격 제어**: <span v-mark.underline.orange>디바이스 조작 및 테스트</span>
- **크로스 플랫폼**: 모든 디바이스에서 <span v-mark.underline.orange>동일한 디버깅 경험</span>

<!--
IVI 와 TV 디바이스마다 긴 디버깅 준비 시간 / 복잡하고  각각 다른 디버깅 방법 / 디버깅 런타임 성능 / 제공되는 디버거 버전이 달라서  등 디버깅 과정이 고통 스러웠다

Chii 을 적용하니 

디바이스 가능 목록에서  한번 클릭으로 바로 디버깅 시작
모든 디바이스에서 원격제어 가능 
모든 디바이스에서 동일 버전 동일 방법 동일 성능 으로 디버깅이 가능해 졌다
-->

---
layout: default
---

# Chii 원격 디버깅 툴

## 적용 사항 

- 별도작업 없이 늘 작동하는 디버깅 <br> QA / DEV 가 아닌 Production 환경에서는 자동으로 디버깅용 스크립트가 제거

```ts {*|1|6}
  createHtmlPlugin({
    inject: {
      tags: [
        {
          attrs: {
            src: 'https://dev-remote-inspector.wavve.com/target.js',
            type: 'text/javascript',
          },
          injectTo: 'head',
          tag: 'script',
        }...
```
<!-- vite 설정에서 Production 빌드가 아니라면 html 내용 추가 하는 플러그인 작성 -->
---
layout: default
---

# Chii 원격 디버깅 툴

#### 디버깅 방법

<img src="/images/page-11-img.png" />

<!--
디버깅 가능한 디바이스 목록이 페이지에가서
inspect 를 클릭하면
-->

---
layout: default
---

# Chii 원격 디버깅 툴

#### 디버깅 화면

<img src="/images/page-12-img.png" class="h-85%" />


---
layout: default
---

# Chii 원격 디버깅 툴

#### 디버깅 컨트롤 영상

<SlidevVideo autoplay controls autoreset="slide" class="h-85%">
  <source src="/images/page-13-mov.mp4" type="video/mp4" />
</SlidevVideo>

---
layout: default
---

# Chii 원격 디버깅 툴

## 🎯 적용 결과

| 항목 | 기존 | 개선 후
|------|------|---------|
| 디버깅 설정 시간 | 10-30분 | 10초 |
| 디버깅 디바이스 전환 속도 | 10-30분 | 3초 |
| 디버깅 같은 방법 갯수  | 1 / 10 | 10 / 10 |
| 디버깅 성능 저하 갯수 | 2 / 10 | 0 / 10 |
| 디버깅 가능 디바이스 목록 | X | O |

---
layout: default
---

# Chii 원격 디버깅 툴

## 추가 개선 사항

- IOS, Android webview 적용
- Chii 버전 자동 업데이트 기능

---
layout: default
---

# Cursor CLI x GitLab CI/CD

## 🤔 왜 Cursor CLI ?

Model 이 `auto` 면 <span v-mark.underline.orange> 무제한 </span>  사용 가능

<v-click>
다만 응답 <strong>퀄리티</strong>가 각 Job 마다 조금식 다른 문제가 있다 <span class="font-size-10">🤦</span>
</v-click>

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 커서에게 프롬프트 전달
````md magic-move {lines: true}

```yaml {*}
# GitLab CI/CD 파이프라인에서 자동 실행
when: merge_request
```

```yaml {4}
# GitLab CI/CD 파이프라인에서 자동 실행
when: merge_request
script:
  - cursor-agent 
```

```yaml {4}
# GitLab CI/CD 파이프라인에서 자동 실행
when: merge_request
script:
  - cursor-agent -p "$(glab mr diff $CI_MERGE_REQUEST_IID)"
```

```yaml {5|6-7}
# GitLab CI/CD 파이프라인에서 자동 실행
when: merge_request
script:
  - cursor-agent -p "diff \n\n $(glab mr diff $CI_MERGE_REQUEST_IID)
  \n 요약 하여 `./summary.md` 에 결과 저장
  \n 리뷰 하여 `./review.json` 에 결과 저장
  "
```

````

<!--
실제 프롬프트는 좀더 상세한 프롬프트 이지만 간략하게 보면

머지때 커서 CLI 에 MR diff 내용을 넣고 요약과 리뷰 내용을 각각 summary.md review.json 에 저장

$CI_MERGE_REQUEST_IID 등은 gitlab CI/CD 내장 변수 이거나 직접 변수로 지정한 변수
-->

---

# Cursor CLI x GitLab CI/CD

### 만들어진 내용 MR에 작성
```yaml {2|3-8|9-13}
script:
  - cursor-agent -p ..."
   # MR에 리뷰 작성 
  - |
    safe-glab discussions -t $GITLAB_TOKEN -m $CI_MERGE_REQUEST_IID
     -p $CI_MERGE_REQUEST_PROJECT_ID -h gitlab.wavve.com
     --version-id $CI_MERGE_REQUEST_DIFF_ID
     --content-path ./review.json
  # MR에 요약 작성   
  - |
    safe-glab notes -t $GITLAB_TOKEN -m $CI_MERGE_REQUEST_IID
     -p $CI_MERGE_REQUEST_PROJECT_ID -h gitlab.wavve.com
     --content-path ./summary.md
```

<!--
파일로 저장 하는 이유는 명확하게 늘 같은 동작 메세지 작성 리뷰 작성 명령을 직접 만든 명령어 셋으로  summary.md review.json 파일을 읽어 처리 하기 위해
-->


---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 추가로 프롬프트에 JSON 포맷을 전달

```text
JSON 포맷은 아래 형태로 작성 한다
[
  {
    // {string} (required) review message
    "body": "대상에 대한 리뷰 메세지 1",
    "position": {
      // {string} diff old file path from the "./diff.patch" (required)
      "oldPath": "/path/to/file1.js",
      // {string} diff new file path from the "./diff.patch" (required)
      "newPath": "/path/to/file1.js",
      // {number} review target diff line number" (optional)
      "newLine": 123,
      "oldLine": 123
    }...
```

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 프롬프트 매개변수 길이 문제
````md magic-move {lines: true}

```yml {0|*}
  script:
    - cursor-agent -p "diff \n\n $(glab mr diff $CI_MERGE_REQUEST_IID) ... "
```

```yml
  script:
    - glab mr diff $CI_MERGE_REQUEST_IID > diff.patch
    - cursor-agent -p "diff \n\n $(glab mr diff $CI_MERGE_REQUEST_IID) ... "
```

```yml
  script:
    - glab mr diff $CI_MERGE_REQUEST_IID > diff.patch
    - cursor-agent -p "diff \n\n `./diff.patch` 파일을 읽어서 ... "
```

````

<!--
diff 내용은 상당히 길어 Cursor cli 매개 변수 길이 제한에 걸린다
-->

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 라인 번호를 잘 알려주지 못하는 문제

```text {0|*}
Rules:
- Base on +newStart in the hunk header.
- Initialize currentLine = newStart.
- Scan the hunk body top → bottom:
  - Lines starting with ' ' (context): currentLine += 1
  - Lines starting with '+' (added):   currentLine += 1
  - Lines starting with '-' (removed): no change
- Ignore file headers (---/+++), hunk headers (@@), and "\ No newline..." lines.
- If multiple hunks exist, only calculate within the hunk that contains the target code.
- If not found, return "NOT FOUND".

... 중략
```

<!--
라인 번호 계산 방법을 알려주어 해결
-->

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 그럼에도 불구하고 라인번호를 잘못 적을 경우

<span>post-discussion.ts</span>
```ts {*|0}{at:0}
function postDiscussions () {
  ...
  .catch(retryDiscussionWithFileInfo({...})
}
```
<span>retry-discussion-with-file-info.ts</span>
```ts {*|5}{at:0}
function retryDiscussionWithFileInfo (payload) {
  ...
  return axios.post(..., {
    body: `${payload.body} \n\n 
    [${newPath}${position.newLine ? `_${position.newLine}` : ''}](${lineCodeUrl})`
  })
}
```

<!--
파일 위치는 AI 가 정확히 작성하기 때문에 파일 위치링크를 추가하고 리뷰 작성
-->

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 프롬프트가 너무 길어 yml 파일 가독성 문제

````md magic-move {lines: true}
```yml {0|*}
  script:
    - cursor-agent -p "diff \n\n $(glab mr diff $CI_MERGE_REQUEST_IID) ... 
      ...
      ...
      ...
      ...
      ...
      ...
      ...
      ...
      ...
    "
```

```yml
  script:
    - cursor-agent -p "$(cat summary-cli-rule.md)"
```
````

<!--
프롬프트를 파일에 작성하고 그걸 CLI 프롬프트로 매개변수로 주입
-->

---
layout: default
---

# Cursor CLI x GitLab CI/CD

### 적용된 화면

<div class="overflow-scroll w-full h-full">
  <img src="/images/page-14-img.png" class="w-140% max-w-140%" />
</div>

---
layout: default
---


# Cursor CLI x GitLab CI/CD

## 👮 보안 

- AI는 생각지도 못한 명령을 실행 할 수도 있다
- 토큰에 지정된 Api 사용 권한은 GitLab 에서 할수 있는 대부분 작업이 가능

<!--
API 권한은 만능 권한 mr 삭제, 프로젝트 삭제 등 모든 권한이 다있다
AI 가 치명적인 명령으로 문제를 만들 수 있기때문에 할 수 있는 일에 제약을 두어야 한다
-->

---

# Cursor CLI x GitLab CI/CD

#### Cursor 가 사용할 수 있는 명령을 권한을 제어하여 보안 적용

```json
{
  "permissions": {
    "allow": [
      "Write(summary.md)",
      "Write(./summary.md)",
      "Write(review.json)",
      "Write(./review.json)",
      "Read(diff.txt)",
      "Read(./diff.txt)"
    ],
    "deny": ["Shell(rm)", "Shell(npm)", "Shell(git)", "Shell(ls)", "Shell(glab)"]
  }
}
```
<!--
명시되지 않은 것은 차단
-->

---
layout: default
---

# Cursor CLI x GitLab CI/CD

## 📊 적용 결과

| 항목 | 기존 | 개선 후 |
|------|------|---------|
| 리뷰 시간 | 10-30분 | 5분 |
| 리뷰 일관성 | 50% | 80% |
| 버그 발견률 | 50% | 80% |


---
layout: default
---

# Cursor CLI x GitLab CI/CD

## 추가 개선 사항

- **응답 시간** 타임 아웃
- 도커 이미지 최적화
- **AI 결과 에러 검출** 하여 재 요약 / 리뷰 시행되도록 추가

---
class: slidev-layout
---

# 감사합니다

## 질문이 있으시면 언제든 말씀해 주세요

### 연락처
- **이메일**: bichi@wavve.com

### 추가 자료
- **이 슬라이드** <br>
<QrCode value="https://deploy-chronicles.vercel.app" size="200" />