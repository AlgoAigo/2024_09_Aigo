# 시저 암호

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12926
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1

## 문제 풀이

### 문제 내용 정리
문장의 각 알파벳을 일정 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 구현. 문자열 s를 거리 n 만큼 민 결과 반환
- 공백은 그대로 공백
- 문자열은 알파벳 소문자, 대문자, 공백으로만 이루어짐
- n은 1이상, 25이하 자연수

### 문제 유형
문자열

### 풀이 방법
주어진 n값의 범위를 보고 아스키코드 값을 이용하여 해결했다. 우선 해당 알파벳의 아스키코드 값이 공백인지 소문자인지 대문자인지 구분하여 공백이면 그대로 반환, 소문자나 대문자면 n을 더해 소문자 또는 대문자의 아스키코드 범위 내에 존재하는지 판단하여 n만큼 민 값을 반환하도록 했다.


### 소스 코드
```kotlin
class Solution {
    fun solution(s: String, n: Int): String {
        var answer = StringBuilder()
        s.forEach { c ->
            val ascii = c.toInt()
            val num = when (ascii) {
                in 65..90 -> {
                    if (ascii + n > 90) {
                        65 + (ascii + n - 91)
                    } else {
                        ascii + n
                    }
                }
                in 97..122 -> {
                    if (ascii + n > 122) {
                        97 + (ascii + n - 123)
                    } else {
                        ascii + n
                    }
                }
                else -> {
                    32
                }
            }
            answer.append(num.toChar().toString())
        }
        return answer.toString()
    }
}
``