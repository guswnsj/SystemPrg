

## if-then 문 사용하기

Bash 셸의 if-then 문 형식은 다음과 같습니다:

```bash
if command
then
    commands
fi
```

- 명령의 종료 상태가 0인 경우, `then` 섹션 아래에 나열된 명령이 실행됩니다.
- 명령의 종료 상태가 다른 값인 경우, `then` 명령은 실행되지 않고, Bash 셸은 다음 명령으로 이동합니다.

## if-then-else 문

if 문 줄의 명령이 종료 상태 코드를 0이 아닌 것을 반환하면 `else` 섹션의 명령이 실행됩니다.

```bash
if command
then
    commands
else
    commands
fi
```

## 숫자 비교 조건식

- `$val1 -gt 5`: 변수 `val1`의 값이 5보다 큰가
- `$val1 -eq $val2`: 변수 `val1`의 값이 변수 `val2`의 값과 같은가

## 문자열 비교

- `[ $USER = $testuser ]`: 사용자 이름이 `$testuser`와 같은가
- `[ $USER != $testuser ]`: 사용자 이름이 `$testuser`와 다른가

