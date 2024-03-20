
[FString 클래스](https://bit.ly/uefstringkr)

**FString의 구조와 활용**
- 다른 타입에서 FString으로의 변환
	- FString::Printf
	- FString::SanitizeFloat
	- FString::FromInt
- C런타임 수전에서 문자열을 처리하는 클래스 FCString
	- 예) 문자열을 찾는 strstr을 사용
- FString에서 다른 타입으로의 변환(안전하진 않음)
	- FCString::Atoi
	- FCString::Atof
- ![[Pasted image 20240321004314.png]]