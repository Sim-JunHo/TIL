# BOF (버퍼 오버플로우)

---

## 개요

버퍼 오버플로우 (Buffer Overflow) 혹은 버퍼 오버런 (Buffer Overrun)은 메모리를 다루는 데에 오류가 발생하여 잘못된 동작을 하는 프로그램 취약점이다.

프로세스가 데이터를 버퍼에 저장할 때, 버퍼의 사이즈를 넘어가 인접한 메모리 주소에 특정 정보를 덮어쓰는 것을 의미한다. 이때 프로그램 변수, 흐름 제어 데이터 등의 정보를 덮어쓸 수 있다.

시스템 해킹에서 댚표적인 공격 방법 중 하나로, 버퍼라는 것은 일반적으로 데이터가 저장되는 곳을 일컫는데, 단순히 메인 메모리만이 아닌 다른 하드웨어에서 사용하는 임시 저장공간 역시 버퍼라고 부른다. 오버플로우란, 흘러넘치는 것을 뜻하는데 이를 조합해보면 결론적으로 버퍼 공간의 크기보다 큰 데이터를 저장하게 해서 일어나는 오버플로우 현상을 이용한 공격이다.

이를 공부하고 실습하기 위해서는 C언어, 어셈블리, 메모리 구조 등에 대한 이해가 필요하다.

---

## BOF에 취약한 함수

C - strcpy, strcat, gets, fscanf, scanf, sprintf, sscanf, vfscanf, vsprintf, vscnaf, vsscanf, strread, strecpy, strtrns 등. 이와 같은 함수들의 특징은 입력받아 처리하는 문자열의 크기를 지정하지 않는다는 점이다.

---

## 메모리 구조

| 메모리      |                        |                    |             |
| ----------- | ---------------------- | ------------------ | ----------- |
| 코드 영역   | 실행할 프로그램의 코드 |                    | 낮은 주소   |
| 데이터 영역 | 전역 변수, 정적 변수   |                    | 아래로 자람 |
| 힙 영역     | 사용자의 동적 할당     | 런타임에 크기 결정 | 위로 자람   |
| 스택 영역   | 지역 변수, 매개변수    | 컴파일시 크기 결정 | 높은 주소   |

---

## stack BOF

ret값을 변조. BOF가 일어나는 배열의 크기와, 그 배열의 끝부분부터 RET값의 주소까지의 거리를 구해야 함.

---

## NOP BOF

NOP를 이용해 썰매를 타듯 내려와 RET 값을 변조해 관리자 권한을 얻어오는 것. 확률적인 방법이므로 여러번의 시도가 필요하다.

setUID권한을 가진 파일이 실행되는 중간에 관리자 권한의 쉘을 호출하는 코드를 삽입해서 권한을 획득한다.

google more

---

## Heap BOF

heap영역은 스택과 달리 필요할때마다 할당을 하는 형태이다. heap 영역에서의 BOF는 RET의 변조가 아닌, 힙에 저장되는 데이터를 변조하거나 함수에 대한 포인터 값의 변조를 목표로 한다.

---

## 기타

### 환경변수를 이용한 BOF

google it

---

참고문헌 : 

https://m.blog.naver.com/PostView.nhn?blogId=luuzun&logNo=50190684185&proxyReferer=https:%2F%2Fwww.google.com%2F

[https://ko.wikipedia.org/wiki/%EB%B2%84%ED%8D%BC_%EC%98%A4%EB%B2%84%ED%94%8C%EB%A1%9C](https://ko.wikipedia.org/wiki/버퍼_오버플로)