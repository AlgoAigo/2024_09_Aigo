# 이진 변환 반복하기

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/70129
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv2


## 문제 풀이

### 문제 내용 정리
0과 1로 이루어진 문자열에 대한 이진변환을 문자열이 "1"이 될 때까지 반복했을 때, 이진변환을 수행한 횟수와 그 과정에서 제거된 0의 개수를 배열에 담아 변환하는 문제
- 이진변환 과정
1. 문자열에 존재하는 0을 전부 제거
2. 문자열 길이를 이진법으로 표현한 문자열로 변환

### 문제 유형
문자열

### 풀이 방법
이진 변환 과정을 함수로 선언해서 문자열이 "1"이 될때 까지 반복해 결과를 출력하도록 했다.
처음 제출한 코드도 통과되긴 했는데 시간이 좀 걸리는 것 같아 다른 사람 풀이를 구경하다가 이진법 수행하는 과정을 직접 연산이 아닌 메서드로 처리할 수 있길래 바꿔서 제출했더니 시간이 확실히 덜 소요됐다!


### 소스 코드
```kotlin
// 처음 제출한 코드
class Solution {
    var zero = 0
    fun solution(s: String): IntArray {
        var answer: IntArray = intArrayOf()
        
        var newString = s
        var cnt = 0
        
        while (newString.length > 1) {
            newString = convertToBinary(newString)
            cnt++
        }
        
        answer = intArrayOf(cnt, zero)
        
        return answer
    }
    
    fun convertToBinary(str: String): String {
        // 0제거
        var newString = str.replace("0", "")
        var len = newString.length
        zero += str.length - len
        
        // 이진변환
        var binaryResult = ""
        while (len > 1) {
            binaryResult = (len % 2).toString() + binaryResult
            len /= 2
        }
        return "1" + binaryResult
    }
}
```

```kotlin
// 최종 코드
class Solution {
    // 제거된 0의 개수를 저장할 변수 (두 함수에서 모두 사용되기 때문에 전역변수로 선언)
    var zero = 0

    fun solution(s: String): IntArray {
        // 변환과정을 거치면서 문자열을 새로 저장하기 위해 변수로 선언, 초기값 s
        var newString = s
        // 이진변환 연산 횟수 저장하기 위한 변수
        var cnt = 0
        
        // 문자열 길이가 1이 될 때 까지 반복
        while (newString.length > 1) {
            // 이진 변환 연산 결과를 newString에 저장
            newString = convertToBinary(newString)
            // 연산 횟수 증가
            cnt++
        }
        
        // 결과 반환
        return intArrayOf(cnt, zero)
    }
    
    // 이진 변환 수행 함수
    fun convertToBinary(str: String): String {
        // replace 함수 이용해 0 제거
        var newString = str.replace("0", "")
        var len = newString.length
        // 기존 문자열 길이에서 0 제거한 문자열 길이를 빼서 제거한 0 개수 카운트
        zero += str.length - len
        
        // toBinaryString을 사용해 문자열 길이 값을 이진수로 변환한 값을 문자열 형태로 반환함
        return Integer.toBinaryString(len)
    }
}
// Java의 Integer 클래스 함수
// Integer.toBinaryString() - 10진수를 2진수로 변환
// Integer.toOctalString() - 10진수를 8진수로 변환
// Integer.toHexString() - 10진수를 16진수로 변환
// Integer.parseInt(s) - 문자열에 해당하는 10진수 integer 반환
// Integer.parseInt(s, n) - 문자열에 해당하는 n진수 integer 반환
```