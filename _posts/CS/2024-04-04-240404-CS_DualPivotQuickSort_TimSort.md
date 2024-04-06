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

`DualPivotQuicksort`는 두 개의 피벗을 활용한 퀵 정렬의 진화된 형태로, **기본 데이터 타입 배열을 더 효율적으로 정렬하기 위해 Java에서 사용**됩니다.<br>
이 알고리즘의 핵심은 배열을 더 작은 값, 중간 값, 그리고 더 큰 값 세 부분으로 나누어 각각을 정렬하는 데에 두 피벗 값을 사용한다는 점입니다.<br>
**작은 배열에 대해서는 `Insertion Sort`를 적용**하여, **`Quick Sort의` 빠른 분할 능력과 `Insertion Sort`의 작은 데이터 세트에 대한 효율성을 결합함으로써 전체적인 정렬 과정을 최적화**합니다. <br>

 - 장점
    - 효율성: 대부분의 경우에서 표준 퀵소트보다 더 빠른 성능을 제공합니다.<br>
        2개의 피벗을 사용하여 배열을 효율적으로 세 부분으로 나누기 떄문입니다.
    - 최적화: 크기가 큰 배열, 많은 데이터를 정렬할 때 성능 이점을 보여줍니다.<br>
        작은 배열에 대해서 `Insertion Sort`를 적용함으로 전체적인 성능을 극대화합니다.
    - 유연성: 다양한 유형의 데이터 분포에 잘 적응합니다.<br>
        두 개의 피벗을 사용함으로써 더 다양한 데이터 분포에 효과적으로 대응할 수 있습니다.

    
 - 단점
    - 비안정성: 동일한 값을 가진 요소들의 상대적 순서가 정렬 과정 중에 변경될 수 있습니다.
    - 복잡성: 두 개의 피벗을 사용하기에 `QuickSort`보다 복잡할 수 있습니다.
    - 최악의 시나리오: 특정 패턴을 가진 데이터에서는 예상보다 더 낮은 성능을 보일 수 있습니다.<br>
        ex: 이미 대부분 정렬이 되어있거나, 매우 작은 범위의 값들로 구성된 배열에서는 `Insertion Sort`의 사용이 더 효과적일 수 있습니다.


## TimSort
`TimSort`는 객체 배열을 정렬하기 위해 사용되는 매우 효율적인 정렬 알고리즘입니다. <br>
`Merge Sort`와 `Insertion Sort`를 결합한 형태로, 데이터의 크기에 따라 **작은 데이터 세트에는 Insertion Sort을 통한 높은 효율**을, **큰 데이터 세트에는 Merge Sort의 안정성과 효율성**을 제공합니다.<br>
`TimSort`는 먼저 배열을 작은 조각으로 나눈 다음, 각 조각을 `Insertion Sort`로 정렬하고, 정렬된 조각들을 `Merge Sort`로 합칩니다. 

 - 장점
    - 안정성:  `TimSort`는 동일한 값을 가진 요소들 사이의 순서를 유지합니다.<br> 
        즉 데이터의 정렬 순서를 보존합니다.
    - 적응성: 데이터의 현재 상태를 분석하여, 이미 정렬된 시퀀스를 식별하고, 효율적으로 나눈 기준에 따라 내부적으로 처리합니다.
    - 대규모 데이터에 적합: 큰 데이터, 복잡한 데이터 구조에 대한 정렬에 이상적입니다.

 - 단점
    - 복잡성: 구현레벨이 높은편이다.
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
