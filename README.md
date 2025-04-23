# kart


🏎️ 카트 기본 움직임 & 컨트롤 로직
🔹 입력 구조
Move 벡터: x = 조향, y = 가속/감속, z = 드리프트

IDrive 인터페이스를 통해 입력 주입 (AI/플레이어 모두 사용 가능)

🔹 이동
rigidbody.AddForce()를 사용해 전진/후진 가속력 적용

입력 벡터 y에 따라 정방향 또는 역방향 힘 적용

🔹 조향 (Steering)
속도에 따라 조향 각도 보정

transform.Rotate() 혹은 rigidbody.rotation으로 프레임 단위 회전

정지 상태에서는 회전 제한

🔹 감속 및 마찰
자연 감속 (drag, angularDrag) 적용

이동 중 brakingFriction, driftGripFactor 등으로 마찰 계수 제어

이동하지 않을 때 저항값 증가로 급감속

⚡ 가속 시스템
🔹 추진력
최대 속도 도달 시 추가 추진 차단

accelerationForce 값 사용해 기본 전진력 제공

후진은 reverseSpeed 제한 내에서 구현

🔹 부스트 시스템 (선택적)
특정 조건에서 accelerationBoost 적용 가능 (예: 드리프트 후 부스터 효과)

속도 곡선에 따라 가속도 보간

🎥 카메라 시스템
해당 로직은 KartCameraFollow.cs 및 카트 프리팹 내 설정에 포함됨

🔹 기본 설정
카메라는 Cinemachine 사용

플레이어 카트에 따라 카메라가 자동 추적

"Follow" 및 "Look At" 타겟을 카트의 특정 트랜스폼에 고정

🔹 회전 및 움직임 보정
FaceCamera.cs: UI 요소(이름표 등)가 항상 카메라 방향을 바라보게 함

카트의 속도나 방향에 따라 카메라가 살짝 뒤처지거나 회전 지연 효과 있음

✅ 요약 정리

기능	설명
기본 움직임	Rigidbody 사용한 힘 기반 가속
조향	속도 기반 회전 각 보정
감속/마찰	angularDrag, custom 마찰 계수 사용
드리프트	입력 기반 조향 보정, 마찰력 약화
카메라 추적	Cinemachine으로 타겟 자동 추적 및 뷰 보정
