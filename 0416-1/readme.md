# 파일 시스템

## 목차
- [파일 시스템의 구조](#파일-시스템의-구조)
- [i-노드와 블록 포인터](#i-노드와-블록-포인터)
- [파일 입출력 구현](#파일-입출력-구현)
- [파일 상태](#파일-상태)
- [파일 타입](#파일-타입)

## 파일 시스템의 구조

파일 시스템은 다음과 같은 주요 구성 요소로 이루어져 있습니다:

### 부트 블록(Boot Block)
- 파일 시스템의 시작 부분에 위치하며, 부트스트랩 코드가 저장됩니다.
- 부트스트랩은 디스크의 운영 체제를 주 메모리로 올리는 역할을 합니다.

### 슈퍼 블록(Super Block)
- 전체 파일 시스템에 대한 정보를 저장하는 블록입니다.
- 총 블록 수, 사용 가능한 i-노드 개수, 사용 중인 블록 수 등의 정보를 포함합니다.

### i-리스트(i-list)
- 각 파일을 나타내는 i-노드들의 리스트입니다.
- 하나의 파일은 하나의 i-노드를 가집니다.

### 데이터 블록(Data Block)
- 파일의 실제 내용(데이터)을 저장하는 블록들입니다.

## i-노드와 블록 포인터

### i-노드(i-node)
- 한 파일은 하나의 i-노드를 가집니다.
- 파일에 대한 모든 정보(파일 타입, 크기, 권한, 소유자 등)를 포함합니다.
- i-노드는 데이터 블록에 대한 포인터를 가지고 있습니다.

### 블록 포인터
- i-노드 내에 있는 데이터 블록의 주소(번호)를 저장하는 영역입니다.
- 직접 블록 포인터, 간접 블록 포인터, 이중 간접 블록 포인터 등이 있습니다.

## 파일 입출력 구현

파일 입출력을 구현하기 위해 커널 내부에는 다음과 같은 자료 구조가 사용됩니다:

### 파일 디스크립터 배열(Fd Array)
- 프로세스 당 하나씩 존재하며, 열린 파일 테이블의 엔트리를 가리킵니다.

### 열린 파일 테이블(Open File Table)
- 현재 열린 모든 파일의 목록을 관리합니다.
- 파일 상태 플래그, 현재 파일 위치 등의 정보를 포함합니다.

### 동적 i-노드 테이블(Active i-node Table)
- 열린 파일들의 i-노드 정보를 저장합니다.

## 파일 상태

파일에 대한 다양한 상태 정보(파일 크기, 사용 권한, 소유자 등)를 i-노드에 저장합니다. `ls -l` 명령어는 이 정보를 이용해 파일 상태를 표시합니다.

## 파일 타입

파일 시스템은 다양한 타입의 파일을 지원합니다:
- 일반 파일
- 디렉터리
- 블록 장치 파일
- 문자 장치 파일
- 심볼릭 링크 파일
- 소켓 파일

이러한 파일 타입은 i-노드의 정보를 통해 구분할 수 있습니다. 
