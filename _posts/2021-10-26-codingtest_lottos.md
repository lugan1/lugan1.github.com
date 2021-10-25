---
title: "[코테] 로또 최고순위와 최저순위 "
tags:
- java
- 코딩테스트
categories:
- 코딩테스트
date: '2021-10-26 07:10:00'
classes: wide
---

# 프로그래머스 Level1 (로또 최고순위와 최저순위)
[https://programmers.co.kr/learn/courses/30/lessons/77484?language=java#](https://programmers.co.kr/learn/courses/30/lessons/77484?language=java#)

<br/>
<br/>

# 문제 요약
- 로또 구매 용지와 당첨번호 이렇게 2개의 배열이 있음
- 숫자 0 은 가려진 번호로 가정한다.
- 숫자 0 으로 가려진 번호가 로또 구매용지에 있을때, 될수있는 최고순위와 최저순위 계산. 자동으로

<br/>
<br/>

# Solution
```java
class Solution {
    
    public int[] solution(int[] lottos, int[] win_nums) {
        
    
        int max = 7;
        int min = 7;
        int zero_count = 0;
        
        for(int i=0; i<win_nums.length; i++){
            if (lottos[i] == 0){
                zero_count = zero_count + 1;
            }
            
            
            for(int j=0; j<win_nums.length; j++){
                if(lottos[j] == win_nums[i]){
                    max = max - 1;
                    min = min - 1;
                }
            }
        }
        
        max = max - zero_count;
        
        if(min == 7){
            min = 6;
        }
        
        if(max == 7){
            max = 6;
        }
        
        int[] answer = {max, min};
        
        return answer;
    }
}
```