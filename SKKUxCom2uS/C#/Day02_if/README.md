## 1. 조건문 `if`

조건문은 **주어진 조건에 따라 서로 다른 코드를 실행하기 위해 사용하는 문법**이다.

C#에서는 주로 `if`, `else if`, `else`를 사용한다.

### 기본 구조

```csharp
if (조건식)
{
    // 조건이 true일 때 실행
}
else if (다른 조건식)
{
    // 앞의 조건은 false이고
    // 현재 조건이 true일 때 실행
}
else
{
    // 모든 조건이 false일 때 실행
}
```

조건식의 결과는 반드시 `bool` 타입인 `true` 또는 `false`가 되어야 한다.

```csharp
int age = 20;

if (age >= 20)
{
    Console.WriteLine("성인");
}
else
{
    Console.WriteLine("미성년자");
}
```

### 여러 조건 사용

논리 연산자를 이용하면 여러 조건을 조합할 수 있다.

```csharp
int age = 25;
bool hasTicket = true;

if (age >= 20 && hasTicket)
{
    Console.WriteLine("입장 가능");
}
```

주요 논리 연산자는 다음과 같다.

| 연산자 | 의미 |
| --- | --- |
| `&&` | AND, 두 조건이 모두 참 |
| `||` | OR, 둘 중 하나 이상 참 |
| `!` | NOT, 조건을 반대로 변경 |

### 중첩 `if`

`if`문 내부에 또 다른 `if`문을 작성할 수도 있다.

```csharp
int level = 10;
int hp = 50;

if (level >= 10)
{
    if (hp > 0)
    {
        Console.WriteLine("전투 가능");
    }
}
```

다만 중첩이 너무 깊어지면 코드의 가독성이 떨어지므로 가능한 한 조건을 단순하게 구성하는 것이 좋다.

---

# 2. 열거형 `enum`

`enum`은 **서로 연관된 상수들을 하나의 타입으로 묶어서 관리하기 위한 자료형**이다.

숫자 자체보다는 **의미가 있는 이름을 사용하고 싶을 때** 유용하다.

예를 들어 플레이어의 상태를 숫자로 표현하면 다음과 같이 작성할 수 있다.

```csharp
int playerState = 0;
```

하지만 `0`이 어떤 상태인지 코드만 보고 바로 알기 어렵다.

`enum`을 사용하면 다음과 같이 표현할 수 있다.

```csharp
enum PlayerState
{
    Idle,
    Move,
    Attack,
    Dead
}
```

사용할 때는 다음과 같이 작성한다.

```csharp
PlayerState state = PlayerState.Idle;

if (state == PlayerState.Idle)
{
    Console.WriteLine("대기 상태");
}
```

이렇게 하면 숫자를 직접 사용하는 것보다 코드의 의미를 훨씬 쉽게 파악할 수 있다.

## enum의 내부 값

`enum`은 내부적으로 정수 값을 가진다.

기본적으로 첫 번째 요소는 `0`부터 시작한다.

```csharp
enum PlayerState
{
    Idle,       // 0
    Move,       // 1
    Attack,     // 2
    Dead        // 3
}
```

직접 값을 지정할 수도 있다.

```csharp
enum ItemGrade
{
    Normal = 1,
    Rare = 2,
    Epic = 3,
    Legendary = 4
}
```

정수로 변환하면 내부 값을 확인할 수 있다.

```csharp
ItemGrade grade = ItemGrade.Epic;

Console.WriteLine((int)grade);
```

출력:

```
3
```

### 게임 개발에서의 활용

게임에서는 상태나 종류를 구분할 때 `enum`을 자주 사용한다.

```csharp
enum CharacterState
{
    Idle,
    Walk,
    Run,
    Attack,
    Dead
}
```

```csharp
enum WeaponType
{
	Sword,
	Bow,
	Staff
}
```

```csharp
enum EnemyType
{
    Normal,
    Elite,
    Boss
}
```

---

# 3. 분기문 `switch-case`

`switch`문은 **하나의 값에 따라 여러 실행 경로로 분기할 때 사용하는 문법**이다.

여러 개의 값과 비교하는 `if-else if`문을 더 읽기 쉽게 표현할 수 있다.

> Python에는 전통적인 형태의 `switch-case` 문법이 없으며, Python 3.10부터는 비슷한 역할을 하는 `match-case`가 존재한다.
> 

### 기본 구조

```csharp
switch (값)
{
    case 값1:
        // 실행 코드
        break;

    case 값2:
        // 실행 코드
        break;

    default:
        // 어떤 case에도 해당하지 않을 때 실행
        break;
}
```

예를 들어 다음과 같이 사용할 수 있다.

```csharp
int number = 2;

switch (number)
{
    case 1:
        Console.WriteLine("하나");
        break;

    case 2:
        Console.WriteLine("둘");
        break;

    case 3:
        Console.WriteLine("셋");
        break;

    default:
        Console.WriteLine("알 수 없는 숫자");
        break;
}
```

## `break`

C#의 `switch`에서는 일반적으로 각 `case`의 실행을 끝내기 위해 `break`를 작성한다.

```csharp
case 1:
    Console.WriteLine("1");
    break;
```

`break`가 없으면 다음과 같은 컴파일 오류가 발생할 수 있다.

```csharp
Control cannot fall through from one case label to another
```

즉, C#에서는 한 `case`의 실행이 그대로 다음 `case`로 넘어가는 것을 허용하지 않는다.

## `default`

어떤 `case`에도 해당하지 않는 경우 실행한다.

```csharp
switch (command)
{
    case "Attack":
        Console.WriteLine("공격");
        break;

    case "Run":
        Console.WriteLine("도망");
        break;

    default:
        Console.WriteLine("알 수 없는 명령");
        break;
}
```

## enum과 switch의 조합

`enum`과 `switch`는 게임 개발에서 함께 사용하는 경우가 많다.

```csharp
enum PlayerState
{
    Idle,
    Move,
    Attack
}

PlayerState state = PlayerState.Attack;

switch (state)
{
    case PlayerState.Idle:
        Console.WriteLine("대기");
        break;

    case PlayerState.Move:
        Console.WriteLine("이동");
        break;

    case PlayerState.Attack:
        Console.WriteLine("공격");
        break;
}
```

플레이어 상태, 몬스터 AI, 게임 상태 등을 처리할 때 활용할 수 있다.

---

# 4. 문자열 `string`

`string`은 **문자들의 집합인 문자열을 저장하는 자료형**이다.

C#에서는 문자열을 큰따옴표 `""`로 표현한다.

```csharp
string name = "Player";
string message = "Hello World";
```

반면 하나의 문자는 `char`를 사용하며 작은따옴표 `''`로 표현한다.

```csharp
char grade = 'A';
```

즉,

```csharp
char c = 'A';
string str = "A";
```

는 서로 다른 자료형이다.

## 문자열 연결

`+` 연산자를 사용하여 문자열을 연결할 수 있다.

```csharp
string name = "Kim";
int level = 10;

string message = "이름: " + name + ", 레벨: " + level;

Console.WriteLine(message);
```

출력:

```csharp
이름: Kim, 레벨: 10
```

## 문자열 보간

C#에서는 `$`를 이용한 **문자열 보간(String Interpolation)**을 사용할 수 있다.

```csharp
string name = "Kim";
int level = 10;

Console.WriteLine($"이름: {name}, 레벨: {level}");
```

문자열 연결보다 읽기 쉬워 자주 사용한다.

## 자주 사용하는 문자열 기능

### Length

문자열의 길이를 반환한다.

```csharp
string text = "Hello";

Console.WriteLine(text.Length);
```

출력:

```csharp
5
```

### Contains()

특정 문자열이 포함되어 있는지 확인한다.

```csharp
string text = "Hello World";

Console.WriteLine(text.Contains("World"));
```

```csharp
True
```

### Replace()

문자열의 특정 부분을 다른 문자열로 변경한다.

```csharp
string text = "Hello World";

string result = text.Replace("World", "C#");

Console.WriteLine(result);
```

```csharp
Hello C#
```

### Split()

특정 문자를 기준으로 문자열을 나눈다.

```csharp
string text = "Apple,Banana,Orange";

string[] fruits = text.Split(',');
```

결과는 다음과 같다.

```csharp
Apple
Banana
Orange
```

---

# 5. `object`

`object`는 C#에서 **모든 자료형의 최상위 기본 타입**이다.

따라서 거의 모든 값을 `object` 변수에 저장할 수 있다.

```csharp
object a = 10;
object b = 3.14;
object c = "Hello";
object d = true;
```

다음과 같이 서로 다른 타입의 값을 저장할 수 있다.

```csharp
object value;

value = 10;
value = "Hello";
value = true;
```

하지만 `object`로 저장하면 원래 타입의 기능을 바로 사용할 수 없기 때문에 다시 원래 타입으로 변환해야 하는 경우가 있다.

---

# 6. 박싱(Boxing)과 언박싱(Unboxing)

C#에는 크게 **값 형식(Value Type)**과 **참조 형식(Reference Type)**이 존재한다.

대표적인 값 형식은 다음과 같다.

```csharp
int
float
double
bool
char
enum
struct
```

`object`는 참조 형식이다.

값 형식 데이터를 `object` 타입으로 변환하는 과정을 **박싱(Boxing)**이라고 한다.

## 박싱

```csharp
int number = 10;

object obj = number;
```

개념적으로 다음과 같은 변환이 발생한다.

```csharp
int
 ↓
object

값 형식 → 참조 형식
```

이를 박싱이라고 한다.

```csharp
int number = 10;
object obj = number;
```

`number`의 값을 `object`가 사용할 수 있는 형태로 감싸서 저장한다고 생각할 수 있다.

---

## 언박싱

`object` 안에 들어 있는 값을 다시 원래 값 형식으로 꺼내는 것을 **언박싱(Unboxing)**이라고 한다.

```csharp
object obj = 10;

int number = (int)obj;
```

개념적으로는 다음과 같다.

```csharp
object
 ↓
int

참조 형식 → 값 형식
```

### 박싱과 언박싱 예제

```csharp
int number = 100;

// Boxing
object obj = number;

// Unboxing
int result = (int)obj;

Console.WriteLine(result);
```

출력:

```csharp
100
```

## 언박싱 시 주의점

언박싱할 때는 **박싱하기 전의 실제 타입과 정확하게 일치해야 한다.**

```csharp
object obj = 10;

int number = (int)obj;
```

이 코드는 정상적으로 동작한다.

하지만 다음 코드는 문제가 발생한다.

```csharp
object obj = 10;

double number = (double)obj;
```

`obj` 안에 실제로 들어 있는 데이터가 `int`이므로 바로 `double`로 언박싱할 수 없다.

필요하다면 먼저 원래 타입으로 언박싱한 뒤 변환해야 한다.

```csharp
object obj = 10;

int value = (int)obj;
double number = value;
```

---

# 7. 박싱·언박싱의 성능 문제

박싱과 언박싱에는 추가적인 작업이 필요하기 때문에 일반적인 값 형식 연산보다 비용이 발생한다.

예를 들어 반복문에서 계속 박싱이 발생한다면 불필요한 메모리 할당과 성능 저하가 발생할 수 있다.

```csharp
for (int i = 0; i < 10000; i++)
{
    object obj = i;
}
```

따라서 타입을 알고 있다면 가능하면 정확한 자료형을 사용하는 것이 좋다.

```csharp
int value = 10;
```

가 일반적으로

```csharp
object value = 10;
```

보다 적절하다.

특히 게임에서는 매 프레임 반복되는 코드에서 불필요한 메모리 할당이 발생하면 **Garbage Collection(GC)**과 연결되어 프레임 드랍의 원인이 될 수 있으므로 주의해야 한다.

---

# 8. 전체 개념 연결

3일차에 배운 내용은 서로 독립적인 개념처럼 보이지만 게임 프로그램에서는 함께 사용되는 경우가 많다.

예를 들어 플레이어 상태를 처리한다고 가정한다.

```csharp
enum PlayerState
{
    Idle,
    Move,
    Attack,
    Dead
}

PlayerState state = PlayerState.Attack;

switch (state)
{
    case PlayerState.Idle:
        Console.WriteLine("플레이어가 대기 중이다.");
        break;

    case PlayerState.Move:
        Console.WriteLine("플레이어가 이동 중이다.");
        break;

    case PlayerState.Attack:
        Console.WriteLine("플레이어가 공격한다.");
        break;

    case PlayerState.Dead:
        Console.WriteLine("플레이어가 사망했다.");
        break;
}
```

여기에 조건문을 추가할 수도 있다.

```csharp
int hp = 0;

if (hp <= 0)
{
    state = PlayerState.Dead;
}
```

결국 다음과 같은 형태로 연결된다.

```csharp
데이터
 ↓
조건 판단
 ↓
상태 변경
 ↓
상태에 따른 분기
 ↓
행동 실행
```

게임 코드에서는 이를 다음과 같이 대응해서 생각할 수 있다.

```csharp
if
→ 조건을 판단한다.

enum
→ 상태나 종류를 정의한다.

switch
→ 상태에 따라 행동을 나눈다.

string
→ 이름, 메시지 등의 문자 데이터를 저장한다.

object
→ 여러 타입을 포괄할 수 있는 최상위 타입이다.

Boxing / Unboxing
→ 값 형식과 object 사이에서 변환이 일어난다.
```

## 핵심 정리

| 개념 | 핵심 |
| --- | --- |
| `if` | 조건의 참/거짓에 따라 코드를 실행한다. |
| `enum` | 관련된 상수들을 이름으로 묶어서 관리한다. |
| `switch-case` | 하나의 값에 따라 여러 실행 경로로 분기한다. |
| `string` | 문자열 데이터를 저장한다. |
| `object` | C# 모든 타입의 최상위 기본 타입이다. |
| Boxing | 값 형식을 `object` 등의 참조 형식으로 변환한다. |
| Unboxing | `object`에 들어 있는 값을 원래 값 형식으로 꺼낸다. |

특히 **`enum + switch`는 Unity에서 상태 관리에 매우 자주 사용되므로 3일차 내용 중에서는 우선순위를 높여 익혀두는 것이 좋다.**