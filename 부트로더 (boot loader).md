# 부트로더 (boot loader)

---

## 개요

### OS를 로딩함

머신이 OS를 로딩하면, BIOS는 512바이트의 MBR을 읽어오는데, 하나의 MBR에 단 하나의 OS의 부트 레코드를 저장 가능하기 때문에, 여러 OS를 사용하려 하는 경우, 문제가 생긴다.

### 마스터 부트 레코드

부트로더 전체 혹은 일부와 파티션 테이블을 가지고 있다. BIOS가 로딩되면 하드 드라이브의 첫 번째 섹터에 있는 데이터를 찾는데, 그것이 MBR이다. MBR에 저장된 데이터를 사용하여 BIOS는 부트로더를 활성화한다.

BIOS는 엑세스 할 수 있는 데이터의 양이 적기 때문에, 대부분의 부트로더는 두 단계로 로딩된다

1. BIOS는 IPL로 알려진 부트로더의 일부를 로딩한다. IPL이 파티션 테이블을 검사하고, 다양한 미디어에 존재하는 데이터를 로딩할 수 있다. 이 작업은 두번째 단계의 부트로더가 처음에 자리잡기 위해 사용된다.
2. 두번째 단계가 부트로더의 핵심과도 같은데, 여기에는 사용자 인터페이스(UI), 커널 로더같은 디스크 등의 부분을 포함하고 있다. 이러한 UI들은 간단한 명령행부터 GUI와 관련된 부분까지 다양하다.

### 부트로더의 두가지 방식.

부트로더는 보통 두가지 방식 중 하나(주 부트로더/제2의 부트로더)로 설정이 되는데, 주 부트 로더는 부트로더의 첫 번째 단계가 MBR에 설치되는 장소이다.

제 2의 부트로더는 부트로더의 첫 번째 단계가 부팅 가능한 파티션에 설치되는 장소이다. 개별 부트로더들이 이때 MBR에 설치되고, 컨트롤을 제2의 부트로더에 전달하도록 설정된다.

---

## LILO (LInux LOader)

- 장점 : LILO는 리눅스 초기부터 있던 부트로더이다. 오래된 부트로더인만큼 리눅스 관련 커뮤니티의 지속적인 지원을 받아 꾸준히 사용되었다.
- 단점 : 커널 변경 시, LILO 명령어를 실행해서 변경해주어야 한다.
- 설정파일은 /etc/lilo.config에 위치한다.

---

## GRUB (GRand Unified Bootloader)

GNU GRUB(이하 그럽) 은 GNU 프로젝트의 부트로더이다. 대부분의 OS의 커널을 불러올 수 있으며, 인자를 넘겨줄 수도 있다.

대부분의 그럽은 GRUB Legacy로 분류된다. 현재는 GRUB2의 개발에 착수되었다.

---

### 기능 

- 동적 설정 가능. 부팅 도중 인자값 조정 가능.
- Bash와 같은 명령줄 인터페이스.
- 사용자 정의 부팅 기능
- 파일 시스템 직접 접근 기능
- 다양한 실행파일형식 지원
- 비 멀티부팅 운영체제 지원
- 사람이 읽을수 있는 설정파일 제공
- 메뉴 인터페이스
  - 그래픽 메뉴 및 배경 그림 사용
  - 비 GUI 인터페이스 사용 가능
- 다양한 파일 시스템 지원
- 자동으로 압축 해제 지원
- 지오메트리 정보 독립
- 모든 RAM을 BIOS 관계없이 인식
- LBA 및 네트워크 지원

---

### 설치

LILO와 다르게 변경 후 재설치가 필요없다. 그럽은 스테이지 단위로 부팅 과정이 구성되어 있으며, GRUB의 스테이지 1은 MBR에 존재한다.

GRUB의 설정 파일은 대개 스테이지 2에서 불리며, 이들은 GRUB이 읽을 수 있는 파티션에 존재한다. 설정 파일이 없으면 명령줄로 가며, 설정 파일은 /boot/grub에 저장되어 있고 배포판별로 파일명이 다르다.

이러한 구조 때문에 GRUB 설정 파일이 있던 파티션만 지웠다면 평소 보던 메뉴가 사라지기에 부팅이 되지 않는 것으로 착각할 수 있다.

---

### 지원하는 파일 시스템

- ext2~4
- IBM JFS
- ISO 9660
- ReiserFS
- SGI XFS
- UFS/UFS2
- FAT계열
- NFTS

---

### 지원하는 OS

- 임의의 멀티부팅이 가능한 커널
- FreeBSD, OpenBSD, NetBSD
- 리눅스





