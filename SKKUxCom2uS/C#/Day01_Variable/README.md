## 1. 변수, 상수

### 변수(Variable)

변수는 프로그램에서 **데이터를 저장하기 위한 메모리 공간**이다.

변수에는 이름과 자료형이 있으며, 저장된 값은 프로그램 실행 중 변경할 수 있다.

C#에서는 다음과 같이 변수를 선언한다.

```csharp
int age = 20;
float height =1 75.5f;
string name = "Kim";
```

기본적인 변수 선언 구조는 다음과 같다.

```
자료형 변수명 = 값;
```

예를 들어 `int age = 20;`에서 다음과 같은 의미를 가진다.

- `int` : 변수에 저장할 데이터의 자료형
- `age` : 변수의 이름
- `20` : 변수에 저장된 값

변수의 값은 이후 변경할 수 있다.

```csharp
int hp = 100;
hp = 80;
hp = 50;
```

---

### 상수(Constant)

상수는 **한 번 값을 지정하면 변경할 수 없는 값**이다.

C#에서는 `const` 키워드를 사용한다.

```csharp
const int MaxLevel = 100;
const float Gravity = 9.8f;
```

다음과 같이 상수의 값을 변경하려 하면 오류가 발생한다.

```csharp
const int MaxLevel = 100;
MaxLevel = 200;// 오류
```

변수와 상수의 가장 큰 차이는 **값을 변경할 수 있는가**이다.

| 구분 | 변수 | 상수 |
| --- | --- | --- |
| 값 변경 | 가능 | 불가능 |
| 선언 | 일반 자료형 | `const` 사용 |
| 예시 | 현재 HP | 최대 레벨, 고정 수치 |

---

## 2. 자료형의 종류

자료형(Data Type)은 **변수가 어떤 종류의 데이터를 저장할 것인지 결정하는 형식**이다.

C#의 대표적인 자료형은 다음과 같다.

### 정수형

소수점이 없는 숫자를 저장한다.

| 자료형 | 크기 | 범위 |
| --- | --- | --- |
| `byte` | 1 Byte | 0 ~ 255 |
| `sbyte` | 1 Byte | -128 ~ 127 |
| `short` | 2 Byte | -32,768 ~ 32,767 |
| `ushort` | 2 Byte | 0 ~ 65,535 |
| `int` | 4 Byte | 약 -21억 ~ 21억 |
| `uint` | 4 Byte | 0 ~ 약 42억 |
| `long` | 8 Byte | 매우 큰 정수 |
| `ulong` | 8 Byte | 매우 큰 양의 정수 |

일반적으로 정수를 사용할 때는 `int`를 가장 많이 사용한다.

```csharp
int hp = 100;
int level = 10;
```

### 실수형

소수점이 있는 숫자를 저장한다.

| 자료형 | 크기 | 특징 |
| --- | --- | --- |
| `float` | 4 Byte | 약 7자리 정밀도 |
| `double` | 8 Byte | 약 15~16자리 정밀도 |
| `decimal` | 16 Byte | 약 28~29자리 정밀도 |

```csharp
float speed = 5.5f;
double distance = 123.456;
decimal money = 1000.50m;
```

C#에서는 `float` 값 뒤에 `f`, C#에서는 실수를 기본적으로 `double` 로 처리한다.  `decimal` 값 뒤에 `m`을 붙인다.

### 문자형

하나의 문자를 저장할 때 `char`를 사용한다.

```csharp
char grade = 'A';
```

`char`는 작은따옴표 `' '`를 사용한다.

### 문자열형

여러 개의 문자를 저장할 때 `string`을 사용한다.

```csharp
string playerName = "Player";
```

`string`은 큰따옴표 `" "`를 사용한다.

### 논리형

참과 거짓을 저장하는 자료형이다.

```csharp
bool isAlive = true;
bool isGameOver = false;
```

게임에서는 조건을 표현할 때 자주 사용한다.

```csharp
bool isJumping = false;
bool isDead = false;
bool hasKey = true;
```

---

## 3. 연산자의 종류

연산자는 변수나 값에 **계산, 비교, 대입 등의 작업을 수행하기 위한 기호**이다.

### 산술 연산자

숫자를 계산할 때 사용한다.

| 연산자 | 의미 | 예 |
| --- | --- | --- |
| `+` | 덧셈 | `10 + 5` |
| `-` | 뺄셈 | `10 - 5` |
| `*` | 곱셈 | `10 * 5` |
| `/` | 나눗셈 | `10 / 5` |
| `%` | 나머지 | `10 % 3` |

```csharp
int a = 10;
int b = 3;
int add = a + b; // 13
int subtract = a - b; // 7
int multiply = a * b; // 30
int divide = a / b; // 3
int remainder = a % b; // 1
```

정수끼리 나눗셈하면 결과 역시 정수가 된다.

```csharp
int result = 10 / 3; // 결과 : 3
```

실수 결과가 필요하면 실수형을 사용한다.

```csharp
float result = 10.0f / 3.0f; // 약 3.333333
```

### 대입 연산자

변수에 값을 저장하거나 계산한 값을 다시 저장한다.

| 연산자 | 의미 |
| --- | --- |
| `=` | 대입 |
| `+=` | 더한 후 대입 |
| `-=` | 뺀 후 대입 |
| `*=` | 곱한 후 대입 |
| `/=` | 나눈 후 대입 |
| `%=` | 나머지를 대입 |

```csharp
int hp = 100;
hp -= 20; // hp = 80
```

`hp -= 20`은 다음 코드와 같다.

```csharp
hp = hp - 20;
```

### 비교 연산자

두 값을 비교하며 결과는 `bool` 값인 `true` 또는 `false`가 된다.

| 연산자 | 의미 |
| --- | --- |
| `==` | 같다 |
| `!=` | 다르다 |
| `>` | 크다 |
| `<` | 작다 |
| `>=` | 크거나 같다 |
| `<=` | 작거나 같다 |

```csharp
int hp = 50;
bool result1 = hp > 0; // true
bool result2 = hp == 0; // false
```

### 논리 연산자

여러 조건을 조합할 때 사용한다.

| 연산자 | 의미 |
| --- | --- |
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

```csharp
int hp = 50;
bool hasKey = true;
bool canEnter = hp > 0 && hasKey;
```

`&&`는 **두 조건이 모두 참일 때 참**이다.

```csharp
true  && true  → true
true  && false → false
false && true  → false
false && false → false
```

`||`는 **둘 중 하나 이상 참이면 참**이다.

```csharp
true  || true  → true
true  || false → true
false || true  → true
false || false → false
```

`!`는 참과 거짓을 반대로 바꾼다.

```csharp
bool isDead = false;
bool isAlive = !isDead; // true
```

### 증감 연산자

값을 1 증가시키거나 감소시킨다.

```csharp
int count = 0;
count++;
count--;
```

다음 코드와 같은 의미를 가진다.

```csharp
count = count + 1; // count++;
count = count - 1; // count--;
```

---

## 4. Bit와 Byte

### Bit

Bit는 **컴퓨터가 데이터를 표현하는 가장 작은 단위**이다.

Bit는 두 가지 값만 표현할 수 있다.

```
0
1
```

즉, 컴퓨터 내부의 모든 데이터는 궁극적으로 `0`과 `1`의 조합으로 표현된다.

### Byte

Byte는 **8개의 Bit를 묶은 단위**이다.

```
1 Byte = 8 Bit
```

예를 들어 1Byte는 다음과 같이 8개의 Bit로 구성된다.

```
00000000
```

8개의 Bit가 각각 `0` 또는 `1`을 가질 수 있으므로 총 경우의 수는 다음과 같다.

```
2^8 = 256
```

따라서 C#의 `byte` 자료형은 다음 범위를 표현한다.

```
0 ~ 255
```

```csharp
byte value = 255;
```

자료형의 크기는 다음과 같이 이해할 수 있다.

```csharp
byte   → 1 Byte → 8 Bit
short  → 2 Byte → 16 Bit
int    → 4 Byte → 32 Bit
long   → 8 Byte → 64 Bit
float  → 4 Byte → 32 Bit
double → 8 Byte → 64 Bit
```

---

## 5. 이진법

이진법(Binary)은 **0과 1 두 개의 숫자를 이용하여 값을 표현하는 방법**이다.

우리가 일상적으로 사용하는 숫자는 10진법이다.

```
0 1 2 3 4 5 6 7 8 9
```

컴퓨터에서는 이진법을 사용한다.

```
0 1
```

이진수의 각 자릿수는 오른쪽부터 `2`의 거듭제곱 값을 가진다.

```
128 64 32 16 8 4 2 1
```

예를 들어 다음 이진수를 살펴본다.

```
00001101
```

각 자리에서 `1`이 있는 값을 더한다.

```csharp
8 + 4 + 1 = 13
```

따라서 다음과 같다.

```
00001101₂ = 13₁₀
```

또 다른 예로 `10`을 이진수로 표현하면 다음과 같다.

```csharp
10 = 8 + 2

00001010
```

즉,

```
10진수 10 → 이진수 1010
```

---

## 6. float와 double의 차이

`float`와 `double`은 모두 **소수점이 있는 실수를 표현하기 위한 부동소수점 자료형**이다. 두 자료형의 가장 큰 차이는 **메모리 크기와 정밀도**이다.

### float

`float`는 **32Bit 부동소수점 자료형**이다.

```csharp
float value=3.14f;
```

C#의 `float`는 32Bit를 사용하며 크게 다음 세 부분으로 구성된다.

```csharp
[부호부] [지수부] [가수부]
```

32Bit `float`의 구조는 다음과 같다.

```csharp
부호부 : 1 Bit
지수부 : 8 Bit
가수부 : 23 Bit
```

개념적으로 다음과 같은 형태로 숫자를 표현한다.

```
가수 × 2^지수
```

예를 들어 이진수 `1010.1`이 있다고 하면 다음과 같이 정규화할 수 있다.

```
1010.1

→ 1.0101 × 2³
```

여기에서

```
1.0101 → 가수
3      → 지수
```

라고 이해할 수 있다.

`float`는 약 **7자리의 유효 자릿수**를 표현할 수 있다.

```csharp
float value = 123.4567f;
```

메모리 사용량이 비교적 적고 연산이 빠르기 때문에 Unity에서는 위치, 회전, 이동속도와 같은 대부분의 실수 계산에 `float`를 사용한다.

```csharp
float moveSpeed = 5.0f;
Vector3 position = new Vector3(1.5f,2.0f,3.5f);
```

---

### double

`double`은 **64Bit 부동소수점 자료형**이다.

```csharp
double value = 3.14;
```

C#의 `double`은 64Bit를 사용하며 `float`와 마찬가지로 다음 세 부분으로 구성된다.

```
[부호부] [지수부] [가수부]
```

64Bit `double`의 구조는 다음과 같다.

```csharp
부호부 : 1 Bit
지수부 : 11 Bit
가수부 : 52 Bit
```

`float`보다 지수부와 가수부에 더 많은 Bit를 사용하기 때문에 **더 큰 범위의 숫자와 더 높은 정밀도**를 표현할 수 있다.

`double`은 약 **15~16자리의 유효 자릿수**를 표현할 수 있다.

```csharp
double value = 123.456789012345;
```

C#에서 소수점이 포함된 숫자 리터럴은 기본적으로 `double`로 취급한다.

```csharp
double a = 3.14; // 가능
float b = 3.14f; // f 필요
```

따라서 다음과 같이 작성하면 오류가 발생한다.

```csharp
float value = 3.14; // 오류
```

`3.14`가 기본적으로 `double`이기 때문이다. `float`로 사용하려면 `f`를 붙여야 한다.

```csharp
float value = 3.14f;
```

---

### 부동소수점의 오차

`float`와 `double` 모두 **이진 부동소수점 방식**을 사용한다.

따라서 `0.1`, `0.2`와 같은 일부 10진수 실수를 이진수로 정확하게 표현할 수 없다.

```csharp
float a = 0.1f;
float b = 0.2f;
float result = a + b;
```

내부적으로는 정확한 `0.3`이 아니라 `0.3`에 매우 가까운 값이 저장될 수 있다.

`double`도 같은 문제가 발생한다.

```csharp
double a = 0.1;
double b = 0.2;
double result = a + b;
```

즉, `double`이라고 해서 부동소수점 오차가 사라지는 것은 아니다. 다만 `float`보다 가수부가 더 크기 때문에 **더 높은 정밀도로 값을 표현하여 오차가 상대적으로 작다.**

따라서 부동소수점 값을 `==`로 직접 비교하는 것은 주의해야 한다.

---

### float와 double 비교

| 구분 | `float` | `double` |
| --- | --- | --- |
| 크기 | 4 Byte | 8 Byte |
| Bit 수 | 32 Bit | 64 Bit |
| 부호부 | 1 Bit | 1 Bit |
| 지수부 | 8 Bit | 11 Bit |
| 가수부 | 23 Bit | 52 Bit |
| 정밀도 | 약 7자리 | 약 15~16자리 |
| 표현 방식 | 이진 부동소수점 | 이진 부동소수점 |
| 메모리 사용량 | 적음 | `float`보다 많음 |
| 주요 용도 | 게임, 그래픽, 물리 | 높은 정밀도가 필요한 계산 |

---

### Unity에서 float를 주로 사용하는 이유

Unity에서는 대부분의 실수 자료형으로 `float`를 사용한다.

예를 들어 `Vector3`의 `x`, `y`, `z` 값도 모두 `float`이다.

```csharp
Vector3 position = new Vector3(1.0f, 2.0f, 3.0f);
```

게임에서 사용하는 위치, 속도, 회전 등의 값은 일반적으로 `double` 수준의 높은 정밀도가 필요하지 않다.

따라서 메모리 사용량이 적고 게임 엔진과 그래픽 연산에서 일반적으로 사용되는 `float`가 적합하다.

반면 매우 큰 좌표계나 높은 수치 정밀도가 필요한 계산에서는 `double`을 고려할 수 있다.

### 핵심 정리

```csharp
float
→ 32 Bit 부동소수점
→ 부호부 1 Bit + 지수부 8 Bit + 가수부 23 Bit
→ 약 7자리 정밀도
→ 4 Byte
→ 숫자 뒤에 f를 붙임
→ Unity의 위치, 속도, 회전 등에 주로 사용

double
→ 64 Bit 부동소수점
→ 부호부 1 Bit + 지수부 11 Bit + 가수부 52 Bit
→ 약 15~16자리 정밀도
→ 8 Byte
→ C#에서 실수 리터럴의 기본 자료형
→ float보다 높은 정밀도가 필요한 계산에 사용

공통점
→ 둘 다 이진 부동소수점 방식
→ 둘 다 부호부 + 지수부 + 가수부로 구성
→ 둘 다 부동소수점 오차가 발생할 수 있음
```