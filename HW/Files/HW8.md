# HW8

8주차 : NAND and NOR Gates

조 명 : 뚝딱뚝딱

2017117876

김승현

1. Design the NAND gate that is illustrated in Fig. 1 so that the worst-case delay is less than 15 ps when a load capacitance of 2 fF is connected t the output.

Try to minimize $\sum_{i = 1}^{4}W_{i}L_{i}$.

Verify your design by running transient simulations. For the inputs X and Y, use the ‘vpwlf’ devices from the ‘analogLib’ library. Set the parameters as shown in Fig. 3 and

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image16.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image16.bmp)

∼/pwl_nand_x’ and ‘∼/pwl_nand_y’ files for the inputs X and Y, respectively. Tip: Use a horizontal marker (keyboard shortcut ‘h’) in the waveform window to measure the delays. Alternatively, you can use the ‘cross’ function from the calculator. Consider the following inverter circuit. The channel lengths of nmos1v and pmos1v devices are all 45 nm. For the capacitor, use the ‘cap’ device from ‘analogLib’.

설계 조건을 요약해보자면, worst-case에서 delay 가 15ps 보다 낮아야 한다는 것이다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image17.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image17.bmp)

왼쪽 그림은 worst-case 에서의 2 input NAND Gate을 나타내었다.

종전의 과제에서 inverter를 구성할 때, PMOS 의 width 는 NMOS의 width 에 pr=1.2를 곱했을 때 *Vi* 가 0.5V 일 때 *Vo* 가 0.5V를 출력함을 확인하였다.

따라서 *βP* = 1.2*βN* 이라고 두고 시작할 수 있다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image18.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image18.bmp)

NMOS 1개만 봤을 때 $\frac{W}{L}$ 의 Size를 가진다면, 두 개가 세로로 연결되어 있을 때 $\frac{W}{2L}$ 와 같다고 볼 수 있다.

PMOS 는 등가로 본 NMOS 사이즈에 1.2를 곱한 크기를 가져야 한다.

만약, worst case 가 아니라 best case 였으면, $\frac{0.3W}{L}$ 을 PMOS 의 사이즈로 했어야 한다.

이를 실제로 Virtuoso에서 도면에 나타내면 다음과 같다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image19.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image19.bmp)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image20.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image20.bmp)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image21.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image21.bmp)

width를 100nm 씩 증가시키며 delay 이 변화되는 것을 관찰하였다.

NAND Gate 의 진리표와 출력결과를 비교해 봤을 때 정상적으로 출력됨을 확인하였다.

[Untitled](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/Untitled%20Database%20f39e58c9ad3641549d4bb86b37ba5f05.csv)

X, Y 가 무엇이냐에 따라 delay 시간은 전체적으로 달랐다.

즉, X=Y=0 일 때와 X=0, Y=1, 일 때는 모두 Z=1 로 같은 결과를 출력하지만

소요되는 시간은 달랐다.

그래서 가장 느린 경우에서 15ps를 만족시키기 위해서서는 width를 많이 키울 필요가 있었다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image22.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image22.bmp)

위 그림은 width 가 1800nm 일 때의 transient simulation 결과이다.

자세한 해석 결과는 다음과 같다.

가장 오래 걸린시간이 14.9075ps 임을 확인할 수 있다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image23.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image23.bmp)

2. Repeat the problem 1. for the NOR gate shown in Fig. 2. Use ‘∼/pwl_nor_x’

and ‘∼/pwl_nor_y’ files for the inputs X and Y, respectively.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image24.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image24.bmp)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image25.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image25.bmp)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image26.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image26.bmp)

왼쪽 그림은 worst-case 에서의 2 input NOR Gate을 나타내었다.

NAND Gate 에서 하던 방법과 마찬가지로 *βP* = 1.2*βN* 이라고 두고 sizing을 하면 된다.

NMOS를 봤을 때 $\frac{W}{L}$ 의 Size를 가진다면, NMOS 사이즈에 1.2를 곱한 크기를 가져야 한다. 따라서 PMOS 의 전체 등가 사이즈는 $\frac{1.2W}{L}$ 이 된다.

이때 2개의 PMOS가 세로로 연결되어있으므로 PMOS 각각의 사이즈는 2배씩 커진 $\frac{2.4W}{L}$가 될 것이다.

만약, worst case 가 아니라 best case 였으면, $\frac{4.8W}{L}$ 을 PMOS 의 사이즈로 했어야 한다.

이를 실제로 Virtuoso에서 도면에 나타내면 다음과 같다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image27.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image27.bmp)

2 input NOR Gate를 symbol 로 만들어서 회로를 만들었다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image28.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image28.bmp)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image29.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image29.bmp)

width를 100nm 씩 증가시키며 delay 이 변화되는 것을 관찰하였다.

그리고 NOR Gate 의 진리표와 출력결과를 비교해 봤을 때 정상적으로 출력됨을 확인하였다.

[Untitled](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/Untitled%20Database%205e56a61ec70d44e2994f0e2e5c08cf3c.csv)

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image30.png](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image30.png)

위 그림은 width 가 673.2nm 일 때의 transient simulation 결과이다.

자세한 해석 결과는 다음과 같다.

가장 오래 걸린시간이 15ps 이다.

![HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image31.bmp](HW8%201e45fffc4adf4bdfa25b2d8cbbd701ab/image31.bmp)