|우선순위|연산자|결합방향|
|------|---|---|
|1|후위연산( ++, -- ), 함수( ), 괄호( ), 배열[ ],구조( ., -> )|좌 -> 우|
|2|전위연산( ++, -- ), 부호( +, - ), NOT( !, ~ ), (casting), sizeof, 포인터( *, & )|좌 <- 우|
|3|산술연산( *, /, %, +, - )|좌 -> 우|
|4|시프트연산( <<, >> ), 비교연산( <, <=, >, >=, ==, != )|좌 -> 우|
|5|비트( &, ^, \| ), 논리( &&, \|\| )|좌 -> 우|
|6|삼항연산자( ? : ), 할당( =, +=, -=, *=, /=, %= ...)|좌 <- 우|

- 증감 > 산술 > 관계 > 논리 > 할당

# 전위연산 vs 후위연산

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FE9jhc%2FbtqFnE4f7Im%2FU2qgQ7w44dVOSq1Qd88KhK%2Fimg.png">

- 전위연산자 : 연산(증/감) 후 할당
- 후위연산자 : 할당 후 연산(증/감)

## ex) a * b + c >= d && d / a - b != 0
- int a = 5, b = 4, c = 5, d = 6
    - (((a * b) + c) >= d) && (((d / a) - b) != 0)
    - (((a * b) + c) >= d) => 1
    - (((d / a) - b) != 0) => 1
    - 결과 1

## ex) d % b + ++a * c--
- int a = 3, b = 4, c = 5, d = 6
    - (d % b) + (++a * c--)
    - ++a : a를 먼저 1 증가시키고 식 수행, a = 4
    - c-- : 식을 먼저 수행하고 1 감소, c = 4
    - (++a * c--) => 20
    - (d % b) => 2
    - 결과 22

## Code

```
int main()
{
    int num1=10;
    int num2=num1--+2;
    num2++;
    printf("num1 : %d\n", num1);
    printf("num2 : %d\n", num2);
}
```

- num2 = num1-- + 2
  - num2 <= num1, num2 == 10
  - num1--, num1 == 9
  - num2 <= + 2, num2 == 12
- 결과 num1 : 9, num2 : 13

```
int main()
{
    int x=1;
    printf("x : %d\n", x++);
    printf("x : %d\n", x++);
    printf("x : %d\n", ++x);
    printf("x : %d\n", x--);
    printf("x : %d\n", x--);
    printf("x : %d\n", --x);
}
```

- 1. x : 1, x == 2
  2. x : 2, x == 3
  3. x : 4, x == 4
  4. x : 4, x == 3
  5. x : 3, x == 2
  6. x : 1, x == 1
    
- 후위연산은 라인이 끝날 때 연산을 수행
