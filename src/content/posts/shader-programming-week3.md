---
title: 쉐이더프로그래밍 4주차 과제
published: 2024-10-03
description: "인하대학교 디자인테크놀로지학과에 개설된 '쉐이더프로그래밍(DET2015)' 과목을 수강하며 작성한 과제입니다."
image: ''
tags: [CG, 수학, 과제]
category: '대학'
draft: false 
lang: ''
---

:::note[들어가기 전에]  
인하대학교 디자인테크놀로지학과에 개설된 '쉐이더프로그래밍(DET2015)' 과목을 수강하며 작성한 과제입니다.  
:::
---

## 쉐이더 프로그래밍 4주차

&nbsp;  
**Math Functions in Unity3D** 
|Function|Function|Function|Function|
|--------|--------|--------|--------|
|[abs(s)](#1-abss)|[dot(a, b)](#15-dota-b)|[modf(x, out ip)](#29-modfx-out-ip)|[setp(a, x)](#43-setpa-x)|
|[acos(s)](#2-acoss)|[exp(x)](#16-expx)|[mul(M, N)](#30-mulm-n)|[tan(x)](#44-tanx)|
|[all(s)](#3-alls)|[exp2(x)](#17-exp2x)|[mul(v, M)](#31-mulv-m)|[tanh(x)](#45-tanhx)|
|[any(s)](#4-anys)|[floor(x)](#18-floorx)|[mul(M, v)](#32-mulv-m)|[transpose(m)](#46-transposem)|
|[asin(s)](#5-asins)|[fmod(x, y)](#19-fmodx-y)|[pow(x, y)](#33-powx-y)|
|[atan(x)](#6-atanx)|[isfinite(x)](#20-isfinitex)|[radians(x)](#34-radiansx)|
|[atan2(y, x)](#7-atan2y-x)|[isinf(x)](#21-isinfx)|[round(x)](#35-roundx)|
|[ceil(x)](#8-ceilx)|[ldexp(x, n)](#22-ldexpx-n)|[rsqrt(x)](#36-rsqrtx)|
|[clamp(x, a, b)](#9-clampx-a-b)|[lerp(a, b, f)](#23-lerpa-b-f)|[saturate(x)](#37-saturatex)|
|[cos(x)](#10-cosx)|[log(x)](#24-logx)|[sign(x)](#38-signx)|
|[cosh(x)](#11-coshx)|[log2(x)](#25-log2x)|[sin(x)](#39-sinx)|
|[cross(a, b)](#12-crossa-b)|[log10(x)](#26-log10x)|[sincos(x, out s, out c)](#40-sincosx-out-s-out-c)|
|[degrees(x)](#13-degreesx)|[max(a, b)](#27-maxa-b)|[sinh(x)](#41-sinhx)|
|[determinant(m)](#14-determinantm)|[min(a, b)](#28-mina-b)|[smoothstep(min, max, x)](#42-smoothstepmin-max-x)|

---

:::note[알리는 말]  
CG(C for Graphics) 언어의 수학 함수에 관해서 설명하지만, 함수의 출력값 확인을 위해 Unity3D의 Mathematics 패키지에서 제공하는 함수를 사용했다. C# 코드에는 Unity3D에서 제공하는 Mathf 클래스가 사용되었고, 편의성을 위해 실수 뒤에 `f`접미사를 붙이지 않았다.  
여기서의 '내부'는 Cg3.1 Toolkit Documentation에 명시된 Reference Implementation을 의미한다.  
:::

:::note[함수 인자의 의미]  
함수 인자로 표기된 로마자의 의미는 다음과 같다.
- x, y, a, b, n, f : 실수형 스칼라나 벡터
- s : 부울형 스칼라나 벡터 (all과 any 메소드 한정)
- s, c : 각각 사인과 코사인  (실수형 스칼라나 벡터)
- m : 실수형 행렬
- M, N : 실수형 행렬 (mul 메소드 한정)
- v : 실수형 벡터
- ip : x의 정수 부분의 스칼라 혹은 벡터
- min, max : 각각 최소값과 최대값 (실수형 스칼라나 벡터)
:::

### 1. abs(s)  
절대값을 반환한다.  
```cs
abs(-2);
>>> 2

abs(3);
>>> 3
```
### 2. acos(s)
아크코사인(arccosine) 값을 반환한다.  
[-1, +1] 사이의 값을 입력받아 [0, $\pi$] 사이의 값을 반환. 즉, $\cos$ 값$\big(\frac{밑변}{빗변}\big)$의 값이 들어가면 라디안($\theta$) 값이 나온다.

아래 예시는 acos 메소드로 출력한 결과이다.
```cs
acos(0.2);
>>> 1.3694384
```
### 3. all(s)
모든 값이 `true`일 때, `true`를 반환한다. bool 타입의 스칼라나 벡터만 인자로 넣을 수 있다.  
아래와 같은 기능을 한다.
```cs
bool all(bool4 a) {
    return a.x && a.y && a.z && a.w;
}

/*-----------사용예시-------------*/

bool3 b3 = new bool3(true, true, true);
bool all = all(b3);

print(all));
>>> true
```
### 4. any(s)
값 중 하나라도 `true`라면, `true`를 반환한다.  
아래와 같은 기능을 한다.
```cs
bool any(bool4 a) {
    return a.x || a.y || a.z || a.w;
}
```
### 5. asin(s)
아크사인(arcsine) 값을 반환한다.  
[-1, +1] 사이의 값을 입력받아 [$-\frac{\pi}{2}$, $\frac{\pi}{2}$] 사이의 값을 반환. 즉, $\sin$ 값$\big(\frac{높이}{빗변}\big)$의 값이 들어가면 라디안($\theta$) 값이 나온다.  

아래 예시는 asin 메소드로 출력한 결과이다.
```cs
asin(0.5);
>>> 0.5235988  // (= 30도)
```
### 6. atan(x)
아크탄젠트(arctangent) 값을 반환한다.  
[-$\infty$, +$\infty$] 사이의 값을 입력받아 [$-\frac{\pi}{2}$, $\frac{\pi}{2}$] 사이의 값을 반환. 즉, $\tan$ 값$\big(\frac{높이}{밑변}\big)$의 값이 들어가면 라디안($\theta$) 값이 나온다.  
비율을 인자로써 넣기 때문에 좌표평면에서 `x`가 0인 경우에는 사용할 수 없다. `y`를 0으로 나눌 수 없기 때문이다. 

아래 예시는 atan 메소드로 출력한 결과이다.
```cs
atan(0.2);
>>> 0.19739556
```
### 7. atan2(y, x)   
여섯번 째의 `atan` 메서드와 비슷한 개념이다. 

다른 점은 atan2 메서드는 [-$\pi$, $\pi$]까지 반환하는 것과 `x`가 0인 경우에도 동작한다. atan 메서드에서는 비율만을 받아 사분면 정보를 알 수 없었지만, atan2 메서드에서는 `y`와 `x`를 개별적으로 입력받아 사분면, 즉, 방향을 계산할 수 있다. 

아래는 결과를 비교해볼 수 있는 코드이다. 
```cs
float y = 1;
float x = -1;
float radians = atan(y / x);      // 약 -0.785 라디안 (= -45도)
float degrees = degrees(radians); // -45도 (실제로는 135도이어야 함)

print(degrees);
>>> -45
```
`x`가 -1이고, `y`가 1이라면 제2사분면에 위치해있음을 알 수 있다. 하지만 실제 출력값은 -45도이다. 엉뚱하게 제4사분면을 가르킨 것이다. ratio 만으로는 제2사분면인지 제4사분면인지 값만으로는 구분할 수 없다. (둘 다 음수값이기만 하다)

따라서 방향을 정확히 하고 싶은 경우에는 아래와 같이 atan2 메소드를 이용해야 한다. 
```cs
float y = 1;
float x = -1;
float radians = atan2(y, x);      // 약 2.356 라디안 (= 135도)
float degrees = degrees(radians); // 135도

print(degrees);
>>> 135
```

마지막으로, 위 내용을 잘 설명한 사진을 첨부한다.

<img src="https://upload.wikimedia.org/wikipedia/commons/7/7a/Atan2_differs_from_arctan.png" width="320">

[Atan2 differs from arctan](https://en.wikipedia.org/wiki/Atan2#/media/File:Atan2_differs_from_arctan.png) by [Jacob Rus](https://commons.wikimedia.org/wiki/User:Jacobolus), CC BY-SA 4.0

### 8. ceil(x)
천장 함수이다. 실수 `x`의 소수 부분이 있다면 일의 자리를 올림하고 소수점 이하는 버린다. 
```cs
ceil(1.4);
>>> 2

ceil(0.001);
>>> 1
```
소수점 이하의 값이 얼마나 작던 값이 존재하면 바로 올림을 하는 무서운 함수이다. 

### 9. clamp(x, a, b)
`x`의 값을 `a`와 `b` 사이의 값으로 한정시킨다. 
- `x` $\le$ `a` 라면, `a`를 반환한다.
- `a` $\lt$ `x` $\lt$ `b` 라면, `x`를 반환한다. 
- `x` $\ge$ `b` 라면, `b`를 반환한다.

```cs
clamp(10, 20, 40);  // 10이 20보다 작으므로, 20반환
>>> 20

clamp(30, 20, 40);  // 30이 20과 40 사이에 있으므로, 30 반환
>>> 30

clamp(50, 20, 40);  // 50이 40을 넘으므로, 40 반환
>>> 40
```
### 10. cos(x)
코사인(cosine) 값을 반환한다. 
인자로 라디안 값을 입력하면, $[-1, +1]$ 사이의 값을 반환한다. 

```cs
float radians = radians(45);
float cos = cos(radians);

print(cos);  
>>> 0.7071067   // (= sqrt(2) / 2)
```
### 11. cosh(x)
쌍곡코사인(hyperbolic cosine) 값을 반환한다.

정의는 다음과 같다.
- $\large \cosh (x) = \frac {\large e^x + e^{-x}} {\large2} $

아래 예시는 cosh 메소드로 출력한 결과이다. 
```cs
cosh(0);  // 쌍곡코사인 함수의 그래프는 (0, 1)을 지난다.
>>> 1
```
### 12. cross(a, b)
 두 개의 성분이 3개인 실수형 벡터(이하 '3차원 벡터')를 인수로 받고 두 벡터의 외적 값을 반환한다. 스칼라 형태로 반환되는 내적(dot) 연산과는 달리 벡터 형태로 출력된다. 

아래는 외적에 관한 애니메이션이다. 

![Cross product.gif](https://upload.wikimedia.org/wikipedia/commons/6/6e/Cross_product.gif)  
[Cross product](https://en.wikipedia.org/wiki/Atan2#/media/File:Atan2_differs_from_arctan.png) by [Lucas Vieira](https://commons.wikimedia.org/wiki/User:LucasVB), Public Domain

외적의 결과로 만들어지는 벡터는 a와 b와 직교한다. 오른손 법칙(반시계방향)에 따라 방향성이 결정된다. 외적 연산에서는 교환법칙이 성립하지 않는다. ( $ a \times b \neq b \times a $ )  
즉, 인자의 a와 b의 순서를 바꾸면 다른 값이 나온다. 
### 13. degrees(x)
입력된 라디안 값을 각도 값으로 변환하는 함수이다. 
```cs
degrees(Mathf.PI);
>>> 180
```
### 14. determinant(m)
행렬식 값을 반환하는 함수이다. 
2x2, 3x3, 4x4 행렬 타입의 변수를 인자로 받는다. 실수 스칼라 값을 반환한다. 
```cs
float2 f2 = new float2(2, 3);
float2 f21 = new float2(4, 3);
float2x2 f2x2 = new float2x2(f2, f21);

float det = determinant(f2x2);

print(det);
>>> -6
```
### 15. dot(a, b)
두 값의 내적 값을 반환하는 함수이다. 

정의는 아래와 같다.
- $ \vec a \cdot \vec b = \sum a_i  b_i $

아래는 예시는 dot 메소드로 출력한 결과이다. 
```cs
float3 a = new float3(3, 1, 2);
float3 b = new float3(2, 6, 1);

float dot = dot(a, b);

print(dot);
>>> 14
```
출력 값은 방향을 가지지 않는 스칼라 값임에 유의해야 한다. 
### 16. exp(x)
$ e ^ x $ 값을 반환하는 함수이다. 
```cs
exp(0);
>>> 1
```
### 17. exp2(x)
$ 2 ^ x $ 값을 반환하는 함수이다. 
```cs
exp2(2);
>>> 4
```
### 18. floor(x)
바닥함수이다. 실수 `x`의 소수 부분이 있다면 소수점 이하는 버린다. 
```cs
floor(3.14);
>>> 3

floor(0.002);
>>> 0
```
### 19. fmod(x, y)
부동 소수점의 나머지 값을 반환하는 함수이다.  
```cs
fmod(-3.2, 2.5);
>>> -0.7
```
내부는 다음과 같이 구현되어 있다.
```cs
float2 fmod(float2 a, float2 b) {
  float2 c = frac(abs(a/b))*abs(b);
  return (a < 0) ? -c : c;   /* if ( a < 0 ) c = 0-c */
}
```
### 20. isfinite(x)
수가 유한수인지 판별하는 함수이다. 무한한 수나 NaN(Not a Number)가 아니라면 `true`를 반환한다. 

아래는 Unity3D에서의 예시이다.
```cs
isfinite(float.MaxValue);
>>> true

isfinite(float.PositiveInfinity);
>>> false
```

무한과 NaN을 만드는 예시는 아래와 같다.
NaN에 관해 설명한 위키백과 링크를 첨부한다. [NaN (위키백과)](https://ko.wikipedia.org/wiki/NaN)
```c
// 양의 무한대
float posInf = 1.0 / 0.0;

// 음의 무한대
float negInf = -1.0 / 0.0;

// NaN (Not a Number)
float nanValue = 0.0 / 0.0;
```

내부는 다음과 같이 정의되어 있다. 
```cs
bool3 isfinite(float3 s)
{
  // By IEEE 754 rule, 2*Inf equals Inf
  return (s == s) && ((s == 0) || (s != 2*s));
}
```
### 21. isinf(x)
`isfinite`와 반대로 무한인지 판별하는 함수이다. 유한한 값이나 NaN(Not a Number)가 아니라면 `true`를 반환한다. 

> NaN은 `isfinite`나 `isinf` 메소드 둘 다 `false`만 나온다. 그렇지만.. NaN을 마주칠 일이 있을까..?
### 22. ldexp(x, n)
본 메소드의 수식은 다음과 같다. 

- $ \text{ldexp(x)} = \text{x} \times (2^n) $

아래는 예시이다. Mathematics 패키지에서는 ldexp를 제공하지 않는다.
```cs
ldexp(1.5, 2);
>>> 48
```
### 23. lerp(a, b, f)
a와 b 두 값 사이를 선형보간한다. 

`a*(1-f) + b*f` 와 동일하게 쓸 수 있다.

```cs
lerp(1, 2, 0.7)
>>> 0.7
```
### 24. log(x)
자연로그와 같은 값을 도출하는 함수이다. 
- $ \text{log(x)} = \log_e(x) $

다음과 같이 정의되어 있다.
```cs
float3 log(float3 a)
{
  float3 rv;
  int i;

  for (i=0; i<3; i++) {
    rv[i] = log(a[i]);  // this is the ANSI C standard library log()
  }
  return rv;
}
```
### 25. log2(x)
밑이 2인 로그와 같은 값을 도출하는 함수이다. 
- $ \text{log(x)} = \log_2(x) $
### 26. log10(x)
밑이 10인 로그와 같은 값을 도출하는 함수이다. 
- $ \text{log(x)} = \log_10(x) $
### 27. max(a, b)
입력된 두 값 중 더 큰 값을 반환한다. 

다음과 같이 구현되어 있다. 
```cs
float3 max(float3 a, float3 b)
{
  return float3(a.x > b.x ? a.x : b.x,
                a.y > b.y ? a.y : b.y,
                a.z > b.z ? a.z : b.z);
}
```
### 28. min(a, b)
입력된 두 값 중 더 작은 값을 반환한다. 
### 29. modf(x, out ip)
나머지 값을 반환하지만, 반환 방식이 조금 특이하다. 

우선 아래의 예시를 먼저 보자.
```cs
float2 number = new float2(3.14, 2.71);
float2 integerPart;
float2 fractionalPart = modf(number, integerPart);

print(integerPart.x, integerPart.y);
>>> 3, 2

print(fractionalPart.x, fractionalPart.y);
>>> 0.14, 0.71
```

`modf` 메소드는 나머지 연산 결과의 소수 부분을 반환한다.  
그리고 `modf` 메소드의 두 번째 인자에 정수 부분을 담아서 보낸다. 
### 30. mul(M, N)
행렬과 행렬 간 곱셈한 값을 반환한다. 

정의는 다음과 같다.  
$ (MN)_{ij} = \sum m_{ik}n_{kj}$

곱셈은 두 행렬이 $ i \times k $와 $ k \times j $와 같이 M의 열과 N의 행의 크기가 같은 경우에만 수행된다. 
### 31. mul(v, M)
벡터와 행렬 간 곱셈한 값을 반환한다.  
벡터와 행렬의 인자 순서가 바뀌면 반환되는 행렬의 크기가 바뀔 수 있기 때문에, 둘은 구분하여 사용해야 한다.  

$ \begin{pmatrix} X & Y & Z & 1 \end{pmatrix} \begin{bmatrix} 1 & 0 & 0 & x \\ 0 & 1 & 0 & y \\ 0 & 0 & 1 & z \\ 0 & 0 & 0 & 1 \end{bmatrix} = \begin{pmatrix} X & Y & Z & Xx + Yy + Zz + 1 \end{pmatrix} $
### 32. mul(M, v)
벡터와 행렬 간 곱셈한 값을 반환한다. 

$ \begin{bmatrix} 1 & 0 & 0 & x \\ 0 & 1 & 0 & y \\ 0 & 0 & 1 & z \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix} = \begin{pmatrix} X + x \\ Y + y \\ Z + z \\ 1 \end{pmatrix} $

스케일링(Scaling)도 만들어볼 수 있다.  
점(혹은 벡터)를 $ (S_x, S_y, S_z) $ 만큼 스케일링 하고 싶을 때 사용한다. 이때 사용되는 행렬을 'Scale Matrix'라고 한다.

$ \begin{bmatrix} S_x & 0 & 0 & 0 \\ 0 & S_y & 0 & 0 \\ 0 & 0 & S_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix} = \begin{pmatrix} X * S_x \\ Y * S_y \\ Z * S_z \\ 1 \end{pmatrix} $

마지막으로 회전이다. 회전은 x축, y축, z축 각각 적용하는 행렬이 다르다. 

- x축 기준 회전  
$ \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos \theta & -\sin \theta & 0 \\ 0 & \sin \theta & \cos \theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix} = \begin{pmatrix} X' \\ Y' \\ Z' \\ 1 \end{pmatrix} $
- y축 기준 회전  
$ \begin{bmatrix} \cos \theta & 0 & \sin \theta & 0 \\ 0 & 1 & 0 & 0 \\ -\sin \theta & 0 & \cos \theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix} = \begin{pmatrix} X' \\ Y' \\ Z' \\ 1 \end{pmatrix} $
- z축 기준 회전  
$ \begin{bmatrix} \cos \theta & -\sin \theta & 0 & 0 \\ \sin \theta & \cos \theta & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix} = \begin{pmatrix} X' \\ Y' \\ Z' \\ 1 \end{pmatrix} $

축을 기준으로 회전한다면 회전하려는 물체의 중심이 원점에 위치해야 한다.  
그러므로 물체의 중심이 원점에 있지 않다면 
1. Translation으로 물체의 중심을 원점으로 이동
2. 원하는 축 회전
3. 과정 1에서 옮긴 만큼 다시 되돌려 원위치

총 세 절차에 따라 회전을 시킬 수 있다. 
### 33. pow(x, y)
`x`를 `y`승한 값을 반환한다. 

정의는 다음과 같다.  
$ \text {pow(x,y)} = x ^ y $

우리가 아는 그대로겠지만, 문서에 따르면 log과 exp 연산을 통해 구현한 것 같다.  
관련해서 풀이한 위키백과 페이지를 링크한다. [Exponentiation (위키백과)](https://en.wikipedia.org/wiki/Exponentiation#Rational_exponents)

자연로그의 성질을 이용하면 다음과 같이 표현이 되므로.. 사실상 같은 식이지만 말이다.   
$ x ^ y = (e ^ {log_e (x)}) ^ y = e ^ {y \cdot \ln(x)}$

**관련해서 탐색을 해보았지만, 아쉽게도 명확한 답을 얻을 수 없었다.**
```cs
pow(2, 3);
>>> 8
```
`x`에 2, `y`에 3을 넣으면 8이 나온다. 
### 34. radians(x)
각도 값(60진법)을 넣었을 때 라디안 값(호도법)으로 변환하여 반환한다. 

```cs
radians(180);
>>> 3.141592
```
### 35. round(x)
반올림한 값을 반환한다. 

단, 계산의 편리함을 위해서 반올림 함수는 'round-to-nearest even'과 'round-to-nearest' 두 가지로 구분한다. 
'round-to-nearest even'은 0~4는 버림, 6~9는 올림한다. 그리고 5의 경우에는 짝수에 가까운 값으로 반올림 한다. 

예시는 다음과 같다. 
```cs
round(7 / 2)  // = 3.5, 3보다는 짝수인 4로
>>> 4

round(9 / 2)  // = 4.5, 5보다는 짝수인 4로
>>> 4
```
계산을 편리하게 하기 위함으로 알고 있다. 

'round-to-nearest' 방식은 0.5를 더한 후 `floor` 메소드로 계산하는 방식이다. 
흔히 일컫는 사사오입이다. 4.5같은 수는 위와 달리 4가 아닌 5를 반환한다. 

> [의문점]  
> 근데.. 그럼 둘을 어떻게 구분하여 사용하는가?
### 36. rsqrt(x)
`x`의 제곱근의 역수를 반환한다. 

정의는 다음과 같다.  
$ \text{rsqrt(x)} = \frac {\large 1} {\large \sqrt{x}} $

```cs
rsqrt(2);
>>> 0.70710677
```
### 37. saturate(x)
입력 값을 0~1 사이 값으로 잘라낸다.
`clamp(x, 0, 1)`과 동일한 기능을 한다. 
### 38. sign(x)
부호에 따라 `x`의 값이 음수이면 -1, 양수라면 1, 0이면 0을 반환한다. 

```cs
sign(-2.1);
>>> -1

sign(0);
>>> 0

sign(3.14);
>>> 1
```
### 39. sin(x)
사인(sine) 값을 반환한다. 
인자로 라디안 값을 입력하면, $[-1, +1]$ 사이의 값을 반환한다. 

```cs
sin(Mathf.PI / 2);  // sin 90도는 입력 제한을 두지 않았거나, 특수 처리를 한 것으로 보임
>>> 1

sin(Mathf.PI);
>>> -8.742278E-08   // 부동소수점 계산의 문제로 보임
```
### 40. sincos(x, out s, out c)
사인(sine) 값과 코사인(cosine) 값을 반환한다.  
입력으로 라디안 값을 주면 인자 s와 c에 각각 `sin(a)`와 `cos(a)`를 담아준다.
### 41. sinh(x)
쌍곡사인(hyperbloic sin) 값을 반환한다. 

정의는 다음과 같다.
- $\large \sinh (x) = \frac {\large e^x - e^{-x}} {\large2} $
### 42. smoothstep(min, max, x)
0과 1 사이로 매핑해서 반환한다.
`min`보다 `x`가 작다면 0이, `max`보다 크다면 1이 반환된다. 

먼저 `clamp` 메소드와 비슷한 처리 후에  
`value = (x - min) / (max - min)`을 하여 값을 압축하고 `lerp` 메소드와 같이 선형보간을 한다. 

구현과 사용 예는 아래와 같다. 
```cs
float smoothstep(float min, float max, float x)
{
    if (x < min) return 0.0;
    if (x > max) return 1.0;

    float t = (x - min) / (max - min);
    t = t * t * (3.0 - 2.0 * t);

    return t;
}

/*-----사용예시-----*/
smoothstep(10.0, 20.0, 12.5);
>>> 0.156
```
### 43. setp(a, x)
계단함수와 같은 값을 반환한다. 

만약 `x`가 `a`보다 크다면 1을, 작다면 0을 반환한다. 

```cs
step(0.5 0.1);
>>> 0

step(0.5, 0.55);
>>> 1
```
### 44. tan(x)
탄젠트(tan) 값을 반환한다. 

`sincos` 메소드를 이용해 구현할 수 있다.
```cs
float tan(float a) {
  float s, c;
  sincos(a, s, c);
  return s / c;
}
```
### 45. tanh(x)
쌍곡탄젠트(hyperbloic tangent) 값을 반환한다. 

정의는 다음과 같다.  
- $\large \tanh (x) = \frac {\large \sinh(x)} {\large \cosh(x)} $ 
### 46. transpose(m)
벡터나 행렬의 열과 행을 바꾸어 반환한다.  
즉, 전치행렬을 반환한다. 

$ n \times m $행렬이 인자로 들어왔다면, $ m \times n $행렬로 반사 대칭한다. 

아래는 `mul` 메소드와 `transpose` 메소드의 관계이다. 
```cs
mul(M,v) == mul(v, tranpose(M))
mul(v,M) == mul(tranpose(M), v)
```