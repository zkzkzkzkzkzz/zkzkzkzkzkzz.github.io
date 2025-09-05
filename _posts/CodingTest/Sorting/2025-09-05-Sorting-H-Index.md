---
title: "H-Index"

categories:
  - Sorting
tags:
  - CodingTest
  - Programmers

toc: true
toc_sticky: true

date: 2025-09-05
last_modified_at: 2025-09-05
---

## 문제

[H-Index](https://school.programmers.co.kr/learn/courses/30/lessons/42747#)

<img alt="image" src="https://github.com/user-attachments/assets/d8a701bb-9a48-409f-917f-8a6fc0b80006" />

## 문제 풀이

정답 자체는 어렵지 않았으나 간과한 부분이 있어 두 번 정도 고친 문제였다.

H-Index는 주어진 배열을 쭉 순회했을 때 자기보다 더 크거나 같은 숫자가 자신 이상일 때의 최댓값을 뜻하는데, 예를 들어, [1, 2, 3, 4]에선 2이상인 숫자는 3개이고, 3이상인 숫자는 2개이다.\
즉, 저 배열에서 H-Index는 2가 된다.

처음엔 주어진 배열을 정렬해서 투포인터로 인덱스를 계산했는데 생각해보니 H-Index의 값은 배열에 없는 값일 수도 있었다.\
(반례 : [5, 6, 7, 8] => 해당 배열에서 H-Index는 4다.)

따라서 중간값을 인덱스가 아닌 특정 값으로 설정하여 탐색할 필요가 있었는데, 0부터 하나씩 올려가며 값을 찾는 것은 매우 많은 시간이 소요되므로 이분 탐색을 사용했다.

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    int answer = 0;
    
    sort(citations.begin(), citations.end());
    
    int size = citations.size() - 1;
    
    int left = 0;
    int right = citations[size];
    
    while (left <= right)
    {
        int mid = (left + right) / 2;
        int cnt = 0;
        
        for (int i = 0; i < size + 1; ++i)
        {
            if (mid <= citations[i]) ++cnt;
        }
        
        if (cnt >= mid)
        {
            answer = mid;
            left = mid + 1;
        }
        else
            right = mid - 1;
    }
    
    return answer;
}
```

최솟값과 최댓값의 중간값인 `mid`를 사용하여 한 번 탐색하고 조건에 맞다면 해당 `mid`를 저장한 뒤 범위를 좁혀 다시 탐색하도록 구현했다.
