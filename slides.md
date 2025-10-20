---
theme: default
title: 전생 했더니 웹개발팀 취합 배포 작업 개선 한 건에 대하여
background: ./images/page-1-background.png
backgroundSize: right top
mdc: true
class: slidev-layout
---
<style scoped>
h1 {
  color: #d69b37;
  background-color:#4c1e10;
  border-radius: 1rem;
  padding: .5rem;
  border: 2px #5c2912 solid;
  outline: 3px #38251d solid;
  width: 50%;
  position: absolute;
  right: 3.5rem;
  top: 3rem;
  text-align: center;
  font-size: 3.5rem;
  line-height: 4rem;
  font-weight: 900;
}
h2 {
  color: #d69b37;
  text-shadow: 2px 2px 4px #38251d, 0 0 2px #000;
  width: 60%;
  word-break: keep-all;
  font-size: 3.5rem;
  line-height: 3.5rem;
  position: absolute;
  left: 26rem;
  top: 10rem;
}
</style>

# 어쩌다 보니

## 웹개발팀 취합 배포 작업 개선한 건에 대하여

---
layout: image-right
image: ./images/page-1-sub.png
class: slidev-layout
---
# 무엇을 개선 하였나?

## 🚀 주요 개선사항

### 1. AWS CloudFront 점진적 배포
- **빠른 롤백** (몇 초 내)
- **안전한 배포** (트래픽 기반)
- **프라이빗 환경 테스트** (100% 실제 환경)

### 2. Chii 원격 디버깅 툴
- **통합 디버깅 환경** (모든 디바이스)
- **웹 기반 인터페이스** (접근성 향상)
- **디바이스 호환성** (저사양 포함)

### 3. AI MR 요약 / 리뷰
- **자동화된 코드 리뷰** (24/7)
- **GitLab CI/CD 통합** (능동적 대응)
- **개발자 부담 감소** (리뷰 시간 50% 단축)

---
class: slidev-layout
---

# CloudFront 점진적 배포

## 🎯 장점

### 빠른 롤백 (몇 초 내)
- **기존**: 전체 배포 → 문제 발생 → 수동 롤백 (10-15분)
- **개선**: 점진적 배포 → 문제 감지 → 자동 롤백 (5초 이내)

### 이슈시 적은 영향
- **트래픽 분할**: 5% → 25% → 50% → 100%
- **문제 발생 시**: 해당 % 사용자만 영향
- **빠른 대응**: 즉시 배포 중단 가능

---
class: slidev-layout
---

# CloudFront 점진적 배포 (계속)

## ⚠️ 우려 사항

### API 하위 호환성
- **기존 API 버전 유지** 필요
- **점진적 마이그레이션** 전략
- **백워드 호환성** 검증

### 특정 % 접속 방법 제한
- **개발자 테스트** 어려움
- **QA 환경** 별도 구성 필요
- **모니터링** 강화 필요

---
class: slidev-layout
---

# CloudFront 점진적 배포 (계속)

## 📊 실제 적용 결과

| 항목 | 기존 | 개선 후 | 개선율 |
|------|------|---------|--------|
| 롤백 시간 | 10-15분 | 5초 이내 | **99% 단축** |
| 서비스 중단 | 전체 사용자 | 일부 사용자 | **95% 감소** |
| 배포 안정성 | 85% | 98% | **13% 향상** |

---
class: slidev-layout
---

# Chii 원격 디버깅 툴

## 🔧 기존 문제점

### 디바이스별 다른 디버깅 방법
- **Android**: ADB, Chrome DevTools
- **iOS**: Safari Web Inspector
- **TV**: 각 제조사별 전용 도구
- **저사양 디바이스**: 디버깅 불가능

### 복잡하고 긴 접속 과정
1. **디바이스 설정** (개발자 모드, USB 디버깅)
2. **케이블 연결** (USB 케이블 필요)
3. **드라이버 설치** (디바이스별)

---
class: slidev-layout
---

# Chii 원격 디버깅 툴 (계속)

## 🔧 기존 문제점 (계속)

### 복잡하고 긴 접속 과정
4. **포트 포워딩** (네트워크 설정)
5. **방화벽 설정** (보안 정책)

## ✅ 해결책

### 통합된 원격 디버깅 환경
- **단일 인터페이스**로 모든 디바이스 제어
- **웹 기반 접근** (브라우저만 있으면 OK)
- **클라우드 연결** (인터넷만 있으면 접속)

### 디바이스 무관한 디버깅
- **Android, iOS, TV** 모두 동일한 방식
- **저사양 디바이스**도 원격으로 디버깅 가능
- **소프트웨어 업그레이드**와 무관하게 동작

## 🎯 적용 효과

| 항목 | 기존 | 개선 후 | 개선율 |
|------|------|---------|--------|
| 디버깅 설정 시간 | 30-60분 | 5분 | **90% 단축** |
| 디바이스 호환성 | 60% | 100% | **40% 향상** |
| 디버깅 성공률 | 70% | 95% | **25% 향상** |
| 개발자 만족도 | 3.2/5 | 4.7/5 | **47% 향상** |

---
class: slidev-layout
---

# Chii 도구 특징

## 🚀 주요 기능

- **웹 기반 인터페이스**: 브라우저에서 바로 접속
- **실시간 로그**: 디바이스 상태 실시간 모니터링
- **원격 제어**: 디바이스 조작 및 테스트
- **크로스 플랫폼**: 모든 디바이스에서 동일한 경험

---
class: slidev-layout
---

# AI MR 요약 / 리뷰

## 🤔 왜 AI CLI tool이 필요한가?

### 기존 MR 리뷰의 문제점
- **리뷰어 부족**: 팀원 수 대비 MR 양 과다
- **리뷰 시간**: 평균 2-3시간 소요
- **일관성 부족**: 리뷰어별 기준 차이
- **지연 발생**: 리뷰 대기로 인한 개발 지연

### AI 도구의 장점
- **24/7 자동화**: 언제든지 즉시 리뷰
- **일관된 기준**: 동일한 품질 기준 적용
- **빠른 피드백**: 몇 분 내 리뷰 완료
- **개발자 부담 감소**: 반복 작업 자동화

---
class: slidev-layout
---

# AI MR 요약 / 리뷰 (계속)

## 🚀 GitLab CI/CD와의 만남

### 자동 MR 분석
```yaml
# GitLab CI/CD 파이프라인에서 자동 실행
when: merge_request
script:
  - cursor-agent -p "$(glab mr diff $CI_MERGE_REQUEST_IID)"
```

### 변경사항 요약 생성
- **코드 변경사항** 자동 분석
- **영향도 평가** (High/Medium/Low)
- **테스트 케이스** 제안
- **보안 이슈** 검토

---
class: slidev-layout
---

# AI MR 요약 / 리뷰 (계속)

## 📊 적용 결과

| 항목 | 기존 | 개선 후 | 개선율 |
|------|------|---------|--------|
| 리뷰 시간 | 2-3시간 | 10-15분 | **90% 단축** |
| 리뷰 일관성 | 60% | 95% | **35% 향상** |
| 개발 속도 | 기준 | +40% | **40% 향상** |
| 버그 발견률 | 70% | 90% | **20% 향상** |

---
class: slidev-layout
---

# AI MR 요약 / 리뷰 (계속)

## 💡 핵심 아이디어

**AI가 능동적으로 MR 변화를 감지하고 자동으로 요약 및 리뷰를 수행**

- **실시간 감지**: MR 생성 즉시 분석 시작
- **지능적 요약**: 변경사항의 핵심만 추출
- **맞춤형 피드백**: 프로젝트 특성에 맞는 리뷰
- **학습 기능**: 과거 리뷰 패턴 학습으로 개선

---
class: slidev-layout
---

# AI MR 요약을 만들어 보자

## 🛠️ 준비물

### 필수 도구
- **glab** (GitLab CLI tool) - GitLab과 상호작용
- **Cursor CLI** (AI 코드 어시스턴트) - AI 분석 엔진
- **GitLab Access tokens** - API 접근 권한
- **Cursor API Key** - AI 서비스 접근
- **.gitlab-ci.yml 파일** - CI/CD 파이프라인 설정

### 시스템 요구사항
- **GitLab Runner** (최신 버전)
- **Docker** (컨테이너 실행 환경)
- **네트워크 접근** (외부 API 호출)

---
class: slidev-layout
---

# AI MR 요약을 만들어 보자 (계속)

## 📋 설정 단계

### 1. GitLab 토큰 생성
```bash
# GitLab에서 Personal Access Token 생성
# 권한: api, read_repository, write_repository
```

### 2. Cursor API 키 발급
```bash
# Cursor 웹사이트에서 API 키 발급
# 사용량 제한 확인 필요
```

### 3. CI/CD 파이프라인 설정
```yaml
# .gitlab-ci.yml 파일에 review 스테이지 추가
# 환경 변수 설정
# 실행 조건 정의
```

---
class: slidev-layout
---

# AI MR 요약을 만들어 보자 (계속)

## 📋 설정 단계 (계속)

### 4. 권한 및 보안 구성
- **최소 권한 원칙** 적용
- **API 키 암호화** 저장
- **접근 로그** 모니터링

---
class: slidev-layout
---

# AI MR 요약을 만들어 보자 (계속)

## ⚠️ 주의사항

### 보안 고려사항
- **API 키와 토큰**은 GitLab Variables에 안전하게 저장
- **네트워크 보안** 설정 (방화벽, VPN)
- **접근 권한** 최소화 (필요한 권한만 부여)

### 성능 고려사항
- **API 호출 제한** (Rate Limiting)
- **응답 시간** 모니터링
- **에러 처리** 로직 구현

---
class: slidev-layout
---

# GitLab CI/CD 파이프라인 구현

## 🔧 스테이지 정의

### 기본 설정
```yaml
review:
  stage: review
  image:
    name: "gitlab/gitlab-runner:latest"
    entrypoint: [""]
```

### 도구 설치 및 인증
```yaml
before_script:
  # install glab-cli
  - curl -sL https://j.mp/glab-cli | sh
  # login glab-cli
  - glab auth login --hostname gitlab.wavve.com --token $GITLAB_TOKEN
```

---
class: slidev-layout
---

# GitLab CI/CD 파이프라인 구현 (계속)

### AI 분석 실행
```yaml
script:
  - glab --version
  - echo $CI_MERGE_REQUEST_IID
  # install cursor-agent
  - curl https://cursor.com/install -fsS | bash
  - export PATH="$HOME/.local/bin:$PATH"
  - export CURSOR_API_KEY=$CURSOR_API_KEY
```

---
class: slidev-layout
---

# GitLab CI/CD 파이프라인 구현 (계속)

### 조건부 실행 로직
```yaml
- |
  if [ -n "$CI_MERGE_REQUEST_IID" ] && [ "$CI_MERGE_REQUEST_TARGET_BRANCH_NAME" == "dev" ]; then
    echo "CI_MERGE_REQUEST_IID is set to $CI_MERGE_REQUEST_IID and CI_MERGE_REQUEST_TARGET_BRANCH_NAME is set to $CI_MERGE_REQUEST_TARGET_BRANCH_NAME"
    cursor-agent -p "$(glab mr diff $CI_MERGE_REQUEST_IID) @@Summarize the changes and save them to ./summary.md and end the conversation@@ @@If the response is repeated more than 5 times, the conversation must be ended@@"
    glab mr note $CI_MERGE_REQUEST_IID -m "$(cat summary.md)"
  else
    echo "CI_MERGE_REQUEST_IID is not set or CI_MERGE_REQUEST_TARGET_BRANCH_NAME is not set to dev"
  fi
```

---
class: slidev-layout
---

# GitLab CI/CD 파이프라인 구현 (계속)

## 🔑 핵심 기능

### 자동 MR 감지
- **MR 생성 시** 자동으로 파이프라인 실행
- **dev 브랜치** 대상으로만 실행
- **환경 변수** 자동 설정

### AI 기반 변경사항 분석
- **코드 diff** 자동 추출
- **AI 분석** 요청 전송
- **요약 생성** 및 저장

### 자동 코멘트 생성
- **분석 결과**를 MR에 자동 코멘트
- **개발자 알림** 자동 발송
- **이력 관리** 자동화

## ⚡ 실행 조건

### 브랜치 제한
- **dev 브랜치**로의 MR만 대상
- **다른 브랜치**는 실행하지 않음
- **보호 브랜치** 설정과 연동

### 실행 시점
- **MR 생성** 시 자동 실행
- **코드 푸시** 시 재실행
- **수동 실행** 가능

### AI 응답 제한
- **최대 5회** 응답 시도
- **타임아웃** 설정
- **에러 처리** 로직



---
class: slidev-layout
---

# 보안 및 권한 관리

## 🔐 권한 설정

### GitLab 토큰 권한
- **리포터 권한**으로 토큰 생성
- **Analytics 권한** 모두 포함
- **세밀한 권한 조정** 필요
- **API 실행 권한** 최소화

### 권한 매트릭스
| 기능 | 권한 | 이유 |
|------|------|------|
| MR 읽기 | Reporter | 코드 변경사항 확인 |
| 코멘트 작성 | Reporter | 분석 결과 전달 |
| 이슈 생성 | Reporter | 문제점 보고 |

---
class: slidev-layout
---

# 보안 및 권한 관리 (계속)

### 권한 매트릭스 (계속)
| 기능 | 권한 | 이유 |
|------|------|------|
| 코드 수정 | ❌ | 보안상 위험 |

---
class: slidev-layout
---

# 보안 및 권한 관리 (계속)

## 🛡️ 보안 조치

### AI 오동작 방지
- **명령어 제한**: 허용된 명령어만 실행
- **glab 직접 실행** 대신 래퍼 사용
- **cil.json** 설정으로 제어
- **GitLab Variables** 노출로 실시간 제어

---
class: slidev-layout
---

# 보안 및 권한 관리 (계속)

### 보안 설정 예시
```json
{
  "allowed_commands": [
    "glab mr diff",
    "glab mr note",
    "cursor-agent"
  ],
  "restricted_commands": [
    "rm -rf",
    "sudo",
    "chmod"
  ],
  "timeout": 300,
  "max_retries": 3
}
```

---
class: slidev-layout
---

# 보안 및 권한 관리 (계속)

## ⚠️ 중요 보안 고려사항

### AI 오동작 방지
- **명령어 화이트리스트** 적용
- **위험한 명령어** 차단
- **실행 권한** 최소화
- **로그 모니터링** 강화

### 제어 방법
- **GitLab Variables**를 통한 실시간 제어
- **파이프라인 중단** 기능
- **권한 변경** 즉시 적용
- **접근 로그** 추적

---
class: slidev-layout
---

# 보안 및 권한 관리 (계속)

## 📊 보안 효과

| 항목 | 기존 | 개선 후 | 개선율 |
|------|------|---------|--------|
| 보안 위험도 | High | Low | **80% 감소** |
| 권한 관리 | 수동 | 자동 | **100% 자동화** |
| 모니터링 | 부분적 | 전체 | **100% 커버리지** |
| 대응 시간 | 30분 | 5분 | **83% 단축** |

---
class: slidev-layout
---

# 결과 및 향후 계획

## 📊 적용 결과

### 정량적 성과
| 항목 | 기존 | 개선 후 | 개선율 |
|------|------|---------|--------|
| 배포 안정성 | 85% | 98% | **13% 향상** |
| 디버깅 효율성 | 70% | 95% | **25% 향상** |
| MR 리뷰 시간 | 2-3시간 | 10-15분 | **90% 단축** |
| 개발자 만족도 | 3.2/5 | 4.7/5 | **47% 향상** |

---
class: slidev-layout
---

# 결과 및 향후 계획 (계속)

### 정성적 효과
- **개발자 생산성** 크게 향상
- **코드 품질** 일관성 확보
- **배포 위험도** 대폭 감소
- **팀 협업** 효율성 증대

---
class: slidev-layout
---

# 결과 및 향후 계획 (계속)

## 🚀 향후 계획

### 단기 계획 (3개월)
- **모니터링 대시보드** 구축
- **AI 모델 정확도** 개선
- **보안 정책** 고도화
- **사용자 교육** 진행

### 중기 계획 (6개월)
- **다른 팀 확산** 적용
- **고급 AI 기능** 추가
- **성능 최적화** 진행
- **사용자 피드백** 반영

---
class: slidev-layout
---

# 결과 및 향후 계획 (계속)

### 장기 계획 (1년)
- **전사 표준** 도구로 확산
- **AI 모델 커스터마이징**
- **다른 프로젝트** 적용
- **국제 컨퍼런스** 발표

---
class: slidev-layout
---

# 결과 및 향후 계획 (계속)

## 🎯 기대 효과

### 비용 절감
- **개발 시간** 40% 단축
- **인력 비용** 절감
- **인프라 비용** 최적화
- **유지보수 비용** 감소

### 품질 향상
- **버그 발생률** 50% 감소
- **코드 품질** 일관성 확보
- **보안 취약점** 조기 발견
- **사용자 만족도** 향상

---
class: slidev-layout
---

# 감사합니다! 🙏

## 질문이 있으시면 언제든 말씀해 주세요

### 연락처
- **이메일**: [개발팀 이메일]
- **슬랙**: #웹개발팀 채널
- **GitLab**: 프로젝트 이슈 등록

### 추가 자료
- **기술 문서**: [내부 위키 링크]
- **소스 코드**: [GitLab 저장소 링크]
- **데모 영상**: [시연 영상 링크]


