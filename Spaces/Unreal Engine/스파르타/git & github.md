### git
- 버전 관리 도구. 형상 관리 도구

### github
- 온라인 코드 저장소

### git 필수 명령어
- 개인
    - git init
    - git add
    - git commit
    - git push
-  협업
    - git clone
    - git pull
    - git branch
    - git checkout
    - git merge


- 브랜치(branch)
    - main 브랜치
    - dev 브랜치
    - feature 브랜치

[git lfs 설정](https://velog.io/@singery00/UE5-Unreal-%ED%8C%80-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-Git-Github-%EC%97%B0%EB%8F%99#gitignore)


#### CommitLint 규칙

- `feat`: 새로운 기능
- `fix`: 버그 수정
- `docs`: 문서 변경
- `style`: 코드 포맷팅 (공백, 세미콜론 등)
- `refactor`: 리팩토링
- `test`: 테스트 추가/수정
- `chore`: 기타 변경 (빌드 작업 등)

- 예시) fix : 시간 수정

[커밋 메시지에 대한 규칙](https://www.conventionalcommits.org/ko/v1.0.0/)

|타입|설명|예시|
|---|---|---|
|`feat`|새로운 기능 추가|`feat: add AI perception system to DronePawn`|
|`fix`|버그 수정|`fix: resolve AI pathfinding stuck issue`|
|`docs`|문서나 주석 관련 변경|`docs: add explanation on behavior tree setup`|
|`style`|코드 스타일 변경 (기능에 영향 없음)|`style: format AIController with clang-format`|
|`refactor`|리팩토링 (기능 변화 없음)|`refactor: separate sensing logic from controller`|
|`test`|테스트 코드 추가나 수정|`test: add unit test for AI target acquisition`|
|`chore`|빌드, 설정 파일 등 기타 작업|`chore: update .gitignore for generated AI data`|
|`perf`|성능 개선|`perf: optimize tick function in behavior component`