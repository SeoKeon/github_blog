# robot-blog (GitHub Pages + Jekyll)

로봇 엔지니어 커리어 전환을 위한 기술 블로그/포트폴리오 저장소입니다.

## Tech Stack

- GitHub Pages
- Jekyll (`minimal-mistakes`)
- MathJax (LaTeX 수식)
- Rouge code highlighting

## Blog Structure

```text
robot-blog
├ _posts
├ _pages
├ _data
├ assets
├ images
├ projects
├ templates
└ README.md
```

## Categories

- Robot Math
- Robot Kinematics
- ROS2
- Robot Control
- Robot Projects
- Study Log

## Post Template

포스트 작성 시 `templates/post-template.md`를 복사해서 사용하세요.

## Example Posts

- 벡터 내적이 로봇에서 왜 중요한가
- 행렬곱을 로봇 좌표변환 관점에서 이해하기
- 2-link robot arm forward kinematics 구현
- Inverse Kinematics 수학 이해
- ROS2 Publisher Subscriber 구조

## GitHub Portfolio Repo Design

```text
robot-learning
├ robot-math
├ robot-kinematics
├ ros2-practice
├ robot-projects
└ robot-simulation
```

연동 원칙:
1. 각 저장소 README에 블로그 포스트 링크 추가
2. 블로그 포스트에 저장소 링크/커밋 해시/실험 결과 이미지 연결
3. `Portfolio` 페이지에서 프로젝트를 난이도 순으로 큐레이션

## Study Topics (30)

1. 벡터 내적/외적과 로봇 적용
2. 기저벡터와 좌표계 해석
3. 행렬곱과 프레임 변환
4. 고유값/고유벡터와 안정성
5. Jacobian의 물리적 의미
6. 2D 회전행렬과 동차좌표
7. DH 파라미터 정리
8. Forward Kinematics 구현
9. Inverse Kinematics 기하해
10. IK 수치해법(Newton-Raphson)
11. Singularity 분석
12. Workspace 시각화
13. Trajectory planning (joint space)
14. Trajectory planning (task space)
15. PID 제어 튜닝 실습
16. State-space 모델링
17. Kalman Filter 기초
18. ROS2 노드/토픽/서비스 정리
19. ROS2 QoS 설정 실험
20. ROS2 tf2 좌표변환 실습
21. URDF 기본 구조 작성
22. Gazebo 시뮬레이션 연동
23. 센서 데이터 전처리 파이프라인
24. 모터 제어 인터페이스 설계
25. CAN/Serial 통신 안정화
26. 실시간 제어 루프 지연 분석
27. 장애물 회피 기본 알고리즘
28. Mobile robot localization 기초
29. 프로젝트 테스트 전략(pytest + ros2 test)
30. 로봇 포트폴리오 프로젝트 회고

## GitHub Pages Setup

1. GitHub에서 `SeoKeon/github_blog` 저장소 생성
2. 이 저장소를 `main` 브랜치로 푸시
3. `Settings > Pages`에서 `Source: GitHub Actions` 선택
4. Actions 탭에서 배포 성공 확인
5. 접속: `https://seokeon.github.io/github_blog/`
