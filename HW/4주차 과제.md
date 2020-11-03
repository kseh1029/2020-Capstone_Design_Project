# 4주차 : 6-T SRAM의 구조 및 동작 원리

SRAM은 두 개의 안정된 상태를 갖는 쌍안정 래치 회로의 각 상태에서 1과 0을 할당하여 저장하는 메모리이다.

쌍안정 회로는 전원이 유지되고 정보를 바꾸어 쓰지 않는 한, 상태의 변화가 없어 정보를 무한히 유지하므로 Static Random Access Momory (SRAM) 이라고 한다. DRAM 과 비교할 때 리프래시 동작이 필요 없으므로 사용이 간편하고 속도가 빠르다. 그러나 SRAM은 단위 셀이 6개의 트랜지스터로 구성되어 DRAM에 비해 집적도가 1/4 정도로 떨어지며, 가격이 비싸다.

① SRAM의 구조

![https://blog.kakaocdn.net/dn/d5fdtT/btqMtzvrtU7/f0Y5Nym2BLxWjpYcYEV4Z1/img.png](https://blog.kakaocdn.net/dn/d5fdtT/btqMtzvrtU7/f0Y5Nym2BLxWjpYcYEV4Z1/img.png)

왼쪽 그림은 4 뱅크로 구성된 SRAM의 내부 구조이다.

데이터 저장공간인 메모리 셀 배열,

특정 메모리 셀에 접근하기 위해 주소를 디코딩 하는 행 디코더와 열 디코더,

증폭감지기 및 I/O 버퍼 회로 등으로 구성되어 있다.

왼쪽 그림에서는 4개의 뱅크로 분할이 되어있다.

SRAM의 읽기 동작은 =0 일 때 칩 선택신호가 활성화 되고, 쓰기 활성화 신호 =1에 의해 읽기모드가 설정되면 출력 활성화 신호 =0에 의해 출력이 데이터 I/O 포트로 연결된다.

주소 포트로 입력된 행주소는 행 디코더에 의해 워드라인 신호로 변환되어 특정 워드라인이 선택된다.

워드라인에 연결된 셀들 중 열 디코더 출력에 의해 특정 비트라인이 선택되고 데이터를 읽어낸다.

메모리 셀에 연결된 비트라인과 반전 비트라인의 미세한 신호변화는 감지증폭기에 의해 증폭되고, 출력 버퍼를 통해 외부로 출력된다.

SRAM의 쓰기 동작은 =0 일 때 칩 선택신호가 활성화 되고, 쓰기 활성화 신호 =0에 의해 쓰기모드가 설정되면 출력 활성화 신호 =1에 의해 I/O 포트의 데이터가 쓰기 구동회로에 연결된다.

어드레스 포트로 입력된 행주소는 행 디코더에 의해 워드라인 신호로 변환되어 특정 워드라인이 선택된다.

![https://blog.kakaocdn.net/dn/cOa2IX/btqMwn1Ra1U/tiaNR50gynPuHAd857OYHk/img.png](https://blog.kakaocdn.net/dn/cOa2IX/btqMwn1Ra1U/tiaNR50gynPuHAd857OYHk/img.png)

워드라인에 연결된 셀들 중 열 디코더 출력에 의해 저장될 셀의 비트라인이 선택되고, 쓰기 구동회로의 데이터가 해당 셀의 과 에 인가되어 쓰기 동작이 이루어진다.

SRAM을 구성하는 칼럼회로는 기본적으로 왼쪽 그림과 유사한 구조를 갖는다.

메모리 셀들이 비트라인 과 반전 비트라인 에 연결되어 있다.

프리차지 회로는 읽기와 쓰기 동작을 위해 비트라인과 반전 비트라인을 로 프리차지 시키는 역할을 한다.

감지증폭기는 과 의 신호 변화를 감지하고 증폭해서 출력으로 보내는 역할을 한다.

쓰기 구동회로를 통해 입력되는 데이터는 교차 결합된 감지증폭기를 통해 과 에 인가된다.

![https://blog.kakaocdn.net/dn/cUsSK7/btqMpKLHdNL/PoI9aYDg5iYE514Fj9Ggv0/img.png](https://blog.kakaocdn.net/dn/cUsSK7/btqMpKLHdNL/PoI9aYDg5iYE514Fj9Ggv0/img.png)

왼쪽 그림은 SRAM의 읽기 동작을 위한 칼럼 회로이다.

다수의 셀들이 비트라인과 반전 비트라인에 연결되어 있다.

pMOSFET 는 클럭신호 에 의해 비트라인과 반전 비트라인을 로 프리차지 시키는 역할을 한다.

=0 에 의해 과 이 프리차지 되고 주소 디코딩에 의해 워드라인 신호 WL=1 이 인가되면, 액세스 트랜지스터 가 도통되어 메모리 셀이 선택된다.

셀 내부의 에 저장된 전압이 액세스 트랜지스터를 통해 과 에 나타나고 과 의 신호 변화는 감지증폭기를 통해 증폭되어 외부로 출력된다.

![https://blog.kakaocdn.net/dn/cG6OkK/btqMtypLwlK/4RfRMHnVTb4hN9kbYTesak/img.png](https://blog.kakaocdn.net/dn/cG6OkK/btqMtypLwlK/4RfRMHnVTb4hN9kbYTesak/img.png)

읽기 동작을 위한 타이밍도는 왼쪽그림과 같다.

(address access time) : 주소가 인가된 시점으로부터 유효한 데이터가 출력되기 까지 소요시간

(chip select to output) : 신호가 인가된 시점으로부터 유효한 데이터가 출력되기 까지 소요시간

(output enable to valid output) : 신호가 인가된 시점으로부터 유효한 데이터가 출력되기 까지 소요시간

(output disable to high-Z) : =1 로 비활성화된 시점으로부터 출력이 고임피던스 상태가 되기 까지의 소요시간

(output hold from address change) : 새로운 주소로 변경된 시점으로부터 이전 주소의 출력 데이터가 유지되는 시간

그 외에 (raed cycle time), (chip select to low-Z output), (output enable to low-Z output),

(chip disable to high-Z output) 이 있다.

![https://blog.kakaocdn.net/dn/c9voxw/btqMqcVAa56/4f0NqHSVoRuHGbRyimp6uK/img.png](https://blog.kakaocdn.net/dn/c9voxw/btqMqcVAa56/4f0NqHSVoRuHGbRyimp6uK/img.png)

왼쪽 그림은 SRAM의 쓰기 동작을 위한 칼럼 회로이다.

클럭신호 =0에 의해 비트라인과 반전 비트라인이 로 프리차지된 상태에서 write=1 에 의해 데이터가 과 에 인가된다.

주소 디코딩에 의해 워드라인 신호 =1 이 인가되면 액세스 트랜지스터 가 도통되어 메모리 셀이 선택되고, 과 의 값이 메모리 셀에 저장된다.

![https://blog.kakaocdn.net/dn/cyfEot/btqMpLDSUi3/A06ndtKZRkblr99fwsRRKk/img.png](https://blog.kakaocdn.net/dn/cyfEot/btqMpLDSUi3/A06ndtKZRkblr99fwsRRKk/img.png)

쓰기 동작을 위한 신호 타이밍도는 왼쪽 그림과 같다.

(address setup time) : =0 이 인가되지 이전에 주소가 안정된 값을 유지해야 하는 준비시간

(address valid to end of write) : =1 에 의해 쓰기 동작이 완료되는 시점까지 유효한 주소값이 유지되어야 하는 시간

(data to write time overlap) : =1 에 의해 쓰기 동작이 완료되기 이전에 데이터가 안정된 값을 유지해야 하는 준비시간

(data hold from write time) : =1 에 의해 쓰기 동작이 완료된 이후에 데이터가 안정된 값을 유지해야하는 유지시간

그 외에 (write cycle time), (chip select to end of write), (write pulse width), (write recovery time), (write to output high-Z), (end write to output low-Z) 가 있다.

② SRAM 셀 회로

![https://blog.kakaocdn.net/dn/ReelL/btqMuPLwrsH/FKYUXkmiM7rKej9yCwE881/img.png](https://blog.kakaocdn.net/dn/ReelL/btqMuPLwrsH/FKYUXkmiM7rKej9yCwE881/img.png)

SRAM 셀은 쌍안정 래치회로의 각 상태에 0과 1을 할당하여 정보를 저장하며, 래치회로에 따라 여러 가지 형태로 구현될 수 있다.

왼쪽 그림은 6-T SRAM 셀 회로이다.

교차결합된 CMOS 인버터와 2개의 액세스 트랜지스터로 구성된다.

교차결합된 인버터는 래치회로를 구성하여 Positive feedback 작용에 의해 데이터를 저장한다.

워드라인은 액세스 트랜지스터의 게이트에 연결되며, 워드라인의 신호가 =1 일 때, 메모리 셀이 선택되어 값의 읽기 또는 쓰기 동작이 이루어진다.

두 개의 비트라인 과 은 메모리 셀과 외부 사이의 데이터를 전달하는 통로 역할을 한다.

6-T SRAM 셀은 값을 읽고 쓰는 스위치 동작 시에만 전력소모가 일어나며 leakage power 이외에는 정적 전력소모가 없다는 것이 장점이지만, 4-T SRAM 회로에 비해 셀 면적이 크다는 단점을 가진다.

③ SRAM 셀의 읽기와 쓰기

![https://blog.kakaocdn.net/dn/Gelam/btqMwmID5Yv/hm54yCVHv2t0ZgSUmV6PcK/img.png](https://blog.kakaocdn.net/dn/Gelam/btqMwmID5Yv/hm54yCVHv2t0ZgSUmV6PcK/img.png)

1) 6-T SRAM 셀 회로의 읽기

왼쪽 그림은 메모리 셀에 데이터 0이 저장되어 있는 경우의 읽기 동작을 나타낸 그림이다.

셀 내부의 두 CMOS 인버터는 교차결합되어 있으므로 과 는 도통상태이고, 와 은 개방상태를 유지하고 있다.

따라서 =0, =1을 유지하고 있다.

비트라인 과 반전 비트라인 을 1로 프리차지 시킨 후, 읽기 동작을 통해 워드라인 =1 로 활성화 시키면 과 에 연결된 액세스 트랜지스터 가 도통된다.

이때 비트라인 의 전압은 도통된 을 통해 0V 로 감소하며, 동시에 노드 의 전압은 프리차지된 비트라인 전압에 의해 상승한다.

노드 의 전압은 도통된 에 의해 낮은 전압을 유지하고 있지만, 도통된 를 통해 유입되는 전류에 의해 상승한다.

읽기 동작이 올바로 이루어지기 위해서는 노드 의 전압이 비트라인의 전압의 영향을 적게 받아야 하므로, 트랜지스터 의 구동력이 액세스 트랜지스터 보다 크게 설계되어야 한다. 이 조건을 읽기 안정화 조건이라고 한다.

읽기 안정화 조건을 만족하면, 프리차지된 비트라인은 와 을 통해 접지로 방전되어 0이 되고, 반전 비트라인은 1을 유지하여 저장된 값 0이 비트라인에 읽히게 된다.

동일한 원리에 의해 메로리 셀에 저장된 1을 읽기 위해서는 트랜지스터 의 구동력이 액세스 트랜지스터 보다 크게 설계되어야 한다.

SRAM 셀의 읽기 안정화 조건을 만족하기 위해서는 트랜지스터의 채널폭이 과 를 만족하도록 설계되어야 한다.

![https://blog.kakaocdn.net/dn/oBMgz/btqMqCGqifh/GpJMygD9BtLKRIq43jGoeK/img.png](https://blog.kakaocdn.net/dn/oBMgz/btqMqCGqifh/GpJMygD9BtLKRIq43jGoeK/img.png)

2) 6-T SRAM 셀 회로의 쓰기

왼쪽 그림은 메모리 셀에 데이터 0이 저장되어 있는 상태에서 데이터 1의 쓰기 동작을 나타낸 그림이다.

비트라인 비트라인 과 반전 비트라인 을 로 프리차지 시킨 후, =0으로 만들어 저장될 데이터 1을 과 에

인가한다.

쓰기동작을 위해 워드라인 =1로 활성화시키면, 과 에 연결된 액세스 트랜지스터 가 도통된다.

메모리 셀의 읽기 동작을 위한 읽기 안정화 조건에 의해 액세스 트랜지스터 의 구동력이 약하게 만들어지므로

에 실린 1이 노드 를 1로 만드는 데 시간이 걸리게 된다. 따라서 쓰기 동작은 를 통해 가 0이 되어야 하며, 이를 위해 액세스 트랜지스터 의 구동력이 보다 크게 설계되어야 한다. 이를 쓰기 가능 조건이라고 한다.

가 0이 되면, 이에 의해 이 도통되어 =1이 되고, 교차 결합된 인버터에 1이 저장된다.

동일한 원리에 의해 1이 저장된 셀에 0을 쓰기 위해서는 액세스 트랜지스터 의 구동력이 보다 크게 설계되어야 한다.

SRAM 셀의 쓰기 가능 조건을 만족하기 위해서는 트랜지스터 채널폭이 와 를 만족하도록 설계되어야 한다.

3) SRAM 셀의 설계 조건

![https://blog.kakaocdn.net/dn/4iOp7/btqMqeFMYxL/qLRqVeakpLcFJdWKbFClRk/img.png](https://blog.kakaocdn.net/dn/4iOp7/btqMqeFMYxL/qLRqVeakpLcFJdWKbFClRk/img.png)

SRAM 셀의 읽기와 쓰기 동작이 올바로 수행되기 위해서는 트랜지스터들의 상대적인 구동력이 왼쪽 그림과 같이 설계되어야 한다.

인버터의 nMOSFET , 는 가장 큰 구동력을 가져야 한다.

액세스 트랜지스터 , 는 중간 정도의 구동력을 가져야 한다.

인버터의 pMOSFET , 는 가장 작은 구동력을 가져야 한다.
