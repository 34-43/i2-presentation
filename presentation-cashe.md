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
# 📁 발표 패키지 구조 >

<div class="grid-container">

<div class="grid-item">

## 🎨 설계 단계

- 🚀 **프로젝트 개요**
- 🎯 **기술적 목표**

</div>

<div class="grid-item">

## 💻 구현 단계

- ⚙️ **핵심 기능 소개**
- 🎥 **영상 시연**
- 🔧 **트러블슈팅 소개**

</div>

</div>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin-top: 2rem;
}
.grid-item {
  padding: 1rem;
  background: rgba(255,255,255,0.1);
  border-radius: 8px;
}
</style>

---
<!-- _class: title -->
## 🎨 설계 단계

- 🚀 **프로젝트 개요**
- 🎯 **기술적 목표**

---

# <span class="stage">설계/</span> <span class="symbol">✨</span> 프로젝트 개요

## <span class="title">주제 선택</span>

<div class="topic-container">
  <div class="topic-main">
    <h3>동시성 제어</h3>
    <div class="level">
      <span class="badge">난이도: 상</span>
    </div>
  </div>

  <div class="service-info">
    -> <h4 style="display: inline;">🎯 온라인 티켓팅 서비스</h4>
  </div>

  > - **동시다발적 요청**에 에한 동시성 제어 주제에 적합
  > - CRUD 를 단순화하여 **도전 목표**에 집중

</div>

<style scoped>
.title {
  border-bottom: 3px solid #4a90e2;
  padding-bottom: 5px;
}

.topic-container {
  margin: 20px;
  font-size: 1.2em;
}

.topic-main {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.badge {
  background-color: #ff7043;
  color: white;
  padding: 5px 10px;
  border-radius: 15px;
  font-size: 0.8em;
}

.service-info, .goal {
  margin-left: 30px;
  margin-bottom: 15px;
}

.service-name {
  color: #4a90e2;
  font-weight: bold;
  margin-left: 20px;
}

.goal-detail {
  margin-left: 20px;
  color: #666;
}

h3, h4 {
  margin: 0;
  color: #333;
}
</style>

---
# <span class="stage">설계/</span> <span class="symbol">✨</span> 프로젝트 개요

## <span class="title">**인터파크**를 참고한 와이어프레임 작성</span>

![bg right:40%](https://file.notion.so/f/f/83c75a39-3aba-4ba4-a792-7aefe4b07895/0dee85e7-2c2d-4b7b-b16c-faf2652dbfd8/i2_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_figjam.png?table=block&id=3ffd847b-b561-4883-966a-92d069587d6e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&expirationTimestamp=1732932000000&signature=Qy7ipO5SovhrnCZnZXovx-LMr82BlmECxQu9Nd6hUDg&downloadName=i2+%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8+figjam.png)

<div class="content-wrapper">
  <div class="description">
    <h3>📋 Interparty 핵심 API</h3>
    <ul class="feature-list">
      <li><span class="highlight">일반 사용자</span>
        <ul>
          <li>공연 전체 조회</li>
          <li>공연의 특정 좌석 예매</li>
        </ul>
      </li>
      <li><span class="highlight">공연 담당자</span>
        <ul>
          <li>공연 정보 등록</li>
        </ul>
      </li>
    </ul>
  </div>
</div>

<style scoped>

.description {
  padding: 20px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.feature-list {
  list-style-type: none;
  padding-left: 0;
}

.feature-list li {
  margin-bottom: 15px;
}

.feature-list ul {
  list-style-type: circle;
  margin: 8px 0;
  padding-left: 20px;
}

.highlight {
  color: #4a90e2;
  font-weight: bold;
}

h3 {
  color: #333;
  margin-top: 0;
  border-bottom: 2px solid #4a90e2;
  padding-bottom: 8px;
}
</style>

---
# <span class="stage">설계/</span> 🎯 기술적 목표

<div class="goals-container">
  <div class="main-goal">
    <h3>🎯 주요 목표: Redis 응용 기능 둘 다 구현</h3>
    <div class="goal-cards">
      <div class="goal-card">
        <h4>🔒 동시성 제어</h4>
        <p>분산 락을 통한 안전한 티켓팅 구현</p>
      </div>
      <div class="goal-card">
        <h4>💨 캐싱</h4>
        <p>빠른 응답을 위한 데이터 캐싱 구현</p>
      </div>
    </div>
  </div>

  <div class="sub-goals">
    <h3>✨ 부가 목표: 플러스 주차 학습 성과 반영</h3>
    <div class="tech-list">
      <div>
        <span class="tech-icon">🛠</span>
        <strong>Kotlin 100%:</strong>
        프로젝트 생성부터 테스트까지 순수 코틀린으로 구현
      </div>
      <div>
        <span class="tech-icon">🐳</span>
        <strong>Docker:</strong>
        MySQL, Redis 등 컨테이너 기반 개발 환경 구성
      </div>
    </div>
  </div>
</div>

<style scoped>
.goals-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 0.5rem;
  font-size: 0.9em;
}

.goal-cards, .tech-stack {
  display: flex;
  gap: 1rem;
  margin-top: 0.5rem;
}

.goal-card, .tech-item {
  background: rgba(49, 130, 206, 0.1);
  padding: 0.8rem;
  border-radius: 8px;
  flex: 1;
}

.goal-card h3 {
  color: #333;
  margin-top: 0;
  border-bottom: 2px solid #4a90e2;
  padding-bottom: 8px;
}
</style>

---
<!-- _class: title -->
## 💻 구현 단계

- ⚙️ **핵심 기능 소개**
- 🎥 **영상 시연**
- 🔧 **트러블슈팅 소개**

---

# <span class="stage">구현/</span> ⚙️ 핵심 기능 소개

## ERD, API 테이블

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
# <span class="stage">구현/</span> 🎥 영상 시연

## 시연 내용
- 내용 작성

## 주요 포인트
- 내용 작성

---
# <span class="stage">구현/</span>🔧 트러블슈팅 소개

---

# 텍스트 스타일 활용

![bg left:40% brightness:0.9](https://via.placeholder.com/800x600/3182ce/ffffff?text=Styles)

- **굵은 글씨** 강조
- *기울임체* 활용
- ~~취소선~~ 표현
- `코드` 표시

> 💡 **디자인 팁**
> 텍스트 강조는 적절히 사용할 때 가장 효과적입니다.

---

# 데이터 시각화

| 항목 | 기본 | 프로 | 엔터프라이즈 |
|:--|:--:|:--:|--:|
| 기능 1 | ✓ | ✓ | ✓ |
| 기능 2 | - | ✓ | ✓ |
| 기능 3 | - | - | ✓ |
| 가격 | 무료 | ₩10,000 | ₩30,000 |

> 💡 표를 활용하여 데이터를 명확하게 전달할 수 있습니다.

---

# 코드 예시

```python
def modern_function(name: str) -> str:
    """현대적인 파이썬 코드 예시"""
    return f"""
    안녕하세요, {name}님!
    현대적인 프레젠테이션에 오신 것을 환영합니다.
    """

result = modern_function("홍길동")
print(result)
```