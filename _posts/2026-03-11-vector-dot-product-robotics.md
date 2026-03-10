---
layout: single
title: "벡터 내적이 로봇에서 왜 중요한가"
date: 2026-03-11 08:00:00 +0900
categories: [Robot Math]
tags: [vector, dot-product, robotics]
---

## 문제

센서 방향 벡터와 목표 방향 벡터가 얼마나 정렬되어 있는지 수치로 판단하고 싶다.

## 개념 설명

내적은 두 벡터의 정렬 정도를 나타낸다. 값이 크면 같은 방향, 0이면 직교, 음수면 반대 방향이다.

## 수식

$$
\mathbf{a}\cdot\mathbf{b}=\|\mathbf{a}\|\|\mathbf{b}\|\cos\theta
$$

단위 벡터를 사용하면 내적값이 바로 $\cos\theta$가 된다.

## Python 코드

```python
import numpy as np

a = np.array([1.0, 2.0])
b = np.array([2.0, 1.0])

dot = np.dot(a, b)
cos_theta = dot / (np.linalg.norm(a) * np.linalg.norm(b))
print("dot:", dot)
print("cos(theta):", cos_theta)
```

## 결과

로봇 heading 제어, 충돌 회피, grasp 방향성 판단에서 유용하다.

## 정리

내적은 로봇 제어에서 "방향 유사도"를 빠르게 계산하는 기본 도구다.
