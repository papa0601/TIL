# [cloudscarper] Client Challenge 'cloudscraper'로 우회하기

📅 **Date:** 2026-01-18
🏷️ **Tags:** #python #requests #cloudscraper #bypass

---

## 1. 💡 What & Why?
> **한 줄 요약:** 웹 크롤링 시 Client Challenge를 cloudscraper로 우회함

- **상황:** 
    - requests 라이브러리로 Fandom Wiki api.php에 접근 시도함
    - User-Agent와 Cookie를 설정했음에도 검색결과 json 대신 Client Challenge라는 이름의 html 문서가 반환됨
    - **원인**: Fandom Wiki가 Cloudflare과 같은 보안 솔루션을 사용하여 단순 HTTP 요청이 아닌 JavaScript 실행 능력이 있는지 검사하기 때문. request 라이브러리는 JS를 실행하지 못하여 해당 테스트를 통과하지 못함.


## 2. 🔧 How? (Code)
- 해결책: request 대신 cloudscraper를 사용하면, cloudscraper가 내부적으로 JavaScript를 사용하여 보안 챌린지를 해결해준다.

```bash
# cloudscraper 설치하기
pip install cloudscraper
```

```python
import cloudscraper

scraper = cloudscraper.create_scraper() # 크롤링하는 녀석, request 대신에 사용한다

response = scraper.get(url, params=params)

# response.json() 등 작업하기...
```

## 3. 🚀 Insight
- 웹 개발에는 조예가 없었는데 이런식으로 크롤링하면서 하나 둘 배워나갈 수 있다...
- Client Challenge 같은게 있는지 알게되었다..

## 4. 🔗 Reference
- 