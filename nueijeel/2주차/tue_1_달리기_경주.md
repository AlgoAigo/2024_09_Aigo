# 달리기 경주

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/178871
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1


## 문제 풀이

### 문제 내용 정리
달리기 경주에서 해설진이 부른 추월한 선수 이름 목록이 주어졌을 때 경주가 끝났을 때 결과를 선수들의 이름이 담긴 배열로 반환하는 문제


### 문제 유형
map 자료구조를 이용

### 예외 상황 및 고려 사항 (선택)
처음에는 배열만을 이용해서 callings 배열을 순회하면서 indexOf 메서드로 해당 선수의 현재 순번을 찾고, 추월한 결과를 반영해주는 식으로 구현을 했는데 테스트에서 시간초과 발생 -> indexOf가 배열 전체에서 해당 요소의 인덱스를 찾아 반환해주다보니 players 배열 크기가 커질수록 연산 횟수가 커짐

### 풀이 방법
map을 이용해서 선수 이름과 현재 순번을 기록했고, 순번이 바뀔 때 별도의 배열에 선수 배열을 저장하지 않고 기존에 파라미터로 주어진 players 배열 자체에서 선수 순서를 바꿔 사용해주었다.

### 소스 코드
```kotlin
class Solution {
    fun solution(players: Array<String>, callings: Array<String>): Array<String> {
        // withIndex를 사용해 컬렉션의 index와 value를 동시에 사용
        // associate를 사용해 players 배열의 value인 선수 이름을 key로, 해당 선수의 현재 순번을 나타내는 index를 value로 하는 map을 생성한다.
        val playerMap = players.withIndex().associate { it.value to it.index }.toMutableMap()
        
        // 해설진에게 이름이 불린 선수 배열을 순회
        callings.forEach { player ->
            // map에서 해당 선수의 현재 순번을 가져옴
            val idx = playerMap[player]!!
            // 추월당한 선수 이름 저장
            val playerName = players[idx - 1]
            // 추월한 선수와 추월당한 선수의 순서를 바꿔줌(기존 배열)
            players[idx - 1] = player
            players[idx] = playerName
            
            // map에서 추월당한 선수와 추월한 선수의 순번 value를 바꿔줌
            playerMap[playerName] = idx
            playerMap[player] = idx - 1
        }
        
        // 최종 결과인 선수 이름 배열을 반환
        return players
    }
}
```