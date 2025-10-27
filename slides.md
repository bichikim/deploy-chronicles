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

<div class="w-full flex justify-end items-end gap-5">
  <span class="font-size-6">이 프레젠테이션 문서 주소 --></span>
  <QrCode value="https://deploy-chronicles.vercel.app" size="240" />
</div>

<!--
안녕 하세요 
웨이브 웹개발팀 김비치 입니다

이 발표 문서는 웹페이지로 서비스 되고 있습니다 
qacode 를 통해 이 프리젠테이션 내용을 보실수 있습니다 

지난 1년동안 개발업무를 하면서 배포에 개선할 점이들이 보였고 그중 일부 개선한 부분을 발표하겠습니다
-->

---
layout: cover
---

# 배포 프로세스 효율  문제

햄뽂 할 수 가 없다

<img src="/images/page-2-1-img.png" class="absolute w-350px bottom-20px right-50px rd-5" />

<!--
저는 대부분 업무에 개선의 여지가 있다고 생각합니다 

그 중 배포 과정에서 "배포 후 위험도 관리 / 디버깅 / 리뷰" 에 개선이 필요하다고 생각 합니다 

한번이라도 행복해 보고 싶었습니다 :) 

-->

---
layout: image-right
image: /images/page-2-img.png
backgroundSize: contain
---

# 🚀 배포 위험도 관리
- **QA vs Production** <br> 드물게 미묘한 환경 차이로 QA에서 발견 못한 이슈
- **전체 사용자 영향** <br> 이슈 발생 시 모든 고객에게 100% 적용
- **롤백 지연** <br> 더 빠른 롤백 시간으로 피해 최소화 필요

<span v-mark.underline.orange class="absolute bottom-400px right-250px">ㅤㅤㅤㅤ</span>
<span v-mark.underline.orange class="absolute bottom-190px right-180px">ㅤㅤㅤㅤ</span>


<!-- 
저는 배포 후 위험도를 개선하고 싶었습니다 

기존에는

QA 과 Production 을 최대한 비슷한 환경을 재현 했지만 미묘한 환경 차이로 QA에서 발견 못한 이슈가 있었고 

프로덕트 배포 후 이슈 발생시 영향받는 사용자가 100% 인원이라 이슈시 영향도가 컸습니다

또한 이슈 발생시 롤백시간이 1-2 분 정도 걸렸고 이런 문제를 개선 하고 싶었습니다

오른쪽 이미지는 슬랙으로 보는 롤백 시간을 유추 할 수 있는 메세지 입니다

1:02 에서 최종 메세지 적은 시간은 1:05분 메세지 적는 시간 포함 3분 걸렸네요 휴먼치고 상당히 빨랐네요

-->

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

# 🚀 AWS CloudFront 점진적 배포 적용
- 트래픽 전환으로 **빠른 롤백** 몇 초 내
- 가중치 % 기반 / 헤더 기반 으로 **이슈시 적은 영향**
- 프로덕트 환경에서 최소 리스크로 테스트 가능

<!-- 
그런데 마침 저희가 사용하는 프론엔드서비스용  AWS CloudFront 에 최근 점진적 배포 기능을 추가되었고

이 것을 사용하여 배포 후 위험도 관리를 달성 할 수 있다고 판단하여 적용 하였습니다

AWS CloudFront 는 트레픽 을 가중치 기반 또는 헤더 기반으로 고객 트레픽을 production 과 production staging 으로 변경 하 수 있습니다 

트래픽 전환으로 기존 production 으로 수초내 롤백 가능

트래픽 기반 / 헤더 기반 으로 **이슈시 적은 영향** 을 고객에게 미치며 

헤더 기반으로 프로덕트 환경에서 최소 리스크로 테스트 배포도 가능 하였습니다
-->

---
image: ./images/page-10-img1.png
---

# 🚀 CloudFront 점진적 배포

#### 기존

<div class="h-90% overflow-hidden">
  <img src="/images/page-10-img1.png" class="h-full scale-120% origin-[10%_75%]" />
</div>

<!--
기존은 

기존에는 GitLab 에서 버킷에 소스코드가 배보 (1) 되고 클라이언트가 CloudFront 를 통해 소스코드를 가져갑니다
-->

---
layout: default
---

# 🚀 CloudFront 점진적 배포

#### 변경 후

<div class="h-90% overflow-hidden">
  <img src="/images/page-10-img2.png" class="h-full scale-120% origin-[0%_55%]" />
</div>

<!--
점진적 배포 적용 후

 GitLab 에서 가중치 % 기반 또는 헤더 기반 새 소스를 올리는 (1) 버켓과 실 프로덕트 새 소스코드를 올리는 (3) 버켓이 있고
 
 가중치 % 기반 또는 헤더 기반에 따라 클라이언트를 (2) 로 보내거나 (4) 로 보내서 점진적 배포가 적용됩나다
-->

---
title: CloudFront 점진적 배포
layout: default
---

# ⚠️ 우려 사항

### API 하위 호환성
- **기존 API 버전 정상 작동 유지** 필요

### 특정 % 접속 방법 제한
- **개발자 테스트** 어려움 <br> 헤더 기반으로 설정 변경해서 확인

### 세션 유지 길이
- 세션 만료로 오작동이 될 가능성 <br> % 기반 접속일 경우 세션 유지기간 300~3600초 (1시간)


<!--
적용 후 추가적으로 해결해야 하거나 고려해야할 상황이 있었습니다 

헤더기반 또는 가중치 기반 production staging 후에 최종 배포 될때 까지  기존 API 버전 정상 작동 유지를 신경 써야 했습니다

가중치 % 기반으로 배포한 경우에 이슈 발생한 경우 헤더 기반으로 변환하야지만 반드시 가중치 기반을 헤더기반으로 변경해야 production staging 배포된 버전으로 접속이 확정 적으로 가능 하다는 제한 사항이 있었습니다

가중치 기반은 production staging 배포된 버전 사용자로 지정된 고객의 세션 유지 시간이 최대 1시간이라 세션 만료 후 고객이 이전 production 리소스를 가져와서 오작동 할 가능 성이 있습니다
-->



---
layout: image-right
image: ./images/page-3-img.png
backgroundSize: contain
---

# 🔧 디버깅 환경의 복잡성
- **디바이스별 다른 방법** <br> IVI, TV 디바이스마다 제조사/버전별 다른 디버깅
- **준비 시간 과다** <br> 디버깅 설정에 10-30분 소요
- **저사양 디바이스 한계** <br> 디버깅 중 속도저하 및 프리징 발생

<span v-mark.underline.orange class="absolute bottom-85px right-430px">ㅤㅤㅤㅤ</span>

<!--
각 디바이스 종류 제조사 버전별 디버깅 방법이 모두 달라 매번 디버깅 문서를 다시 봐야 했습니다
그리고 방법이 다양 하다보니 여러 디바이스를 전환하며 디버깅 할때 상당한 시간을 소요하였습니다

디버깅 과정도 꾀 길어 최종 디버깅 하기 까지 10-30분 정도 소요 되었습니다

저사양 디바이스는 디버깅 중에 앱의 속도 저하 및 디버깅 툴의 프리징이 발생 했습니다

오른쪽 이미지는 삼성 타이젠 TV 만 하더라고 디버깅 하는 방법을 적은 문서로 215 줄의 방법 설명이 되어있습니다 꾀 복장하죠 특히 삼성 디버깅 연결은 오류가 나면 그냥 종료되고 이유도 안알려 줍니다
-->

---
layout: image-right
image: ./images/page-6-img.png
backgroundSize: contain
---

<style scoped>
  .slidev-page > div {
    overflow: visible;
    white-space: nowrap;
  }
</style>

# 🐛 Chii 원격 디버깅 툴 적용

## 주요 기능 및 효과

- **디바이스 전환** <br> 디바이스 목록 페이지에서 디버깅 <span v-mark.underline.orange>바로 접속 및 전환</span>
- **원격 제어** <br> 디버깅에서 <span v-mark.underline.orange>디바이스 조작 및 테스트</span>
- **같은 환경** <br> 브라우저 개발자 도구와 <span v-mark.underline.orange>같은 디버깅 방법</span>
- **크로스 플랫폼** <br> 모든 디바이스에서 <span v-mark.underline.orange>동일한 최신 버전 디버깅 경험</span>

<!--
Chii 이라는 원격 디버깅 툴을 모든 디바이스에 적용 했습니다

오른쪽 이미지는 저장소에 실제 있는 이미지 이며 저의 취향을 반영 하는 이미지는 아닙니다

이 툴의 주요 기능으로 (여기서 스페이스키로 줄 표시 불러야됨)

이 툴이 적용된 작동 중인 디바이스 목록을 표시해주고 

브라우저에서 개발자 디버깅 툴과 같이 조작 및 변경 테스트 할 수 있고

모든 디바이에서 같은 모양 같은 기능으로 테스트 가능 합니다
-->

---
layout: default
---

# Chii 원격 디버깅 툴

## 적용 방법

- QA / DEV 가 아닌 Production 환경에서는 자동으로 디버깅용 스크립트가 제거

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
<!-- 

적용 방법은 간단합니다 저희가 올린 chii 서비스를 하는 주소의 스크립트를 주입하여 스크립트가 실행되도록 하면 됩니다

저는 vite 설정에서 Production 빌드가 아니라면 html 본문에 스크립트를 내용 추가 하는 플러그인 작성하여 적용 하였습니다

-->
---
layout: default
---

# Chii 디버깅 방법

<img src="/images/page-11-img.png" />

<!--
디버깅 시작은 간단 합니다 

디버깅 가능한 디바이스 목록이 페이지에가서

inspect 를 클릭하면
-->

---
layout: default
---

# Chii 디버깅 화면

<img src="/images/page-12-img.png" class="h-85%" />



<!--
친숙한 inspect 화면이 나옵니다 그리고 디버깅 하면 됩니다
-->

---
layout: default
---

# Chii 디버깅 컨트롤 영상

<SlidevVideo autoplay controls autoreset="slide" class="h-85%">
  <source src="/images/page-13-mov.mp4" type="video/mp4" />
</SlidevVideo>

<!--
디버깅 영상을 보겠습니다 엘리먼트 삭제 페이지 새로 고침 등 기존 브라우저 개발자 툴에서 할 수 있는 대부분 작업이 가능 합니다
-->

---
layout: default
---

# Chii 원격 디버깅 툴

## 추가 개선 사항

- IOS, Android webview 적용
- Chii 버전 자동 업데이트 기능

<!--
지금은 IVI LG webos Samsung tizen 에만 디버깅을 적용 했지만 추후 
IOS, Android webview 에도 적용할 예정 입니다

지금은 Chii 버전이 서비스 중인 Chii 가 다시 배포 하기 전까지는 업데이트가 안되는데 
주기적으로 버전 확인을 해서  Chii 버전 자동 업데이트 기능을 추가할 예정 입니다
-->

---
layout: image-right
image: ./images/page-4-img.png
backgroundSize: contain
---

# 📝 코드 리뷰 비효율성
- **리뷰 시간 과다**: GitLab MR 리뷰에 수십분 소요
- **누락 발생**: 리뷰에서 체크 못한 부분들 빈번
- **일관성 부족**: 리뷰어별 기준 차이

<span v-mark.underline.orange class="absolute bottom-57px right-270px">ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ</span>

<!-- 
저희 팀은 dev 브랜치에 합칠때 MR 을 하고 그때 코드 리뷰를 권장 하는데요 

리뷰 때 코드를 파악하는데 꾀 소요되고

리뷰를 해야 될 부분을 누락하기도 하고 

리뷰 일관성도 부족하고 오른쪽 이미지는 제가 리뷰를 진행했는데요 잘 보지도 않고 리뷰를 했네요

그래서 개선이 필요했습니다 AI 도움이 필요 했습니다
-->

---
layout: image-right
image: ./images/page-7-img.png
backgroundSize: 26em 26em
---

<style scoped>
  .slidev-page > div {
    overflow: visible;
    white-space: nowrap;
  }
</style>

# 🤖 Cursor CLI x GitLab CI/CD

## 개선 목표

- dev 브랜치 MR 에 의한 **자동화된 코드 요약 / 리뷰**
- **요약을 MR 메세지로 작성**
- 리뷰 **코드의 위치**를 표기하고 **MR 리뷰 작성**

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

<!-- 
리뷰 개선 목표는 다음과 같습니다 

AI 가 dev 브랜치 MR 에 반응해서 자도으로 변경된 코드를 요약하고 리뷰를 해줬으면 했습니다

저는 Giblab cli 와 오래동안 이용해 오던 Cursor 의 CLI tool 를 사용하면 구현 가능 할 것 같았습니다

오른쪽 그림은 MR 리퀘스트에 맞춰 Gitlab CI/CD 로 메세지를 작성가능 한지 확인한 화면 입니다

-->

---
layout: default
---

# 🤖 Cursor CLI x GitLab CI/CD

## 그런데 🤔 왜 Cursor CLI ?

Model 이 `auto` 면 <span v-mark.underline.orange> 무제한 </span>  사용 가능

<v-click>
다만 응답 <strong>퀄리티</strong>가 각 Job 마다 조금식 다른 문제가 있다 <span class="font-size-10">🤦</span>
</v-click>

<!--
제가 오래 쓴거 말고 중요한 이유로 model 이 auto 로 지정하면 무제한 사용 가능 한 이유가 있습니다

다만 모델이 계속 변함으로 쿨레티가 각 job 요약 마다 조금식 다른 문제가 있지만 90% 이상 도움 될만한 요약 및 리뷰를 해줬습니다
-->

---
layout: default
---

# 🤖 gitlab.yml Job 구현 작업

### 커서에게 프롬프트 전달

.gitalb-ci.yml
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
실제 프롬프트는 표시된 내용보다 좀더 상세한 프롬프트 이지만 간략하게 보면

머지때 커서 CLI 에 

$CI_MERGE_REQUEST_IID 로 가져온 mr id 를 넣어 glab gitlab Cli tool 로
 
 MR diff 내용 가져와 프롬프트로 넣고 요약과 리뷰 내용을 각각 summary.md review.json 에 저장
-->

---

#  🤖 만들어진 내용 MR에 작성 스크립트 추가
```yaml {*|2|3-8|9-13}
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

명확하게 늘  리뷰 작성 명령을 처리하기 위해 summary.md review.json 로 파일을 저장한 후 

직접 제작한 gitlab cli tool 로 메세지를 작성 하도록 스크립트를 추가 했습니다 

AI 직접 명령을 실행하게 하면 드문 확율로 명령을 잘못사용하거나 명령을 실행 안하는 문제가 있었습니다
-->


---
layout: default
---

# 🤖 추가로 프롬프트에 JSON 포맷을 전달

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
<!--
review.json 같은 경우엔 json 형식도 프롬프트로 알려주었습니다
-->
---
layout: default
---

# 🤖 프롬프트 매개변수 길이 문제 발생
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
그런데 
diff 내용은 상당히 길어 Cursor cli 매개 변수 길이 제한에 걸렸씁니다 그래서 diff 내용을 diff.patch 파일로 저장하고 그 diff.patch 파일을 AI 가 읽도록 프롬프트를 바꿨습니다
-->

---
layout: default
---

# 🤖 라인 번호를 잘 알려주지 못하는 문제

```text
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
또 AI 요약과 리뷰를 사용하다보니 라인번호를 잘못 알고 json 파일을 만드는 문제가 있어 diff.patch 파일 내용을 보고 라인번호를 계산하는 방법을 프롬프트로 알려주었습니다 
라인 번호 계산 방법을 알려주어 해결
-->

---
layout: default
---

#  🤖 그럼에도 불구하고 라인번호를 잘못 적을 경우

<span>post-discussion.ts</span>
```ts {*|0}{at:0}
function postDiscussions () { ...
  .catch(retryDiscussionWithFileInfo({...})
}
```
<span>retry-discussion-with-file-info.ts</span>
```ts {*|4}{at:0}
function retryDiscussionWithFileInfo (payload) { ...
  return axios.post(..., {
    body: `${payload.body} \n\n 
    [${newPath}${position.newLine ? `_${position.newLine}` : ''}](${lineCodeUrl})`
  })
}
```

<!--
그럼에도 불구하고 라인번호를 잘못 작성하는 경우가 간혹 있어서 그럴경우 
리뷰내용에 파일 위치링크를 추가하고 리뷰 작성 하는 동작이 되도록 직접 만든 gitlab cli 툴을 업그레이드 하였습니다
-->

---
layout: default
---

# 🤖 프롬프트가 너무 길어 yml 파일 가독성 문제

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
이러한 내용들을 프롬프트로 추가하다보니 프롬프트가 잔뜩 들어간 .gitlab.cli 파일이 되어 버렸고 가독성을 위해 
summary-cli-rule.md 파일에 프롬프트를 작성하고 그걸 프롬프트로 사용하도록 스크립트를 변경 하였습니다
-->

---
layout: default
---

# 🤖적용된 화면

<div class="overflow-scroll w-full h-full">
  <img src="/images/page-14-img.png" class="w-140% max-w-140%" />
</div>

---
layout: default
---

<!--
그래서 최종 결과로 AI 가 dev MR 요청에 반응하여 변경 점을 요약하고 변경 점에 대한 리뷰도 작성하게 되었습니다
-->

# 🤖 AI 👮 보안 

- AI는 생각지도 못한 명령을 실행 할 수도 있다
- 토큰에 지정된 Api 사용 권한은 GitLab 에서 할수 있는 대부분 작업이 가능

<img v-click src="/images/page-15-img.png" class="absolute w-250px left-65% top-20%" />

<!--
API 권한은 만능 권한 mr 삭제, 프로젝트 삭제 등 모든 권한이 다있습니다 그리고 그 권한을 AI에게 주면 생각지도 못하는 동작을 할 수도 있습니다
그래서 AI 할 수 있는 일에 제약을 두어야 했습니다
-->

---

# 🤖 Cursor 가 사용할 수 있는 명령을 권한을 제어하여 보안 적용

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
Cursor cli tool 에는 할 수 있는 것과 없는 명령을 적는 json 파일이 있고 할 수 있는 명령과 아닌 명령을 추가 하였습니다 대부분 하지 못하도록 설정 했습니다 

만약 명시되지 않은 룰은 안되는 것이 기본 값입니다  
-->

---
layout: default
---

# 🤖 추가 개선 사항

- **응답 시간** 타임 아웃
- 도커 이미지 최적화
- **AI 결과 에러 검출** 하여 재 요약 / 리뷰 시행되도록 추가
- MR 이 갱신되도 요약을 추가로 새로 만드는 것이 아니라 기존 요약 내용을 수정 하는 것으로 작동


<!--
추후 추가로 개선 하고 싶은 내용이 있습니다
아직 격지는 않았지만 응답시간이 상당히 길어길 경우 타임아웃시키는 스크립트가 추가되어야 될 것같습니다 
AI 응답이 최종적으로 원하는 내용을 작성하는 것이 아닐경우 재 요약 / 리뷰 요청을 하는 검증 스크립트를 추가하고 싶습니다
MR 이 자주 갱신되면 요약을 계속 새로 만들어 메세지가 상당히 길어지는데 갱신되면 기존 요약과 리뷰를 수정하는 쪽으로 스크립트를 수정하면 좋을 것 같습니다
-->
---
class: slidev-layout
---

# 감사합니다

## 질문이 있으시면 언제든 말씀해 주세요
- **이메일**: bichi@wavve.com

### 퀴즈
- Cursor Cli tool 을 코드 리뷰 툴로 사용한 이유는 무엇 일까요?

### 추가 자료
- **이 슬라이드 링크** <br>
<QrCode value="https://deploy-chronicles.vercel.app" size="200" />
<img src="/images/page-10-1-img.gif" class="absolute right-18% bottom-1% h-210px" />

<!-- 

지금까지 들어주셔서 감사합니다 

추가 질문은 이메일로 질문 주세요 

퀴즈는 ...

다시한번 이 슬라이드 링크 주소 Qrcode 입니다 

혹시 필요하시면 보세요 
-->
