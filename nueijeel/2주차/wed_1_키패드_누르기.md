# 키패드 누르기

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/67256
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1


## 문제 풀이

### 문제 내용 정리
스마트폰 키패드 배열에서 누를 번호가 담긴 배열이 주어질 때 번호가 1, 4, 7이면 왼손 엄지, 3, 6, 9이면 오른손 엄지, 2, 5, 8, 0이면 두 엄지 손가락 중 현재 키패드 위치에서 더 가까운 엄지손가락(같다면 오른손잡이 - 오른엄지, 왼손잡이 - 왼엄지)으로 눌러야한다. 각 번호를 누른 엄지 손가락을 순서대로 나타낸 문자열을 반환하는 문제. 왼손엄지는 L로, 오른손엄지는 R로 표기한다. 맨 처음 왼손엄지는 *, 오른손엄지는 # 키패드에서 시작.

### 문제 유형
구현

### 풀이 방법
처음에 2, 5, 8, 0일때 현재 왼,오른 엄지 위치에서 해당 번호까지 거리를 계산하는 로직이 명료하지 않게 짜져서 질문하기에서 힌트를 좀 참고했다. * 0 # 배열 부분을 각각 10 11 12로 두고 거리를 계산하라고 해서 0일때를 11로 하고, 왼쪽 엄지 시작 위치를 10으로 오른 엄지 시작 위치를 12로 두었다. 거리 계산은 타켓 번호에서 현재 엄지 위치를 뺀 절대값을 구하고, 그 값을 3으로 나눈 값과 3으로 나눈 나머지를 더해서 계산했다. 계산한 양쪽 거리를 비교해 더 가까운 쪽 엄지로 누르도록 했다.


### 소스 코드
```kotlin
class Solution {
    fun solution(numbers: IntArray, hand: String): String {
        // 누른 엄지 방향을 저장할 변수
        var answer = StringBuilder()
        // 각 엄지의 시작 위치값 (왼엄지:10, 오른엄지:12)
        var leftP: Int = 10
        var rightP: Int = 12
        
        // 눌러야할 번호 배열 순회
        numbers.forEach { number ->
            // 눌러야할 번호 값에 따라 분기
            when (number) {
                // 1, 4, 7일 경우
                1, 4, 7 -> {
                    // 왼쪽 엄지로 눌렀음을 저장
                    answer.append("L")
                    // 왼엄지 위치를 저장하는 변수에 해당 번호 저장
                    leftP = number
                }
                // 3, 6, 9
                3, 6, 9 -> {
                    // 오른 엄지로 눌렀음을 저장
                    answer.append("R")
                    // 오른 엄지 위치를 저장하는 변수에 해당 번호 저장
                    rightP = number
                }
                // 2, 5, 8, 0
                else -> {
                    // 만약 해당 숫자가 0이면 11로 치환
                    var num = if (number == 0) 11 else number

                    // 타겟 번호로부터 왼엄지 거리 계산
                    val leftD = Math.abs(num - leftP) / 3 + Math.abs(num - leftP) % 3
                    // 타겟 번호로부터 오른엄지 거리 계산
                    val rightD = Math.abs(num - rightP) / 3 + Math.abs(num - rightP) % 3

                    // 두 거리가 같을 경우
                    if (leftD == rightD) {
                        // 오른손잡이이면
                        if (hand == "right") {
                            // 오른손으로 누름
                            answer.append("R")
                            rightP = num
                        } else { // 왼손잡이이면
                            // 왼손으로 누름
                            answer.append("L")
                            leftP = num
                        }
                    } else if (leftD > rightD) { // 왼손의 거리가 더 멀면
                        // 오른손으로 누름
                        answer.append("R")
                        rightP = num
                    } else { // 오른손의 거리가 더 멀면
                        // 왼손으로 누름
                        answer.append("L")
                        leftP = num
                    }
                }
            }
        }
        
        // 결과 값을 문자열 형태로 출력
        return answer.toString()
    }
}
```