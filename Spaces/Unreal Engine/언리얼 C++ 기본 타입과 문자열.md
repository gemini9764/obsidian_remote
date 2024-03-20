**게임 제작의 특징**
- 데이터 정보가 명확해야 한다
- 단일 컴퓨터에서 최대 퍼포먼스를 뽑아내야 한다
- 네트워크 상에서 데이터 통신이 효율적이고 안정적이어야 한다

**C++ 최신 규약에서는 int는 최소 32비트를 보장하도록 규정되어 있음**
- C++는 시대의 변화와 맞게 개선 되어 왔다
- 이 때문에 플랫폼에 따라 다르게 동작하기도 하는 플랫폼 파편화(Platform Fragmentation)이 발생 가능
- 특정 플랫폼에서는 64bit로 해석될 수도 있음
- 따라서 데이터를 저장할 때 int 타입의 크기를 확신할 수 없음
- 데이터 타입의 애매 모호함은 게임 개발 시 문제를 일으킬 수 있음

**언리얼 엔진에서 사용하는 기본 타입**
- ==bool== = ==boolean== 값(bool 크기 추정 금지), ==BOOL==은 컴파일되지 않습니다
- ==TCHAR== = character(TCHAR 크기 추정 금지)
- ==uint8== = unsigned byte(1 byte)
- ==int8== = signed byte(1 byte)
- ==uint16== = unsigned "short"(2 byte)
- ==int16== = signed "short"(2 byte)
- ==uint32== = unsigned int(4 byte)
- ==int32== = signed int(4 byte)
- ==uint64== = unsigned "quad word"(8 byte)
- ==int64== = signed "quad word"(8 byte)
- ==float== = single precision floating point(4 byte)
- ==double== = double precision floating point(8 byte)
- PTRINT = 포인터를 가질 수 있는 integer(PTRINT 크기 추정 금지)

**bool 타입의 선언**
- 데이터 전송을 고려한 참/거짓 데이터의 지정
- bool은 크기가 명확하지 않음
- 헤더에는 가급적 bool 대신 uint8 타입을 사용하되 Bit Field 오퍼레이터를 사용
- 일반 uint8과의 구분을 위해 b접두사를 사용
- Cpp 로직에서는 자유롭게 bool을 사용

[[캐릭터 인코딩]]
[[FString의 구조와 활용]]
[]
