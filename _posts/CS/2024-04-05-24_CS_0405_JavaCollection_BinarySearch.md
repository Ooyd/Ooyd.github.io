---
layout: post
title: "정렬과 이진 탐색 이해하기"
date: '2024-04-05 03:00:00 +0900'
description: 'CodingTest'
categories: [Computer Science Fundamentals, Algorithms]
tags: [Sorting, Binary Search]

---
# 정렬과 이진 탐색 이해하기
코딩 테스트 준비 과정에서 중요한 알고리즘중 두 가지, 정렬과 이진탐색에 대해 간단하게 정리해보려고 작성한 글입니다.

## 정렬 (Java Collection) : 데이터를 체계적으로 배치하기

정렬은 데이터를 일정한 순서대로 나열하는 처리 방법입니다.<br>
Java에서는 **Collections와 Arrays** 클래스를 통해 컬렉션과 배열의 데이터를 손쉽게 정렬할 수 있습니다.


### Java의 정렬 알고리즘 : Tim Sort를 사용한(생략가능)
- Java의 정렬 메소드들은 내부적으로 Tim Sort 알고리즘을 사용합니다.<br>
- Tim Sort는 병합 정렬과 삽입 정렬의 장점을 결합한 안정적인 정렬 알고리즘으로, 최악의 경우에도 O(n log n)의 시간 복잡도를 보장합니다.
- **큰 데이터 세트에 대한 효율성**과 **작은 데이터 세트에 대한 민첩함**을 동시에 제공하기 때문에, 다양한 크기의 데이터를 처리하는 데 유용합니다.

#### Tim Sort 알아볼때 봤었던 글들(생략가능)

- [Tim sort에 대해 알아보자](https://d2.naver.com/helloworld/0315536)
- [Java - Tim Sort](https://st-lab.tistory.com/276)
- [Tim sort_Wiki](https://ko.wikipedia.org/wiki/%ED%8C%80%EC%86%8C%ED%8A%B8)

### 정렬 설명
Array와 Collection의 경우에 대한 예제 코드는 다음과 같습니다:

- Array의 경우 예제코드
```java
Integer[] array = {9, 5, 3, 7, 2};
Arrays.sort(array);
System.out.println(Arrays.toString(array)); // [2, 3, 5, 7, 9]
```

- Collection의 경우 예제코드

```java
List<Integer> list = new ArrayList<>(Arrays.asList(9, 5, 3, 7, 2));
Collections.sort(list);
System.out.println(list); // [2, 3, 5, 7, 9]
```

### 정렬 알고리즘에서 Stream 활용 방법
Java 8 이상부터 Stream API를 사용해 간결하게 사용가능합니다.
<br>
Stream API는 데이터를 효율적으로 처리할 수 있는 기능을 제공하며, `sorted()`
메소드를 사용하면 데이터를 쉽게 정렬할 수 있습니다.<br>
`sorted()` 메소드는 **Tim Sort 알고리즘**을 사용합니다.

```java
List<Integer> sortedList = list.stream().sorted().collect(Collectors.toList());
System.out.println(sortedList); // [2, 3, 5, 7, 9]
```

[Stream 학습](https://www.inflearn.com/course/the-java-java8?utm_source=google&utm_medium=pmax&utm_campaign=catalogue_regular_1-ALL-Price-1000&utm_content=responsive_branding_re&utm_term=240207_all&gad_source=1&gclid=Cj0KCQjwn7mwBhCiARIsAGoxjaJCzuMyOaWiy7qV2CDPK2eBmcf9yC7zOT0rEv6glHbMAmu2VpLh5toaAoS8EALw_wcB)


## 이진 탐색(Binary Search)
- 이진 탐색은 정렬된 배열에서 특정한 값을 찾아내는 효율적인 방법입니다.
- 이진 탐색은 시작할 때 중간값을 선택하고, 찾고자 하는 값이 중간값보다 큰지 작은지를 판단하여 탐색 범위를 줄여나갑니다.
- 이진탐색은 데이터가 정렬되어있어야지 사용가능합니다.


### 시간복잡도
- O(log n). 탐색할 때마다 범위를 절반으로 나누어서 빠른 탐색속도 보장합니다.

### 구현 코드
이진 탐색을 구현한 코드는 다음과 같습니다:


```java
public int binarySearch(int[] arr, int target) {
    int low = 0;
    int high = arr.length - 1;

    while(low <= high) {
        int mid = low + (high - low) / 2; // 중간값 계산
        if(arr[mid] == target) {
            return mid; // 타겟을 찾은 경우
        } else if(arr[mid] < target) {
            low = mid + 1; // 타겟이 중간값보다 큰 경우
        } else {
            high = mid - 1; // 타겟이 중간값보다 작은 경우
        }
    }

    return -1; // 타겟을 찾지 못한 경우
}
```


### 코딩 테스트에서의 활용
이진 탐색은 주어진 문제의 **데이터가 정렬되어 있어야 사용 가능**하며, **특정 값을 찾거나, 가장 가까운 값을 찾아야 할 때 유용**합니다. <br>
예를 들어, 정렬된 배열에서 특정 값의 위치를 찾는 문제나, 정렬된 배열에서 특정 값보다 큰 가장 작은 값을 찾는 문제 등에서 이진 탐색을 활용할 수 있습니다.


