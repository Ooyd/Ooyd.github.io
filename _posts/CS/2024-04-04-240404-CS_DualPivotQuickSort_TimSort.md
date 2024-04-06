---
layout: post
title: "Java 정렬 알고리즘 이해하기: DualPivotQuicksort vs TimSort"
date: '2024-04-06 03:00:00 +0900'
description: 'Java의 다양한 정렬 알고리즘 탐구'
categories: [Computer Science Fundamentals, Data Structure]
tags: [Heap, Priority Queue, HashTable]

---
# Java 정렬 알고리즘 이해하기 : DualPivotQuicksort vs TimSort

Java는 다양한 데이터 유형과 상황에 맞게 최적화된 내장 정렬 알고리즘을 제공합니다.<br>
특히, 기본 데이터 타입 배열을 정렬할 때는 `Arrays.sort()` 메소드 내부에서 `DualPivotQuicksort`를 사용하는 반면, 객체 배열을 정렬할 때는 `Collections.sort()` 메소드 내부에서 `TimSort`를 사용합니다. <br>
 이 글에서는 각 알고리즘이 어떻게 다른지 간단하게 살펴보려합니다.

## DualPivotQuicksort

`DualPivotQuicksort`는 이름에서 알 수 있듯이 두 개의 피벗을 사용하는 퀵 정렬의 변형입니다.<br>
이 알고리즘은 Java에서 기본 데이터 타입의 배열을 정렬할 때 사용되는 고급 정렬 알고리즘입니다. <br>
두 개의 피벗을 사용하여 배열을 세 부분으로 나누고, 이 세 부분을 각각 정렬하는 방식으로 작동합니다.

 - 장점
    - 효율성: 대부분의 경우에서 표준 퀵소트보다 더 빠른 성능을 제공합니다.
    - 최적화: 특히 정렬해야 할 데이터의 양이 많을 때 성능 이점이 큽니다.
    - 유연성: 다양한 유형의 데이터 분포에 잘 적응합니다.
    
 - 단점
    - 비안정성: 같은 값을 가진 요소의 상대적 순서가 정렬 후에 바뀔 수 있습니다.
    - 복잡성: 알고리즘의 이해와 구현이 단순 퀵소트보다 복잡할 수 있습니다.
    - 최악의 시나리오: 특정 패턴에서 복잡해지기 때문에 데이터에서는 성능이 저하될 수 있습니다.(여기에 디테일한 예시가 있어야할거같음.)



## TimSort
`TimSort`는 객체 배열을 정렬하기 위해 사용되는 매우 효율적인 정렬 알고리즘입니다. <br>
`Merge Sort`와 `Insertion Sort`를 결합한 형태로, **작은 데이터 세트에는 Insertion Sort의 높은 효율**을, **큰 데이터 세트에는 Merge Sort의 안정성과 효율성**을 제공합니다.<br>
`TimSort`는 먼저 배열을 작은 조각으로 나눈 다음, 각 조각을 `Insertion Sort`로 정렬하고, 정렬된 조각들을 `Merge Sort`로 합칩니다. 

 - 장점
    - 안정성: 같은 값을 가진 요소의 상대적 순서가 유지됩니다.
    - 적응성: 데이터의 초기 정렬 상태를 파악하여, 이미 정렬된 부분을 더 효율적으로 처리합니다.
    - 대규모 데이터에 적합: 큰 데이터 세트에 대해 매우 효율적으로 동작합니다.

 - 단점
    - 복잡성: 구현이 복잡하며, 알고리즘의 모든 세부 사항을 이해하는 데 시간이 걸릴 수 있습니다.
    - 메모리 사용: 추가적인 메모리를 사용할 수 있습니다.

## 결론

`DualPivotQuicksort`와 `TimSort`는 각기 다른 상황과 데이터 유형에 최적화된 Java의 두 주요 정렬 알고리즘입니다.<br>
**`DualPivotQuicksort`는 기본 데이터 타입 배열에 대해 빠르고 효율적인 정렬을 제공하는 반면, `TimSort`는 객체 배열에 대해 안정적이고 효율적인 정렬을 보장합니다.**


## Reference
1. [Velog](https://velog.io/@disdos0928/%EC%96%B4%EB%96%A4-%EC%A0%95%EB%A0%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C)
2. [Dual Pivot Quick Sort](https://dev.to/s_awdesh/double-pivot-quick-sort--javas-default-sorting-algorithm-1m4)
3. [Tim Sort](https://www.geeksforgeeks.org/timsort/?ref=header_search)
4. [Open JDK Dual Pivot Quick Sort](https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/util/DualPivotQuicksort.java)
5. [Open JDK Tim Sort](https://github.com/openjdk-mirror/jdk7u-jdk/blob/master/src/share/classes/java/util/TimSort.java)
