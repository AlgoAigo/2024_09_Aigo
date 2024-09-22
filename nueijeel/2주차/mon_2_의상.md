# 의상

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42578
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv2


## 문제 풀이

### 문제 내용 정리
코니가 가진 의상들이 담긴 배열이 주어질 때 서로 다른 옷을 입는 경우의 수를 반환하는 문제
> 의상은 각 종류별로 최대 한가지 씩만 착용 가능하고 하루에 최소 한개의 의상은 착용해야 함

### 문제 유형
해시

### 풀이 방법
해시 맵을 이용해 의상 종류 별로 의상 수를 저장해 코디 경우의 수를 계산함
의상 종류 별로 해당 종류를 착용하지 않는 경우의 수 까지 포함하여 모든 조합을 계산한 뒤 결과 값에서 모든 종류의 의상을 착용하지 않는 경우의 수(1)만 제거해준다


### 소스 코드
```kotlin
class Solution {
    fun solution(clothes: Array<Array<String>>): Int {
        // 의상 종류에 따른 의상 수를 저장하기 위한 해쉬맵
        val hashMap = HashMap<String, Int>()
        
        // 주어진 의상 수만큼 반복
        for (i in 0 until clothes.size) {
            // getOrDefault 메서드를 사용하여 해쉬맵에 해당 의상 타입이 이미 저장되어 있다면 해당하는 value값에 1을 더해 저장하고
            // 처음 저장하는 의상 타입일 경우 디폴트값 0에 1을 더해 저장
            hashMap[clothes[i][1]] = hashMap.getOrDefault(clothes[i][1], 0) + 1
        }
        
        // 의상 조합 경우의 수를 계산할 변수
        // 각 경우의 수를 곱해줘야하기 때문에 초깃값 1로 설정
        var result = 1
        // 해쉬맵의 value 값을 순회
        for (num in hashMap.values) {
            // result에 해당 의상 타입 개수 + 1을 곱해줌
            // +1은 해당 의상 타입을 아무것도 착용하지 않는 경우의 수임
            result *= (num + 1)
        }
        // 최종 결과 값에서 모든 종류의 의상을 착용하지 않는 경우를 제거해 반환
        return --result
    }
}
```