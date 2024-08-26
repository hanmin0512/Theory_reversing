# X86 Assembly

## 서론

### 어셈블리
David Wheeler는 EDSAC을 개발하면서 어셈블리 언어와 어셈블러라는 것을 고안했다. 이를 통해 개발자들이 어셈블리어로 코드를 작성하면 어셈블러가 컴퓨터가 이해할 수 있는 기계어로 번역해주는 역할을했다.

리버스 엔지니어는 여기에 더해 기계어를 어셈블리언어로 번역하는 역어셈블러가 개발 됐다.

### x64 어셈블리 언어 기본 구조

명령어와 피연산자로 구성된다.
| opcode | operand1 | operand2 |
|--------|----------|----------|
| mov | eax, | 5 |

5를 eax 레지스터에 대입하라는 명령어 이다.


| 명령어 종류 | 코드 |
|----------|----------|
| 데이터 이동 | mov, lea |
| 산술 연산 | inc, dec, add, sub |
| 논리 연산 | and, or, xor, not |
| 비교 | cmp, test |
| 분기 | jmp, je, jg |
| 스택 | push, pop |
| 프로시져 | call, ret, leave |
| 시스템 콜 | syscall | 

### 피연산자
피연산자(operand)에는 총 3가지 종류가 올 수 있다.
- 상수(Immediate Value)
- 레지스터(Register)
- 메모리(Memory)

메모리 피연산자는 []로 둘러싸인 거으로 표현되며, 앞에 크기 지정자 TYPE PTR이 추가될 수 있습니다. 타입에는 BYTE(1바이트), WORD(2바이트), DWORD(4바이트), QWORD(8바이트)가 올 수 있다.

| 메모리 피연산자 | 설명 |
|----------|----------|
| QWORD PTR [0x8048000] | 0x8048000의 데이터를 8바이트만큼 참조 |
| DWORD PTR [0x8048000] | 0x8048000의 데이터를 4바이트만큼 참조 |
| WORD PTR [rax] | rax가 가르키는 주소에서 데이터를 2바이트 만큼 참조 |

### 데이터 이동(mov)
| 메모리 피연산자 | 설명 |
|----------|----------|
| mov rdi, rsi | rsi의 값을 rdi에 대입 |
| mov QWORD PTR[rdi], rsi | rsi의 값을 rdi가 가리키는 주소에 대입 |
| mov QWORD PTR[rdi+8*rcx], rsi | rsi의 값을 rdi+8*rcx가 가리키는 주소에 대입 |
| lea rsi, [rbx+8*rcx] | rbx+8*rcx 를 rsi에 대입 |

예시1) ebx = 0x14215 일 때, 메모리주소 0x14215의 값은 5가 저장되어 있다고 가정한다.
mov eax, [ebx] => ebx값이 가리키는 메모리 주소에 저장된 값 5를 eax에 저장한다는 의미 이다.

예시2) rdi=0x14215(메모리주소), rsi = 0xDEADBEEFCAFEBABE(64비트 값) 이다. QWORD는 8bytes 이다.
mov QWORD PTR[rdi], => rsi 0x14215주소에 데이터 0xDEADBEEFCAFEBABE를 저장

예시3) rdi = 0x1000, rcx=2(count), rsi= 0xDEADBEEFCAFEBABE
mov QWORD PTR[rdi+8*rcx], rsi => 0x1000 + (8*2) ==> rsi = 0x1010 (16진수) 
===> 0x1010 주소에 rsi 값을 저장한다 [0x1010] = 0xDEADBEEFCAFEBABE
(이 명령어는 배열의 특정 요소에 접근하여 값을 저장하는 일반적인 패턴입니다. 배열 요소의 크기가 8바이트이고, rcx가 배열의 인덱스를 나타낸다면, 이 명령어는 rcx 인덱스에 해당하는 배열 요소에 rsi의 값을 저장하는 역할을 한다.)





