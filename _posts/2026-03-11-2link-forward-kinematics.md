---
layout: single
title: "2-link robot arm forward kinematics 구현"
date: 2026-03-11 08:40:00 +0900
categories: [Robot Projects]
tags: [2link, forward-kinematics, python]
---

## 문제

2-링크 매니퓰레이터의 조인트 각도에서 엔드이펙터 위치를 구하고 싶다.

## 개념 설명

2D 평면에서 링크 길이 $l_1, l_2$와 각도 $\theta_1, \theta_2$를 사용하면 말단 좌표를 계산할 수 있다.

## 수식

$$
x = l_1\cos\theta_1 + l_2\cos(\theta_1 + \theta_2)
$$
$$
y = l_1\sin\theta_1 + l_2\sin(\theta_1 + \theta_2)
$$

## Python 코드

```python
import numpy as np

l1, l2 = 1.0, 0.8
t1, t2 = np.deg2rad(30), np.deg2rad(45)

x = l1*np.cos(t1) + l2*np.cos(t1+t2)
y = l1*np.sin(t1) + l2*np.sin(t1+t2)

print(f"end-effector: ({x:.3f}, {y:.3f})")
```

## 결과

조인트 각도 변화에 따른 말단 위치를 수치적으로 검증할 수 있다.

## 정리

forward kinematics는 IK, trajectory planning의 기초 단계다.
