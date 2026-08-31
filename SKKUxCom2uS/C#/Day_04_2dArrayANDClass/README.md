# 5일차 학습 정리

# 2차원 배열과 클래스

## 1. 2차원 배열

2차원 배열은 데이터를 **행(Row)과 열(Column)** 형태로 저장하는 배열이다.

표나 좌표, 게임 맵과 같이 데이터를 격자 형태로 관리할 때 유용하다.

```csharp
int[,] numbers = new int[3, 4];
```

위 배열은 다음과 같은 구조를 가진다.

```
        열(Column)
        0   1   2   3
행  0  [ ] [ ] [ ] [ ]
    1  [ ] [ ] [ ] [ ]
    2  [ ] [ ] [ ] [ ]
```

즉,

```csharp
new int[3, 4]
```

는

```
3행 4열
```

을 의미한다.

---

## 2. 2차원 배열 선언

### 선언 후 크기 지정

```csharp
int[,] array = new int[3, 4];
```

### 선언과 동시에 값 초기화

```csharp
int[,] array =
{
    { 1, 2, 3 },
    { 4, 5, 6 },
    { 7, 8, 9 }
};
```

구조는 다음과 같다.

```
1 2 3
4 5 6
7 8 9
```

즉 3행 3열 배열이다.

---

## 3. 2차원 배열 접근

2차원 배열은 다음과 같이 접근한다.

```csharp
array[행, 열]
```

예를 들어,

```csharp
int[,] array =
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};

Console.WriteLine(array[0, 0]); // 1
Console.WriteLine(array[0, 2]); // 3
Console.WriteLine(array[1, 1]); // 5
```

따라서 일반적으로 다음처럼 기억하면 된다.

```
i → Row → 행
j → Column → 열
```

```csharp
array[i, j]
```

---

## 4. 2차원 배열의 길이

1차원 배열에서는 `Length`만 사용하면 되지만, 2차원 배열에서는 각 차원의 크기를 구하기 위해 `GetLength()`를 사용한다.

```csharp
int[,] array = new int[3, 5];

Console.WriteLine(array.GetLength(0));
Console.WriteLine(array.GetLength(1));
```

결과

```
3
5
```

### 의미

```csharp
array.GetLength(0)
```

첫 번째 차원의 길이 → **행의 개수**

```csharp
array.GetLength(1)
```

두 번째 차원의 길이 → **열의 개수**

따라서 반복문에서는 다음과 같이 사용한다.

```csharp
for (int i = 0; i < array.GetLength(0); i++)
{
    for (int j = 0; j < array.GetLength(1); j++)
    {
        Console.WriteLine(array[i, j]);
    }
}
```

---

## 5. Length와 GetLength()

2차원 배열에서도 `Length`를 사용할 수 있다.

다만 `Length`는 **전체 원소의 개수**를 반환한다.

```csharp
int[,] array = new int[3, 4];

Console.WriteLine(array.Length);
```

결과

```
12
```

즉,

```
Length
→ 전체 원소 개수

GetLength(0)
→ 행의 개수

GetLength(1)
→ 열의 개수
```

이다.

---

# 객체지향 프로그래밍

## 6. 객체지향 프로그래밍이란?

객체지향 프로그래밍(Object-Oriented Programming, OOP)은 프로그램을 여러 개의 **객체(Object)**로 나누어 설계하는 프로그래밍 방식이다.

객체는 일반적으로

```
데이터 + 기능
```

을 함께 가진다.

예를 들어 게임의 `Player`를 생각하면 다음과 같다.

```
Player

데이터
- 이름
- 체력
- 공격력
- 이동속도

기능
- 이동
- 공격
- 피격
- 사망
```

C#에서는 이러한 객체를 만들기 위한 설계도로 **클래스(Class)**를 사용한다.

---

# 객체지향의 주요 개념

## 7. 추상화

추상화(Abstraction)는 객체에서 필요한 핵심적인 특징만 뽑아내어 표현하는 것이다.

현실의 모든 정보를 프로그램에 구현할 필요는 없다.

예를 들어 게임에서 자동차를 구현한다고 생각한다.

현실의 자동차에는 수많은 정보가 존재한다.

```
엔진 구조
연료 분사 방식
브레이크 구조
타이어 재질
차량 무게
제조 공정
...
```

하지만 레이싱 게임에서는 다음 정도만 필요할 수 있다.

```csharp
class Car
{
    public float speed;
    public float acceleration;

    public void Move()
    {
    }

    public void Brake()
    {
    }
}
```

즉,

> 프로그램에서 필요한 특징만 선택해서 모델링하는 것이 추상화다.
> 

---

## 8. 캡슐화

캡슐화(Encapsulation)는 **관련된 데이터와 기능을 하나의 객체 안에 묶는 것**이다.

예를 들어 플레이어의 체력과 데미지 처리 기능을 하나의 클래스에 넣는다.

```csharp
class Player
{
    int hp = 100;

    public void TakeDamage(int damage)
    {
        hp -= damage;
    }
}
```

`hp`라는 데이터와 `TakeDamage()`라는 기능이 `Player` 클래스 안에 함께 들어 있다.

즉,

```
데이터
+
데이터를 처리하는 기능
=
하나의 객체
```

로 묶는 개념이다.

---

## 9. 은닉화

은닉화(Information Hiding)는 객체 내부의 데이터를 외부에서 마음대로 접근하거나 수정하지 못하도록 제한하는 것이다.

접근 제한자를 사용하여 구현할 수 있다.

예를 들어 다음 코드는 문제가 발생할 수 있다.

```csharp
class Player
{
    public int hp = 100;
}
```

외부에서 다음과 같은 코드가 가능하기 때문이다.

```csharp
player.hp = -999999;
```

따라서 중요한 데이터는 외부에서 직접 접근하지 못하게 제한한다.

```csharp
class Player
{
    private int hp = 100;

    public void TakeDamage(int damage)
    {
        hp -= damage;

        if (hp < 0)
        {
            hp = 0;
        }
    }
}
```

외부에서는

```csharp
player.TakeDamage(10);
```

처럼 정해진 방법을 통해서만 데이터를 변경하게 만든다.

### 정리

```
캡슐화
→ 데이터와 기능을 하나로 묶는다.

은닉화
→ 내부 데이터를 외부에서 함부로 접근하지 못하게 한다.
```

두 개념은 서로 관련이 있지만 정확히 같은 의미는 아니다.

---

# 클래스

## 10. 클래스란?

클래스(Class)는 **객체를 만들기 위한 설계도**다.

예를 들어 다음과 같은 클래스가 있다고 하자.

```csharp
class Player
{
    public string name;
    public int hp;

    public void Attack()
    {
        Console.WriteLine("공격!");
    }
}
```

이 클래스 자체가 실제 플레이어 객체는 아니다.

`Player`라는 객체를 어떻게 만들 것인지 정의한 **설계도**다.

객체를 생성하려면 `new`를 사용한다.

```csharp
Player player = new Player();
```

이렇게 만들어진 `player`를 **인스턴스(Instance)**라고 한다.

### 관계

```
클래스
↓
객체를 만들기 위한 설계도

new
↓
객체 생성

인스턴스
↓
실제로 생성된 객체
```

---

# 필드

## 11. 필드(Field)

필드는 클래스 내부에서 선언된 변수다.

객체가 가지고 있는 데이터를 저장한다.

```csharp
class Player
{
    public string name;
    public int hp;
    public int attackPower;
}
```

여기서

```csharp
name
hp
attackPower
```

가 필드다.

객체를 만들면 각각의 객체가 자신의 필드 값을 가질 수 있다.

```csharp
Player player1 = new Player();
Player player2 = new Player();

player1.hp = 100;
player2.hp = 200;
```

```
player1
hp = 100

player2
hp = 200
```

같은 클래스로 만들었더라도 각각 별개의 객체다.

---

# 메서드

## 12. 메서드(Method)

메서드는 클래스 내부에서 특정 기능이나 행동을 정의한 함수다.

```csharp
class Player
{
    public int hp;

    public void Attack()
    {
        Console.WriteLine("공격한다.");
    }

    public void TakeDamage(int damage)
    {
        hp -= damage;
    }
}
```

사용 방법

```csharp
Player player = new Player();

player.Attack();
player.TakeDamage(10);
```

객체지향적으로 생각하면

```
필드
→ 객체가 가지고 있는 상태 / 데이터

메서드
→ 객체가 수행할 수 있는 행동
```

이라고 볼 수 있다.

---

# 메서드 오버로딩

## 13. 메서드 오버로딩(Method Overloading)

메서드 오버로딩은 **같은 이름의 메서드를 여러 개 정의하는 것**이다.

단, 매개변수의 개수나 자료형이 달라야 한다.

```csharp
class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }

    public float Add(float a, float b)
    {
        return a + b;
    }
}
```

사용할 때 전달되는 매개변수에 따라 적절한 메서드가 선택된다.

```csharp
Calculator calculator = new Calculator();

calculator.Add(1, 2);
calculator.Add(1, 2, 3);
calculator.Add(1.5f, 2.5f);
```

### 중요한 점

반환형만 다른 것은 오버로딩이 아니다.

다음 코드는 사용할 수 없다.

```csharp
int Test(int value)
{
    return value;
}

float Test(int value)
{
    return value;
}
```

매개변수가 완전히 동일하기 때문에 컴파일러가 어떤 메서드를 호출해야 할지 구분할 수 없다.

---

# 생성자

## 14. 생성자(Constructor)

생성자는 객체가 생성될 때 자동으로 호출되는 특별한 메서드다.

주로 객체의 초기값을 설정할 때 사용한다.

생성자의 이름은 **클래스 이름과 동일하다.**

```csharp
class Player
{
    public string name;
    public int hp;

    public Player()
    {
        name = "Player";
        hp = 100;
    }
}
```

객체를 생성하면

```csharp
Player player = new Player();
```

생성자가 자동으로 호출된다.

---

## 15. 매개변수가 있는 생성자

생성자에도 매개변수를 사용할 수 있다.

```csharp
class Player
{
    public string name;
    public int hp;

    public Player(string playerName, int playerHp)
    {
        name = playerName;
        hp = playerHp;
    }
}
```

객체 생성

```csharp
Player player = new Player("Knight", 100);
```

결과

```
name = "Knight"
hp = 100
```

생성자도 메서드처럼 **오버로딩**할 수 있다.

```csharp
class Player
{
    public string name;
    public int hp;

    public Player()
    {
        name = "Player";
        hp = 100;
    }

    public Player(string playerName)
    {
        name = playerName;
        hp = 100;
    }

    public Player(string playerName, int playerHp)
    {
        name = playerName;
        hp = playerHp;
    }
}
```

---

# 접근 제한자

## 16. 접근 제한자(Access Modifier)

접근 제한자는 클래스나 필드, 메서드 등에 **어디에서 접근할 수 있는지**를 지정한다.

대표적으로 다음이 있다.

| 접근 제한자 | 의미 |
| --- | --- |
| `public` | 어디에서든 접근 가능 |
| `private` | 해당 클래스 내부에서만 접근 가능 |
| `protected` | 해당 클래스와 상속받은 클래스에서 접근 가능 |
| `internal` | 같은 Assembly 내부에서 접근 가능 |

초기 학습 단계에서는 우선

```
public
private
```

를 확실하게 이해하는 것이 중요하다.

---

## 17. public

외부에서도 접근할 수 있다.

```csharp
class Player
{
    public int hp = 100;
}
```

```csharp
Player player = new Player();

player.hp = 50;
```

가능하다.

---

## 18. private

해당 클래스 내부에서만 접근할 수 있다.

```csharp
class Player
{
    private int hp = 100;
}
```

외부에서

```csharp
player.hp = 50;
```

로 접근할 수 없다.

대신 메서드를 통해 접근하도록 만들 수 있다.

```csharp
class Player
{
    private int hp = 100;

    public void TakeDamage(int damage)
    {
        hp -= damage;
    }
}
```

이러한 방식을 통해 객체의 내부 상태를 보호할 수 있다.

---

# this

## 19. this 키워드

`this`는 **현재 객체 자기 자신**을 의미한다.

예를 들어 다음 코드가 있다.

```csharp
class Player
{
    private string name;

    public Player(string name)
    {
        this.name = name;
    }
}
```

여기에는 이름이 같은 두 변수가 있다.

```csharp
private string name;
```

클래스의 필드

그리고

```csharp
string name
```

생성자의 매개변수다.

따라서

```csharp
this.name
```

은 현재 객체의 필드 `name`을 의미한다.

```csharp
name
```

은 생성자로 들어온 매개변수를 의미한다.

즉,

```csharp
this.name = name;
```

은

```
현재 객체의 name 필드
=
전달받은 name 값
```

이라는 의미다.

---

## 20. this의 의미

다음과 같은 객체가 있다고 생각한다.

```csharp
Player player1 = new Player("Knight");
Player player2 = new Player("Wizard");
```

`player1`의 생성자에서 `this`는 `player1`을 가리킨다.

`player2`의 생성자에서 `this`는 `player2`를 가리킨다.

즉,

> `this`는 현재 해당 코드를 실행하고 있는 객체 자신을 가리킨다.
> 

---

# null

## 21. null이란?

`null`은 **참조하고 있는 객체가 없다**는 것을 의미한다.

예를 들어 다음 코드에서

```csharp
Player player = null;
```

`player`라는 변수는 존재하지만 실제 `Player` 객체를 가리키고 있지 않다.

```
player
  ↓
null

가리키는 객체 없음
```

반면

```csharp
Player player = new Player();
```

은 실제 객체를 생성하고 해당 객체를 참조한다.

```
player
  ↓
Player 객체
```

---

## 22. NullReferenceException

`null` 상태인 변수에서 필드나 메서드에 접근하면 오류가 발생한다.

```csharp
Player player = null;

player.Attack();
```

실행하면 대표적으로 다음 예외가 발생한다.

```
NullReferenceException
```

즉,

> 참조할 객체가 존재하지 않는데 객체의 기능이나 데이터를 사용하려고 했다는 의미다.
> 

Unity에서도 매우 자주 만나게 되는 오류다.

예를 들어

```csharp
GameObject target;

target.SetActive(false);
```

에서 `target`에 아무 객체도 할당되지 않았다면 `NullReferenceException`이 발생할 수 있다.

---

# 값 형식 VS 참조 형식

## 23. 값 형식(Value Type)

값 형식은 변수 자체가 **실제 값**을 저장한다.

대표적인 값 형식은 다음과 같다.

```
int
float
double
bool
char
struct
enum
```

예를 들어

```csharp
int a = 10;
int b = a;
```

메모리 개념을 단순화하면 다음과 같다.

```
a → 10
b → 10
```

`a`의 값이 `b`에 **복사**된다.

따라서

```csharp
b = 20;
```

으로 변경해도

```
a = 10
b = 20
```

이 된다.

```csharp
int a = 10;
int b = a;

b = 20;

Console.WriteLine(a); // 10
Console.WriteLine(b); // 20
```

두 변수는 서로 독립적이다.

---

# 참조 형식

## 24. 참조 형식(Reference Type)

참조 형식 변수는 객체의 실제 데이터를 직접 저장하는 것이 아니라 **객체를 가리키는 참조**를 저장한다.

대표적인 참조 형식은 다음과 같다.

```
class
string
array
object
delegate
```

예를 들어 클래스를 만들어 본다.

```csharp
class Player
{
    public int hp;
}
```

객체를 생성한다.

```csharp
Player player1 = new Player();

player1.hp = 100;
```

그리고 다음과 같이 대입한다.

```csharp
Player player2 = player1;
```

이때 새로운 `Player` 객체가 만들어지는 것이 아니다.

`player1`과 `player2`가 **같은 객체를 참조한다.**

```
player1 ─┐
         ↓
      Player 객체
        hp = 100
         ↑
player2 ─┘
```

따라서

```csharp
player2.hp = 50;
```

으로 수정하면

```csharp
Console.WriteLine(player1.hp);
```

결과도

```
50
```

이 된다.

둘이 같은 객체를 바라보고 있기 때문이다.

---

# 25. 값 형식과 참조 형식 비교

### 값 형식

```csharp
int a = 10;
int b = a;

b = 20;
```

결과

```
a = 10
b = 20
```

구조

```
a → 10

b → 20
```

각자 자신의 값을 가진다.

---

### 참조 형식

```csharp
Player a = new Player();
a.hp = 100;

Player b = a;

b.hp = 20;
```

구조

```
a ─┐
   ↓
Player 객체
hp = 20
   ↑
b ─┘
```

따라서

```
a.hp = 20
b.hp = 20
```

이 된다.

---

## 26. 배열도 참조 형식이다

배열도 참조 형식이라는 점이 중요하다.

```csharp
int[] array1 = { 1, 2, 3 };

int[] array2 = array1;
```

새로운 배열이 복사되는 것이 아니다.

```
array1 ─┐
        ↓
     [1, 2, 3]
        ↑
array2 ─┘
```

따라서

```csharp
array2[0] = 100;
```

으로 수정하면

```csharp
Console.WriteLine(array1[0]);
```

결과 역시

```
100
```

이 된다.

---

## 27. 배열을 실제로 복사하려면

독립적인 배열을 만들고 싶다면 실제 데이터를 복사해야 한다.

예를 들어 `Clone()`을 사용할 수 있다.

```csharp
int[] array1 = { 1, 2, 3 };

int[] array2 = (int[])array1.Clone();

array2[0] = 100;

Console.WriteLine(array1[0]); // 1
Console.WriteLine(array2[0]); // 100
```

이 경우 서로 다른 배열을 사용한다.

```
array1 → [1, 2, 3]

array2 → [100, 2, 3]
```

---

# 28. string은 조금 특별하다

`string`은 **참조 형식**이다.

```csharp
string str = "Hello";
```

하지만 문자열은 **불변(Immutable)**이라는 특징을 가지고 있다.

즉, 생성된 문자열 자체를 변경할 수 없다.

```csharp
string str = "Hello";

str += " World";
```

겉보기에는 기존 문자열에 `" World"`가 추가된 것처럼 보인다.

실제로는 새로운 문자열 객체가 만들어지고 `str`이 새로운 객체를 가리키게 된다.

개념적으로는

```
처음

str
 ↓
"Hello"

이후

"Hello"

str
 ↓
"Hello World"
```

와 같은 과정이다.

따라서 반복적으로 문자열을 수정해야 할 경우 `StringBuilder`가 유리할 수 있다.

---

# 29. 값 형식과 참조 형식 핵심 비교

| 구분 | 값 형식 | 참조 형식 |
| --- | --- | --- |
| 저장 | 실제 값 | 객체에 대한 참조 |
| 대입 | 값 복사 | 참조 복사 |
| 서로 영향 | 없음 | 같은 객체라면 있음 |
| `null` | 기본적으로 불가능 | 가능 |
| 대표 자료형 | int, float, bool, struct, enum | class, array, string, object |

※ Nullable Value Type인 `int?`, `bool?` 등은 `null`을 가질 수 있다.

---

# 30. 값 형식과 참조 형식에서 가장 중요한 부분

다음 두 코드를 비교하면 이해하기 쉽다.

### 값 형식

```csharp
int a = 10;
int b = a;

b = 100;
```

결과

```
a = 10
b = 100
```

`10`이라는 **값이 복사**되었다.

---

### 참조 형식

```csharp
Player a = new Player();

Player b = a;

b.hp = 100;
```

결과

```
a와 b가 같은 Player 객체를 바라본다.
```

따라서 한쪽에서 객체의 내용을 바꾸면 다른 쪽에서도 변경된 값이 보인다.

### 핵심

```
값 형식
A → 값
B → 복사된 값

참조 형식
A ─┐
   → 같은 객체
B ─┘
```

---

# 31. Unity에서 왜 중요한가?

Unity에서는 대부분의 주요 객체가 클래스이기 때문에 참조 형식에 대한 이해가 매우 중요하다.

대표적으로

```csharp
GameObject
Transform
Rigidbody
Animator
MonoBehaviour
```

등은 클래스다.

예를 들어

```csharp
GameObject target1 = target;
GameObject target2 = target1;
```

이라고 작성했다고 해서 GameObject가 하나 더 생성되는 것이 아니다.

두 변수가 같은 GameObject를 참조한다.

```
target1 ─┐
         ↓
      GameObject
         ↑
target2 ─┘
```

실제 GameObject를 새로 생성하려면 Unity에서는 일반적으로

```csharp
Instantiate()
```

를 사용한다.

따라서

```
변수를 복사한다
≠
게임 오브젝트를 복제한다
```

라는 점을 반드시 구분해야 한다.

---

# 32. 전체 흐름 정리

## 2차원 배열

```
array[행, 열]

GetLength(0)
→ 행

GetLength(1)
→ 열

Length
→ 전체 원소 개수
```

---

## 객체지향 프로그래밍

```
추상화
→ 필요한 특징만 뽑아 표현한다.

캡슐화
→ 데이터와 기능을 하나의 객체로 묶는다.

은닉화
→ 내부 데이터를 외부에서 함부로 접근하지 못하도록 보호한다.
```

---

## 클래스

```
Class
→ 객체의 설계도

Object / Instance
→ 클래스를 기반으로 실제 생성된 객체

Field
→ 객체의 데이터 / 상태

Method
→ 객체의 기능 / 행동

Constructor
→ 객체 생성 시 실행되는 초기화 코드
```

---

## 메서드 오버로딩

```
같은 메서드 이름
+
다른 매개변수
```

예시

```csharp
Attack()
Attack(int damage)
Attack(int damage, float range)
```

---

## 접근 제한자

```
public
→ 외부 접근 가능

private
→ 클래스 내부에서만 접근 가능
```

---

## this

```
this
→ 현재 객체 자기 자신
```

주로 필드와 매개변수의 이름이 같을 때 사용한다.

```csharp
this.name = name;
```

---

## null

```
null
→ 참조하고 있는 객체가 없음
```

null 상태에서 객체에 접근하면

```
NullReferenceException
```

이 발생할 수 있다.

---

# 33. 핵심 암기

```
2차원 배열
array[행, 열]

GetLength(0)
→ 행

GetLength(1)
→ 열
```

```
클래스
→ 객체를 만들기 위한 설계도

객체
→ 클래스로 실제 만들어진 데이터
```

```
필드
→ 객체의 상태

메서드
→ 객체의 행동

생성자
→ 객체를 만들 때 실행되는 초기화 코드
```

```
캡슐화
→ 데이터 + 기능을 하나로 묶는다.

은닉화
→ 외부의 직접적인 접근을 제한한다.

추상화
→ 필요한 특징만 추려서 표현한다.
```

그리고 가장 중요하게 기억할 것은 다음이다.

```
값 형식의 대입
→ 값이 복사된다.

참조 형식의 대입
→ 객체 자체가 복사되는 것이 아니라
   같은 객체를 가리키는 참조가 복사된다.
```

게임 개발에서 클래스와 배열을 계속 사용하게 되므로 **값 복사인지, 참조 복사인지 구분하는 습관**이 중요하다.