# JadenCase 문자열 만들기

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12951
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv2


## 문제 풀이

### 문제 내용 정리
문자열 s가 주어질 때 JadenCase로 바꾼 문자열을 반환
- JadenCase : 모든 단어의 첫 문자가 대문자이고, 그 외 알파벳은 소문자인 문자열. 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 표기.

### 문제 유형
문자열

### 풀이 방법
주어지는 문자열을 전부 소문자로 변환 후, 공백을 기준으로 단어 단위로 분리한다. 이후 단어 첫 글자가 문자인지 판별해 대문자로 변환해준 뒤 다시 공백과 함께 문자열로 출력

### 예외 상황 및 고려 사항 (선택)
공백문자가 연속해서 나올 수 있기 때문에 해당 케이스는 그대로 공백을 반환하면 됨


### 소스 코드
```kotlin
class Solution {
    fun solution(s: String): String {
        var answer = s.toLowerCase().split(" ").map { word ->
            if (word.isNotEmpty() && word[0].isLetter()) {
                word[0].toUpperCase() + word.substring(1)
            } else {
                word
            }
        }.joinToString(" ")
    
        return answer
    }
}
```