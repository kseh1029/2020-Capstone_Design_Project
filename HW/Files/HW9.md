# HW9

9주차 : XOR Gate and Full Adder

조 명 : 뚝딱뚝딱

**그림 1-1) Inverter 내부 회로**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image32.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image32.bmp)

XOR gate. Design the XOR gate so that the worst-case delay from (X or Y) to Z is less than 80 ps. The inverters are of the same type as shown in the figure. Verify your design through transient simulations. For the inputs X and Y, use the ‘vpwlf’ devices from the ‘analogLib’ library with the pwl files ‘∼/pwl xor x’ and ‘∼/pwl xor y’, respectively. Set the ‘Period of the PWL’ as 1.6 ns. Use the supply voltage of 1 V.

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image33.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image33.bmp)

XOR 이나 Full Adder를 설계하기 위해서는 Inverter 의 사용이 필요하다.

이전 과제에서 설계한 PMOS Width 와 NMOS Width 의 1.2 배의 차이를 이용하지 않고 주어진 Width를 이용해 설계를 진행하였다.

설계에 앞서 Exclusive OR 의 진리표를 통해 PMOS 와 NMOS 관점에서 회로를 구성한 후 CMOS 구조로 연결하였다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%20c4ab626acc894906b43ff1109957500b.csv)

**표1-1) XOR 진리표**

PMOS 에서는 Z = A’B + AB’ 으로 회로를 구성하면 된다.

NMOS 에서는 Z’ 으로 회로를 구성해야 한다. Z’ = (A’B + AB’)’ = (A+B’)(A’+B) 이므로 AA’+AB+A’B’+B’B 에 의해 Z’=AB+A’B’ 이 된다.

**그림1-2) XOR CMOS 회로**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image34.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image34.bmp)

따라서 왼쪽 그림처럼 회로를 구성할 수 있다.

이 때, 입력에 NOT 이 들어간 부분을 확인할 수 있다.

사전에 주어진 PMOS Width 175nm, NMOS Width 120nm 의 Inverter를 이용해 NOT 으로 입력을 해줄 수 있다.

그리고 Worst-case에서도 XOR Gate 로 정상동작을 할 수 있도록 Sizing을 해줄 필요성이 있다.

앞선 과제에서 PMOS 와 NMOS 의 Width length 가 1.2 배 차이남을 확인하였다.

**그림1-3) XOR Worst-Case**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image35.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image35.bmp)

Worst-case 의 경우 다음과 같다.

NMOS 의 사이즈를 $\frac{W}{L}$ 이라고 가정할 때, NMOS 2개를 큰 소자로 본다면 2배 나눠진 $\frac{W}{2L}$ 가 된다.

여기에 pr=1.2 가 곱한 $\frac{1.2W}{2L}$가 PMOS 2개를 큰 소자로 본 사이즈이며,

2배를 곱한 $\frac{1.2W}{L}$ 가 PMOS 각각의 사이즈이다.

**그림1-4) XOR Gate 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image36.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image36.bmp)

nmos1v, pmos1v를 처음 추가시켰을 때 default 로 지정되는 width 와 length를 그대로 사용하여 schematic을 구성하였다.

**그림1-5) XOR Gate Test bench 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image37.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image37.bmp)

앞서 만든 XOR Gate를 symbol 로 만들어서 delay를 측정하기 위한 회로를 구성하였다.

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image38.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image38.bmp)

위와 같은 환경에서 transient Analysis를 진행하였다.

**그림1-5) XOR Gate Test bench 신호흐름선도 (Width 120nm)**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image39.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image39.bmp)

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%2041a0b9aad3ed44189155df6422bdcb48.csv)

**표1-2) Width 120nm 기준 Delay (단위 : ps)**

테스트 해본 결과, 정상적으로 Exclusive OR Gate로 작동을 하였다.

설계조건인 80ps 이내의 Delay를 가지므로 적합한 설계라고 판단할 수 있다.

**그림1-5) Width 변화에 따른 XOR Gate 신호흐름선도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image40.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image40.bmp)

**그림1-6) Width 변화에 따른 XOR Gate 신호흐름선도 확대**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image41.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image41.bmp)

Width 가 커질수록 delay 가 길어지고 있음을 확인할 수 있다.

**그림1-7) XOR Gate Test bench 신호흐름선도 (W 670nm)**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image42.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image42.bmp)

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%201a37ef1c5ed84109a1d5de8ac39c1709.csv)

**표1-3) Width 670nm 기준 Delay (단위 : ps)**

Width 가 670nm 일 때 delay 가 80ps 로 걸치게 된다.

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image43.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image43.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image44.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image44.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image45.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image45.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image46.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image46.bmp)

**Channel Width 가 커질수록 동작 속도가 나빠지는 것에 대한 고찰**

일반적으로 I = Aqnv 이므로 Channel Width 가 증가하면 electron 과 hole 이 많이 움직일 수 있기 때문에

동작 속도는 좋아져야 한다.

하지만 실제로는 Inverter 와 XOR Gate 에서의 delay가 증가했다.

Subthreshold Leakage $I_{D(\text{OFF})} = \mu_{n}C_{\text{ox}}\frac{W}{L}\frac{\gamma{V_{T}}^{2}}{2\sqrt{2\Phi_{F} + V_{\text{SB}}}}e^{\frac{- V_{\text{TH}}}{\text{nV}_{T}}}$ 이므로, W 가 증가할수록 Off current가 증가한다고 볼 수 있다.

해당 현재 gpdk045을 사용한 공정은 45nm 공정으로 집적도가 상당히 높고, *V*DD 가 낮은 동작을 하고 있으므로 Power Equation $P = C_{L}{V_{\text{DD}}}^{2}f + \frac{2}{3}\beta_{n}(\frac{V_{\text{DD}}}{2 - V_{\text{THn}}})^{3}t_{r}f + V_{\text{DD}}I_{\text{OFF}}$ 에서 *V*DD 가 큰 공정에 비해 Leakage Power *V*DD*I*OFF 가 크게 차지할 것으로 예상된다. 그 이유는 Dynamic Power, Short-circuit Power 부분에서 제곱, 세제곱이 있지만 1을 제곱하므로 1V 로 계산되기 때문이다.

이로 인해 Leakage Current 증가로 소자의 동작 특성이 나빠진 것 같다.

2. Fig. 2 shows a delay measurement setup for a full adder. Design the full adder such that the worst-case delay from (A, B, or C

IN

) to (S or C

OUT

) is less than 150 ps. The inverters are of the same type as the ones in Fig. 1. Verify your design through simulations. Use the pwl files ‘∼/pwl fa a’, ‘∼/pwl fa b’, and ‘∼/pwl fa cin’ for the inputs A, B, and C

IN

, respectively. Set the ‘Period of the PWL’ as 8.8 ns. Use the supply voltage of 1 V.

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image47.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image47.bmp)

설계에 앞서 Full Adder 의 진리표를 통해 PMOS 와 NMOS 관점에서 회로를 구성한 후 CMOS 구조로 연결하였다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%20d7e438db27c54028bab91fb34b2b673b.csv)

**표2-1) 2bits Full Adder 진리표**

우선 Sum 에 대한 회로를 만들기 위해 Sum 과 Sum’ 의 논리식을 알아야 한다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%2088bebf0a55994052866815d0b4280760.csv)

**표2-2) Sum 의 카르노맵**

Sum 과 Sum’ 의 카르노맵은 다음과 같다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%2026dc11e8fb41440a94fc5bcb6cd87359.csv)

**표2-3) Sum‘ 의 카르노맵**

이 카르노맵을 논리식으로 정리하면 다음과 같다.

Sum = A’B’Cin + ABCin + A’BCin’ + AB’Cin’

Sum‘ = A’B’Cin‘ + A’BCin + ABCin’ + AB’Cin

PMOS 에서는 Sum 으로 NMOS 에서는 Sum’ 으로 회로를 구성해야 한다.

**그림2-1) Full Adder 의 Sum 회로**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image48.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image48.bmp)

따라서 왼쪽 그림처럼 회로를 구성할 수 있다.

이 때, 입력에 NOT 이 들어간 부분을 확인할 수 있다.

사전에 주어진 PMOS Width 175nm, NMOS Width 120nm 의 Inverter를 이용해 NOT 으로 입력을 해줄 수 있다.

그리고 Worst-case에서도 XOR Gate 로 정상동작을 할 수 있도록 Sizing을 해줄 필요성이 있다.

앞선 과제에서 PMOS 와 NMOS 의 Width length 가 1.2 배 차이남을 확인하였다.

**그림2-2) Full Adder**

**Sum Worst-Case**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image49.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image49.bmp)

Worst-case 의 경우 다음과 같다.

NMOS 의 사이즈를 $\frac{W}{L}$ 이라고 가정할 때, NMOS 3개를 큰 소자로 본다면 3배 나눠진 $\frac{W}{3L}$ 가 된다.

여기에 pr=1.2 가 곱한 $\frac{1.2W}{3L}$가 PMOS 3개를 큰 소자로 본 사이즈이며,

3배를 곱한 $\frac{1.2W}{L}$ 가 PMOS 각각의 사이즈이다.

다음으로 Cout 에 대한 회로를 만들기 위해 Cout 과 Cout’ 의 논리식을 알아야 한다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%2074a104dc1065463c9fdd65a4c1a8bd72.csv)

**표2-4) Cout 의 카르노맵**

Sum 과 Sum’ 의 카르노맵은 다음과 같다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%20015a915257564c6ead22446ee910eab3.csv)

**표2-5) Cout‘ 의 카르노맵**

이 카르노맵을 논리식으로 정리하면 다음과 같다.

Cout = AB + BCin + CinA

Cout‘ = A’B’ + A’Cin’ + B’Cin’

PMOS 에서는 Cout 으로 NMOS 에서는 Cout’ 으로 회로를 구성해야 한다.

따라서 다음 그림처럼 회로를 구성할 수 있다.

**그림2-4) Full Adder**

**Cout Worst-Case**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image50.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image50.bmp)

**그림2-3) Full Adder 의 Cout 회로**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image51.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image51.bmp)

Worst-case 의 경우 NMOS 의 사이즈를 $\frac{W}{L}$ 이라고 가정할 때, NMOS 3개를 큰 소자로 본다면 2배

나눠진 $\frac{W}{2L}$ 가 된다. 여기에 pr=1.2 가 곱한 $\frac{1.2W}{2L}$가 PMOS 2개를 큰 소자로 본 사이즈이며, 2배를 곱한

$\frac{1.2W}{L}$ 가 PMOS 각각의 사이즈이다.

**그림2-5) Full Adder 의 Sum 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image52.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image52.bmp)

**그림2-6) Full Adder 의 Cout 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image53.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image53.bmp)

**그림2-7) Full Adder 전체 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image54.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image54.bmp)

**그림2-8) Full Adder Test bench 회로도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image55.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image55.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image56.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image56.bmp)

**그림2-9) Full Adder Test bench (Width 120nm)**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image57.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image57.bmp)

테스트 결과 Full Adder 에 맞는 연산 결과를 나타내고 있다.

하지만, Sum 의 일부분에서 노이즈가 타는 모습을 볼 수 있었다.

**그림2-10) Width 변화에 따른 Full Adder 신호흐름선도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image58.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image58.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image59.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image59.bmp)

Width 가 증가할수록 delay 시간이 증가하였고, 일부 모양이 변형되는 부분이 있었다.

1) 신호흐름선도에서 Sum 과 Cout에는 delay 차이가 존재하는 것을 볼 수 있다.

그 이유는 Cout의 경우 직렬로 2개의 MOSFET을 통과하고, Sum의 경우 직렬로 3개의 MOSFET을 통과하기 때문이다. 즉, Sum의 경우 TR 1개가 직렬로 더 연결되어 있으므로 Channel length가 Cout에 비해 더 크기 때문에 delay가 더 증가한 것이다.

2) 지금의 Full Adder는 출력이 2개가 존재하는 다중 출력 회로이므로 Sum과 Cout의 공통항을 중복하여 사용한다면 더 좋은 성능의 Full Adder를 설계할 수 있을 것이다.

다음으로 관습적으로 사용하는 Full Adder CMOS 구조를 사용하였다.

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image60.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image60.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image61.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image61.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image62.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image62.bmp)

**그림2-11) Conventional Full Adder Test bench 회로도**

**그림2-12) Conventional Full Adder Test bench (Width 120nm)**

**그림2-10) Width 변화에 따른 Conventional Full Adder 신호흐름선도**

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image63.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image63.bmp)

![HW9%20a80d9f27f92a4c9aa6827986e693222b/image64.bmp](HW9%20a80d9f27f92a4c9aa6827986e693222b/image64.bmp)

마찬가지로 Width 가 증가할수록 delay 시간이 증가하였고, 일부 모양이 변형되는 부분이 있었다.

[Untitled](HW9%20a80d9f27f92a4c9aa6827986e693222b/Untitled%20Database%20b2be98d3b8824fd18db05e6efbcbc228.csv)

**표2-6) Width 120nm 기준 Delay (단위 : ps)**

Full Adder 결과의 일부의 Delay를 측정하여 기록한 표 이다.

과제에서 제안된 150ps 이내로 작동되는 모습을 확인할 수 있다.