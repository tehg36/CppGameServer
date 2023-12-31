
## 라이브러리 생성

- 정적 라이브러리
	- 빌드시 해당 라이브러리 내용이 포함되어 나간다
	- 일일히 관리 필요가 없다
- DLL (동적 연결 라이브러리)
	- 빌드시 DLL 을 포함시켜줘야 한다
	- 따로 관리를 해야한다


## 생성된 프로젝트 속성 설정
#### Server Core 프로젝트
- 출력 디렉토리 설정
	- 해당 프로젝트 우클릭 -> \[속성] 창
	- 구성 : 모든 구성으로 설정
	- 플랫폼 : 모든 플랫폼
	- 출력 디렉터리 -> 생성한 Libraries 폴더 입력
	- 설정후에 프로젝트 빌드

> 서버의 핵심적인 기능을 따로 분류하여, 다른곳에서도 참조가능

### Game Server 프로젝트
- 기본 구성 설정
	- \[속성] -> 구성속성 -> C/C++ -> 미리컴파일된 헤더
	- 미리 컴파일된 헤더 \[사용안함] -> \[사용] 으로 변경
	- 미리 컴파일된 헤더 파일 \[stdfx.h] -> \[pch.h] 으로 변경
	- pch.cpp 우클릭 -> \[속성] -> 미리 컴파일된 헤더 -> \[사용] -> \[만들기] 로변경
- 출력 디렉터리 설정
	- 프로젝트 속성 -> 일반 -> 출력 디렉터리 편집
		- `$(SolutionDir)Binary\$(Configuration)\`
- 라이브러리 설정
	- 포함 디렉터리, 라이브러리 디렉터리 설정
	- 프로젝트 속성 -> VC++ 디렉터리
		- 포함 디렉터리 수정 : 새로운 경로 추가
			- `$(SolutionDir)ServerCore\`
		- 라이브러리 디렉터리 수정 : 새로운 경로 추가
			- `$(SolutionDir)Libraries\`
	- 따로 링커 부분에서 연결하는 방법도 있지만 번거로우므로, pch.h 에 포함
```cpp
#ifdef _DEBUG
#pragma comment(lib, "Debug\\ServerCore.lib")
#else
#pragma comment(lib, "Release\\ServerCore.lib")
#endif
```
- 프로젝트 빌드
- \[ctl + f5] 로 실행시켜보면 정상 동작 하는 것 확인 가능

### Dummy Client 프로젝트
- 출력 디렉터리 설정
	- 프로젝트 속성 -> 일반 -> 출력 디렉터리 편집
		- `$(SolutionDir)Binary\$(Configuration)\`
- 라이브러리 설정
	- 포함 디렉터리, 라이브러리 디렉터리 설정
	- 프로젝트 속성 -> VC++ 디렉터리
		- 포함 디렉터리 수정 : 새로운 경로 추가
			- `$(SolutionDir)ServerCore\`
		- 라이브러리 디렉터리 수정 : 새로운 경로 추가
			- `$(SolutionDir)Libraries\`
	- 따로 링커 부분에서 연결하는 방법도 있지만 번거로우므로, pch.h 에 포함
- 프로젝트 빌드
- \[ctl + f5] 로 실행시켜보면 정상 동작 하는 것 확인 가능

