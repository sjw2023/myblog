---
layout: post
title: "프로그래머스 DFS/BFS 문제 풀이"
date: 2023-06-28
categories: jekyll update
---

# 프로그래머스 코딩테스트 연습 
# 문제 : 네트워크 - 레벨 3
- 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다. 컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

- 제한 사항

컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
computer[i][i]는 항상 1입니다.

- 입출력 예

n	computers	return
3	[[[[1, 1, 0], [1, 1, 0], [0, 0, 1]]]]	2
3	[[[[1, 1, 0], [1, 1, 1], [0, 1, 1]]]]	1

```java
    class Solution {
        public int solution(int n, int[][] computers) {
            int answer = 0;
            int numberOfNodes = n;
            //방문한 노드목록
            boolean [] visited = new boolean [numberOfNodes];
            //방문하지 않은 노드를 따라 DFS실행 하면서 네트워크 카운트
            for(int i=0; i<computers.length; i++){
                answer += DFS( visited, computers, i );
            }
            return answer;
        }
        public int DFS( boolean [] visited, int [][] computers, int root){
            int net = 0;
            //If root has been visited already it means cycle
            if(visited[root] == true){
                return 0;
            }
            //Mark root node as visited
            visited[root] = true;
            //For each adjacent nodes in computers
            for( int i=0; i<computers[root].length; i++){
                //If adjacent node has not been visited then visit node with marking as visited
                if(computers[root][i] == 1){
                    DFS(visited, computers, i);
                }
            }
            return 1;
        }
    }
```
- 접근 방법
입력값이 이미 그래프의 근접 노드 매트릭스를 의미 하므로 단순히 입력값을 이용하여 DFS를 수행 하기만하면된다.

- 풀이 설명
입력받은 근접 노드 정보를 이용하여 네트워크 그래프 상의 모든 노드를 한번씩 DFS를 사용하여 탐색하도록 한다. DFS한번 탐색에 한개의 네트워크가 탐색이 되며 DFS를 네트워크 상의 모든 노드에 한번씩 적용하면 모든 네트워크를 탐색할수있다.

- 더 생각해 볼점
단순 DFS 알고리즘 말고도 다익스트라, 벨만포드 등을 적용하는법도 수행하면 좋을듯 하다.