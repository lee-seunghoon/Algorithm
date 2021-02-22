# 344. Reverse String

| 제한 사항 |
| --------- |
| 없음      |



## 문제

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).



## 입출력

Example 1

```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

Example 2

```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```



## 출처

https://leetcode.com/problems/reverse-string/



## 내 정답 #1

> runtime : **420ms** / Memory Usage: **18.3 MB**

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        # 맨 마지막 요소 앞에서부터 차례대로 뺀다음에 append 시키면서 정렬...
        new = s
        num = len(s)-2
        
        while num > -1:
            s.append(s.pop(num))
            num -= 1
```



## 책 풀이 참고 정답 #2

> two pointer swap 알고리즘
>
> Runtime: **200ms** / Memory Usage: **18.3 MB**

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s)-1
        
        while left < right :
            # 서로 값 swap 해주기
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```



## 책 풀이 참고 정답 #3

> 파이썬 슬라이싱 기능 꼼수
>
> Runtime: **188ms** / Memory Usage: **18.6 MB**

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        s[:] = s[::-1]
        
        # 참고로 s = s[::-1] 이렇게 하면 오류난다.
```





## Feedback

> * 두개의 값을 swap 해주는 알고리즘 익히기
> * 슬라이싱을 적절히 사용해서 원하는 결과 얻기



---

