# [any활용] any로 코드와 로직을 일치시킨다

📅 **Date:** 2026-02-04
🏷️ **Tags:** #브레인스토밍 #진정한실력

---

## 1. 💡 What & Why?
> **한 줄 요약:** 조건문을 더 명확하게 작성하기
- **상황:** 
    검색 결과, 문서 제목에 예외 단어가 포함되면 다음 검색 결과를 확인하는 로직을 짜고자 하였음.
    기존 코드에서는 작동은 하지만 논리 구조가 난잡함
    -> 문서 제목에서 금지 단어들이 모두 발견되지 않으면... -> 건너뜀

    수정된 코드에서는 의도하는 로직과 코드의 흐름이 일치함
    -> 금지된 단어가 문서 제목에 하나라도 있으면... -> 건너뜀

## 2. 🔧 How? (Code)
```python
SEARCH_TARGET_EXCEPTION = ("disambiguation", "album") # 검색 예외 단어 설정

# 기존 코드
if not all((search_result_json[1][i].find(ignore_word) == -1 for ignore_word in SEARCH_TARGET_EXCEPTION)):
    continue

# 수정된 코드
if any(ignore_word in name for ignore_word in SEARCH_TARGET_EXCEPTION):
    continue
```

## 3. 🚀 Insight
- 조건문의 조건과 내가 짜고자하는 로직을 일치시키면, 더 간결하고 이해도 쉬운 코드를 만들 수 있다!

## 4. 🔗 Reference
- 