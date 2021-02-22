# 125. Valid Palindrome

| 제한 사항                                                    |
| ------------------------------------------------------------ |
| - `1 <= s.length <= 2 * 105` <br />- `s` consists only of printable ASCII characters. |



## 문제

Given a string `s`, determine if it is a palindrome, considering only `alphanumeric characters` and ignoring cases.



## 입출력

Example 1

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

Example 2

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```



## 출처

https://leetcode.com/problems/valid-palindrome/



## 책 참고 정답 #1

> Runtime: **284ms** / Memory Usage: **19.4 MB**

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        
        text = []
        
        for alpha in s:
            # 값이 숫자나 문자형태면 true로 분별
            if alpha.isalnum():
                # 대소문자 구분 없애야 해서 한 형태로 다 바꿔서 리스트로 넣기
                text.append(alpha.lower())
        
        while len(text)>1:
            if text.pop(0) != text.pop():
                return False
            
        return True
```



## 책 참고 정답 #2

> data를 리스트가 아니라 데크 형식으로만 줘도 시간이 확 감소
>
> 데크 자료형에는 인덱스를 쓸 수 없다.
>
> Runtime: **52 ms** / Memory Usage: **19.3 MB**

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        
        text: Deque = collections.deque()
        
        for alpha in s:
            if alpha.isalnum():
                text.append(alpha.lower())
        
        while len(text)>1:
            if text.popleft() != text.pop():
                return False
            
        return True
```



## 책 참고 정답 #3

> 파이썬 슬라이싱의 기교
>
> Runtime: **52ms** / Memory Usage: **20.8 MB**

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        
        text = []
        
        for alpha in s:
            if alpha.isalnum():
                text.append(alpha.lower())
        
        if text[:] != text[::-1]:
            return False
        else:
            return True
```



## Feedback

> * .pop() 의 특성을 잘 활용하자.
> * .pop()은 맨 마지막 요소를 출력해주고 기존 리스트 안에서 빼준다.
> * .pop() 안에 인덱스 값으로 뺄 값을 지정할 수 있다.
> * 데크 자료형에 대한 이해 필요 (왜 실행 속도가 감소할까?)
> * 파이썬의 슬라이싱은 그 자체가 객체다. 즉, 인덱스처럼 값을 뽑아주는 것이 아니다
> * 슬라이싱의 type을 보면 원본 타입을 그대로 출력해준다.



---

