# Unity & C# 학습 정리 — 1일차

## 1. 유니티 구성 요소

Unity 프로젝트의 기본적인 구조는 다음과 같다.

**프로젝트(Project) → 씬(Scene) → 게임오브젝트(GameObject) → 컴포넌트(Component)**

하나의 프로젝트 안에 여러 개의 씬이 존재하고, 씬 안에 여러 게임오브젝트가 존재한다. 각 게임오브젝트는 여러 개의 컴포넌트를 가질 수 있다.

---

## 1-1. 프로젝트(Project)

### 개념

**하나의 게임이나 애플리케이션을 구성하는 전체 작업 단위이다.**

프로젝트에는 게임 제작에 필요한 모든 리소스와 설정이 포함된다.

예를 들어 다음과 같은 요소가 프로젝트에 포함된다.

- Scene
- C# Script
- Prefab
- Material
- Texture
- Audio
- Animation
- Project Settings

### 예시

RPG 게임을 제작한다면 하나의 `RPGGame` Unity 프로젝트를 만들고 그 안에 다음과 같은 요소를 구성할 수 있다.

```
RPGGame
 ├─ MainMenu Scene
 ├─ Village Scene
 ├─ Dungeon Scene
 ├─ Player
 ├─ Monster
 ├─ UI
 ├─ Script
 ├─ Material
 └─ Audio
```

### 핵심

> **Project = 하나의 게임 전체**
> 

---

## 1-2. 씬(Scene)

### 개념

**게임의 하나의 화면이나 공간을 구성하는 단위이다.**

씬 안에는 게임에 등장하는 여러 GameObject가 배치된다.

### 예시

게임을 다음과 같이 여러 씬으로 나눌 수 있다.

```
MainMenu
    ↓
Stage1
    ↓
Stage2
    ↓
Ending
```

RPG의 경우 다음과 같이 장소별로 씬을 구성할 수도 있다.

```
Village
Dungeon
BossRoom
```

### 주요 용도

- 메인 메뉴
- 게임 스테이지
- 로딩 화면
- 마을
- 던전
- 엔딩 화면

각 화면이나 공간을 별도의 Scene으로 관리할 수 있다.

### 핵심

> **Scene = 게임의 하나의 화면 또는 공간**
> 

---

## 1-3. 게임오브젝트(GameObject)

### 개념

**Scene 안에 존재하는 모든 객체의 기본 단위이다.**

Unity에서는 캐릭터, 카메라, 조명, 아이템 등 대부분의 객체를 GameObject로 관리한다.

예를 들어 다음과 같은 요소가 모두 GameObject이다.

```
Player
Enemy
Main Camera
Directional Light
Sword
Tree
UI Canvas
```

GameObject 자체는 특별한 기능을 가지지 않는다.

실제 기능은 **Component를 추가하는 방식으로 구성한다.**

### 예시

`Player`라는 GameObject를 만들었다고 해서 자동으로 이동하거나 충돌하는 기능이 생기는 것은 아니다.

```
Player (GameObject)
```

여기에 여러 Component를 추가하여 실제 플레이어의 기능을 구성한다.

### 핵심

> **GameObject = 게임 세계에 존재하는 객체의 기본 틀**
> 

---

## 1-4. 컴포넌트(Component)

### 개념

**GameObject에 기능이나 특성을 부여하는 요소이다.**

Unity는 하나의 GameObject에 여러 Component를 조합하여 하나의 객체를 구성한다.

예를 들어 Player는 다음과 같이 구성할 수 있다.

```
Player (GameObject)
 ├─ Transform
 ├─ Mesh Renderer
 ├─ Collider
 ├─ Rigidbody
 └─ PlayerController
```

### 대표적인 Component

| Component | 역할 |
| --- | --- |
| Transform | 위치, 회전, 크기를 관리한다. |
| Mesh Renderer | 3D 모델을 화면에 표시한다. |
| Collider | 충돌 영역을 설정한다. |
| Rigidbody | 물리 효과를 적용한다. |
| Camera | 게임 화면을 촬영한다. |
| Light | Scene에 조명을 제공한다. |
| Audio Source | 소리를 재생한다. |
| C# Script | 직접 작성한 게임 로직을 실행한다. |

### Transform

모든 GameObject는 기본적으로 **Transform Component**를 가진다.

Transform은 다음 세 가지 값을 관리한다.

```
Position → 위치
Rotation → 회전
Scale → 크기
```

### C#과 Component

Unity에서 작성하는 C# 스크립트 역시 GameObject에 추가하는 **Component**로 사용할 수 있다.

예를 들어 다음과 같은 스크립트를 작성한다.

```
publicclassPlayerController :MonoBehaviour
{
}
```

이 스크립트를 Player에 추가하면 다음과 같이 하나의 Component가 된다.

```
Player
 ├─ Transform
 ├─ Rigidbody
 ├─ Collider
 └─ PlayerController
```

### 핵심

> **Component = GameObject에 기능을 추가하는 부품**
> 

---

# 2. 유니티 주요 개념

## 2-1. 프리팹(Prefab)

### 개념

**미리 만들어 놓은 GameObject를 재사용할 수 있도록 Asset으로 저장한 것이다.**

게임에서는 동일하거나 비슷한 객체를 여러 번 사용하는 경우가 많다.

예를 들어 몬스터를 여러 마리 생성해야 할 때 매번 다음 작업을 반복하면 비효율적이다.

```
GameObject 생성
Collider 추가
Rigidbody 추가
Script 추가
Material 설정
```

완성된 몬스터를 Prefab으로 만들어두면 동일한 구조의 GameObject를 쉽게 재사용할 수 있다.

### 예시

```
Enemy Prefab
 ├─ Transform
 ├─ Mesh Renderer
 ├─ Collider
 ├─ Rigidbody
 └─ EnemyController
```

이 Prefab을 이용하여 Scene에 여러 개의 Enemy를 배치할 수 있다.

```
Enemy
Enemy
Enemy
Enemy
Enemy
```

각 Enemy는 동일한 Prefab을 기반으로 생성된다.

### 장점

- 동일한 객체를 쉽게 재사용할 수 있다.
- 반복 작업을 줄일 수 있다.
- 여러 객체를 일관성 있게 관리할 수 있다.
- Prefab 원본의 변경 사항을 여러 Instance에 반영할 수 있다.
- 코드에서 동적으로 생성할 수 있다.

C#에서는 주로 `Instantiate()`를 사용하여 Prefab을 생성한다.

```
Instantiate(enemyPrefab);
```

### 핵심

> **Prefab = 재사용하기 위해 저장해 둔 GameObject 설계도**
> 

---

## 2-2. 머터리얼(Material)

### 개념

**3D 오브젝트의 표면이 어떻게 보일지를 결정하는 Asset이다.**

쉽게 말하면 오브젝트의 **재질**을 결정한다.

같은 3D 모델이라도 Material에 따라 서로 다른 재질로 표현할 수 있다.

예를 들면 다음과 같다.

```
금속
나무
돌
유리
플라스틱
```

### Material에서 설정할 수 있는 요소

대표적으로 다음과 같은 요소를 설정할 수 있다.

- 색상
- 텍스처
- 반사 정도
- 표면의 매끄러움
- 투명도
- 발광

### Material과 Shader

Material은 내부적으로 **Shader**를 사용하여 화면에 어떻게 표현될지를 결정한다.

관계를 단순화하면 다음과 같다.

```
Shader
   ↓
Material
   ↓
GameObject
```

Shader는 **어떻게 화면에 그릴 것인지**를 결정하고, Material은 Shader가 사용할 색상, 텍스처, 반사값 등의 데이터를 저장한다.

### 예시

```
Player
 └─ Mesh Renderer
       └─ KnightMaterial
              ├─ Texture
              ├─ Color
              ├─ Metallic
              └─ Smoothness
```

### 핵심

> **Material = 오브젝트 표면의 시각적인 재질을 결정하는 요소**
> 

---

## 2-3. 스카이박스(Skybox)

### 개념

**게임 세계의 배경을 둘러싸는 환경 표현 방식이다.**

플레이어가 게임 세계를 바라봤을 때 멀리 보이는 하늘이나 주변 환경을 표현하는 데 사용한다.

예를 들어 다음과 같은 환경을 표현할 수 있다.

- 하늘
- 구름
- 우주
- 산
- 노을
- 던전 배경

실제로 매우 큰 배경 오브젝트를 만드는 것이 아니라 카메라 주변을 이미지나 환경으로 둘러싼 것처럼 표현한다.

### 예시

판타지 게임에서는 다음과 같은 Skybox를 사용할 수 있다.

```
푸른 하늘
구름
산
노을
```

우주 게임에서는 다음과 같이 표현할 수 있다.

```
별
은하
우주 공간
```

### 특징

Skybox는 단순히 배경만 표현하는 것이 아니라 **Scene의 환경 조명에도 영향을 줄 수 있다.**

예를 들어 밝은 낮 Skybox를 사용하면 Scene 전체의 환경광도 밝게 구성할 수 있다.

### 핵심

> **Skybox = 게임 세계를 둘러싸고 있는 배경 환경**
> 

---

# 3. 전체 관계 정리

지금까지의 개념을 하나의 게임 구조로 연결하면 다음과 같다.

```
Unity Project
│
├─ MainMenu Scene
│
└─ Game Scene
    │
    ├─ Player (GameObject)
    │   ├─ Transform
    │   ├─ Rigidbody
    │   ├─ Collider
    │   └─ PlayerController
    │
    ├─ Enemy (GameObject)
    │   ├─ Transform
    │   ├─ Collider
    │   └─ EnemyController
    │
    ├─ Main Camera
    └─ Directional Light
```

반복적으로 사용하는 `Enemy`는 다음과 같이 저장할 수 있다.

```
Enemy Prefab
```

Enemy의 외형에는 다음 요소를 적용한다.

```
Material
```

Scene 전체의 배경에는 다음 요소를 적용할 수 있다.

```
Skybox
```

---

# 4. 1일차 핵심 정리

| 개념 | 한 줄 정리 |
| --- | --- |
| **Project** | 하나의 게임 전체를 관리하는 작업 단위이다. |
| **Scene** | 게임의 하나의 화면 또는 공간이다. |
| **GameObject** | Scene에 존재하는 객체의 기본 단위이다. |
| **Component** | GameObject에 기능을 부여하는 요소이다. |
| **Prefab** | GameObject를 재사용할 수 있도록 저장한 설계도이다. |
| **Material** | 오브젝트 표면의 시각적인 재질을 결정한다. |
| **Skybox** | 게임 세계를 둘러싸는 배경 환경이다. |