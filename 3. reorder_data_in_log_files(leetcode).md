# 937. Reorder Data in Log Files

| 제한 사항                                                    |
| ------------------------------------------------------------ |
| 1 <= logs.length <= 100<br />3 <= logs[i].length <= 100<br />All the tokens of logs[i] are separated by a single space.<br />logs[i] is guaranteed to have an identifier and at least one word after the identifier. |



## 문제

You are given an array of `logs`. Each log is a space-delimited string of words, where the first word is the **identifier**.

There are two types of logs:

- **Letter-logs**: All words (except the identifier) consist of lowercase English letters.
- **Digit-logs**: All words (except the identifier) consist of digits.

Reorder these logs so that:

1. The **letter-logs** come before all **digit-logs**.
2. The **letter-logs** are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
3. The **digit-logs** maintain their relative ordering.

Return *the final order of the logs*.



## 입출력

Example 1

```
Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]

Explanation:
The letter-log contents are all different, so their ordering is "art can", "art zero", "own kit dig".
The digit-logs have a relative order of "dig1 8 1 5 1", "dig2 3 6".
```

Example 2

```
Input: logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
Output: ["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
```



## 출처

https://leetcode.com/problems/reorder-data-in-log-files/



## 내 정답

```python
class Solution:
    def reorderLogFiles(self, logs: List[str]) -> List[str]:
        
        # 정렬할 내용 중에서 숫자와 문자를 구분한다. (숫자, 문자 변수를 새로 만든다)
        letter, num = [], []
        
        # logs 안에 있는 값을 하나씩 불러와서 분리해준 후 2번째 위치해 있는 값이 숫자인지 판별한다 (split, isdigt 함수 사용)
        for log in logs :
            if log.split()[1].isdigit() : # <<< 숫자인 경우
                num.append(log)
            else:
                letter.append(log)
                
        # 숫자와 문자가 구분된 상황으로 숫자는 입력 순서대로 들어가 있어서 정렬이 필요 없다.
        # 문자 리스트 안에 있는 값들을 정렬해줘야 하는데, 각 요소의 [0]값은 identifier 이므로, [1]부터 나오는 값을 기준으로 정렬! (key 사용)
        
        letter.sort(key= lambda x : (x.split()[1:], x.split()[0]))
        # 즉, 키값을 람다 함수로 줬다. 첫번째 기준은 x.split()[1:] 이다. >>> 각 값의 [1]부터 나오는 값을 기준으로 정렬한다.
        # 만약 [1:] 값이 모두 같으면 identifier로 정렬하도록 두번째 정렬 기준인 x.split()[0]을 부여했다.
        
        return lettet + num  # <<< 문자가 숫자보다 항상 먼저 나오도록 결합해준다. / 리스트끼리 더하면 각 요소들이 합해져서 한 리스트 만든다.
        
```



## Feedback

> * 변수를 줄 때, 튜플 형식으로 주는 버릇을 길러보자 (한 줄 깔끔)
> * split 함수는 원본을 건드리지 않는다!
> * 숫자인지 판별하는 함수 isdigit() >>> is~ 이 함수들 종류에 대해 더 살펴보자 (ex. isalnum())
> * split 한 후의 값은 리스트고 묶이기 때문에 인덱스를 사용할 수 있다!
> * .sort() / sorted() 함수 모두 key를 매개변수로 가지고 있다! 
> * 참고로 .sort() 는 리스트에만 쓸 수 있고 , sorted()는 다른 문자열에도 사용 가능하다.
> * 또한, .sort() 는 원본을 변경시키고, sorted()는 원본을 그대로 둔다.
> * key 안에는 변수 자체를 줘도 되지만, 함수를 줘서 그 함수값을 변수로 사용할 수 있다.



---

