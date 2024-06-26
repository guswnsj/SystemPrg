
# 파일 시스템 - 디렉터리, 링크

## 목차
- [디렉터리](#디렉터리)
    - [디렉터리 엔트리](#디렉터리-엔트리)
    - [디렉터리 리스트](#디렉터리-리스트)
    - [st_mode 필드](#st_mode-필드)
    - [디렉터리 생성](#디렉터리-생성)
    - [디렉터리 삭제](#디렉터리-삭제)
    - [디렉터리 구현](#디렉터리-구현)
- [링크](#링크)
    - [링크 구현](#링크-구현)
    - [링크의 종류](#링크의-종류)
    - [심볼릭 링크](#심볼릭-링크)
- [핵심 정리](#파일-시스템-핵심-개념-정리)

## 디렉터리
### 디렉터리 엔트리
- 디렉터리 안에는 디렉터리 엔트리로 저장되어 있습니다.

### 디렉터리 리스트
- `opendir()` 함수로 디렉터리를 열고, `readdir()` 함수로 디렉터리 엔트리를 하나씩 읽어올 수 있습니다.

### `st_mode` 필드
- `lstat()` 시스템 호출로 파일 타입과 사용권한 정보를 얻을 수 있습니다.
- `st_mode` 필드에 파일 타입, 특수 용도, 사용 권한 정보가 저장됩니다.

### 디렉터리 생성
- `mkdir()` 시스템 호출로 새로운 디렉터리를 만들 수 있습니다.

### 디렉터리 삭제
- `rmdir()` 시스템 호출로 비어 있는 디렉터리를 삭제할 수 있습니다.

### 디렉터리 구현
- 디렉터리도 일종의 파일로 구현되며, 디렉터리 엔트리에 파일 이름과 i-노드 번호가 저장됩니다.

## 링크
### 링크 구현
- `link()` 시스템 호출로 기존 파일에 대한 새로운 이름을 만들 수 있습니다.
- `unlink()` 시스템 호출로 링크를 삭제할 수 있습니다.

### 링크의 종류
- 하드 링크: 같은 파일 시스템 안에서만 사용 가능한 링크
- 심볼릭 링크: 실제 파일의 경로명을 저장하고 있는 간접적인 링크

### 심볼릭 링크
- `symlink()` 시스템 호출로 심볼릭 링크를 만들 수 있습니다.
- `readlink()` 시스템 호출로 심볼릭 링크의 실제 내용을 읽을 수 있습니다.

## 파일 시스템 핵심 개념 정리
- 표준 Unix 파일 시스템의 구성
- 파일 입출력 구현을 위한 커널 내부 자료 구조
- i-노드의 역할
- 디렉터리의 구조
- 링크의 종류와 특징 
