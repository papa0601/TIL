# [bs4-table] beautifulsoap로 크롤링한 사이트에서 table 내용 추출하기

📅 **Date:** 2026-01-22
🏷️ **Tags:** #크롤링 #beautifulsoap # table

---

## 1. 💡 What & Why?
> **한 줄 요약:** 보카로 위키에서 가사 크롤링할 때 table에 자료가 들어있어, 자료 구조를 이해하고 추출함

- **상황:** 
table header (th)에 각 열의 이름이 적혀있음
tr (행) -> td (열) 이 구조로 되어있음

**특이사항**
연습곡 アンテナ39기준으로 Japanese / Romaji로 되어있었는데,
가사 자체가 영어인 부분은 Japanese행에 적히고 Romaji가 비어있어서 처리가 필요했음

## 2. 🔧 How? (Code)
Japanese(일본어)가 헤더에 적힌 테이블을 가사 테이블로 인식해서 가져오기
```python
#TODO 버전이 여러개인 곡의 경우에는 바로 break하지 않고 다른 버전의 가사 테이블을 추가로 찾아야할 수 있음
for table in tables: # tables는 bs4의 .select()로 가져온 테이블들임
    headers = table.select("th") # 헤더 선택
    for header in headers:
        if header.text.find("Japanese") != -1: # 헤더에 Japanese라는 텍스트가 있으면
            lyrics_table = table # 가사 테이블로 지정
            break
    if lyrics_table:
        break
```

(보컬이 1인인 경우) 테이블의 첫번째 tr이 테이블 헤더(Japanese인지 Romaji인지 적힌 부분)이고, 이를 인식해서 테이블 열 길이, 열 이름을 불러오는 부분
```python
#TODO 보컬이 여러명인 경우 이것 위에 보컬에 해당하는 가사 색을 알려주는 부분이 있을 수 있음 (확실하지 않음)
rows = lyrics_table.find_all("tr") # 위에서 찾은 가사 테이블의 모든 tr을 찾음
lyrics_types = rows[0].select("th") # 맨 첫번째 행에서 테이블 헤더들을 가져옴
lyrics_type_string = []
for lyrics_type in lyrics_types:
    lyrics_type_string.append(lyrics_type.text.strip()) # 테이블 헤더의 텍스트 뽑아내기
rows = rows[1:]
```

```python
for i in range(len(lyrics_type_string)):
    # output 폴더에 '곡 이름'/'Japanese/Romaji'.txt 파일을 생성하기 
    with open(f"./output/{wiki_doc_name}/{lyrics_type_string[i].strip()}.txt", "w", encoding="utf-8") as f:
        for row in rows:
            td = row.find_all("td")
            if len(td) > i:
                f.write(td[i].text.strip() + '\n')
            else: # 특이사항을 처리하는 부분: 가사가 아예 영어인 경우 이런식으로 첫 번째 열에 그냥 들어있음
                f.write(td[0].text.strip() + '\n')
```




## 3. 🚀 Insight
- **크롤링 공부할 때는 html 자료구조에 대한 기본적인 이해가 필요하다**
- 디버깅한다고 요청 계속 보냈더니 한 번씩 요청이 짤렸다, 그래서 요청을 txt에 저장해두고 꺼내면서 디버깅했다
    : 서버에 계속 요청을 보내면 거절당할 수 있다 ㅎㅎ

## 4. 🔗 Reference
- 없음