# 📅 TIL - ItemEffectComponent 시스템 구현

## 🎯 목표

아이템 획득 / 악행(Malice) 변화 / 보상(Reward) 획득 시
👉 자동으로 VFX + 사운드를 재생하는 시스템 구현

---

## 🧩 구현 개요

### ✅ 핵심 컴포넌트

* `UItemEffectComponent`
* 캐릭터에 붙어서 이벤트 감지 후 이펙트 실행

📌 감지 대상 이벤트

* Item 획득 → `ItemManagerComponent`
* Malice 변화 → `MaliceComponent`
* Reward 획득 → `CharacterRewardComponent`

---

## 🔗 이벤트 바인딩 구조

```cpp
// Item 획득
CachedItemManager->DelegateAddItem.AddUObject(this, &UItemEffectComponent::OnItemAdded);

// Malice 변화
CachedMaliceComponent->OnMaliceChanged.AddDynamic(this, &UItemEffectComponent::OnMaliceChanged);

// Reward 획득
CachedRewardComponent->OnRewardAcquired.AddUObject(this, &UItemEffectComponent::OnRewardAcquired);
```

👉 BeginPlay에서 모든 이벤트 연결

---

## 📦 데이터 구조 (핵심 ⭐)

### 1️⃣ 아이템 이펙트

```cpp
USTRUCT(BlueprintType)
struct FItemEffectData
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    FName ItemID;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TObjectPtr<UNiagaraSystem> VFX;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TObjectPtr<USoundBase> Sound;
};
```

### 2️⃣ Malice 이펙트

```cpp
USTRUCT(BlueprintType)
struct FMaliceEffectData
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    int32 MaliceCount = 1;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TObjectPtr<UNiagaraSystem> VFX;

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    TObjectPtr<USoundBase> Sound;
};
```

👉 데이터 기반 설계 (Data Driven)
👉 블루프린트에서 쉽게 확장 가능

---

## ⚙️ 동작 흐름

### 🟢 1. 아이템 획득

```cpp
void OnItemAdded(int32 SlotIndex, const UItemDefinition* ItemDefinition)
{
    for (const FItemEffectData& EffectData : ItemEffects)
    {
        if (EffectData.ItemID == ItemDefinition->ItemId)
        {
            PlayItemEffect(EffectData);
            return;
        }
    }
}
```

---

### 🔴 2. Malice 변화

```cpp
void OnMaliceChanged(int32 NewCount)
{
    for (const FMaliceEffectData& EffectData : MaliceEffects)
    {
        if (EffectData.MaliceCount == NewCount)
        {
            PlayMaliceEffect(EffectData, NewCount);
            return;
        }
    }
}
```

---

### 🟡 3. Reward 획득 (확장 기능 ⭐)

```cpp
void OnRewardAcquired(const URewardDefinition* RewardDefinition)
{
    FName RewardID = RewardDefinition->ItemId;

    for (const FItemEffectData& EffectData : ItemEffects)
    {
        if (EffectData.ItemID == RewardID)
        {
            PlayItemEffect(EffectData);
            return;
        }
    }
}
```

👉 Item / Event 보상 통합 처리

---

## 🎆 이펙트 실행

### VFX

```cpp
UNiagaraFunctionLibrary::SpawnSystemAtLocation(
    GetWorld(),
    EffectData.VFX,
    SpawnLocation
);
```

### Sound

```cpp
UGameplayStatics::PlaySoundAtLocation(
    this,
    EffectData.Sound,
    SpawnLocation
);
```

---

## 🧠 핵심 설계 포인트

### ✅ 1. 로컬 플레이어만 실행

```cpp
APawn* OwnerPawn = Cast<APawn>(Owner);
if (OwnerPawn && !OwnerPawn->IsLocallyControlled())
{
    return;
}
```

👉 멀티플레이 중복 실행 방지

---

### ✅ 2. 데이터 기반 확장성

* ItemID 추가만으로 기능 확장 가능
* 코드 수정 없이 유지보수 가능

---

### ✅ 3. 이벤트 통합 구조

* Item / Malice / Reward → 하나의 컴포넌트에서 처리

---

## 🐞 디버깅 로그 전략

```cpp
UE_LOG(LogTemp, Warning, TEXT("Item Added"));
UE_LOG(LogTemp, Warning, TEXT("Match found"));
UE_LOG(LogTemp, Warning, TEXT("VFX spawned"));
UE_LOG(LogTemp, Warning, TEXT("Sound played"));
```

👉 어느 단계에서 문제인지 빠르게 확인 가능

---

## 💡 배운 점

* 🔹 Delegate 기반 이벤트 시스템 이해
* 🔹 Data Driven 설계의 중요성
* 🔹 멀티플레이에서 Local 처리 필요성
* 🔹 Item / Reward / Event 통합 구조 설계

---

## 🚀 개선 아이디어

* [ ] DataAsset 기반으로 리팩토링
* [ ] 소켓 기반 VFX (캐릭터 → 무기)
* [ ] UI 피드백 연동
* [ ] 이벤트 ID 기반 확장

---

## 🧾 한 줄 정리

👉 **"아이템 / 이벤트 기반 이펙트를 데이터로 관리하는 구조 구현 완료"**
