# HW5

5주차 : NAND 및 NOR Gate의 구조 및 동작

조 명 : 뚝딱뚝딱

2017117876

김승현

논리설계자들은 NAND 와 NOR 게이트를 자주 사용하는데 AND 혹은 OR 게이트보다는 일반적으로 더 빠르고 더 적은 부품을 사용하기 때문이다.

이러한 NAND, NOR 게이트는 CMOS 구조로 설계가 된다.

그 이유는, 기본적으로 인버터를 설계할 때 CMOS 구조로 설계가 되는데, 여기에서 확장된 것 이라고 생각할 수 있다.

![HW5%206c593e7de6a147a09645d997df9a621b/image17.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image17.bmp)

NMOS에서 게이트에 *V*DD 를 걸면, 트랜지스터는 turn on 되고 출력단에서 최대 *V*DD − *V*THN 만큼의 전압만 나온다. 게이트에 0V를 걸면 트랜지스터는 turn off 가 되고 출력단에서 0V 가 나온다. 즉 NMOS 는 낮은 전압은 정확하게 뱉어내지만 높은 전압은 Threshold Voltage 만큼 차감된 전압이 출력된다.

PMOS에서 게이트에 *V*DD 를 걸면, 트랜지스터는 turn off 되고 출력단에서는 *V*THP가 나오고, 게이트에 0V를 걸면, 트랜지스터는 turn on 되고 출력단에서는 *V*DD 가 나오게 된다. 즉 PMOS 는 높은 전압은 정확하게 뱉어내지만 낮은 전압은 Threshold Voltage 만큼은 최소한 가지고 출력이 된다.

이 둘의 특징을 조합하여 출력에서 정확하게 *V*DD, 0V 로 뱉어내는 것이다.

NAND Gate 과 NOR Gate 의 동작 방식을 알기 전에 CMOS 인버터의 동작방식을 먼저 알 필요가 있다.

![HW5%206c593e7de6a147a09645d997df9a621b/image18.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image18.bmp)

처음 0 ≤ *VI*⟨*V*THN 일 땐 채널이 형성되지 않아서 NMOS 가 꺼져있다.

$V_{\text{THN}} \leq V_{I}\langle\frac{V_{\text{DD}}}{2}$ 일 땐 *VI* 가 *V*GS − *V*THN 보다는 크다.

NMOS 는 포화상태, PMOS 는 선형상태를 이루게 된다.

$\frac{V_{\text{DD}}}{2} \leq V_{I}$ 가 되면 *V*DS 가 $\frac{V_{\text{DD}}}{2}$ 보다 낮아졌으므로, *V*OV가 *V*DS 보다 큰 상황이 되어 NMOS 가 선형조건을 만족하게 된다.

NMOS나 PMOS 나 정상 동작을 하기 위해선 *V*THN 이나 ∣ *V*THP ∣ 중 큰 값보다 *V*DD 가 크면 된다.

Logic threshold voltage 인 부분은 *VI* = *VO* 인 부분이며 이 부분에서 NMOS 와 PMOS가 둘다 포화돼 *ID* 가 가장 잘 흐른다.

CMOS 로 만든 회로의 장점은 파워 소모가 적고 *V*DD 에서 0V 까지 Full Swing을 하므로 노이즈에 강하다.

최소 동작 파워 서플라이 전압도 *V*THN 이나 ∣ *V*THP ∣ 중 큰 값보다 *V*DD 가 크면 되므로 낮게 잡을 수 있다.

심지어 비율을 완벽하게 맞추지 않아도 동작은 한다.

![HW5%206c593e7de6a147a09645d997df9a621b/image19.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image19.bmp)

NMOS에서 Gate가 0V 일 때 Turn off 이므로 *V*out 은 Floating 된 상태이다.

Gate가 *V*DD 일 때 Turn on 이 되고, *V*eqalign*i*  가 *V*DD 라면 *V*OUT = *V*DD − *V*THN 이다.

Gate가 *V*DD 일 때 Turn on 이 되고, *V*eqalign*i*  가 0V 라면 *V*OUT = 0*V* 이다.

PMOS에서 Gate가 *V*DD 일 때 Turn off 이므로 *V*out 은 Floating 된 상태이다.

Gate가 0V 일 때 Turn on 이 되고, *V*eqalign*i*  가 *V*DD 라면 *V*OUT = *V*DD 이다.

![HW5%206c593e7de6a147a09645d997df9a621b/image20.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image20.bmp)

*V*

eqalign*i* 

가 0V 라면

*V*

OUT

= ∣

*V*

THP

∣ 이다.

위의 특성을 고려하여 논리회로처럼 간단하게 왼쪽 그림처럼 생각할 수 있다.

**① NAND Gate**

![HW5%206c593e7de6a147a09645d997df9a621b/image21.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image21.bmp)

[Untitled](HW5%206c593e7de6a147a09645d997df9a621b/Untitled%20Database%204151b9dac066453da18f052d3ccba71f.csv)

출력은 *F* = (*X*1*X*2...*Xn*)′ = *X*1′ + *X*2′ + ... + *Xn*′ 이다.

NAND Gate 의 출력은 입력들 중에서 하나 혹은 그 이상이 0 일때만 1이 된다.

만약, 2 입력 NAND Gate 라면 다음과 같은 Truth Table을 가지게 될 것이다.

2 개의 입력을 가진 NAND Gate를 설계하기 위해선 우선 NMOS 에서는 반전출력 *F* ′ 을 구해야 하고, PMOS 에서는 출력 *F* 를 구해야한다.

NAND Gate *F* = (AB)′ 이므로 *F* = *A* ′ + *B* ′ 이 된다. 이는 PMOS 에 적용이 된다.

*F* ′ = AB 이며 이는 NMOS 에 적용이 된다.

OR의 경우 MOSFET을 병렬로, AND의 경우 직렬로 연결하면 되므로 다음과 같은 회로도가 완성이 된다.

![HW5%206c593e7de6a147a09645d997df9a621b/image22.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image22.bmp)

이때 PMOS 와 NMOS 의 전자이동도가 다르다는 것을 인식하고 사이즈를 매칭해줄 필요성이 있다.

$I_{\text{DN}} = \frac{1}{2}k_{n}{V_{\text{ov}}}^{2} = \frac{1}{2}\mu_{n}C_{\text{ox}}\frac{W}{L}(V_{\text{GS}} - V_{\text{THN}})^{2}$ 이므로 *I*DP 와 비교했을 때 나머지 조건은 다 똑같다고 보고,

$\mu_{n}\frac{W_{n}}{L_{n}} = \mu_{p}\frac{W_{p}}{L_{p}}$ 를 만족하면 될 것이다.

일반적으로 *μn* = 2.5 *μp* 로 매칭할 수 있다.

매칭할때에는 최악의 상황인 Worst Case 로 고려해야 한다

Worst Case 의 경우 병렬로된 트랜지스터는 다 꺼졌다고 생각하면 된다.

만약 PMOS 의 소자 길이가 $\frac{W}{L}$ 였다면, $2.5\mu_{p}\frac{W_{n}}{L_{n}} = \mu_{p}\frac{W}{L}$ 이 되므로, NMOS 전체의 $\frac{W_{n}}{L_{n}} = \frac{1}{2.5}\frac{W}{L}$ 이 된다.

2개의 NMOS 가 직렬로 연결되어 있으면 그 개수만큼 값을 곱한 값이 NMOS 각각의 사이즈가 된다.

즉, NMOS 각각은 $\frac{W_{n}}{L_{n}} = \frac{2}{2.5}\frac{W}{L}$. PMOS 각각은 $\frac{W_{p}}{L_{p}} = \frac{W}{L}$ 가 된다.

![HW5%206c593e7de6a147a09645d997df9a621b/image23.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image23.bmp)

*A*

=

*V*

DD

,

*B*

= 0

*V*

라고 가정을 해본다.

이때, $F = \overline{\text{AB}}$ 밑에 커패시터 *CL* 을 달아준다.

NMOS 기준에서 위에 있는 트랜지스터는 turn on 이 되고, 아래에 있는 트랜지스터는 turn off 가 된다.

PMOS 기준에서 왼쪽이 있는 트랜지스터는 turn on, 오른쪽에 있는 트랜지스터는 turn off 가 된다.

오른쪽 PMOS 가 켜져 있으므로 *V*DD 가 *CL* 에 충전될 것이다.

*A* = 0*V*, *B* = 0*V* 인 상황이거나 *A* = 0*V*, *B* = *V*DD 인 상황도 마찬가지 일 것이다.

하지만, *A* = *V*DD, *B* = *V*DD 라면 다른 상황이 일어난다.

![HW5%206c593e7de6a147a09645d997df9a621b/image24.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image24.bmp)

*C*

*L*

에 충전된 전압이 NMOS 2개를 통해 방전이 될 것이다.

결국 *CL* 에 걸리는 전압은 0V 가 된다.

[Untitled](HW5%206c593e7de6a147a09645d997df9a621b/Untitled%20Database%20ba6992a6b5034b1d949924edcf33d390.csv)

이를 표로 정리하면 다음과 같이 NAND Gate로 동작함을 확인할 수 있다.

**② NOR Gate**

![HW5%206c593e7de6a147a09645d997df9a621b/image25.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image25.bmp)

출력은 *F* = (*X*1 + *X*2 + ... + *Xn*)′ = *X*1′*X*2′...*Xn*′ 이다.

만약, 2 입력 NOR Gate 라면 다음과 같은 Truth Table을 가지게 될 것이다.

[Untitled](HW5%206c593e7de6a147a09645d997df9a621b/Untitled%20Database%203444b8ffc8b242c7b68190ee70755c68.csv)

![HW5%206c593e7de6a147a09645d997df9a621b/image26.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image26.bmp)

2 개의 입력을 가진 NOR 를 설계하기 위해선 우선 NMOS 에서는 반전출력 *F* ′ 을 구해야 하고, PMOS 에서는 출력 *F* 를 구해야한다.

NAND Gate *F* = (*A* + *B*)′ 이므로 *F* = *A* ′*B* ′ 이 된다. 이는 PMOS 에 적용이 된다.

*F* ′ = *A* + *B* 이며 이는 NMOS 에 적용이 된다.

NAND Gate를 설계할 때처럼 전자이동도를 고려하여 사이징을 해주기 위해

$\mu_{n}\frac{W_{n}}{L_{n}} = \mu_{p}\frac{W_{p}}{L_{p}}$ 를 만족하면 될 것이다.

일반적으로 *μn* = 2.5 *μp* 로 매칭할 수 있다.

만약 NMOS 의 소자 길이가 $\frac{W}{L}$ 였다면, $\mu_{n}\frac{W_{n}}{L_{n}} = \mu_{p}\frac{W_{p}}{L_{p}}$ 에서 $\frac{W_{n}}{L_{n}} = \frac{W_{}}{L_{}}$이 되므로, $2.5\mu_{p}\frac{W_{}}{L_{}} = \mu_{p}\frac{W_{p}}{L_{p}}$ 가 되고, PMOS 전체의 $\frac{W_{p}}{L_{p}} = 2.5\frac{W}{L}$ 이 된다.

2개의 PMOS 가 직렬로 연결되어 있으면 그 개수만큼 값을 곱한 값이 NMOS 각각의 사이즈가 된다.

즉, NMOS 각각은 $\frac{W_{n}}{L_{n}} = \frac{W_{}}{L_{}}$. PMOS 각각은 $\frac{W_{p}}{L_{p}} = 5\frac{W}{L}$ 가 된다.

동작이 어떻게 하는지 확인하기 위해서 *A* = *V*DD, *B* = 0*V* 라고 가정을 해본다.

![HW5%206c593e7de6a147a09645d997df9a621b/image27.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image27.bmp)

$F = \overline{A + B}$ 밑에 커패시터

*C*

*L*

을 달아준다.

NMOS 기준에서 왼쪽에 있는 있는 트랜지스터는 turn off 가 되고, 오른쪽에 있는 트랜지스터는 turn on 된다.

PMOS 기준에서 위쪽이 있는 트랜지스터는 turn off, 아래쪽에 있는 트랜지스터는 turn on 된다.

직렬로 연결된 PMOS 중 한 개 라도 OFF 되어 있으므로 *CL* 에 충전된 전압이 오른쪽 NMOS 통해 방전이 될 것이다. 즉 0V 가 출력된다.

*A* = *V*DD, *B* = *V*DD 인 상황이거나 *A* = 0*V*, *B* = *V*DD 인 상황도 마찬가지 일 것이다.

하지만, *A* = 0*V*, *B* = 0*V* 라면 다른 상황이 일어난다.

![HW5%206c593e7de6a147a09645d997df9a621b/image28.bmp](HW5%206c593e7de6a147a09645d997df9a621b/image28.bmp)

*C*

*L*

에

*V*

DD

가 걸리게 된다.

결국 *CL* 에 걸리는 전압은 *V*DD 가 된다.

[Untitled](HW5%206c593e7de6a147a09645d997df9a621b/Untitled%20Database%20872dd7af378a4cafa39e047ca096b079.csv)

이를 표로 정리하면 다음과 같이 NOR Gate 로 동작함을 확인할 수 있다.