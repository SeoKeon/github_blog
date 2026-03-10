---
layout: single
title: "Inverse Kinematics 수학 이해"
date: 2026-03-10 09:00:00 +0900
categories: [Robot Kinematics]
tags: [ik, geometry, manipulator]
---

## 문제

목표 위치가 주어졌을 때 조인트 각도를 계산하고 싶다.

## 개념 설명

2-link arm은 코사인 법칙을 이용해 기하학적으로 IK를 구할 수 있다. 해는 elbow-up/down 두 가지가 존재한다.

## 수식

$$
\cos\theta_2 = \frac{x^2+y^2-l_1^2-l_2^2}{2l_1l_2}
$$

## Python 코드

```python
import numpy as np

def ik_2link(x, y, l1=1.0, l2=0.8):
    c2 = (x*x + y*y - l1*l1 - l2*l2) / (2*l1*l2)
    s2 = np.sqrt(max(0.0, 1-c2*c2))
    t2 = np.arctan2(s2, c2)
    k1 = l1 + l2*np.cos(t2)
    k2 = l2*np.sin(t2)
    t1 = np.arctan2(y, x) - np.arctan2(k2, k1)
    return t1, t2
```

## 결과

작업공간 내부 목표점에 대해 조인트 해를 계산할 수 있다.

## 정리

IK는 제어/경로계획과 직접 연결되므로 수학적 제약 조건 이해가 중요하다.
