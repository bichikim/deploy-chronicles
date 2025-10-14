---
theme: default
title: 전생 했더니 웹개발팀 취합 배포 작업 개선 한 건에 대하여
background: ./images/page-1-background.png
backgroundSize: right top
mdc: true
---
<style>

</style>

# 어쩌다 보니{style="color:#d69b37;background-color:#4c1e10;border-radius:1rem;padding:.5rem;border:2px #5c2912 solid;outline:3px #38251d solid;width:50%;position:absolute;right:3.5rem;top:3rem;text-align:center;font-size:3.5rem;line-height:4rem;font-weight:900"}

## 웹개발팀 취합 배포 작업 개선한 건에 대하여{style="color:#d69b37;text-shadow: 2px 2px 4px #38251d, 0 0 2px #000;width:60%;word-break:keep-all;font-size:3.5rem;line-height:3.5rem;position:absolute;left:26rem;top:10rem"}

---

# 무엇을 개선 하였나?

- 카나리? (이거 뭐라고 불러야 하지?) 배포 추가
- 원격디버깅
- AI PR 요약 / 리뷰

---

# 여기는 카나리 배포 내용

장점: 
  굉장히 빠른 롤백 (트레픽 제거로 롤백) (이게 되나?)
  이슈시 적은 타력량
  프라이빗 100% 사용환경 테스트

우려 사항:
  api 가 하위 호환이 안되면 카나리 대상이 아닌 접속은 동작오류가 난다 

---

## 여기는 원격디버깅 리뷰

기존문제: 디바이스 마다 디버깅 방법이 다르고 디버깅을 위한 접속 과정이 복잡하고 길며 저사양 디바이스일 경우 디버깅이 안되거나 디바이스 소프트웨어 업그레이드 후에 디버깅이 안되는 경우가 발생

---

### 여기는 AI PR / 리뷰 

AI 명령어 인터페이스 x gitlab cli = 오잉? 

