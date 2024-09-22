# 체육복

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42862
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1


## 문제 풀이

### 문제 내용 정리
여벌 체육복이 있는 학생이 체육복을 도난당한 학생에게 체육복을 빌려주어 체육 수업을 들을 수 있는 학생 수의 최댓값을 구하는 문제
> 여벌 체육복이 있는 학생이 체육복을 도난당했을 경우 남은 체육복은 하나로 간주해 다른 학생에게 체육복 빌려줄 수 없음
> 여벌 체육복을 가져온 학생과 체육복을 도난당한 학생 번호는 각각 중복이 없음
> 전체 학생 수는 2 - 30명

### 문제 유형
그리디

### 풀이 방법
우선 여벌 체육복을 가진 학생이 체육복 도난당한 경우를 먼저 처리하고, 여벌 체육복을 가진 학생이 체육복을 빌려줄 수 있는지를 반복문과 조건문을 통해 확인함

### 예외 상황 및 고려 사항 (선택)
제출 후 30개 테스트케이스 중에서 2개가 실패했다고 떴는데 list가 정렬되어 있지 않을 경우를 고려하지 않아서 해당 코드를 추가해줌


### 소스 코드
```kotlin
class Solution {
    fun solution(n: Int, lost: IntArray, reserve: IntArray): Int {
        // 도난당한 학생 배열과 여벌 체육복 있는 학생 배열을 수정 가능한 list로 변환
        val lostList = lost.toMutableList()
        val reserveList = reserve.toMutableList()
        
        // intersect 메서드를 이용해 여벌 체육복을 가진 학생이 도난 당한 경우를 제거함
        val intersection = lostList.intersect(reserveList)
        lostList.removeAll(intersection)
        reserveList.removeAll(intersection)
        
        // 남은 항목을 정렬
        lostList.sort()
        reserveList.sort()
        
        // 여벌 체육복 있는 학생들 리스트를 순회
        for (r in reserveList) {
            when {
                // 해당 학생 번호보다 1 작거나 1 큰 학생 번호를 가진 학생이 도난당했을 경우 
                // 도난 리스트에서 해당 학생을 제거(빌려주는 것으로 간주)
                lostList.contains(r - 1) -> lostList.remove(r - 1)
                lostList.contains(r + 1) -> lostList.remove(r + 1)
            }
        }
        
        // 전체 학생 수 중에서 체육복을 도난 당했는데 빌릴 수 없는 학생들 수를 뺀 값을 리턴
        return n - lostList.size
    }
}
```