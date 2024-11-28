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
---

<!-- _class: title -->
# 동시성 제어 기반 <br>티켓팅 서비스 구현
### 12조 **i2**

<br>

김혜진 · 이한식 · 장재혁 · 이지훈

![bg right:40%](image.png)

---
# ⚡️ 발표 패키지 구조

<div class="grid-container">

<div class="grid-item">

## 🎨 설계 단계

- 👥 **팀 소개**
- 🎯 **프로젝트 개요**
- 🚀 **기술적 목표**

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
# 👥 팀 소개

<div class="grid-container">
<div class="grid-item">

## 팀원 소개
- 내용 작성
- 내용 작성

</div>
<div class="grid-item">

## 역할 분담
- 내용 작성
- 내용 작성

</div>
</div>

---
# 🎯 프로젝트 개요

## 프로젝트 배경
- 내용 작성

## 프로젝트 목표
- 내용 작성

---
# 🚀 기술적 목표

## 사용 기술
- 내용 작성

## 아키텍처
- 내용 작성

---
# ⚙️ 핵심 기능 소개

## 주요 기능
- 내용 작성

## 기술적 특징
- 내용 작성

---
# 🎥 영상 시연

## 시연 내용
- 내용 작성

## 주요 포인트
- 내용 작성

---
# 🔧 트러블슈팅 소개

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