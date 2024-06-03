
# Linux 파일 시스템과 디스크 관리

## 주요 파일 시스템
- **EXT4**: 리눅스의 대표적인 저널링 파일 시스템
- **XFS**: 확장성이 뛰어난 64bit 저널링 파일 시스템
- **ZFS**: 안정성, 성능, 데이터 보호 기능이 강화된 파일 시스템
- **NTFS**: Windows의 기본 파일 시스템으로, 안정성과 보안 기능이 강화됨

## 주요 디스크 관리 명령어
- **df**: 마운트된 파일 시스템의 디스크 여유 공간 확인
- **du**: 특정 디렉터리의 디스크 사용량 확인
- **lsblk**: 시스템에 연결된 블록 장치 정보 확인
- **fdisk**: 파티션 관리 도구
- **blkid**: 블록 장치의 UUID, 파일 시스템 유형 정보 확인
- **mount**: 파일 시스템을 디렉터리에 마운트

## 파일 시스템 점검 및 복구
- **bad block**: 디스크의 불량 섹터
- **fsck**: 파일 시스템 무결성 검사 및 복구
- **badblocks**: 디스크의 불량 섹터 검사

## Bad Block 관리

### Bad Block이란?
- 데이터를 읽어올 수 없는 디스크 저장 장치의 불량 블록
- 다른 용어로 'bad sector'라고도 부름

### Bad Block 발생 원인
- Soft Bad Block: 논리적인 요인으로 인한 문제
  - 정전, 비트 오류, 펌웨어 등의 문제
- Hard Bad Block: 물리적인 요인으로 인한 문제
  - 저장 장치에 물리적인 문제 (충격, 먼지 침투 등)

### fsck (file system check)
- Linux 파일 시스템에서 파일을 체크하고 수리하는 명령어
- 옵션:
  - `-A`: 모든 파일 시스템 점검
  - `-R`: 루트 파일 시스템을 제외한 나머지 점검
  - `-V`: 자세히 출력
  - `-f`: 강제 검사
  - `-y`: 모든 질문에 yes로 대답
  - `-a`: 문제 발생 시 자동 복구

### badblocks
- Linux에서 하드디스크나 기타 저장 장치의 배드 블록을 검사하는 명령어
- 옵션:
  - `-b 블록크기`: 블록크기 지정
  - `-o 파일명`: 배드 블록 리스트를 파일에 기록
  - `-v`: 자세한 출력 모드
  - `-w`: 읽기/쓰기 모드로 배드블록 검사
  - `-n`: 비파괴 읽기/쓰기 모드로 검사
