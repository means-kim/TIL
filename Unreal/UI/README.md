# 🎬 Unreal Engine Intro Splash 구현 (Widget 기반)

## 📌 개요

패키징된 EXE 실행 시 다음과 같은 인트로 연출을 구현합니다:

```
검은 화면 → 로고 Fade In → 유지 → Fade Out → 게임 시작
```

---

## 🎯 구현 방식

* **Widget 기반 구현 (Level Sequence 미사용)**
* 기존 코드 수정 없이 **컴포넌트 추가 방식**
* 멀티플레이 안전 (로컬 클라이언트에서만 실행)

---

# 📁 파일 구조

```
A302/Source/A302Client/UI/
 ├── IntroSplashComponent.h
 ├── IntroSplashComponent.cpp
 └── IntroSplashWidget.h
```

---

# 🧩 1. Widget (WBP_IntroSplash) 제작

## 1️⃣ 위젯 생성

* 경로: `Content/WorkSpace/UI/`
* Widget Blueprint 생성
* 부모 클래스: `IntroSplashWidget`
* 이름: `WBP_IntroSplash`

---

## 2️⃣ 레이아웃 구성

```
Canvas Panel (Root)
 ├── Image (BlackBackground)
 └── Image (LogoImage)
```

---

## 3️⃣ BlackBackground 설정

* Anchor: Full Screen
* Color: (0,0,0,1)
* ZOrder: 0

👉 항상 검은 화면 유지 역할

---

## 4️⃣ LogoImage 설정

* Anchor: Center
* Alignment: (0.5, 0.5)
* Position: (0, 0)
* Render Opacity: 0 (초기 숨김)
* ZOrder: 1

---

# 🎬 2. 애니메이션 설정

## 🔥 핵심 구조

```
Canvas → 항상 보임 (검정)
Logo → 페이드 대상
```

---

## 1️⃣ FadeInAnim

* 대상: `LogoImage`
* Track: Render Opacity

| 시간   | 값   |
| ---- | --- |
| 0.0s | 0.0 |
| 1.5s | 1.0 |

---

## 2️⃣ FadeOutAnim

* 대상: `LogoImage`
* Track: Render Opacity

| 시간   | 값   |
| ---- | --- |
| 0.0s | 1.0 |
| 1.5s | 0.0 |

---

## ❗ 중요

* Canvas Panel에는 애니메이션 적용 ❌
* LogoImage만 페이드 적용 ⭕

---

# 🧠 3. Widget C++ 클래스

## 📄 IntroSplashWidget.h

```cpp
UCLASS(Abstract)
class A302CLIENT_API UIntroSplashWidget : public UUserWidget
{
    GENERATED_BODY()

public:
    void PlayFadeIn();
    void PlayFadeOut();

protected:
    UPROPERTY(Transient, meta = (BindWidgetAnim))
    TObjectPtr<UWidgetAnimation> FadeInAnim;

    UPROPERTY(Transient, meta = (BindWidgetAnim))
    TObjectPtr<UWidgetAnimation> FadeOutAnim;
};
```

---

# 🧩 4. Component (IntroSplashComponent)

## 역할

* 위젯 생성 및 표시
* FadeIn / FadeOut 제어
* 사운드 재생
* 자동 제거

---

## 주요 흐름

```
BeginPlay
 → Delay
 → Widget 생성
 → AddToViewport
 → FadeIn
 → Sound
 → Delay
 → FadeOut
 → Remove
```

---

# 🧱 5. PlayerController 연결

## 1️⃣ BP 생성

```
BP_IntroPlayerController
(부모: MyPlayerController)
```

---

## 2️⃣ 컴포넌트 추가

* IntroSplashComponent 추가

---

## 3️⃣ 설정

| 항목           | 값               |
| ------------ | --------------- |
| Intro Widget | WBP_IntroSplash |
| Intro Sound  | 선택              |

---

## 4️⃣ 적용

```
Project Settings → Maps & Modes
→ PlayerController = BP_IntroPlayerController
```

---

# 🎮 6. 실행 흐름

```
게임 실행
 → 검은 화면 즉시 표시
 → 로고 Fade In
 → 유지
 → Fade Out
 → 위젯 제거
 → 게임 시작
```

---

# 🔒 멀티플레이 안전성

| 항목       | 처리                     |
| -------- | ---------------------- |
| 서버 실행 방지 | IsLocalController() 체크 |
| 리플리케이션   | 사용 안 함                 |
| UI 영향 범위 | 클라이언트 전용               |

---

# ⚠️ 트러블슈팅

## ❌ 검은 화면 안 보임

* Canvas Opacity를 0으로 설정한 경우
  👉 Canvas는 항상 1 유지

---

## ❌ 애니메이션 안됨

* FadeInAnim / FadeOutAnim 이름 불일치
* BindWidgetAnim 누락

---

## ❌ 로고 안 보임

* LogoImage Opacity 초기값 확인 (0)
* 애니메이션 트랙 대상 확인

---

## ❌ 실행 자체 안됨

* PlayerController 교체 안함

---

# 👍 최종 정리

👉 검은 화면은 **항상 유지 (Canvas + Background)**
👉 로고만 **Opacity로 페이드 처리**

```
Canvas (검정) → 고정
Logo → Fade In / Out
```

---

# 🚀 향후 확장

* ESC로 스킵 기능
* 로고 Scale 애니메이션
* 사운드 페이드
* 브랜드 로고 추가

---
