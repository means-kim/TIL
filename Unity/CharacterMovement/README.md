# Unity 2D 플레이어 이동 시스템 - Input System 기반

Unity Input System을 활용한 컴포넌트 기반 2D 플레이어 이동 구현

---

## 📋 개요
SOLID 원칙을 따르는 모듈화된 2D 플레이어 컨트롤러

- **Unity Input System** 기반 입력 처리
- **컴포넌트 기반 아키텍처** (각 기능 분리)
- **상태 머신** 패턴 적용
- **방향성 점프** (이동 중/제자리 구분)

---

## 🏗️ 아키텍처

### 컴포넌트 구조
    PlayerController (코디네이터)
     ├── PlayerInputComponent → 입력 수신
     ├── PlayerMovementComponent → 이동 + 지면 감지
     ├── PlayerStateComponent → 상태 관리 (Idle/Walk/Jump)
     └── PlayerJumpComponent → 점프 로직

### 단일 책임 원칙 (SRP) 적용

| 컴포넌트 | 책임 |
|---------|------|
| `PlayerInputComponent` | Input System에서 입력 읽기 |
| `PlayerMovementComponent` | Rigidbody2D 속도 제어 + 지면 체크 |
| `PlayerStateComponent` | 상태 전환 로직 |
| `PlayerJumpComponent` | 점프 힘 적용 |
| `PlayerController` | 컴포넌트 간 조율 + 실행 순서 보장 |

---

## 🎮 입력 시스템

### Input Actions 설정
**Action Map**: `Player`

- **Move**: Vector2 (WASD, 방향키)
- **Jump**: Button (Space)

### PlayerInputComponent
```csharp
public class PlayerInputComponent : MonoBehaviour
{
    [SerializeField] private InputActionReference moveAction;
    [SerializeField] private InputActionReference jumpAction;

    public float HorizontalInput { get; private set; }
    public bool JumpPressed { get; private set; }

    void Update()
    {
        Vector2 moveInput = moveAction?.action.ReadValue<Vector2>() ?? Vector2.zero;
        HorizontalInput = moveInput.x;

        JumpPressed = jumpAction?.action.triggered ?? false;
    }
}
```

## 🏃 이동 시스템
### PlayerMovementComponent
```
public class PlayerMovementComponent : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 6f;
    [SerializeField] private Transform groundCheckPoint;
    [SerializeField] private LayerMask groundLayer;

    public bool IsGrounded { get; private set; }
    public float LastFacingDirection { get; private set; } = 1f;

    public void FixedTick(float horizontalInput)
    {
        CheckGround();

        Rigidbody.linearVelocity = new Vector2(
            horizontalInput * moveSpeed,
            Rigidbody.linearVelocity.y
        );
    }
}
```

---

## 🦘 점프 시스템
### 동작 방식
- 제자리 점프: ⬆️
- 이동 중 점프: ↗️ / ↖️
### PlayerJumpComponent
```
public class PlayerJumpComponent : MonoBehaviour
{
    [SerializeField] private float jumpForceY = 12f;

    public void TryJump(Rigidbody2D rb, bool isGrounded, float facingDirection)
    {
        if (!isGrounded) return;

        rb.linearVelocity = new Vector2(rb.linearVelocity.x, 0f);
        rb.AddForce(new Vector2(0f, jumpForceY), ForceMode2D.Impulse);
    }
}
```

---

## 🎭 상태 관리
### PlayerStateComponent
```
public enum PlayerMovementState
{
    Idle,
    Walk,
    Jump
}

public class PlayerStateComponent : MonoBehaviour
{
    public PlayerMovementState CurrentState { get; private set; }

    public void UpdateState(float horizontalVelocity, bool isGrounded)
    {
        if (!isGrounded)
            CurrentState = PlayerMovementState.Jump;
        else if (Mathf.Abs(horizontalVelocity) > 0.1f)
            CurrentState = PlayerMovementState.Walk;
        else
            CurrentState = PlayerMovementState.Idle;
    }
}
```

--- 

## 🎯 PlayerController

```
void Update()
{
    if (_input.JumpPressed)
        _jumpRequested = true;
}

void FixedUpdate()
{
    _movement.FixedTick(_input.HorizontalInput);

    if (_jumpRequested)
    {
        _jump.TryJump(_movement.Rigidbody,
                      _movement.IsGrounded,
                      _movement.LastFacingDirection);
        _jumpRequested = false;
    }

    _state.UpdateState(_movement.Rigidbody.linearVelocity.x,
                       _movement.IsGrounded);

    SyncAnimator();
}
```

---

# 🎨 Animator 연동
```
private void SyncAnimator()
{
    animator.SetFloat("Speed", Mathf.Abs(_movement.Rigidbody.linearVelocity.x));
    animator.SetBool("IsJumping", _state.CurrentState == PlayerMovementState.Jump);
}
```

---

## ⚙️ Unity 설정 가이드
### GameObject 구성
```
[Player]
 ├── Rigidbody2D
 ├── Collider2D
 ├── PlayerController
 ├── PlayerInputComponent
 ├── PlayerMovementComponent
 ├── PlayerStateComponent
 ├── PlayerJumpComponent
 └── GroundCheck
 
```

## 🎯 핵심 설계
### 점프 방식
- ❌ 수평 힘 추가
- ✅ 현재 속도 유지 + 수직 힘
### 입력 처리
- Update: 입력
- FixedUpdate: 물리

---

## 🚀 확장
```
public class PlayerDashComponent : MonoBehaviour {}
public class PlayerWallJumpComponent : MonoBehaviour {}
```

## 📁 파일 구조
```
Assets/Scripts/Player/
├── PlayerMovementState.cs
├── PlayerInputComponent.cs
├── PlayerMovementComponent.cs
├── PlayerStateComponent.cs
├── PlayerJumpComponent.cs
└── PlayerController.cs
```

## 🎮 조작

| 입력    | 동작     |
| ----- | ------ |
| A / ← | 왼쪽 이동  |
| D / → | 오른쪽 이동 |
| Space | 점프     |

## 💡 배운 점
- Input System 활용
- 자연스러운 점프 구현
- Update vs FixedUpdate 분리
- 컴포넌트 기반 설계

---

## 🔧 개선
- Coyote Time
- Jump Buffer
- Variable Jump
- Dash
- Wall Jump


## 🏷️ 태그

#Unity #2D #InputSystem #ComponentBased #SOLID #GameDev