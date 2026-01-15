# [Git-init] 초기 설정 오류 해결하기

📅 **Date:** 2026-01-15
🏷️ **Tags:** #깃 #초기설정

---

## 1. 💡 What & Why?
> **한 줄 요약:** 레포를 깃허브에 올릴 때 커밋이 없어서 일어나는 문제를 해결함

- **상황:**  'git push'를 입력 -> 'src refspec main does not match any' 에러 발생
- **원인:** 로컬 레포에 **커밋**이 하나도 없어서 보낼 브랜치(main)이 만들어지지 않았음

## 2. 🔧 How? (Code)
```bash
# 0. 이메일과 이름 등록하기
git config --global user.email "myemail@example.com"
git config --global user.name "myusername"

# 0. 깃허브에 레포 연결하기
git remote add origin your_repo_link

# 1. 파일 담고 커밋하기 (브랜치 만들기!)
git add . # 모든 파일을 스테이지에 올림
git commit -m "First Commit"

# 2. 깃허브에 보내기
git push -u origin main

```

## 3. 🚀 Insight
- Git은 빈 커밋은 전송하지 않는다

## 4. 🔗 Reference
- 