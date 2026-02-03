# [zip()사용하기] 리스트 두 개 이상에서 하나씩 요소를 뽑을 때는 zip()을!

📅 **Date:** 2026-02-04
🏷️ **Tags:** #zip #슬기로운for문생활 #간결화

---

## 1. 💡 What & Why?
> **한 줄 요약:** zip()을 이용하여 길이가 같은 두 리스트에서 값을 깔끔하게 뽑아내자!

- **상황:** 
    기존에는 두 개 이상의 리스트에서 값을 뽑을 경우에, i로 돌려서 각각 뽑거나 enumerate를 사용하였지만
    zip을 이용하여 깔끔하게 추출할 수 있었다!

## 2. 🔧 How? (Code)
```python
# 아쉬운 코드 예시 (i로 각 돌리기)
for idx in range(len(lyrics_type_list)):
    with open(os.path.join(target_directory, lyrics_type_list[idx] + '.txt'), "w", encoding="utf-8") as f:
        f.write("\n".join(lyrics[idx]) + "\n")

# 아쉬운 코드 예시 (enumerate) <- 실제로 내가 짜던 방식인데 이제보면 참 이해안됨
for idx, lyric in enumerate(lyrics):
    with open(os.path.join(target_directory, lyrics_type_list[idx] + '.txt'), "w", encoding="utf-8") as f:
        f.write("\n".join(lyric) + "\n")

# 아름다운 코드
for lyric_type, lyric in zip(lyrics_type_list, lyrics):
    with open(os.path.join(target_directory, lyric_type + '.txt'), "w", encoding="utf-8") as f:
        f.write("\n".join(lyric) + "\n")
```

## 3. 🚀 Insight
- 내가 활용하지 못하는 기능들이 많다, 자만하지 말자.
- zip()은 내가 배웠던 것이지만 써먹지 못했다, 이런 죽은 지식을 줄이자!

## 3-1. 💡 Additional Ideas
- zip을 활용하면, dict의 key: value를 깔끔하게 매칭시킬 수 있다!
```python
# 키-값 쌍으로 묶어서 딕셔너리 생성
lyric_dict = dict(zip(lyrics_type_list, lyrics))
```
- strict 옵션을 주어, 길이가 다를 때 오류를 발생시킬 수 있다 (기본값은 그냥 더 짧은 리스트 기준으로 짤림) (python 3.10 이상)
```python
# 길이가 다르면 에러를 발생시켜 실수를 방지함
for lyric_type, lyric in zip(lyrics_type_list, lyrics, strict=True):
    # ... (생략)
```
오류가 발생한다
```python
Traceback (most recent call last):
  File "...\TIL\ref_test.py", line 4, in <module>
    for char, num in zip(lyrics_type_list, lyrics, strict=True):
                     ~~~^^^^^^^^^^^^^^^^^^^
ValueError: zip() argument 2 is longer than argument 1
```

## 4. 🔗 Reference
- https://docs.python.org/3/library/functions.html#zip
