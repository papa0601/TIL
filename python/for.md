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
for lyric_type, lyric in zip(lyrics_type_list, lyrics):
    with open(os.path.join(target_directory, lyric_type + '.txt'), "w", encoding="utf-8") as f:
        f.write("\n".join(lyric) + "\n")
```

## 3. 🚀 Insight
- 내가 활용하지 못하는 기능들이 많다, 자만하지 말자.
- zip()은 내가 배웠던 것이지만 써먹지 못했다, 이런 죽은 지식을 줄이자!

## 4. 🔗 Reference
- 