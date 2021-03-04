# Q1. 동전 0

| 시간 제한 | 메모리 제한 |
| --------- | ----------- |
| 1 초      | 256 MB      |

## 문제

준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.

동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

## 출력

첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)



### 예제입력 & 출력

```
<입력1>
10 4200
1
5
10
50
100
500
1000
5000
10000
50000

<출력1>
6

<입력2>
10 4790
1
5
10
50
100
500
1000
5000
10000
50000

<출력2>
12
```



## 출처

https://www.acmicpc.net/problem/11047



## 내 정답

```python
n, k = map(int,input().split())
a = []

for i in range(n):
    coin = int(input())
    if coin <= k:
        a.append(coin)

a.sort(reverse=True)
coin_num = 0
coin_rest = k

for i in a :
    portion = int(coin_rest // i)
    rest = k % i
    
    if coin_rest != 0 :
        coin_num += portion
        coin_rest = rest
        
    elif coin_rest == 0 :
        break    
        
print(coin_num)
```



## Feedback

> * 조금 더 짧고, 간단한 최적의 해를 구하는 코딩 구현 사고 방식 필요



---

