# 819. Most Common Word

| 제한 사항                                                    |
| ------------------------------------------------------------ |
| - `1 <= paragraph.length <= 1000` <br />- `0 <= banned.length <= 100<br />`<br />- `1 <= banned[i].length <= 10`<br />- The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)<br />- paragraph only consists of letters, spaces, or the punctuation symbols `!?',;.`<br />- There are no hyphens or hyphenated words.<br />- Words only consist of letters, never apostrophes or other punctuation symbols. |



## 문제

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.



## 입출력

Example 1

```
Input: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"

Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```



## 출처

https://leetcode.com/problems/most-common-word/



## 내 정답 #1

> Runtime: **76ms** / Memory Usage: **14.2 MB**

```python
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        
        for x in "!?',;.":
            paragraph = paragraph.replace(x, ' ')
        
        new = list()
        
        for i in paragraph.split():
            new.append(i.lower())
        
        max_num = 0
        result = None
        
        for x in new:
            if new.count(x) > max_num :
                if x not in banned:
                    max_num = new.count(x)
                    result = x
        
        return result
```



## 책 참고 정답 #2

> Data cleansing
>
> 정규식 ==> `\w` : 단어문자 ,  `^`: not  
>
> re.sub(*pattern*, *repl*, *string*, *count=0*, *flags=0*)
>
> re.sub(조건, 바꿀것, 대상문자열)
>
> 리스트 컴프리헨션 안에서 조건문까지...

```python
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        
        words = [word for word in re.sub(r'[^\w]', ' ', paragraph).lower().split()
                	if word not in banned]
        # r'[^\w]' == 문자가 아닌 모든 것
        # if word not in banned ==> word 값이 banned 안에 없다면!
        
        # 개수 담아두는 변수 딕셔너리 ... defaultdict(기본값)
        
        counts = collections.defaultdict(int)
        # ==> 디폴트 class가 정수type, 비어 있는 딕셔너리 형태 변수 생성
        # ==> defaultdict(<class 'int'>, {})
        
        for word in words :
            # counts dict 변수에 새로운 key와 value 값을 아래와 같은 방법으로 줄 수 있다.
            counts[word] += 1
        
        return max(counts, key=count.get) # ==> 딕셔너리 변수인 counts에서 값이 가장 큰 키를 가져온다.
```



## 책 참고 정답 #3

> collections.Counter() 사용
>
> .most_common()
>
> Runtime: **16ms** / Memory Usage: **14.4 MB**

```python
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        
        words = [word for word in re.sub(r'[^\w]', ' ', paragraph).lower().split()
                        if word not in banned]
		
        # Counter를 통해 리스트 안에 있는 각 값들이 몇번 사용됐는지 dict 형식으로 변환
        counts = collections.Counter(words)
        
        # .most_common(1) 이것을 통해 가장 많이 쓴 단어 1개만 리스트 안 튜플 형태로 출력 ==> [('ball',2)]
        return counts.most_common(1)[0][0]
```





## Feedback

> * str.replace(old, new, count)
> * split() 할 때, 띄어쓰기 2개 있어도 같이 분리 기준으로 사용
> * 리스트 컴프리헨션 안에서 조건문 쓸 수 있는지 처음 알았음.
> * re.sub()
> * 정규표현식...
> * defaultdict()
> * colections는 무엇일까?
> * collections.Counter()
> * .most_common()



---

