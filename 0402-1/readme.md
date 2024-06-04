
# Make 시스템

## Makefile
### 설치
```bash
sudo apt-get install gcc make  # make 설치
make -v  # 버전 확인
```

### Makefile의 구조
```
대상: 의존성
    명령
```
- 대상 - 만들어질 파일
- 의존성 - 소스
- 명령

### 예제
- `Makefile`
- `main.c`
    - `hello.c`
        - `hello.h`
    - `world.c`
        - `world.h`

# C언어 `<...>`와 `"..."`의 차이
- 컴파일러가 헤더 파일을 검색하는 위치의 차이
- 표준 라이브러리 파일들과 사용자 정의 헤더 파일들을 구분하여 관리하는데 사용됨
- **`#include <...>` (부등호)**
    - → 시스템 표준 경로
    - 시스템 또는 컴파일러의 표준 라이브러리 경로에서 헤더 파일을 검색
    - 표준 라이브러리나 외부 라이브러리 헤더 파일을 포함할 때 사용됨
    - ex) `#include <stdio.h>`
- **`#include "..."` (쌍따옴표)**
    - → 소스 파일의 디렉터리
    - 현재 작업 중인 소스 코드 파일과 같은 디렉토리에서 헤더 파일을 검색
    - 찾지 못하면, 시스템의 표준 라이브러리 경로에서 검색을 시도
    - 주로 사용자 정의 헤더 파일을 포함할 때 사용됨
    - ex) `#include "myheader.h"` (사용자가 작성한 헤더 파일) 


# Linux 시스템 프로그래밍

## 1. 파일 생성 및 닫기

### `create()` 파일 생성
- path가 나타내는 파일을 생성하고 쓰기 전용으로 엶
- 파일이 이미 존재하는 경우 그 내용을 삭제하고 엶
```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int creat (const char *path, mode_t mode);
// 파일 생성에 성공하면 파일 디스크립터를, 실패하면 -1을 리턴
```

### `close()` 파일 닫기
- fd(file description)이 나타내는 파일을 닫음
```c
#include <unistd.h>

int close( int fd );
// fd가 나타내는 파일을 닫음
// 성공하면 0, 실패하면 -1을 리턴
```

## 2. 파일 읽기

### `read()` 데이터 읽기
- fd(file description)이 나타내는 파일에서 nbytes 만큼 읽고, buf(버퍼)에 저장함

```c
#include <unistd.h>

ssize_t read (int fd, void *buf, size_t nbytes);
// 파일 읽기에 성공하면 읽은 바이트 수
// 파일의 끝을 만나면 0
// 실패하면 -1을 리턴
```

## 3. 파일 디스크립터
- 파일 디스크립터(fd)는 
	- 파이프, FIFO, 소켓, 터미널, 디바이스, 일반 파일 등 
	  종류에 상관없이 모든 열려있는 파일을 참조할 때 사용됨
	- open했다면, 실행 파일을 만들고 실행했다면
	  파일 디스크립터를 사용 가능함
	- 어떤 파일을 실행했을 때 모니터와 키보드도 연결됨
		- 모니터, 키보드도 파일에 해당

## 4. 예제 - `fsize.c`
- 파일을 읽고 파일의 사이즈를 출력하는 프로그램
- 파일은 바이트의 연속이므로 리턴 타입으로 `char`가 사용됨
```c title:"fsize.c"
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#define BUFSIZE 512

/* 파일 크기를 계산 한다 */
int main(int argc, char *argv[]) 
{
	char buffer[BUFSIZE];
	int fd;
	ssize_t nread;
	long total = 0;
	if ((fd = open(argv[1], O_RDONLY)) == -1) 
		perror(argv[1]);
	/* 파일의 끝에 도달할 때까지 반복해서 읽으면서 파일 크기 계산 */
	while( (nread = read(fd, buffer, BUFSIZE)) > 0)
		total += nread;
	close(fd);
	printf ("%s 파일 크기 : %ld 바이트 \n", argv[1], total);
	exit(0);
}
``` 
