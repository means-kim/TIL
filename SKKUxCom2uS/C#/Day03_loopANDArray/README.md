# C# 3일차 학습 정리

## 1. 반복문

반복문은 **같은 코드를 여러 번 실행하기 위해 사용하는 문법**이다.

게임에서는 반복문을 매우 자주 사용한다.

예를 들어 다음과 같은 상황에서 활용한다.

- 몬스터 목록을 순회한다.
- 인벤토리 아이템을 확인한다.
- 플레이어 목록을 검사한다.
- 배열에 저장된 데이터를 출력한다.
- 특정 조건을 만족할 때까지 작업을 반복한다.

C#에서 대표적으로 사용하는 반복문은 다음과 같다.

- `for`
- `foreach`
- `while`

반복문의 흐름을 제어하기 위해 다음 키워드도 사용한다.

- `continue`
- `break`

---

# 2. for문

`for`문은 **반복 횟수가 명확할 때 주로 사용하는 반복문**이다.

기본 구조는 다음과 같다.

```csharp
for (초기식; 조건식; 증감식)
{
    실행할 코드;
}
```

예시

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}
```

출력

```csharp
0
1
2
3
4
```

### 동작 순서

```csharp
초기식
↓
조건식 확인
↓
코드 실행
↓
증감식
↓
조건식 확인
↓
반복
```

위 코드에서는

```csharp
int i = 0;
```

반복문에서 사용할 변수 `i`를 만들고 0으로 초기화한다.

```csharp
i < 5
```

`i`가 5보다 작은 동안 반복한다.

```csharp
i++
```

한 번 반복할 때마다 `i`를 1 증가시킨다.

---

## 배열과 for문

`for`문은 배열과 함께 매우 자주 사용한다.

```csharp
int[] numbers = { 10, 20, 30, 40 };

for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

`i`를 배열의 `index`로 사용할 수 있기 때문에 배열의 모든 요소에 접근할 수 있다.

```csharp
numbers[0]
numbers[1]
numbers[2]
numbers[3]
```

### 게임 개발에서의 예

```csharp
Enemy[] enemies = new Enemy[10];

for (int i = 0; i < enemies.Length; i++)
{
    // 모든 적에게 특정 작업 수행
}
```

예를 들어

- 모든 적의 HP 검사
- 모든 아이템 확인
- 모든 슬롯 초기화
- 모든 스테이지 데이터 처리

등에 사용할 수 있다.

---

# 3. foreach문

`foreach`문은 **배열이나 컬렉션 안의 모든 요소를 하나씩 가져와 사용할 때 편리한 반복문**이다.

기본 구조

```csharp
foreach (자료형 변수 in 배열)
{
    실행할 코드;
}
```

예시

```csharp
int[] numbers = { 10, 20, 30 };

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

출력

```csharp
10
20
30
```

`for`문처럼 index를 직접 관리할 필요가 없다.

---

## for와 foreach 비교

### for

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

장점

- index를 사용할 수 있다.
- 특정 위치의 값을 수정하기 쉽다.
- 반복 범위를 직접 조절할 수 있다.

예를 들어

```csharp
numbers[2] = 100;
```

처럼 특정 요소에 접근할 수 있다.

---

### foreach

```csharp
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

장점

- 코드가 간단하다.
- index 관리가 필요 없다.
- 모든 요소를 순회할 때 읽기 쉽다.

따라서 다음처럼 생각할 수 있다.

```csharp
index가 필요하다
→ for

모든 데이터를 단순히 확인한다
→ foreach
```

---

# 4. while문

`while`문은 **조건이 참인 동안 계속 반복하는 반복문**이다.

기본 구조

```csharp
while (조건)
{
    실행할 코드;
}
```

예시

```csharp
int count = 0;

while (count < 5)
{
    Console.WriteLine(count);
    count++;
}
```

출력

```csharp
0
1
2
3
4
```

---

## while문의 특징

`for`문은 반복 횟수가 정해져 있을 때 사용하기 좋다.

반면 `while`문은 **언제 끝날지 정확히 알 수 없고 특정 조건을 만족할 때까지 반복해야 할 때** 사용하기 좋다.

예

```csharp
while (playerHp > 0)
{
    // 전투 진행
}
```

또는

```csharp
while (true)
{
    // 계속 실행

    if (조건)
    {
        break;
    }
}
```

게임에서는 상태가 바뀔 때까지 반복해야 하는 로직에서 사용할 수 있다.

---

# 5. continue

`continue`는 반복문을 완전히 종료하지 않고 **현재 반복만 건너뛰고 다음 반복으로 이동**한다.

예시

```csharp
for (int i = 0; i < 5; i++)
{
    if (i == 2)
    {
        continue;
    }

    Console.WriteLine(i);
}
```

출력

```csharp
0
1
3
4
```

`i == 2`인 경우 아래 코드를 실행하지 않고 다음 반복으로 넘어간다.

---

## 게임 개발 예시

죽은 몬스터는 처리하지 않는 경우

```csharp
foreach (Enemy enemy in enemies)
{
    if (enemy.IsDead)
    {
        continue;
    }

    enemy.UpdateAI();
}
```

즉,

```
이번 요소는 무시하고 다음 요소를 처리한다.
```

라고 생각하면 된다.

---

# 6. break

`break`는 **반복문 자체를 즉시 종료한다.**

예시

```csharp
for (int i = 0; i < 10; i++)
{
    if (i == 5)
    {
        break;
    }

    Console.WriteLine(i);
}
```

출력

```csharp
0
1
2
3
4
```

`i == 5`가 되는 순간 반복문이 종료된다.

---

## continue와 break 차이

```csharp
continue
현재 반복만 건너뛴다.
→ 다음 반복은 계속 실행한다.

break
반복문 전체를 종료한다.
→ 다음 반복도 실행하지 않는다.
```

게임에서 특정 데이터를 찾으면 더 이상 검색할 필요가 없는 경우 `break`를 사용할 수 있다.

```csharp
foreach (Item item in inventory)
{
    if (item.Id == targetId)
    {
        Console.WriteLine("아이템 발견");
        break;
    }
}
```

---

# 7. 배열(Array)

배열은 **같은 자료형의 여러 데이터를 하나의 변수로 관리하기 위한 자료구조**이다.

예를 들어 플레이어 점수 5개를 저장한다고 가정한다.

배열을 사용하지 않는다면

```csharp
int score1 = 10;
int score2 = 20;
int score3 = 30;
int score4 = 40;
int score5 = 50;
```

처럼 각각 변수를 만들어야 한다.

배열을 사용하면

```csharp
int[] scores = { 10, 20, 30, 40, 50 };
```

처럼 하나의 변수로 관리할 수 있다.

---

# 8. 배열 선언

배열은 다음과 같이 선언한다.

```csharp
자료형[] 배열이름;
```

예

```csharp
int[] numbers;
```

배열을 생성하려면 `new`를 사용할 수 있다.

```csharp
int[] numbers = new int[5];
```

이는 정수 5개를 저장할 수 있는 배열을 생성한다.

```csharp
[0][0][0][0][0]
```

`int`의 기본값은 `0`이기 때문에 처음에는 모두 0으로 초기화된다.

---

## 배열 선언과 동시에 값 넣기

```csharp
int[] numbers = {10, ㄴ20, 30 };
```

또는

```csharp
int[] numbers = new int[]
{
    10,
    20,
    30
};
```

처럼 작성할 수도 있다.

---

# 9. 배열의 index

배열에서 각각의 데이터가 위치한 번호를 `index`라고 한다.

중요한 점은 **index가 0부터 시작한다는 것**이다.

```csharp
int[]numbers= {10,20,30,40 };
```

배열의 구조

```csharp
index    0    1    2    3
value   10   20   30   40
```

따라서

```csharp
numbers[0]
```

은 `10`이다.

```csharp
numbers[2]
```

는 `30`이다.

---

## 배열 값 변경

```csharp
numbers[1] =1 00;
```

변경 전

```csharp
10 20 30 40
```

변경 후

```csharp
10 100 30 40
```

---

# 10. 배열의 Length

배열의 길이는 `Length`를 사용해서 확인할 수 있다.

```csharp
int[] numbers = { 10, 20, 30 };

Console.WriteLine(numbers.Length);
```

결과

```csharp
3
```

배열을 반복문으로 순회할 때 매우 자주 사용한다.

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

---

# 11. 배열의 마지막 index

배열의 index는 0부터 시작하므로

```csharp
마지막 index = Length - 1
```

이다.

예를 들어

```csharp
int[]numbers = {10, 20, 30 };
```

이라면

```csharp
Length = 3

index
0
1
2
```

따라서 마지막 요소는

```csharp
numbers[numbers.Length - 1]
```

로 접근할 수 있다.

---

# 12. IndexOutOfRangeException

배열의 범위를 벗어난 index에 접근하면 오류가 발생한다.

```csharp
int[] numbers = { 10, 20, 30 };

Console.WriteLine(numbers[3]);
```

배열에 존재하는 index는

```csharp
0
1
2
```

뿐이므로 `numbers[3]`은 존재하지 않는다.

이 경우

```csharp
IndexOutOfRangeException
```

이 발생한다.

따라서 반복문에서 다음처럼 작성하는 것이 중요하다.

```csharp
i < numbers.Length
```

잘못된 예

```csharp
i <= numbers.Length
```

배열의 마지막 index는 `Length - 1`이기 때문이다.

---

# 13. Array의 여러 기능

C#의 `Array` 클래스에는 배열을 다룰 수 있는 여러 기능이 존재한다.

---

## Array.Sort()

배열을 정렬한다.

```csharp
int[]numbers = {5, 2, 4, 1, 3 };
Array.Sort(numbers);
```

결과

```csharp
1 2 3 4 5
```

---

## Array.Reverse()

배열의 순서를 뒤집는다.

```csharp
int[] numbers = { 1, 2, 3 };

Array.Reverse(numbers);
```

결과

```csharp
3 2 1
```

---

## Array.IndexOf()

특정 값의 index를 찾는다.

```csharp
int[] numbers = { 10, 20, 30 };

int index = Array.IndexOf(numbers, 20);
```

결과

```csharp
1
```

값을 찾지 못하면 `-1`을 반환한다.

---

## Array.Clear()

배열의 특정 범위를 기본값으로 초기화한다.

```csharp
int[] numbers = { 10, 20, 30, 40 };

Array.Clear(numbers, 1, 2);
```

결과

```csharp
10 0 0 40
```

---

# 14. 배열의 특징

배열에는 중요한 특징이 있다.

### 1. 같은 자료형만 저장한다.

```csharp
int[] numbers;
string[] names;
float[] damages;
```

---

### 2. 크기가 고정되어 있다.

```csharp
int[] numbers = new int[5];
```

배열을 생성한 이후 크기를 10으로 늘리는 식으로 직접 변경할 수 없다.

이 때문에 데이터 개수가 계속 변해야 한다면 `List<T>`와 같은 컬렉션을 사용하는 경우가 많다.

---

### 3. index를 이용해 데이터에 빠르게 접근할 수 있다.

```csharp
numbers[3]
```

처럼 원하는 위치의 데이터에 바로 접근할 수 있다.

---

# 15. 2차원 배열

배열을 여러 차원으로 만들 수도 있다.

예를 들어 2차원 배열은 표 또는 맵처럼 사용할 수 있다.

```csharp
int[,] map = new int[3, 4];
```

구조

```csharp
[ ][ ][ ][ ]
[ ][ ][ ][ ]
[ ][ ][ ][ ]
```

값을 넣을 때는

```csharp
map[0, 0] = 1;
map[1, 2] = 5;
```

처럼 사용한다.

게임에서는

- 타일맵
- 보드게임
- 퍼즐
- 격자형 맵 데이터

등을 표현할 때 사용할 수 있다.

---

# 16. BigInteger

`BigInteger`는 **일반적인 정수 자료형의 범위를 넘어서는 매우 큰 정수를 저장하기 위한 자료형**이다.

C#의 대표적인 정수 자료형인 `long`은 표현할 수 있는 범위가 제한되어 있다.

```csharp
long

약
-9.22 × 10^18
~
+9.22 × 10^18
```

이 범위를 넘어서는 숫자를 저장하면 `long`으로는 처리할 수 없다.

이때 `BigInteger`를 사용할 수 있다.

---

# 17. BigInteger 사용 방법

`BigInteger`를 사용하려면 다음 namespace가 필요하다.

```csharp
using System.Numerics;
```

예시

```csharp
BigInteger number = BigInteger.Parse(
    "123456789012345678901234567890"
);
```

일반적인 숫자 자료형으로는 저장하기 어려운 매우 큰 수도 저장할 수 있다.

---

## BigInteger 연산

일반적인 정수처럼 연산할 수 있다.

```csharp
BigInteger a = BigInteger.Parse("999999999999999999999");
BigInteger b = BigInteger.Parse("100000000000000000000");

BigInteger result = a + b;
```

다음과 같은 연산도 가능하다.

```csharp
+
-
*
/
%
```

---

# 18. BigInteger 장점

### 매우 큰 정수를 표현할 수 있다.

`int`, `long`의 범위를 신경 쓰지 않고 큰 정수를 처리할 수 있다.

예

```csharp
1
10000
100000000
100000000000000000000000000
...
```

---

### 계산이 비교적 편하다.

문자열로 큰 숫자를 직접 계산하는 것보다

```csharp
a + b
```

처럼 일반적인 숫자처럼 사용할 수 있기 때문에 구현이 편하다.

---

# 19. BigInteger 단점

BigInteger는 숫자의 크기가 정해져 있지 않기 때문에 일반적인 정수 자료형보다 더 많은 메모리와 연산 비용이 필요하다.

즉,

```csharp
int
long
```

보다 일반적으로 느리다.

따라서 `long` 범위에서 충분히 처리할 수 있다면 굳이 `BigInteger`를 사용할 필요는 없다.

---

# 20. 게임에서 BigInteger가 사용되는 경우

특히 다음과 같은 게임에서 매우 큰 숫자가 등장할 수 있다.

- 방치형 게임
- 클리커 게임
- 키우기 게임
- 인플레이션이 큰 RPG

예

```csharp
1000

1000000

1000000000000

100000000000000000000000000000000
```

공격력이나 골드가 계속 증가한다면 `long`의 범위를 넘어설 수 있다.

이런 경우 `BigInteger`를 하나의 해결 방법으로 사용할 수 있다.

다만 실제 게임에서는 성능과 숫자 표현 방식 때문에

```csharp
값 + 지수
```

형태의 별도 큰 수 자료형을 구현하기도 한다.

---

# 21. string의 특징

C#의 `string`은 **불변(Immutable) 객체**이다.

불변이라는 것은 한 번 생성된 문자열의 내용을 직접 변경할 수 없다는 의미이다.

예를 들어

```csharp
string text = "Hello";

text += " World";
```

겉보기에는 기존 문자열에 `" World"`가 붙은 것처럼 보인다.

하지만 내부적으로는 기존 문자열 자체를 변경하는 것이 아니라

```csharp
"Hello"
```

와

```csharp
" World"
```

를 이용해

```csharp
"Hello World"
```

라는 새로운 문자열 객체를 생성한다.

---

# 22. 반복적인 문자열 연결의 문제

다음과 같은 코드를 생각해 볼 수 있다.

```csharp
string text = "";

for (int i = 0; i < 10000; i++)
{
    text += i;
}
```

문자열을 추가할 때마다 새로운 문자열이 생성될 수 있다.

```csharp
""
↓
"0"
↓
"01"
↓
"012"
↓
"0123"
↓
...
```

이 과정에서 많은 임시 문자열 객체가 생성될 수 있다.

결과적으로

- 메모리 사용 증가
- Garbage Collection 부담 증가
- 성능 저하

가 발생할 수 있다.

---

# 23. StringBuilder

`StringBuilder`는 **문자열을 반복적으로 추가하거나 수정할 때 효율적으로 처리하기 위한 클래스**이다.

사용하려면 다음 namespace가 필요하다.

```csharp
usingSystem.Text;
```

---

# 24. StringBuilder 사용 방법

```csharp
StringBuilder sb = new StringBuilder();

sb.Append("Hello");
sb.Append(" ");
sb.Append("World");

string result = sb.ToString();
```

결과

```csharp
Hello World
```

---

# 25. Append()

문자열의 뒤에 데이터를 추가한다.

```csharp
StringBuilder sb = new StringBuilder();

sb.Append("A");
sb.Append("B");
sb.Append("C");
```

결과

```csharp
ABC
```

---

# 26. AppendLine()

문자열을 추가하고 줄바꿈한다.

```csharp
StringBuilder sb = new StringBuilder();

sb.AppendLine("Hello");
sb.AppendLine("World");
```

결과

```csharp
Hello
World
```

로그나 여러 줄의 문자열을 만들 때 유용하다.

---

# 27. Insert()

특정 위치에 문자열을 삽입한다.

```csharp
StringBuilder sb = new StringBuilder("Hello World");

sb.Insert(6, "C# ");
```

결과

```csharp
Hello C# World
```

---

# 28. Remove()

특정 위치의 문자열을 제거한다.

```csharp
StringBuilder sb = new StringBuilder("Hello World");

sb.Remove(5, 6);
```

결과

```csharp
Hello
```

---

# 29. Replace()

문자열의 특정 내용을 다른 내용으로 변경한다.

```csharp
StringBuilder sb = new StringBuilder("Hello World");

sb.Replace("World", "Unity");
```

결과

```csharp
Hello Unity
```

---

# 30. Clear()

StringBuilder에 저장된 내용을 모두 제거한다.

```csharp
sb.Clear();
```

기존 `StringBuilder` 객체를 다시 사용할 수 있다.

---

# 31. StringBuilder의 장점

문자열을 여러 번 연결하거나 수정할 때 일반적인 `string` 연결보다 효율적일 수 있다.

예를 들어

```csharp
string text = "";

for (int i = 0; i < 10000; i++)
{
    text += i;
}
```

보다

```csharp
StringBuilder sb = new StringBuilder();

for (int i = 0; i < 10000; i++)
{
    sb.Append(i);
}

string text = sb.ToString();
```

가 반복적인 문자열 생성 상황에서 유리하다.

### 장점

- 불필요한 문자열 객체 생성을 줄일 수 있다.
- 많은 문자열을 연결할 때 성능이 좋다.
- 문자열을 삽입, 삭제, 수정하기 편하다.
- GC 부담을 줄일 수 있다.

---

# 32. StringBuilder의 단점

항상 `StringBuilder`가 좋은 것은 아니다.

간단한 문자열 연결에서는 코드가 오히려 복잡해질 수 있다.

예를 들어

```csharp
string name = "Kim";
string text = "Hello " + name;
```

정도의 단순한 문자열 연결에는 굳이 `StringBuilder`를 사용할 필요가 없다.

```csharp
StringBuilder sb = new StringBuilder();

sb.Append("Hello ");
sb.Append(name);

string text = sb.ToString();
```

오히려 코드가 길어진다.

또한 `StringBuilder` 자체도 객체이므로 생성 비용이 존재한다.

---

# 33. StringBuilder는 언제 사용하는가?

다음과 같은 경우 사용을 고려할 수 있다.

### 문자열을 반복문에서 계속 연결할 때

```csharp
for (int i = 0; i < 10000; i++)
{
    sb.Append(i);
}
```

---

### 많은 문자열을 하나로 합칠 때

예

```csharp
로그 생성
CSV 데이터 생성
텍스트 파일 내용 생성
긴 UI 문자열 생성
```

---

### 문자열을 자주 수정해야 할 때

```csharp
추가
삭제
삽입
교체
```

작업이 반복되는 경우 유용하다.

---

# 34. string과 StringBuilder 비교

| 구분 | string | StringBuilder |
| --- | --- | --- |
| 특징 | 불변 객체 | 내부 데이터를 수정 가능 |
| 짧은 문자열 | 적합 | 굳이 필요 없음 |
| 반복적인 문자열 연결 | 비효율적일 수 있음 | 효율적 |
| 코드 단순성 | 간단함 | 상대적으로 복잡함 |
| 객체 생성 | 수정할 때 새 문자열 생성 가능 | 기존 버퍼 재사용 |
| 주요 사용 | 일반적인 문자열 | 반복적인 문자열 생성 |

쉽게 정리하면

```csharp
문자열을 몇 번만 합친다
→ string

문자열을 수십~수천 번 반복해서 합친다
→ StringBuilder 고려
```

---

# 35. 게임 개발 관점에서 StringBuilder

게임에서는 매 프레임 실행되는 코드의 성능이 중요하다.

예를 들어 다음처럼 매 프레임 문자열을 계속 생성하면

```csharp
void Update()
{
    string text = "HP : " + hp + " / " + maxHp;
}
```

상황에 따라 문자열 객체가 계속 생성될 수 있다.

특히

- 대량 로그 생성
- 디버그 정보 생성
- 네트워크 메시지 구성
- 파일 데이터 생성
- 여러 데이터를 하나의 문자열로 조합

등에서는 `StringBuilder`를 고려할 수 있다.

하지만 UI 문자열처럼 단순한 문자열 몇 개를 합치는 수준이라면 성능을 지나치게 걱정해서 모든 코드를 `StringBuilder`로 작성할 필요는 없다.

---

# 36. 4일차 핵심 정리

## 반복문

```csharp
for
→ 반복 횟수를 알고 있을 때

foreach
→ 배열이나 컬렉션의 모든 요소를 순회할 때

while
→ 조건을 만족하는 동안 계속 반복할 때
```

---

## 반복문 제어

```csharp
continue
→ 현재 반복만 건너뛰고 다음 반복 실행

break
→ 반복문 자체를 종료
```

---

## 배열

```csharp
여러 개의 같은 자료형 데이터를 하나의 변수로 관리한다.

index는 0부터 시작한다.

배열의 마지막 index
= Length - 1
```

대표적인 사용

```csharp
array[index]
array.Length

Array.Sort()
Array.Reverse()
Array.IndexOf()
Array.Clear()
```

---

## BigInteger

```csharp
int / long의 범위를 넘어서는 매우 큰 정수를 처리하기 위한 자료형
```

사용

```csharp
usingSystem.Numerics;
```

방치형, 클리커, 키우기 게임처럼 매우 큰 숫자를 다루는 경우 활용할 수 있다.

---

## StringBuilder

```csharp
문자열을 반복적으로 추가하거나 수정할 때 사용하는 클래스
```

사용

```csharp
usingSystem.Text;
```

대표적인 기능

```csharp
Append()
AppendLine()
Insert()
Remove()
Replace()
Clear()
ToString()
```

핵심 기준

```csharp
간단한 문자열
→ string

많은 문자열을 반복적으로 연결/수정
→ StringBuilder
```

---

# 37. 게임 클라이언트 개발자로서 기억할 핵심

이번 4일차 내용은 실제 게임 개발에서 매우 자주 사용된다.

```csharp
반복문
→ 여러 게임 오브젝트와 데이터를 처리한다.

배열
→ 여러 데이터를 묶어서 관리한다.

BigInteger
→ 일반적인 정수 범위를 초과하는 게임 수치를 처리할 수 있다.

StringBuilder
→ 반복적인 문자열 생성으로 발생하는 불필요한 메모리 할당을 줄일 수 있다.
```

특히 배열과 반복문은 거의 항상 함께 사용하게 된다.

```csharp
for (int i = 0; i < enemies.Length; i++)
{
    enemies[i].TakeDamage(10);
}
```

따라서 이번 내용에서 가장 중요한 흐름은

```csharp
여러 데이터를 배열에 저장한다.
        ↓
반복문으로 배열을 순회한다.
        ↓
각 데이터에 필요한 작업을 수행한다.
```

라고 이해하면 된다.