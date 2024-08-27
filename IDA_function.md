# IDA

## 개요
(IDA)는 Hex-Rays 사에서 제작한 디스어셈블러다.

## 기능

### 파일 열기

> File -> Open -> 파일 선택
혹은 드래그

### Function window
IDA가 분석한 프로그램의 함수 목록을 보여주는 윈도우다.
해당 윈도우에서 ctrl + f키를 사용하여 원하는 함수를 찾을 수 있다.

<img width="304" alt="스크린샷 2024-08-27 오후 6 00 13" src="https://github.com/user-attachments/assets/9bf0f4ff-b61b-4ac2-ad36-895369e5d3a1">

### Graph overview

함수를 그래프화 하여 보여줘, 함수 흐름파악에 용이하다.

<img width="299" alt="스크린샷 2024-08-27 오후 6 02 56" src="https://github.com/user-attachments/assets/a7bbdbaa-11b6-457d-9a2e-40329e45403c">



### Output window

분석 과정을 메시지로 출력한다. 해당 창을 통해 IDA의 분석 과정을 알 수 있다.

<img width="452" alt="스크린샷 2024-08-27 오후 6 04 39" src="https://github.com/user-attachments/assets/663e8784-4e73-421b-9dd1-7fc17c4d06a1">


### View

디컴파일 결과, Hex-View, 구조체 목록 등의 화면을 표시한다.

<img width="668" alt="스크린샷 2024-08-27 오후 6 02 46" src="https://github.com/user-attachments/assets/ef4d66a2-f889-4847-9aad-e68ec49453a1">



### 함수 및 변수 이름 재설정 기능

단축키 N을 사용해 함수 및 변수 이름을 재설정이 가능하다. 정의되지 않은 함수 및 변수의 경우 해당 기능을 통해 이름을 설정하여 분석 속도를 향상시킬 수 있다.

<img width="558" alt="스크린샷 2024-08-27 오후 6 09 10" src="https://github.com/user-attachments/assets/4e0c8222-56b4-4305-87e0-69878f895c61">



### 함수 및 변수 타입 변경 기능

임의의 함수 또는 변수를 클릭하고, 단축키 Y를 사용하면 해당 함수 및 변수의 타입을 지정할 수 있다. 함수의 경우, 전달되는 매개 변수를 추가하거나, 타입을 변경할 수 있다.

<img width="734" alt="스크린샷 2024-08-27 오후 6 15 31" src="https://github.com/user-attachments/assets/c5f7f23b-95b7-4309-a921-f8ceed0a1aed">


### Cross reference (Xref)

임의의 함수 또는 변수를 클릭하고, 단축키 X를 사용하면 해당 함수 및 변수가 사용되는 영역을 재참조할 수 있다.

<img width="731" alt="스크린샷 2024-08-27 오후 6 10 16" src="https://github.com/user-attachments/assets/ac921d16-a475-45c6-a578-347c22247a82">

<img width="380" alt="스크린샷 2024-08-27 오후 6 14 12" src="https://github.com/user-attachments/assets/1f16c206-e4be-40b7-bb08-47d91398d0fa">




### Strings (문자열)

단축키 Shift + F12를 사용해 바이너리에서 사용하는 모든 문자열을 조회할 수 있다. 함수의 심볼이 존재하지 않거나, 복잡할 경우 문자열을 통해 분석 시간을 크게 단축할 수 있다.

<img width="464" alt="스크린샷 2024-08-27 오후 6 16 34" src="https://github.com/user-attachments/assets/a9fdcc33-e42e-4917-a790-2a1ffc226144">


### Decompile (디컴파일)

IDA에서 제공하는 가장 강력한 기능으로, 어셈블리를 C 언어 형태로 변환하여 보여준다.

<img width="509" alt="스크린샷 2024-08-27 오후 6 18 22" src="https://github.com/user-attachments/assets/c66901b0-0774-4a9e-904d-c4f27fd2e9ae">














