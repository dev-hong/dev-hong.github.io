---
title: "백준 1475번 방 번호"
excerpt: "본 글은 '백준'의 알고리즘 문제를 풀이하는 내용이 들어있습니다. 문제에 대한 출처는 'baekjoon'입니다. 문제는 방 번호를 만들기 위해 0~9까지 들어있는 숫자세트가 몇개가 필요한지 구하는 문제입니다."
search: true
categories: 
  - Algorithm
  - Baekjoon
tags: 
  - 알고리즘
  - Python
  - 백준
last_modified_at: 2019-04-27T13:34:00+09:00
toc: true
toc_sticky: true
comments: true
header:
    teaser: /assets/images/thumbnail/2019/190427-baekjoon-algorithm-ex1475.png
---

<i class="fas fa-exclamation-circle"></i> 아래 문제는 **백준**에서 가져온 문제입니다. 해당 사이트에서 문제를 접할 수 있습니다. <a href="https://www.acmicpc.net/problem/1475" target="_blank">https://www.acmicpc.net/problem/1475</a>
{: .notice--danger}


## 문제

다솜이는 은진이의 옆집에 새로 이사왔다. 다솜이는 자기 방 번호를 예쁜 플라스틱 숫자로 문에 붙이려고 한다.  

다솜이의 옆집에서는 플라스틱 숫자를 한 세트로 판다. 한 세트에는 0번부터 9번까지 숫자가 하나씩 들어있다. 다솜이의 방 번호가 주어졌을 때, 필요한 세트의 개수의 최솟값을 출력하시오. (6은 9를 뒤집어서 이용할 수 있고, 9는 6을 뒤집어서 이용할 수 있다.)  

## 예제

```bash
# 입력
9999

# 출력
2
```

## 풀이

`6`과 `9`는 서로 상하 위치만 바꾸면, 같이 사용할 수 있기 때문에, **같은 숫자로 취급**해서 문제를 풉니다. (본 글에서는 `9`를 `6`으로 취급해서 풀었습니다.)

본 글에서는 크기가 `9`(0부터 8까지)인 배열을 만들어서 입력 받은 수를 하나씩 꺼내서 `count`를 했습니다. `count`를 모두 한 다음에 그 중 가장 큰 수를 꺼내면 됩니다.  

하지만 여기서 주의해야할 부분이 `6`입니다. `9`의 경우도 `6`으로 취급하여 카운트를 했기 때문에 **절반으로 나눠**줘야 합니다. 만약 `6`의 개수가 홀수인 경우는 한 세트가 더 필요한 경우이기 때문에 **반올림**을 해줍니다.  

|n|n/2|round(n/2)|
|:---|:---|:---|
|2|1.0|`1 set`|
|3|1.5|`2 set`|
|4|2.0|`2 set`|
|5|2.5|`3 set`|

즉, 정리하면...

- 6과 9를 같은 숫자로 취급한다.
- 입력받은 수를 `counting`한다.
- 6의 경우(또는 9), 절반으로 나눈다음 반올림을 한다.


### 1. Python으로 풀기

<i class="fas fa-exclamation-circle"></i> `Python`의 `round()` 함수는 `round to the nearest even` 함수이므로 주의할 것.
{: .notice--danger}

처음에 풀었을 때, 계속 틀리길래 반례가 있는 줄 알았습니다. 그런데 못찾겠더군요. 알고보니 파이썬의 반올림을 해주는 `round()` 함수에 문제가 있었습니다.  

```python
print(round(2.5))
```

여기서 저희는 `3`이란 결과를 기대하겠지만, `2`라는 결과가 나옵니다. 보통 생각하는 반올림 함수가 아닌 `round to the nearest EVEN` 함수입니다. 이게 무슨 뜻이냐하면...  

가장 가까운 짝수로 반올림을 한다는 것인데, 아래 예를 보면 이해가 쉬워집니다.

|n|round(n)|
|:---|:---|
|1.5|2|
|2.5|2|
|3.5|4|
|4.5|4|
|5.5|6|
|6.5|6|

즉, 소숫점이 `0.5`이고 일의 자리가 **짝수인 경우는 반올림을 해도 내림**이 되버립니다.  

#### 1.1. 코드

```python
# -*- coding: utf-8 -*-
import sys

_input = sys.stdin.readline()[:-1]  # 개행문자 제외
cnt = [0, 0, 0, 0, 0, 0, 0, 0, 0]  # 0부터 8까지

for n in _input:
    index = int(n)
    if index == 9:
        index = 6  # 9인 경우, 6으로 재할당
    cnt[index] += 1  # counting

cnt[6] = (cnt[6] + 1) // 2  # round() 함수는 쓰지 않음
print(max(cnt))
```

위에서 말했듯이 `round()` 함수에 문제가 있기 때문에, `6`의 경우는 `+1` 한 뒤에 2를 나눈뒤 소수점을 버리는 방법으로 문제를 풀었습니다.  

그리고, 입력을 받을때, `[:-1]` 부분이 있는데, 맨 마지막에 `\n` 개행문자가 들어가기 때문에 제외를 했습니다.

## 결과

|채점 번호|아이디|문제 번호|결과|메모리|시간|언어|코드 길이|
|:---|:---|:---|:---|:---|:---|:---|:---|
|12938540|hongku|1475|맞았습니다!!|29056KB|56ms|Python 3|243B|

<i class="far fa-laugh-wink"></i> 문제의 풀이 방법은 매우 다양합니다. 좀 더 효율적이고 좋은 방법이 있다면 **댓글**이나 **이메일**로 알려주세요. 같이 문제 풀어봅시다 :)
{: .notice--success}