# 🎵 Animation Sound System (AnimNotify 기반 사운드 재생)

언리얼 엔진에서 **애니메이션 타이밍에 맞춰 사운드를 재생하기 위해 Custom AnimNotify를 구현**한다.

예를 들어 다음과 같은 상황에서 사용된다.

- 발자국 사운드
- 무기 휘두르는 사운드
- 공격 히트 사운드
- 상호작용 사운드

AnimNotify를 사용하면 **애니메이션 특정 프레임에서 정확한 타이밍으로 사운드를 실행**할 수 있다.

---

# 1️⃣ Custom AnimNotify 클래스 생성

새로운 AnimNotify 클래스를 만들어 애니메이션에서 사운드를 실행하도록 구현한다.

## PlaySound.h

```cpp
#pragma once

#include "CoreMinimal.h"
#include "Animation/AnimNotifies/AnimNotify.h"
#include "PlaySound.generated.h"

class USoundBase;

UCLASS()
class A302_API UPlaySound : public UAnimNotify
{
    GENERATED_BODY()

public:

    // 재생할 사운드
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Sound")
    USoundBase* Sound;

    // 소켓 이름 (선택)
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Sound")
    FName SocketName;

    // 볼륨
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Sound")
    float VolumeMultiplier = 1.0f;

    // 피치
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Sound")
    float PitchMultiplier = 1.0f;

public:

    virtual void Notify(
        USkeletalMeshComponent* MeshComp,
        UAnimSequenceBase* Animation
    ) override;
};
```

---

## PlaySound.cpp

```cpp
#include "Animation/AnimNotify/PlaySound.h"
#include "Kismet/GameplayStatics.h"
#include "Components/SkeletalMeshComponent.h"
#include "Sound/SoundBase.h"

void UPlaySound::Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation)
{
    if (!MeshComp || !Sound)
    {
        return;
    }

    FVector Location = MeshComp->GetComponentLocation();

    // 소켓이 지정되어 있으면 소켓 위치 사용
    if (SocketName != NAME_None)
    {
        Location = MeshComp->GetSocketLocation(SocketName);
    }

    UGameplayStatics::PlaySoundAtLocation(
        MeshComp,
        Sound,
        Location,
        VolumeMultiplier,
        PitchMultiplier
    );
}
```

---

# 2️⃣ 코드 설명

### Notify()

AnimNotify가 실행될 때 호출되는 함수이다.

애니메이션에서 Notify가 있는 프레임이 실행되면 이 함수가 자동으로 호출된다.

---

### 주요 변수 설명

| 변수 | 설명 |
|---|---|
| Sound | 재생할 사운드 |
| SocketName | 사운드가 발생할 위치 |
| VolumeMultiplier | 볼륨 조절 |
| PitchMultiplier | 피치 조절 |

---

### 사운드 위치 결정

```cpp
FVector Location = MeshComp->GetComponentLocation();
```

기본적으로 **캐릭터 위치에서 사운드가 재생된다.**

---

### 소켓 위치 사용

```cpp
Location = MeshComp->GetSocketLocation(SocketName);
```

예를 들어 다음과 같이 사용 가능하다.

- `foot_l` → 발자국 사운드
- `weapon_socket` → 무기 사운드
- `hand_r` → 손 사운드

---

### 사운드 재생

```cpp
UGameplayStatics::PlaySoundAtLocation(...)
```

월드 위치에서 사운드를 재생한다.

---

# 3️⃣ 애니메이션에 적용 방법

### 1️⃣ 애니메이션 또는 몽타주 열기

```
Animation Sequence
또는
Anim Montage
```

---

### 2️⃣ Notify 추가

타임라인에서

```
Right Click
→ Add Notify
→ PlaySound
```

---

### 3️⃣ Notify 설정

Notify를 선택하면 Details 패널에서 설정 가능

| 옵션 | 설명 |
|---|---|
| Sound | 재생할 사운드 |
| SocketName | 사운드 위치 |
| VolumeMultiplier | 볼륨 |
| PitchMultiplier | 피치 |

---

# 4️⃣ 사용 예시

## 발자국 사운드

```
Notify 위치 : 발이 땅에 닿는 프레임
SocketName : foot_l / foot_r
Sound : FootstepSound
```

---

## 무기 휘두르는 사운드

```
Notify 위치 : 공격 시작 프레임
SocketName : weapon_socket
Sound : SwordSwing
```

---

## 상호작용 사운드

```
Notify 위치 : 상호작용 시작
Sound : InteractionSound
```

---

# 5️⃣ 사운드 에셋 선택

언리얼에서는 보통 두 가지 사운드 타입을 사용한다.

### SoundWave

```
원본 사운드 파일
```

---

### SoundCue (추천)

```
여러 사운드를 조합 가능
랜덤 재생 가능
볼륨 조절 가능
```

예)

```
발자국 SoundCue
 ├ Footstep1
 ├ Footstep2
 ├ Footstep3
 └ Footstep4
```

이 경우 AnimNotify가 실행될 때 **랜덤 발자국 사운드가 재생된다.**

---

# 6️⃣ 장점

AnimNotify 방식의 장점

- 애니메이션 타이밍 정확
- 코드 수정 없이 애니메이션에서 제어 가능
- VFX / Sound / Weapon / Event 모두 동일 방식 사용 가능

예

```
AnimNotify
 ├ SpawnVFX
 ├ PlaySound
 ├ ShowWeapon
 └ HideWeapon
```

---

# 7️⃣ 확장 가능

추후 다음 기능도 쉽게 추가 가능

- Surface 기반 발자국 사운드
- 랜덤 Pitch
- 네트워크 사운드 동기화
- Footstep System

---

# 📌 정리

AnimNotify를 활용하면

```
Animation → 특정 프레임
        → Notify 호출
        → Sound 실행
```

구조로 **애니메이션과 사운드를 정확하게 동기화할 수 있다.**