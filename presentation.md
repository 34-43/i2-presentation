---
marp: true
theme: default
paginate: true
header: "**12조 프로젝트 발표**"
footer: "© 2024 Interparty"
style: |
  @import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
  @import url('https://cdn.jsdelivr.net/gh/wanteddev/wanted-sans/packages/wanted-sans/fonts/webfonts/variable/complete/WantedSansVariable.css');
  
  section {
    background: linear-gradient(135deg, #f8fafc, #e2e8f0);
    font-family: 'Pretendard Variable', 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
  }
  
  section.title {
    background: linear-gradient(135deg, #1a365d, #2b6cb0);
    color: white;
    position: relative;
    overflow: hidden;
  }
  section.title::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: 
      radial-gradient(circle at 20% 20%, #4299e180 0%, transparent 25%),
      radial-gradient(circle at 80% 80%, #63b3ed80 0%, transparent 25%);
    z-index: 0;
  }
  section.title h1 {
    font-family: 'Wanted Sans Variable';
    font-weight: 700;
    color: white;
    font-size: 3.5em;
    margin-bottom: 0.3em;
    background: none;
    position: relative;
    z-index: 1;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  }
  section.title h3 {
    font-family: 'Wanted Sans Variable';
    font-weight: 500;
    color: #bfdbfe;
    font-size: 1.5em;
    position: relative;
    z-index: 1;
  }
  section.title h1, section.title h2 {
    font-size: 2.5em;
    color: white;
  }
  section.lead {
    background: linear-gradient(135deg, #2c5282, #2b6cb0);
    color: white;
  }
  section.lead h1, section.lead h2 {
    color: white;
  }
  h1 {
    color: #2d3748;
    background: linear-gradient(transparent 70%, #bfdbfe 70%);
    display: inline-block;
  }
  h2 {
    color: #4a5568;
  }
  strong {
    color: #3182ce;
  }
  ul li {
    margin: 0.5em 0;
  }
  blockquote {
    background: #ffffff80;
    border-left: 4px solid #3182ce;
    padding: 1em;
    margin: 1em 0;
  }
  table {
    background: #ffffff80;
  }
  code {
    background: #2d3748;
    color: #e2e8f0;
  }
  img {
    background-color: transparent !important;
  }
  section {
    justify-content: flex-start;
  }
  .stage {
    font-size: 0.7em;
    background: rgba(49, 130, 206, 0.1);
    padding: 2px 6px;
    border-radius: 4px;
    color: #3182ce;
    margin-left: 8px;
    vertical-align: middle;
  }
---

<!-- _class: title -->
# 동시성 제어 기반 <br>티켓팅 서비스 구현
### 12조 **i2**

<br>

김혜진 · 이한식 · 장재혁 · 이지훈

![bg right:40%](image.png)


---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개

## CRUD 기초 구현 (ERD, API)

<div class="erd-container">
  <div class="erd-item">
    <img src="image-1.png" 
         alt="메인 ERD 다이어그램" 
         style="height: 350px; object-fit: contain;">
  </div>
  
  <div class="erd-item">
    <img src="image-2.png" 
         alt="API 테이블" 
         style="height: 350px; object-fit: contain;">
  </div>
</div>

<div class="placeholder-image">
  <img src="https://images.velog.io/images/park9910/post/dc139b53-7a2c-4973-ba88-23fb96b06b2e/image.png" alt="spring-security">
</div>

<style scoped>
.erd-container {
  display: flex;
  justify-content: center;
  gap: 2rem;
}

.erd-item {
  background: rgba(255, 255, 255, 0.5);
  display: flex;
  align-items: center;
}

.placeholder-image {
  position: fixed;
  bottom: 50px;
  right: 100px;
  z-index: 100;
}

.placeholder-image img {
  width: 300px;
  height: 100px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>

---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개

<div style="display: flex; flex-direction: column; align-items: center;">
  <img src="image-4.png" alt="alt text" style="margin: 20px 0; border-radius: 16px;">
  <p style="text-align: center;">
    <strong>동시성 문제</strong>가 발생하기 쉬운 <code>예매 API</code> 구현
  </p>
</div>

---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개
> 100 개의 자리 * 10 명의 동시성 요청 

- 동시 요청 스레드 수 : 1000
- 예매 실패 횟수 예상 : 900

<div class="code-container">
  <div class="code-block">

  ```java
  필요 :900
  실제 :814
  <클릭하여 차이점 확인>

  예매 실패 횟수: 814 회
  예매된 좌석 번호 목록: [1, 2, 26, 27, 3, 28, 31, 32, 14, 
  4, 18, 16, 17, 20, 22, 23, 43, 24, 25, 5, 13, 44, 42, 
  40, 41, 46, 39, 47, 38, 47, 45, 48, 37, 50, 36, 35, 34, 
  33, 30, 29, 6, 7, 7, 8, 9, 10, 11, 12, 15, 19, 21, 51,
  ```
  </div>
  <div class="code-block">

  ```java
  예매 실패 횟수: 900 회
  예매된 좌석 번호 목록: [1, 17, 2, 3, 48, 47, 18, 19, 39, 
  43, 44, 20, 46, 45, 40, 7, 42, 11, 12, 14, 15, 22, 53, 
  23, 21, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 
  36, 37, 38, 52, 51, 49, 50, 4, 5, 6, 8, 10, 9, 13, 16, 
  41, 56, 57, 55, 54, 65, 68, 67, 82, 80, 58, 69, 59, 81, 
  77, 60, 61, 74, 78, 76, 62, 63, 88, 64, 89, 90, 87, 91, 
  92, 86, 83, 93, 85, 70, 71, 79, 72, 66, 73, 75, 84, 94, 
  95, 96, 97, 99, 100, 98]
  ```
  </div>
</div>

<style scoped>
  p {
    font-size: 0.8em;
  }

  pre {
    background: #2d3748;
    color: #e2e8f0;
  }

  .code-container {
    display: flex;
    justify-content: space-between;
    gap: 2rem;
  }

  .code-block {
    flex: 1;
  }

  .code-block pre {
    margin: 0;
    font-size: 0.8em;
  }
</style>

---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개

![bg right:40%](https://file.notion.so/f/f/83c75a39-3aba-4ba4-a792-7aefe4b07895/44ae197f-8d6f-42c1-95e9-c25cf000bf90/image.png?table=block&id=8a770c59-9893-459d-81f3-d69f34f5a89e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&expirationTimestamp=1732939200000&signature=tHIPCUJuvfbau7XcqJOIQ0aifMAzHTaZmbYZnou92to&downloadName=image.png)

## 캐싱 구현
| 지표 | 조회 v1 | 조회 v2 | 차이 |
|:--|:--:|:--:|--:|
| Total Requests | 620 | 613 | 거의 동일 |
| Avg Resp Time | 315ms | 110ms | 65% 향상 |
| 90th Percentile | 513ms | 57ms | 88.9% 향상 |
| Max Resp Time | 4,425ms | 4,379ms | 거의 동일 |

<style scoped>
table {
  font-size: 0.8em;  /* 기본 폰트 크기의 80%로 축소 */
}
</style>

---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개

## 로컬에서의 Docker 활용
```makefile
up:
  wsl docker run -td --name redis_interparty -p 6379:6379 redis:alpine

down:
  wsl docker stop redis_interparty && wsl docker rm redis_interparty

ping:
  wsl redis-cli ping

clear:
  wsl sudo systemctl stop redis && wsl docker container prune -f
```

<style scoped>
pre {
  background: #2d3748;
  color: #e2e8f0;
}
</style>

---
# <span class="stage">구현/</span> 🎥 영상 시연

<div class="video-container">
  <a href="유튜브_링크" target="_blank">
    <img src="https://img.youtube.com/vi/VIDEO_ID/maxresdefault.jpg" alt="데모 영상" style="width: 50%; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
    <div class="play-button">▶</div>
  </a>
</div>

<style scoped>
.video-container {
  position: relative;
  text-align: center;
  margin: 2em 0;
}

.play-button {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 4em;
  color: white;
  text-shadow: 0 0 10px rgba(0,0,0,0.5);
  opacity: 0.8;
}

.video-container:hover .play-button {
  opacity: 1;
}
</style>

---
# <span class="stage">구현/</span>🔧 트러블슈팅 소개

> 분산 락과 Transactional 범위 문제

> UUID 중복 생성 문제

> Redis 빌드 테스트로 인한 CI 불가능 문제

---

# <span class="stage">Q&A</span> 💬 질의응답

<div style="display: flex; justify-content: center; align-items: center; height: 70vh;">
  <h1 style="font-size: 4em; color: #3182ce;">Q & A</h1>
</div>

<style scoped>
h1 {
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
  background: none;
}
</style>
