# 49. Group Anagrams

| 제한 사항                                                    |
| ------------------------------------------------------------ |
| - `1 <= strs.length <= 104` <br />- `0 <= strs[i].length <= 100`<br />- strs[i] consists of lower-case English letters.<br /> |



## 문제

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.



## 입출력

Example 1

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

Example 2

```
Input: strs = [""]
Output: [[""]]
```

Example 3

```
Input: strs = ["a"]
Output: [["a"]]
```





## 출처

https://leetcode.com/problems/group-anagrams/





## 책 참고 정답 #1

> - collections.defaultdict(list) ==> dict 자료형을 만드는데, 값(value) type이 list인 !
>- ''.join(x) ==> x 안에 있는 값들을 '' 이걸로 다 묶음
> - sorted(str) ==> 문자열은 각 단어로 해부된 리스트 형태로 return
>- dict 값들을 전부 불러오는 함수 == .values() 

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        new = collections.defaultdict(list)
        
        for x in strs :
            new[''.join(sorted(x))].append(x)
        
        return new.values()
```





## Feedback

> * 딕셔너리 틀을 활용할 줄 알아야 한다.
> * 팀소트 정렬 방식에 대해 알아보기 (vs 퀵정렬, 병합 정렬)



---

