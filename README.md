# Reversing Engineering

## 개요
### Reversing Engineering 개념
완성된 소프트웨어를 해체하고 분석하여 구조와 기능, 디자인을 파악하는 행위이다.

### Reversing Engineering의 용도
- 프로그램의 보안성을 평가하거나 악성코드를 분석할 때
- 유료로 판매되는 프로그램들이 정품 인증을 하는지 분석 후 크랙할 때
- 소프트웨어 학습 및 연구 (프로그램 전체적인 작동 원리)
- 각종 악성코드나 불법 프로그램의 분석 및 대응

### 윤리적 위험성
> 상용 프로그램의 지적 재산권을 침해할 수 있다는 위험성도 존재합니다.

## 배경
소프트웨어를 분석할 때는 일반적으로 큰 구조를 관찰한다. 이후 프로그램을 실행해보며 동작을 관찰 할 수 있다. 더욱 더 자세한 분석이 필요할 때는 특정 부분을 세밀하게 분석한다. 정적 분석과 동적 분석 중 한 방법만을 고수하는 것이 아니라 상황에 따라 적절한 방법을 선택해야 한다. 어떤 상황에 어떤 방법을 선택할 것이냐가 리버싱 실력을 좌우하는 중요한 요소이다.

### 정적 분석
외적인 관찰만을 통해 정보를 알아내는 것

### 동적 분석
프로그램 실행을 통해 동작을 분석하는 것

### 프로그램
연산 장치가 수행해야 하는 동작을 정의한 것이다. 프로그램을 연산 장치에 전달하면, CPU는 적혀있는 명령들을 처리하여 프로그래머가 정의한 동작을 수행한다. 

컴퓨터는 프로그램을 메모리에 저장할 수 있었는데, 기존의 컴퓨터들보다 월등히 많은 프로그램을 저장할 수 있었으며, 저장된 프로그램을 사용하는 것도 간편해졌다. 그래서 이제는 컴퓨터의 대부분이 Stored-Program Computer의 형태로 개발된다. 소프트웨어 개발자, 해커 등 많은 정보 분야의 엔지니어들이 프로그램을 바이너리(Binary)라고 부르곤 하는데, 이는 프로그램이 저장 장치에 이진(Binary) 형태로 저장되기 때문이다 소프트웨어 개발자, 해커 등 많은 정보 분야의 엔지니어들이 프로그램을 바이너리(Binary)라고 부르곤 하는데, 이는 프로그램이 저장 장치에 이진(Binary) 형태로 저장되기 때문입니다


### 컴파일
CPU가 처리해야 할 명령어를 프로그래밍 언어로 작성한 소스코드를 컴퓨터가 이해할 수 있는 기계어의 형식으로 변역하는 것을 컴파일이라고 한다.

> 어떤 언어로 작성된 소스 코드를 Object Code로 번역 하는 것

### 컴파일러
컴파일을 해주는 소프트웨어
- GCC
- Clang
- MSVC

### 전처리
컴파일러가 소스 코드를 어셈플리어로 컴파일 하기전에, 필요한 형식으로 가공하는 과정
1. 주석 제거
2. 매크로 치환(매크로의 이름은 값으로 치환)
3. 파일 병합

#### 전처리 과정 파일 병합
```
gcc -E add.c > add.i
```
> add.c 파일을 위 명령어를 통해 전처리 한결과인 add.i파일 내용을 볼 수 있다.(주석 있을 시 주석 제거, 매크로는 값으로 치환을 한다)
<img width="1003" alt="스크린샷 2024-08-25 오후 2 34 45" src="https://github.com/user-attachments/assets/6735b88e-7517-4a4b-b37c-6dd5407a374e">



## 요약
이 보고서는 윈도우 PE 바이너리 파일을 리버스 엔지니어링 하는 것을 다룬다.

## 컴파일 과정
C로 작성된 소스 코드를 어셈블리어로 변역하는 과정이다. gcc에서는 아래와 같은 옵션을 사용하여 최적화하여 효율적인 어셈블리 코드를 생성 해준다.
```
-o -o0 -o1 -o2 -o3 -os -ofast -og
```

### C 언어 컴파일
C언어로 작성된 코드는 일반적으로 전처리, 컴파일, 어셈블, 링크의 과정을 거쳐 바이너리 파일이 된다.

```
gcc -o opt opt.c -O2
gdb opt
```
<img width="1103" alt="스크린샷 2024-08-25 오후 2 49 27" src="https://github.com/user-attachments/assets/6e411c96-4553-47cd-ba55-b585b501bed8">

> add.i 파일을 어셈블리 코드로 컴파일
```
gcc -S add.i -i add.S
```
<img width="948" alt="스크린샷 2024-08-25 오후 2 51 01" src="https://github.com/user-attachments/assets/da2f8913-6e5c-4366-bc2c-7d009a38116e">

## 어셈블
어셈블(Assemble)은 컴파일로 생성된 어셈블리어 코드를 ELF 형식의 Object파일로 변환 하는 과정이다. Object파일로 변환되고 난 후 어셈블리 코드가 기계어로 번역되므로 더이상 사람이 이해하기 어려워진다.

> 리눅스 실행파일: ELF
> 윈도우 실행파일: PE

### 어셈블 과정
```
gcc -c add.S -o add.o
file add.o
hexdump add.o
```

<img width="626" alt="스크린샷 2024-08-25 오후 2 56 57" src="https://github.com/user-attachments/assets/609a525f-cd61-4b21-a146-9dfb1aca4717">

## 링크
여러 목적 파일들을 연결하여 실행 사능한 바이너리로 만드는 과정

###링킹 과정
```
#include <stdio.h>

int main() { printf("Hello, world!"); }
```
위 코드에서 printf 함수를 호출 하지만 printf 함수는 libc라는 공유라이브러리에 정의되어 있다. 링커는 바이너리가 printf를 호출하면 libc의 함수가 실행될수 있도록 연결해준다. 이렇게 링크 과정을 거치고 나면 실행할 수 있는 프로그램이 완성 된다.

#### add.o 목적파일 링크 과정
add.o 목적 파일을 링크하는 명령어 이다. 링크 과정에서 링커는 main 함수를 찾는다. 하지만 add.c 소스 코드에는 main 함수의 정의가 없으므로 에러가 발생한다. 이를 방지 하기 위해 '--unresolved-symbols'를 컴파일 옵션에 추가해 준다.

```
$ gcc add.o -o add -Xlinker --unresolved-symbols=ignore-in-object-files
$ file add
```
<img width="874" alt="스크린샷 2024-08-25 오후 3 16 59" src="https://github.com/user-attachments/assets/129e53a4-344f-4e1a-b2d6-8e2a8ba2f0b0">




## 디스 어셈블
어셈블의 역과정을 디스 어셈블 이라고 하며, 바이너리 파일을 어셈블리어 재번역하는 과정이다.

## 디컴파일
컴파일 역과정을 디컴파일 이라고 하며, 어셈블리어를 고급언어로 바이너리 파일을 번역하는 과정이다.

코드를 작성할 때 사용했던 변수나 함수의 이름 등은 컴파일 과정에서 전부 사라지고, 코드의 일부분은 최적화와 같은 이유로 컴파일러에 의해 완전히 변형 되기도 한다. 이런 어려움으로 인해 디컴파일러는 일반적으로 바이너리의 소스 코드와 동일한 코드를 생성하지 못한다. 그러나 이러한 오차가 바이너리의 동작을 왜곡하지 않는다면 분석 효율측면에서 매우 좋기 때문에 디컴파일러를 사용할 수 있다면 반드시 디컴파일러를 사용하는 것이 유리하다.

### 디컴파일러 툴 종류
- Hex Rays
- Ghidra
- IDA Freeware

등

## 정적 분석
정적 분석은 프로그램을 실행 시키지 않고 분석하는 방법이다.

### 정적 분석의 장점
- 프로그램의 전체구조(함수, 호출 관계, API, 문자열)를 파악하기 쉽다.
- 분석 환경 제약으로 부터 자유롭다.
- 바이러스와 같은 악성 프로그램으로 부터 안전하다.

### 정적 분석의 단점
- 난독화가 적용되면 분석이 어려워진다.
- 다양한 동적 요소를 고려하기 어렵다.


## 동적 분석
동적 분석은 프로그램을 실행시키면서 분석하는 방법이다.

### 동적 분석의 장점
- 코드를 자세히 분석해보지 않고도 프로그램의 개략적인 동작을 파악할 수 있다.

### 동적 분석의 단점
- 분석 환격을 구축하기 어려울 수 있다.
- 안티 디버깅이 존재 할 수 있다.

## 컴퓨터 구조
컴퓨터가 효율적으로 작동할 수 있도록 하드웨어 및 소프트웨어 기능을 고안하고 구성하는 방법이다.
- 기능 구조의 설계
- 명령어 집합구조
- 마이크로 아키텍처
- 기타 하드웨어 및 컴퓨팅 방법

### 기능 구조의 설계
- 폰 노이만 구조
- 하버드 구조
- 수정된 하버드 구조

### 명령어 집합 구조
- x86, x86-64
- ARM
- MIPS
- AVR

### 마이크로 아키텍처
- 캐시 설걔
- 파이프라이닝
- 슈퍼 스칼라
- 분기 예측
- 비순차적 명령어 처리

### 하드웨어 및 컴퓨팅 방법론
- 직접 메모리 접근

#### 폰 노이만 구조
근대의 컴퓨터는 연산과 제어를 위해 중앙처리장치를 저장을 위해 기억장치를, 제어 신호를 교환 할수 있는 버스라는 전자 통로를 사용한다.

##### 중앙처리장치
CPU는 프로그램의 연산을 처리하고 시스템을 제어하는 컴퓨터의 두뇌이다. 코드를 불러오고, 실행하고, 결과를 저장하는 일련의 모든 과정이 CPU에서 일어난다. CPU는 산술/논리 연산을 처리하는 ALU, 제어장치, 레지스터 등으로 구성된다.

##### 기억장치
기억장치는 컴퓨터가 동작하는데 필요한 여러 데이터를 저장하기 위해 사용된다. 주기억장치(RAM), 보조기억장치(HDD, SSD)로 분류된다.


##### 버스
컴퓨터 부품과 부품 사이 또는 컴퓨터와 컴퓨터 사이에 신호를 전송하는 통로. 데이턱 ㅏ이동하는 데이터 버스, 주소를 지어하는 주소 버스, 읽기/쓰기를 제어하는 제어 버스가 있다. 이외에도 랜선이나 데이터 전송을 목적으로 하는 소프트웨어, 프로토콜 등도 버스라고 불린다.


## 명령어 집합 구조
CPU가 해석하는 명령어의 집합을 의미한다. 프로그램 코드는 기계어로 작성되어 있으며, 프로그램을 실행하면 기계어로 작성된 명령어를 CPU가 읽고 처리한다.

## x86-64 아키텍처
범용적이고 중립적으로 지칭되는 x86-64라는 명칭의 아키텍처 기반의 CPU를 대부분 탑재하고 있다. 64, 32 비트는 CPU가 한번에 처리할 수 있는 데이터 크기이다. 컴퓨터과학에서는 이를 CPU가 이해할 수 있는 데이터 단위로 WORD라고 한다. 32비트 아키텍처에서는 ALU는 32비트까지 계산할 수 있으며, 레지스터의 용량 및 각종 버스들의 대역복도 32비트 이다.

### WORD가 크면 유리한 점
현대의 PC는 대부분 64비트 아키텍처의 CPU를 사용하는데, 그 이유 중 하나는 32비트 아키텍처의 CPU가 제공할 수 있는 가상메모리의 크기가 작기 때문이다. 가상메모리는 CPU가 프로세스에게 제공하는 가상의 메모리 공간인데, 32비트 아키텍처에서는 4GB가 최대로 제공하는 가상메모리 크기이다. 많은 메모리 자원을 소모하는 저문 소프트웨어나 고사양의 게임 등을 실행할 때는 부족한 크기 이다.

반면 64비트 아키텍처는 이론상 16헥사바이트의 가상 메모리를 제공한다.

### x86-64의 여려 명칭
- Intel64
- IA-32e
- EM64T
- AMD64

## x86-64 아키텍처 [레지스터]
CPU의 내부 저장장치로, CPU가 빠르게 접근하여 사용할 수 있는 저장장치이다. 산술 연산에 필요한 데이터를 저장하거나 주소를 저장하고 참조하는 등의 다양한 용도로 사용된다.

### 레지스터 종류
- 범용 레지스터
- 세그먼트 레지스터
- 명령어 포인터 레지스터
- 플래그 레지스터

#### 범용 레지스터
x86-64에서 각각의 범용 레지스터는 8바이트를 저장할 수 있으며, 부호 없는 정수를 기준으로 2^64 -1까지 나타낼 수 있다.



| 이름 | 용도 |
|--------|----------|
| rax    | 함수의 반환 값  |
| rbx    | x64에서 주된 용도 없음   |
| rcx    | 반복문의 반복 횟수, 각종 연산의 시행 횟수   |
| rdx    | x64에서 주된 용도 없음   |
| rsi    | 데이터를 옮길 때 원본을 가리키는  포인터   |
| rdi    | 데이터를 옮길 때 목적지를 가리키는 포인터   |
| rbp    | 스택의 바닥을 가리키는 포인터   |


#### 세그먼트 레지스터
현대 x64에서 세그먼트 레지스터 cs, ds, ss는 코드영역과 데이터, 스택 메모리 영역을 가리킬 때 사용된다.

#### 명령어 포인터 레지스터
기계어로 작성된 부분을 CPU가 어느 부분의 코드를 실행할지 가리키는게 명령어 포인터 레지스터의 역할이다. x64아키텍처의 명ㄹ여어 레지스터는 rip이며, 크기는 8바이트 이다.

#### 플래그 레지스터
프로세서의 현재 상태를 저장하고 있는 레지스터로, x64 아키텍처에서는 RFLAGS라고 불리는 64비트 크기의 플래그 레지스터가 존재한다.

| 플래그 | 의미 |
|--------|----------|
| CF    | 부호 없는 수의 연산 결과가 비트의 범위를 넘을 경우 설정된다.  |
| ZF    | 연산의 결과가 0일 경우 설정된다.   |
| SF    | 연산의 결과가 음수일 경우 설정된다.   |
| OF    | 부호 있는 수의 연산 결과가 비트 범위를 넘을 경우 설정된다.   |






