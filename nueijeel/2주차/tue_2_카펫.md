# 카펫

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42842
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv2


## 문제 풀이

### 문제 내용 정리
Leo가 본 카펫의 갈색, 노란색 격자 수가 각각 주어질 때 카펫의 가로, 세로 크기를 담은 배열 반환하는 문제
-> 카펫은 가로길이 >= 세로길이 이고, 맨 가장자리 한줄만 갈색으로 이루어져있는 형태

### 문제 유형
브루트포스

### 풀이 방법
가장자리 갈색 격자는 1줄로만 이루어져 있기 때문에 노란 격자가 배치될 수 있는 경우에 따라 주어진 갈색 격자 개수로 1줄을 만들 수 있는 경우를 찾으려고 했다. 

### 소스 코드
```kotlin
class Solution {
    fun solution(brown: Int, yellow: Int): IntArray {
        // 결과로 반환할 정수형 배열 선언
        var answer = IntArray(2, {0})
        
        // 노란색 격자가 배치되는 줄 수
        for (height in 1 .. yellow) {
            // 노란 격자가 완전히 같은 개수로 height개 분할되지 않는다면 해당 경우 고려하지 않음
            if (yellow % height != 0) continue
            // 노란 격자가 height만큼 분할되었을 때 한 줄의 가로 길이
            val width = yellow / height
            // 현재의 노란격자 배치를 전부 둘러싼 개수가 갈색 격자 개수와 동일한 경우
            if (brown == (width + height) * 2 + 4) {
                // 해당 가로 길이와 세로 길이를 배열에 저장
                answer[0] = width + 2
                answer[1] = height + 2
            }
        }
        
        // 결과 반환
        return answer
    }
}
```