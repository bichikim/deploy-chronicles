# AI MR 리뷰 자동화 프로젝트 작업 히스토리

## 🎯 프로젝트 배경
- **제안**: 팀원이 [CodeRabbit.ai](https://www.coderabbit.ai/) 같은 AI MR 리뷰 서비스 도입 제안
- **판단**: AI CLI tool로 충분히 구현 가능하다고 판단하여 자체 개발 결정

---

## 📋 개발 단계별 진행 과정

### 1단계: 기본 MR 요약 기능 구현
**목표**: GitLab MR에 자동으로 변경사항 요약 메시지 전송

**구현 과정**:
- GitLab MR 메시지 전송 명령어 가능 여부 확인 ✅
- `.gitlab.yml` 파이프라인 구성
- MR diff를 AI CLI tool 프롬프트에 직접 전달하여 요약 생성
- **핵심 설계**: 
  - 요약 내용을 `summary.md` 파일로 저장
  - **메시지 전송은 별도로 glab 명령어 직접 작성하여 실행**

### 2단계: 기술적 제약사항 해결
**문제**: MR diff가 너무 길면 프롬프트 아규먼트 길이 제한에 걸림

**해결책**:
- diff를 `diff.patch` 파일로 추출
- 프롬프트에서 `diff.patch` 파일을 읽도록 변경

### 3단계: 코드 리뷰 기능 추가
**목표**: 각 변경사항에 대한 상세한 코드 리뷰 자동 생성

**구현 과정**:
- `diff.patch` 파일을 읽어서 AI가 리뷰 생성
- 리뷰 결과를 `review.json` 배열 형태로 저장
- **기술적 도전**: GitLab 리뷰 API는 있지만 glab 명령어에는 없음
- **해결**: 직접 만든 명령어로 `review.json`을 순차적으로 읽어 MR 리뷰 작성

### 4단계: 성능 최적화
**개선사항**: 
- AI CLI tool 명령을 두 번 실행할 필요 없음
- 요약과 리뷰를 한 프롬프트에 통합
- `summary.md`와 `review.json` 동시 생성

### 5단계: 오류 처리 및 안정성 개선
**발견된 문제**:
- 리뷰 파일 위치가 틀리면 리뷰 작성 실패 또는 렌더링 오류 발생

**해결 과정**:
1. `diff.patch` 파일을 읽고 정확한 실제 파일 위치의 라인 계산 방법을 프롬프트에 추가
2. 여전히 리뷰 작성 실패하는 경우 발생
3. **최종 해결책**: 라인 번호 오류 시 파일명과 해당 파일 링크를 포함한 대체 리뷰 생성하도록 명령어 수정

---

## 🛠️ 사용된 기술 스택
- **GitLab CI/CD** 파이프라인
- **glab** (GitLab CLI)
- **AI CLI tool** (Cursor Agent)
- **GitLab API** 직접 호출
- **diff.patch** 파일 처리
- **Node.js** (safe-glab 커스텀 CLI)
- **NVM** (Node.js 버전 관리)

## 🔧 실제 구현 세부사항

### GitLab CI/CD 파이프라인 구성
```yaml
review:
  image: "gitlab/gitlab-runner:latest"
  before_script:
    # Node.js 22 설치 및 설정
    # glab-cli 설치 및 GitLab 인증
    # safe-glab 커스텀 CLI 빌드
    # cursor-agent 설치 및 API 키 설정
  script:
    # MR diff를 diff.patch로 추출
    # cursor-agent로 요약 및 리뷰 생성
    # safe-glab으로 GitLab에 메시지 전송
  rules:
    # dev 브랜치로의 MR만 실행
```

### 핵심 명령어들
- **diff 추출**: `glab mr diff $CI_MERGE_REQUEST_IID > diff.patch`
- **AI 분석**: `cursor-agent -p "$(cat summary-cli-rule.md)"`
- **요약 전송**: `node ./packages/safe-glab/dist/index.mjs notes ...`
- **리뷰 전송**: `node ./packages/safe-glab/dist/index.mjs discussions ...`

### 커스텀 safe-glab CLI
- **목적**: GitLab API 직접 호출을 위한 안전한 래퍼
- **기능**: MR 노트 및 디스커션 작성
- **보안**: 제한된 권한으로 안전한 API 호출

## 📊 최종 결과
- ✅ MR 요약 자동화 완성
- ✅ 코드 리뷰 자동화 완성  
- ✅ GitLab CI/CD 통합 완료
- ✅ 오류 처리 로직 완비
- ✅ **개인 프로젝트**로 완전 구현 및 테스트 완료 