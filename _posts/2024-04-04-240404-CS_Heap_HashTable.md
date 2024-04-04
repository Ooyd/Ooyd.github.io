---
layout: post
title: "Heap, Priority Queue, HashTable 이해하기"
date: '2024-04-02 03:00:00 +0900'
description: 'CodingTest'
categories: [Computer Science Fundamentals, Data Structure]
tags: [Heap, Priority Queue, HashTable]

---
# 힙, 우선순위 큐, 해시 테이블 이해하기

코딩 테스트를 준비할 때마다, Heap, Priority Queue, HashTable 같은 자료구조에 대해 간단히 정리하여 이해하고 활용하는 것이 중요합니다.

<br>

## 힙(Heap)

힙은 완전 이진 트리를 기반으로 한 자료구조로, 각 노드가 자식 노드보다 작거나 같은(Min Heap) 또는 크거나 같은(Max Heap) 값을 가집니다. 우선순위 큐 구현에 이상적입니다. <br>
최대값 또는 최소값을 빠르게 찾아내야 할 때 유용한 완전 이진 트리 기반의 자료구조입니다.

### 주요 연산
- `insert(key)`: 새로운 요소를 힙에 추가합니다.
- `extractMax()` / `extractMin()`: 힙에서 최댓값 또는 최솟값을 제거하고 반환합니다.
- `peek()`: 힙의 최댓값 또는 최솟값을 조회하지만 제거하지는 않습니다.

### 코딩 테스트에서의 활용
- **동적 데이터 집합에서 최댓값 또는 최솟값 접근이 자주 필요할 때**: <br>
실시간으로 데이터가 추가/제거되며, 이 중 최댓값 또는 최솟값을 빠르게 접근해야 하는 경우
- **우선순위가 있는 작업 스케줄링이 필요할 때**: <br> 
작업들이 우선순위를 가지고 있으며, 우선순위가 가장 높은 작업부터 처리해야 하는 경우



<br><br>

## 우선순위 큐(Priority Queue)

우선순위 큐는 요소들이 우선순위를 가지고 있으며, 우선순위가 가장 높은 요소부터 제거되는 자료구조입니다.

### 주요 연산
- `push(element, priority)`: 주어진 우선순위를 가진 요소를 우선순위 큐에 삽입합니다.
- `pop()`: 우선순위가 가장 높은 요소를 우선순위 큐에서 제거하고 반환합니다.
- `peek()`: 우선순위가 가장 높은 요소를 조회하지만 제거하지는 않습니다.

### 우선 순위 정의하는 람다식의 예제
#### 숫자 비교 (오름차순/내림차순)
- 오름차순 우선 순위 : 가장 낮은 숫자가 높은 우선순위를 갖습니다.
```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>((a, b) -> a - b);
```
- 내림차순 우선 순위 : 가장 높은 숫자가 높은 우선순위를 갖습니다.
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
```

#### 문자열 길이 비교
- 짧은 문자열 우선순위: 문자열 길이가 짧은 것이 높은 우선순위를 갖습니다.
```java
PriorityQueue<String> byLength = new PriorityQueue<>((a, b) -> a.length() - b.length());
```
- 긴 문자열 우선순위: 문자열 길이가 긴 것이 높은 우선순위를 갖습니다.
```java
PriorityQueue<String> byLengthDesc = new PriorityQueue<>((a, b) -> b.length() - a.length());
```

#### 복잡한 객체 비교
- 객체의 특정 필드를 기준으로 우선순위를 정할 수 있습니다. 예를 들어, 사람(Person) 객체가 있고, 이를 나이(age)를 기준으로 우선순위를 정하려면:

```java
class Person {
    String name;
    int age;
}

PriorityQueue<Person> byAge = new PriorityQueue<>((a, b) -> a.age - b.age);
```
#### 복합 조건 비교
- 때로는 여러 조건을 결합하여 우선순위를 정의할 필요가 있습니다. 예를 들어, 사람 객체를 나이가 같을 경우 이름의 알파벳 순으로 정렬하고 싶다면:

```java
PriorityQueue<Person> complexOrder = new PriorityQueue<>((a, b) -> {
    if (a.age == b.age) return a.name.compareTo(b.name);
    else return a.age - b.age;
});
```

### 코딩 테스트에서의 활용
- **다양한 요소들 중에서 우선순위에 따라 처리 순서를 결정해야 할 때**: 
<br> 예를 들어, 여러 사용자의 요청을 우선순위에 따라 처리하거나, 네트워크 트래픽을 관리할 때 유용합니다.
- **그래프 알고리즘에서 최소 비용 문제를 해결해야 할 때**: <br>
다익스트라 알고리즘과 같이 최소 비용 또는 최소 시간으로 목적지에 도달하는 경로를 찾는 문제에 적합합니다.


<br><br>

## 해시 테이블(HashTable)

해시 테이블은 키를 값에 매핑하는데 사용되는 자료구조입니다. 해시 함수를 사용해 키를 배열 인덱스로 변환하고, 이 인덱스를 사용해 값을 저장 또는 검색합니다.
<br> 빠른 데이터 검색, 삽입, 삭제를 가능하게 합니다.

### 주요 연산
- `put(key, value)`: 주어진 키에 값을 저장합니다.
- `get(key)`: 주어진 키에 해당하는 값을 조회합니다.
- `remove(key)`: 주어진 키와 그 키에 해당하는 값을 해시 테이블에서 제거합니다.


### 코딩 테스트에서의 활용
- **데이터에 대한 빠른 접근이 필요할 때**: <br>
예를 들어, 사용자 ID로 사용자 정보를 빠르게 검색해야 하는 경우
- **중복 체크나 빈도수 계산이 필요할 때**: <br>
 문자열 내의 문자 빈도수 계산이나, 배열 내의 중복 요소 검사 등 데이터의 특성을 분석할 때 유용합니다.