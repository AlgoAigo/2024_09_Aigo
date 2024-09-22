# 이상한 문자 만들기

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12930
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1

## 문제 풀이

### 문제 내용 정리
문자열 s의 각 단어의 짝수번째 알파벳은 대문자, 홀수번째 알파벳은 소문자로 바꾼 문자열 반환
- s는 한 개 이상의 단어로 구성, 공백으로 각 단어 구분

### 문제 유형
문자열

### 풀이 방법
공백 기준으로 단어를 구분한 뒤, 각 단어의 인덱스 값이 홀수이면 대문자, 짝수이면 소문자로 문자 변환. 각 단어를 다시 공백과 함께 출력

### 예외 상황 및 고려 사항 (선택)
문자열 전체를 기준으로 짝/홀수 알파벳이 아니라 단어 기준으로 짝/홀수 알파벳을 변환해야함


### 소스 코드
```kotlin
class Solution {
    fun solution(s: String): String {
        val words = s.split(" ").map { word ->
            word.mapIndexed { index, char ->
                if (index % 2 == 0) char.uppercaseChar() else char.lowercaseChar()
            }.joinToString("")
        }

        return words.joinToString(" ")
    }
}
```