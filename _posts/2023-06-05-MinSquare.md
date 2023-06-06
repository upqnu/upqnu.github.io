---
layout: single
title: "코딩테스트 : 최소 직사각형 문제"
categories: 코딩테스트
tag: [코딩테스트, 알고리즘, 완전탐색]
---
  
### 최소 직사각형
<https://school.programmers.co.kr/learn/courses/30/lessons/86491>
  
```java
public class MinSquare { 
    // 1. 주어진 sizes 배열에서 가로, 세로 중 더 긴 쪽을 가로(또는 세로) - 더 짧은 쪽은 세로(또는 가로)로 변경한 후,
    // 2. 가로, 세로 중 가장 큰 값을 서로 곱해서 지갑의 크기를 구한다.
    public int solution1(int[][] sizes) {
        int answer = 0;
        // 1. 구현
        int hori = 0, vert = 0; // 각각 가로, 세로의 최대 길이
        for(int i=0; i< sizes.length; i++) {
            if(sizes[i][0] < sizes[i][1]) { // sizes[i][0]을 가로, sizes[i][1]을 세로로 가정 -> 가로 <세로이면
                int tmp = sizes[i][1];
                sizes[i][1] = sizes[i][0];
                sizes[i][0] = tmp; // 가로, 세로를 서로 바꾼다.
            }
            // 2. 구현
            if(sizes[i][0] > hori) hori = sizes[i][0];
            if(sizes[i][1] > vert) vert = sizes[i][1];
        }
        answer = hori * vert;
        return answer;
    } 

    public static void main(String[] args) {
        MinSquare ms = new MinSquare();
        int[][] sizes = { {60, 50}, {30, 70}, {60, 30}, {80, 40} };
        int[][] sizes2 = { {14, 4}, {19, 6}, {6, 16}, {18, 7}, {7, 11} };
        System.out.println(ms.solution1(sizes2)); 
    } 
}
```
  
(더 나은 방법으로 구현하면 추가하겠습니다)
