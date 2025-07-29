GameMode 클래스 - 총괄 관리자

1. 플레이어 캐릭터 - Pawn 클래스 or Character 클래스
2. PlayerController 클래스 - 캐릭터에 빙의
3. 게임 규칙 관리 - 로직(함수) - 점수의 규칙
4. GameState 클래스 - 게임 전역 데이터 - 점수
   PlayerState 클래스 - 개별 개릭터마다의 데이터

Player Controller

1. 입력 처리 - Enhanced Input System - 언리얼 엔진 5
2. 카메라 제어 로직
3. UI와의 상호작용
4. Possess - 빙의 / UnPossess

Enhanced Input System

- 사람 전용 IMC
- 자동차 전용 IMC
- Input Mapping System(IMC)(스위치)
    - IA들을 총괄해서 관리하는

- Input Action(IA) - 추상적인 행동(전선)
    - 점프 -> IA_JUMP     -> Jump 함수
    - 마우스 회전 -> IA_Look    -> Look 함수
    - 이동 -> IA_Move

- 캐릭터 행동
1. 이동 WASD
2. 마우스 회전
3. 점프
4. 스프린트 shift


#### 위쳐3 전투시스템

1. 퍽 시스템
    - 스킬트리 시스템
    - 인자 시스템

2. 라이브 전투
    - 표식
    - 검술
    - 탕약
