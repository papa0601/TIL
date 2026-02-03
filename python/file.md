# [읽기/쓰기] 파이썬에서 파일을 읽고 쓰는 함수의 사용에 관한 정리

📅 **Date:** 2026-02-04
🏷️ **Tags:** #파일 #읽기 #쓰기

---

## 1. 💡 What & Why?
> **한 줄 요약:** 리스트(iterable)는 ..lines(), 한 덩어리는 read()/write()

- **상황:** 
    read — 파일 전체를 문자열 하나로 읽기 (하나의 str에 중간중간 \n 포함)
    readlines — 파일을 줄단위로 리스트로 읽기 (각 요소 마지막에 \n 포함)
    write — 문자열 하나를 파일에 쓰기
    writelines — 리스트를 파일에 쓰기 (자동 줄바꿈 X)

## 2. 🔧 How? (Code)
```text
<file.txt>
안녕하세요
반갑습니다

```
다음과 같이 사용할 수 있다
```python
with open("file.txt", "r") as f:
    content = f.read()
# content = "안녕하세요\n반갑습니다\n"

with open("file.txt", "r") as f:
    lines = f.readlines()
# lines = ["안녕하세요\n", "반갑습니다\n"]

with open("file.txt", "w") as f:
    f.write("안녕하세요\n반갑습니다\n")

with open("file.txt", "w") as f:
    f.writelines(["안녕하세요\n", "반갑습니다\n"])
```


## 3. 🚀 Insight
- 단일 str에서 writelines()를 사용하면, 글자를 하나하나 적으므로 비효율적이다
```python
# FIXME str은 iterable이라 작동하나, 비효율적이다 
string = "예시 문장입니다, 반갑습니다."
with open("file.txt", "w") as f:
    f.writelines(string)
```

- 한국어 Windows에서는 기본 인코딩이 cp949이므로 문제가 발생할 수 있다.
```python
with open("file.txt", "w", encoding="utf-8") as f: # 인코딩을 명시해야 깨지지 않는 경우가 많다.
    ...
```

## 3-1. 💡 Additional Ideas
- 줄바꿈 문자가 붙어있지 않은 str로 이루어진 리스트를 파일에 쓸 때, 각 요소 끝에 줄바꿈을 넣으려면 다음과 같이 할 수 있다.
```python
# generator 방식을 이용하여 줄바꿈 더하기
f.writelines(l + "\n" for l in mylist)

# 문자열에 join()하는 방식으로 줄바꿈 더하기 (더 깔끔하다)
f.write("\n".join(lyric) + "\n")
```

- 파일에서 한 줄씩 처리하는 것이 가능한 경우, 한 줄씩 순차적으로 읽는것이 메모리 차원에서 효율적이다 (특히 파일이 큰 경우)
```python
# 다만 파일을 통째로 처리하거나, 인덱스를 넘나들기, 또는 여러번 순회하는 경우에는 한 번에 읽어들이는게 낫다.
with open("file.txt", "r") as f:
    for line in f:
        ...
```

## 4. 🔗 Reference
- https://docs.python.org/3/library/functions.html#open