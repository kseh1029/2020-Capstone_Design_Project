# Project

**Design Project**

**Spring, 2020**

**ITEC401011**

**Professor: Jae Hoon Shim**

1. **Abstract**

본 설계의 특징은 다음과 같다.

- 동기식 SRAM Array

Enable 신호에 Row Decoder를 동기화하여 Enable 신호가 인가될 때만 Word Line이 선택되고, Read, Write 동작이 발생하게 하였다. Enable 신호의 사용으로 설계가 간단해지고 동작 분석이 용이하였다. 그리고 SRAM Cell의 Hold mode 동작을 보장할 수 있고, Gate delay문제 해결을 위한 setup time, hold time 설정이 용이하였다. 하지만 Read와 Write 동작을 분리할 수 없기 때문에 최적의 Read cycle, Write cycle을 만드는 데는 한계가 존재했다.

- Pre-Charge Circuit

BL과 BLB가 pre-charge에 의하여 충전될 때 균형적으로 충전될 수 있게 PFET을 BL과 BLB 사이에 연결하였다. 따라서 불균형하게 초기 전압 값을 가지고 있어도 Pre-charge 후에는 비슷한 Pre-charge level을 가지도록 하였다.

- Row Decoder

Enable 신호에 Row Decoder를 동기화하여 입력인 Address 신호에 상관없이 Device를 on, off 할 수있게 설계하였다. 그리고 2단 Partial Decoding으로 사용되는 TR의 개수를 줄여 전력 소모를 줄였다.

- Column Decoder

A[0] 신호를 입력으로 8words*8bit SRAM Array를 16words*4bits SRAM Array로 변환시켰다. A[0] 신호로 왼쪽 column(또는 왼쪽 페이지)을 선택하거나 오른쪽 column을 선택할 수 있게 하였다. 이로 인해 사용되는 Sense Amplifier와 Write Driver의 개수를 줄여 전력 소모, 면적, cost를 줄일 수 있었다.

- CMOS Transmission Gate

SRAM Array에 사용되는 Pass TR을 CMOS Transmission Gate로 대체하여 Low signal과 High signal 모두 잘 전달할 수 있게 하였다.

- Sense Amplifier

SA의 BL, BLB와 SA의 cross coupled inverter 사이에 CMOS Transmission Gate를 삽입하여 Write 동작과 Read 동작 시에 스위치 역할을 할 수 있게 하였다. 따라서 Latch type SA의 단점인 leakage 문제를 해결하였다. 그리고 cross coupled inverter의 VDD, GND와 연결되는 TR의 게이트 입력에 control 신호를 인가하여 Read 동작이 일어나지 않을 때에는 전원을 off 시킬 수 있게 하였다. 따라서 전력 소모를 줄일 수 있었다.

- Write Driver

Write control 신호를 통하여 Write 동작이 일어나지 않을 때에는 Write Driver를 off 시켜 전력 소모를 줄일 수 있었다.

- 참고사항

PRE : Pre-Charge Circuit의 Control Signal (Active Low)

EN : Common Enable Signal (Active Low)

A[3:1] : Row Decoder의 Address Signal

A[0] : Column Decoder의 Left Page, Right Page 선택을 위한 Signal

RWSEL : Read or Write operation을 선택해주는 Signal

(초기 16 cycle RWSEL=0 -> Write 동작, 후기 16 cycle RWSEL=1 -> Read 동작)

SAE : Sense Amplifier Control Signal (Active High)

WEN : Write Driver Control Signal (Active Low)

RDATA[3:0] : Sense Amplifier 를 통해 Read 한 data

WDATA[3:0] : Write Driver 를 통해 Write 할 data

1. **Sub-Blocks Introduction**

**2.1 Pre-charge Circuits**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image0.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image0.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image1.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image1.bmp)

**<Pre-charge circuit Schematic>**

**2) the reasons you have chosen the particular structure**

Read 동작 시에는 이전 cycle 동작의 결과로 SA와 직접적으로 연결되는 BL과 BLB의 초기 전압 값이 다를 수 있다. 이로 인해 Pre-charge 시에 BL과 BLB의 Pre-charge level mismatching 문제가 발생하게 되고, 이는 Destructive Read (Read upset)의 원인이 된다. 따라서 Pre-charge circuit의 BL과 BLB 사이에 PFET을 연결하여 BL과 BLB가 Pre-charge 될 때, 균형을 잡아주도록 한다.

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20b0d9f8b5dbb04b5eb32d851828e54834.csv)

BL과 BLB의 Pre-charging 충전량 및 속도를 증가시킬 수 있는 방법은 다음과 같다.

- **Pre-charge circuit의 control signal인 PRE의 on time을 증가시킨다.**

현재 Pre-charge circuit의 control signal인 PRE는 PFET을 이용한 active low input 이다. 따라서 PRE=0을 인가해주는 시간을 증가시킨다면 BL과 BLB의 Pre-charge level이 증가할 것이다.

- **pre_pass를 증가시킨다.**

pre_pass가 증가하면 VDD와 연결된 PFET의 channel width가 증가하므로 pre-charging 통로의 폭이 증가하게 된다. 따라서 동일 시간에 더 많은 양의 전하를 흘려보낼 수 있으므로 pre-charging 속도가 증가한다.

- **pre_balance를 증가시킨다.**

pre_balance가 증가하게 되면 BL과 BLB 중 potential이 낮은 곳에서 충전이 더 원활하게 발생되게 할 수 있다. 2) the reasons you have chosen the particular structure에서 언급한대로 Read 동작 시에는 BL과 BLB의 초기 전압 값 mismatching으로 인해 Read failure가 발생할 수 있으므로 pre_balance를 증가시켜 BL과 BLB의 불균형을 해소해야만 한다.

**<BL, BLB의 초기 전압 불균형>**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image2.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image2.bmp)

예를 들어, 좌측의 그림은 Read 동작 시에 이전 Read 동작의 결과로 SA와 직접적으로 연결되어 있는 BL과 BLB의 초기 전압 값이 불균형한 것을 볼 수 있다.(주황색: 600mV / 노란색: GND)

이 때 pre_balance 값을 증가한다면 Pre-charging 동작이 끝난 후 BL과 BLB의 pre-charge level이 비슷하게 될 것이다. 따라서 read upset을 방지할 수 있다.

**<Pre-charge 시뮬레이션>**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image3.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image3.bmp)

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

본 설계의 Pre-charge circuit은 단순 통과 역할 하는 PFET 2개와 BL, BLB의 균형적 charging을 위한 PFET 1개로 이루어져있다. 이 3개의 PFET 게이트 입력으로 Pre-charge circuit의 control signal인 PRE 신호가 입력된다. PFET을 이용하여 Pre-charge circuit을 구성하였으므로 Active Low 입력을 가진다. 따라서 PRE=0이 입력되면 3개의 PFET이 turn on 되어 Pre-charge circuit이 ON 되게 된다.

Pre-charge circuit이 ON되면 64bit SRAM의 전원인 VDD의 charge가 PFET을 통과하여 BL과 BLB로 흐르게 된다. Read와 Write 동작을 위한 충분한 전압 값이 BL과 BLB에 전달된다면 PRE=1이 되어 Pre-charge circuit은 전체 회로와 분리되게 된다.

**Design Consideration**

Write 동작을 위한 사전 Pre-charge 동작에서는 SRAM Cell과 직접적으로 연결된 BL과 BLB의 전압 레벨을 VDD 까지 증가시켜야 한다. 하지만 Read 동작을 위한 Pre-charge 동작에서는 SA와 직접적으로 연결된 BL과 BLB의 전압 레벨을 VDD 까지 증가시켜야 했다. 따라서 Read 동작을 위한 Pre-charge에서는 Pre-charge 동작이 원활히 수행되지 못하였다.(SA에 direct로 연결된 BL과 BLB는 Pre-charge circuit과 직접적으로 연결되어 있지 않고, 중간에 Column Decoder를 지나므로 Write 동작보다 pre-charge 속도가 느릴 수 밖에 없다.)

따라서 Read 동작 시에는 PRE control signal의 on time을 증가시키거나 pre_pass 변수를 증가시켜 Pre-charge 충전량을 인위적으로 증가시킬 수 있게 하였다. 그리고 read upset 방지를 위해 pre_balance 변수도 적절하게 증가시켜 read 동작이 일어나기 전 SA와 연결된 BL, BLB가 균등하게 Pre-charge가 되도록 하였다.

**Sizing of TR**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%209735e55e6e534623ab7c7b80d0da2d24.csv)

pre_balance 변수 값을 pre_pass 보다 크게 설정하여 균등한 Pre-charge가 잘 되도록 하였다.

**2.2 Row Decoder**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image4.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image4.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image5.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image5.bmp)

**<Row Decoder Schematic>**

**2) the reasons you have chosen the particular structure**

- **Enable**

Enable 신호를 Row Decoder의 제어 신호로 입력해주었다. 따라서 A[3:1] address line이 EN 신호에 동기화된다. 이로 인한 이점은 다음과 같다.

➜ A[3:1]의 변화에 의한 gate delay 문제를 손쉽게 해결 할 수 있다. EN=1 일 때는 word line이 Row Decoder의 출력을 항상 0으로 유지하게 한다. 따라서 A[3:1] 입력 변화로 발생하는 gate delay 문제 해결을 위한 setup time을 EN=1인 구간을 조절함으로서 쉽게 설정할 수 있다.

➜ EN=0 일 때만 word line이 ON 될 수 있으므로 simulation 분석이 용이하다.

➜ EN=1 일 때, 모든 word line이 OFF 되므로 모든 CELL을 hold 모드에 위치시킬 수 있다. 따라서 Read 또는 Write 동작을 하지 않을 때에는 CELL을 hold 모드에 위치시켜 외부 환경으로부터 Cell에 저장된 data를 보호할 수 있다.

➜ EN에 address line이 동기화 되어 있으므로 EN 신호로 read 또는 write 1 cycle 조절이 용이하다.

- **Partial Decoding**

현재 A[3:1] 신호를 입력으로 받는 3 to 8 Row Decoder는 일반적인 Full Decoding 방식이 아닌 2단 partial decoding 방식으로 설계하였다. 따라서 사용하는 TR의 개수를 줄여주게 되어 전력 소모 관점에서 이점을 가진다.

본 설계의 3 to 8 Partial Row Decoder는 입력신호 A[3:1]의 반전을 위한 inverter 3ea, 1단 decoding에서 사용되는 2 input NAND 게이트 4ea, 2단 decoding에서 사용되는 3 input NOR 게이트 8ea를 사용한다. 따라서 총 70ea의 TR을 사용하게 된다. 이는 Full Decoding 방식에서 86개를 사용하는 것에 비해 적은 수치이다.(Full Decoding에서는 입력신호 A[3:1]의 반전을 위한 inverter 3ea, 4 input NAND 게이트 8ea, NAND 게이트 출력 반전을 위한 inverter 8ea 사용함.)

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%209a143fcb68384c048ba0bc555cfb1f34.csv)

Row Decoder의 Device delay는 다음과 같이 이론적으로 유추해볼 수 있다.

Device delay = inv delay + 2-input NAND delay + 3-input NOR delay

본 설계에서 사용하는 모든 inverter, NAND gate, NOR gate는 이전 종합설계프로젝트 과제에서 디자인한 소자를 사용하였다. (worst case matching 후에 inverter delay = 약 10ps, 2 input nand gate delay = 약 15ps, 2 input nor gate delay = 약 15ps, 3 input nor gate = 약 18ps로 설계하였음.)

따라서 Device delay = 10ps + 15ps + 18ps = 약 43ps 로 유추해볼 수 있다. 하지만 본 설계의 Row Decoder는 enable 신호에 동기화 되어있으므로 EN = 0이 될 때, 3 input nor gate delay만 고려해주면 된다. 시뮬레이션 결과 EN이 ON될 때, word line이 ON 되는 delay 시간은 다음과 같았다.

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image6.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image6.bmp)

**<Enable 신호를 가진 Row Decoder 지연 시간>**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image7.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image7.bmp)

**<Enable 신호를 가진 Row Decoder Simulation>**

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

EN=1이 되면 3 input NOR gate의 출력이 항상 0이 되므로 모든 word line은 OFF 된다. 따라서 모든 Access TR을 OFF 시키므로 cell은 hold mode에서 동작된다. EN=0이 되면 address line 변화에 따라 word line이 활성화되어 해당 word line의 cell이 선택된다. 주의할 점으로 EN=0을 인가하기 전에 충분한 시간동안 EN=1을 유지 시켜서 setup time을 보장해주어야 한다. 즉, EN=1인 구간에서 address 신호 변화에 의한 gate delay를 해소시켜야만 한다.

**Design Consideration**

A[3:1] address 신호는 enable 신호에 동기화되어 변화한다. 따라서 enable 신호의 주기가 T라면 A[1]의 주기는 2T, A[2]의 주기는 4T, A[3]의 주기는 8T가 되도록 입력신호를 인가하여야 한다.

**Sizing of TR**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20a48ba342baa6432ba11d305a5ea58c01.csv)

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20c760ff383619437198d437520686ac3c.csv)

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20b43e3c7c39bf48a1a32aada360dcbdfa.csv)

**2.3 Column Decoder**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image8.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image8.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image9.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image9.bmp)

**<Column Decoder Schematic>**

**2) the reasons you have chosen the particular structure**

Column Decoder의 목적은 Row Decoder에 의해 8words*8bits로 설계된 SRAM Array를 16words*4bits의 SRAM Array로 바꾸는 것이다. 따라서 사용되는 SA와 Writer Driver의 개수를 최소화 시킬 수 있다.(본 설계에서는 SA, WD 4ea 사용) SA와 WD에는 많은 TR이 사용되므로 SA와 WD의 사용 개수를 줄인다면 전력 소모를 줄일 수 있고, SRAM full structure의 면적을 줄일 수 있는 이점이 있다. 또 device cost 측면에서도 유리하다.

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20d1812c81d49c4660b8a600cec5580dbd.csv)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image10.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image10.bmp)

CMOS 전달 게이트의 채녈 폭 변수 column_passn, column_passp가 증가한다면 BL, BLB에서 전하가 통과할 수 있는 통로의 폭이 커지기 때문에 BL과 BLB에 동기화 되어있는 모든 line에서의 charge 변화가 빠르게 일어난다. 즉, read 또는 write 시의 동작 속도가 빨라진다.

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image11.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image11.bmp)

**<Column Decoder의 page select test>**

A[0]=0일 때 왼쪽 페이지가 선택되어 Pre-charge 신호 이후 LABL(왼쪽 페이지 BL)과 BL_A(Column Decoder 출력)가 같게 되고, A[0]=1이 되면 오른쪽 페이지가 선택되어 Pre-charge 신호 이후 RABL(오른쪽 페이지 BL)과 BL_A가 같아진다. 따라서 Column Decoder가 정상적으로 동작하는 것을 확인 할 수 있다.

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

Column Decoder의 입력 신호 A[0]가 0이 되면 왼쪽 페이지가 선택되고, 그 반대의 경우에는 오른쪽 페이지가 선택된다. 즉 A[0]=0이면 왼쪽 Column의 BL, BLB가 SA와 WD에 연결되고, A[0]=1이면 오른쪽 Column의 BL, BLB가 연결된다.

초기 설계 시에 Column Decoder의 PASS TR 역할을 PFET으로 동작하게 하였다. 그런데 PFET은 Low signal을 잘 전달하지 못하므로(*VS*⟩ ∣ *V*THP ∣, TR ON 조건 만족 해야함.) 항상 ∣ *V*THP ∣ level에서 신호가 걸렸다. 따라서 PFET을 CMOS 전달게이트로 대체하여 Low / High signal 모두를 잘 전달하도록 하였다.

**Design Consideration**

Read / Write 동작 시에 중간 통로 역할을 하는 Column Decoder의 CMOS Pass TR의 채널 폭이 작다면 BL, BLB의 charge 변화가 정상적으로 발생하지 않았다. 따라서 BL, BLB 통로에서의 charge 변화 속도가 느리다면 column_passp, column_passn을 증가시켜 통로의 폭을 키워주었다.

**Sizing of TR**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20f1ca7856487f48f492d25c99a9010daa.csv)

**2.4 Sense Amplifiers**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image12.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image12.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image13.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image13.bmp)

**<Sense Amplifier Schematic>**

**2) the reasons you have chosen the particular structure**

- **저전력 및 빠른 읽기 속도 / 안정성**

저전력 및 빠른 읽기 속도를 가지므로 Latch type sense amplifier를 선택하였다. 그리고 Pre-charge level으로 VDD를 사용하므로 안정성에 이점이 있다. 하지만 예기치 못한 문제가 발생하였다.

- **Leakage 개선**

Write 동작 시에 SA는 OFF되지만 SA와 WD는 같은 Column을 공유하고 있으므로 SA의 parasitic capacitance가 WD의 BL, BLB와 연결되는 문제가 발생하였다. 따라서 Write 동작을 하기 위한 Pre-charge 단계에서 charge가 빠지면 안 되는 Bit Line에서 leakage가 생기는 문제가 발생하였다. 따라서 이 문제를 해결하기 위하여 RWSEL control 신호를 가지는 CMOS 전달 게이트를 SA의 Bit Line과 SA cross coupled inverter 사이에 연결하였다. 따라서 Write 동작 시에는 SA가 BL과 완전히 분리될 수 있도록 설계하였다. 스위치 역할을 하는 CMOS 전달 게이트를 도입하기 이전에는 Write 동작 시 Pre-charge에서 leakgae가 발생하였지만, 도입 이후 leakage가 발생하지 않았다.

- **SA Bit line path**

2.3의 Column decoder와 마찬가지로 SA BL의 TR은 단순히 신호를 전달하는 PASS TR 역할을 한다. 따라서 CMOS 전달게이트로 PASS TR을 구성하여 Low / High signal을 잘 전달하도록 하였다.

- **VDD / GND TR**

cross coupled inverter의 VDD / GND 와 연결되어 있는 게이트 입력에 SAE(Read Control signal)를 입력하여 SA가 OFF 될 때는 VDD와 GND line이 끊어지게 하였다. 따라서 불필요한 전력소모를 줄일 수 있었고, Read 동작 시에 SA의 Bit Line과 SRAM Cell에서 발생하는 charge 변화를 SA의 Bit Line에서 잘 보존할 수 있도록 하였다.(SA Bit Line의 charge가 SA의 cross coupled inverter의 GND로 빠지지 않고, VDD에 의해 영향을 받지 않게 하였음.)

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20e2669b48bd3944e5995e04c0d04c1aeb.csv)

- sa_vddpass / sa_gndpass를 증가하면 SAE 신호가 들어온 후 발생하는 read 속도를 증가시킬 수 있다.
- sa_passn / sa_passp를 증가하면 SAE 신호가 들어오기 전 SA의 BL, BLB에서의 작은 전압 변화량을 증가시킬 수 있다.
- Read cycle 3. Design Results 참고.

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

- RWSEL

Write 동작 시에는 항상 RWSEL=0으로 인가하여 SA cross coupled inverter와 SA BL, BLB 사이의 CMOS 전달게이트를 OFF 시킨다. 따라서 Write 시에 SA의 parasitic capacitance에 의한 leakge 문제를 방지할 수 있다.

Read 동작 시에는 항상 RWSEL=1이 되어 SA BL, BLB와 SA cross coupled inverter가 항상 연결된다.

- SAE (Active High)

평소에는 SAE=0을 유지하고 있으므로 SA와 direct로 연결되어있는 BL, BLB의 CMOS 전달 게이트가 항상 ON 된다. 그리고 SA cross coupled inverter의 VDD와 GND는 항상 OFF 되어 불필요한 전력 손실을 차단한다. 그리고 Read 시에만(SAE=1이 될 때) SA의 inverter가 동작되도록 한다.

Read 동작 시에 1) PRE=0이 되어 SA와 direct로 연결되어 있는 BL, BLB가 pre-charging 된다.

2) 그 후 enable 신호를 통해 읽고자 하는 word line이 ON 되면 SA의 BL과 SRAM Cell에서 작은 전압 변화가 생긴다.

3) 그 후 SAE=1이 되면 SA BL, BLB의 CMOS 전달 게이트가 OFF 되고, SA 내부의 cross coupled inverter가 외부 회로와 완전히 분리된다. 따라서 그 때 2번에서 발생한 미세한 작은 전압변화를 감지 및 증폭하여 RDATA OUT으로 내보낸다.

**Design Consideration**

Read 동작 시에는 반드시 다음과 같은 Control 신호 순서가 지켜져야 한다.

1) PRE=0

SA와 direct로 연결된 BL, BLB가 VDD 까지 충분히 pre-charging 되어야 한다. 그렇지 않다면 후에 Read 동작 시 read upset이 발생할 수도 있다.

➜ 따라서 충분히 pre-charging 되는 시간이 보장 되어야하며 pre-charge 충전량 및 충전 속도는 pre_pass / pre_balance 변수로 조절할 수 있다.

2) EN=0 (word line ON)

SRAM Cell은 Q는 0, QB는 1과 같이 상호 반대의 논리 값을 저장하고 있다. 따라서 word line이 ON 되면 0이 저장되어 있는 Bit Line에서 전압 감쇠가 심할 것이다. 따라서 word line이 ON 되어 있는 구간을 통해 SA의 BL에서 작은 전압 변화를 만든다. 따라서 작은 전압 변화를 만들기 위해 충분한 시간동안 SA의 BL, BLB와 CELL을 연결시켜 주어야 한다.

➜ CR의 증가로 전압 변화량을 증가시킬 수 있다. CR이 증가한다면 SRAM Cell의 PDN의 구동력이 Access TR보다 강력해지기 때문에 discharging 속도가 증가하게 된다.

3) SAE=1 (SA ON)

SAE에 1이 인가되면서 SA는 외부 회로와 완전히 분리된다. 이 때 2번의 결과로 SA의 BL, BLB에는 작은 전압 차이가 있고 cross coupled inverter에서 이 작은 전압 변화를 감지 및 증폭하여 RDATA를 출력한다. 따라서 SA inverter가 감지 및 증폭하는 충분한 시간동안 SAE=1이 유지되어야 한다.

➜ sa_vddpass / sa_gndpass를 증가하면 SA cross coupled inverter의 동작속도를 증가 시킬 수 있다.

**Sizing of TR**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20c3a64e5b9345452dbcb9c60e491ae6e4.csv)

**2.5 Write Drivers**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image14.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image14.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image15.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image15.bmp)

**<Write Driver Schematic>**

**2) the reasons you have chosen the particular structure**

WEN(write contol signal) 신호로 write 동작을 하지 않을 때에는 확실하게 외부 회로와 WD 회로를 분리시킬 수 있고, 그리고 WDATA(입력 data) 신호로 BL 또는 BLB 한 곳을 확실히 discharging 시켜서 write 동작 수행 전 SRAM Cell의 BL과 BLB에 wdata를 Full swing한 값으로 준비시켜 안정적인 쓰기 동작이 가능한 장점이 있다.

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%2085a500632ae9470894868868f0620942.csv)

- wd_passtop / wd_passbottom을 증가시키면 WDATA를 SRAM Cell의 BL과 BLB에 입력하는 속도를 증가시킬 수 있다.

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image16.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image16.bmp)

**<Write 0101 Operation>**

위의 결과는 직접 SRAM Cell의 Q state를 측정하여 Write 0101 operation을 확인한 것이다.

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image17.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image17.bmp)

**<Write 0111 Operation>**

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

- **** WEN=0

Write Driver의 위쪽의 NFET이 OFF 되어 WD가 외부 회로와 분리됨.

- WEN=1

1) PRE=0이 되어 SRAM CELL의 BL과 BLB가 VDD로 Pre-charge 된다.

2) PRE=1이 되어 Pre-charge circuit은 외부 회로와 분리되고, WEN=1이 되어 WDATA가 BL, BLB에 준비된다.

3) EN=0이 되어 word line이 ON 되면 Cell 내부 inverter에 의해 writing이 이루어진다.

**Design Consideration**

Read 동작 시와 마찬가지로 상단의 Analysis of the circuits에서 언급한 Control 신호의 순서와 각 Control 신호에서 발생하는 동작의 충분한 시간을 보장해주어야 한다.

따라서 Pre-charge를 위해서는 pre_pass, pre_balance, PRE control signal on time을 조정하며 BL, BLB가 충분히 pre-charge 되도록 해야 한다.

그리고 WEN=1이 될 때 wd_passtop, wd_passbottom을 조정하여 BL과 BLB에 wdata 값이 미리 써져있도록 해야 한다. 마지막으로 가장 중요한 점은 Write 동작 수행시 read stability 조건에 의하여 CR 값이 크므로 PR 값을 충분히 작게 해주어 SRAM Cell cross coupled inverter의 inverting에 의한 writing 동작이 잘 이루어지도록 하여야 한다.

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%209565af2e9f344fde8e301806299824b8.csv)

**Sizing of TR**

**2.6 SRAM Cell**

**1) Circuit Schematic diagrams**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image18.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image18.bmp)

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image19.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image19.bmp)

**<6T SRAM CELL Schematic>**

**2) the reasons you have chosen the particular structure**

4T SRAM에 비해 SNM이 뛰어나서 안정적으로 동작하고, 동작속도가 빠르다. 하지만 전력소모가 크고, 차지하는 면적이 크다는 단점이 있다. 하지만 이번 설계는 전력소모 보다는 동작속도에 중점을 맞추는 설계이므로 6T SRAM을 사용하였다.

**3) Specifications of the sub-blocks**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20069cdf4ce8354a7f83e9c6742f54af3c.csv)

PR을 감소시키면 SRAM Cell의 cross coupled inverter의 inverting에 의한 writing 동작이 잘 일어나게 되고, CR을 증가시키면 Read 동작시의 작은 전압 변화량을 증가시켜 Read 동작이 잘 일어나게 한다.

**4) Analysis of the circuits and design considerations (including sizing of**

**transistors)**

**Analysis of the circuits**

Write Driver와 Latch type SA를 이용하여 Read / Write 동작을 수행함.

**Design Consideration**

모든 설계 값을 정하고 최종 Read 동작을 확인할 때 CR, PR 값 조정에 Read, Write 동작이 매우 민감하게 반응하였다. 따라서 CR, PR 값을 조정할 때에는 매우 작은 변화만을 주며 시뮬레이션을 반복적으로 진행하였다.

**Sizing of TR**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%2067cefad0bb654f148917c13c245793b7.csv)

1. **Design Results**

**< Process Corner : tt (NFET : Typical, PFET : Typical), Temperature : 25’C >**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image20.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image20.bmp)

최초 설계에 사용한 Process Corner 인 mc 의 경우 통계적인 결과를 이용하였으므로 현실적인 결과를 얻었다. Process Corner 가 tt 일 때 NFET 과 PFET 의 동작 스피드는 Typical 하므로 가장 Ideal 한 경우이다. 통계적인 결과로 얻은 mc 와 tt 는 비슷한 동작 속도를 가질 것이며 실제로도 mc 와 tt의 결과는 거의 동일했다.

**< Process Corner : fs (NFET : Fast, PFET : Slow), Temperature : 25’C >**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image21.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image21.bmp)

Process Corner 가 fs 일 때에는 NFET 이 빠르고 PFET 이 느리다. Write Driver 는 4개의 NFET을 가지고 있으므로 NFET 의 구동력이 커지면서 더 우수한 쓰기 능력을 확인할 수 있었다.

Pre-Charge Circuit 는 PFET 에 직접적으로 영향을 받지만 본 설계에서 Pre-charge PFET의 Width를 상당히 크게 잡았으므로 PFET 의 작아진 구동력이 Pre-Charging 에 큰 영향을 주지 않았다.

**< Process Corner : sf (NFET : Slow, PFET : Fast), Temperature : 25’C >**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image22.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image22.bmp)

Process Corner 가 sf 일 때에는 NFET 이 느리고 PFET 이 빠르다.

fs 일 때 와는 반대로 Write Driver 에 있는 4개의 NFET 의 구동력이 떨어지면서 쓰기가 제대로 되지 않고 있다. 쓰기가 제대로 되지 않았기 때문에 읽기 또한 올바른 결과를 얻지 못했다.

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image23.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image23.bmp)

**< Process Corner : mc, Temperature : 25’C >**

Write 동작이 정상적으로 되기 위하여 PRE – WEN – EN(word line) 의 순서로 Control 신호를 인가하였다. 그리고 각 구간에서 정상적인 동작을 하도록 충분한 시간을 보장해주었다.

마찬가지로 Read 동작 시에 PRE – EN – SAE의 순서로 Control 신호를 인가하였고, 각 구간에서 정상적인 동작을 하도록 충분한 시간을 보장해주었다.

시뮬레이션 결과 16 cycle Write 이후 16 cycle Read가 올바른 논리 값을 읽는 것을 확인 할 수 있었다.

**3.2 Performance Summary**

**1) Total Read/Write time**

본 설계는 공통 enable 신호에 동기화된 동기식 SRAM 이다. 따라서 모든 Read, Write 동작은 Active Low Enable 신호가 Low 일 때 발생한다. 현재 Enable 신호의 주기는 period = 1800[ps]이므로 16 cycle read time은 28800[ps]이고, 16 cycle write time 역시 28800[ps]이다. 따라서 total read/write time은 57600[ps]이다.

**2) Total energy consumption**

![Project%2071bf3773a8884bb5a8c76dc973c5851b/image24.bmp](Project%2071bf3773a8884bb5a8c76dc973c5851b/image24.bmp)

현재의 SRAM Array는 1V VDD 독립전압원에 의해 구동된다.

따라서 32cycle 회로 동작 중 VDD에서 소모하는 전력은 다음과 같다.

*P*total = 16.119[mW]

따라서 *P* × *T*2 = 0.05347[fW • *s*]

**3) Number of used devices**

[Untitled](Project%2071bf3773a8884bb5a8c76dc973c5851b/Untitled%20Database%20b34233c6ecf5475692ad9491385d91f8.csv)

1. **Conclusion**

동기식 SRAM으로 설계를 진행하면서 설계가 간편하고, 분석이 용이하여 Write, Read 동작에서 문제가 발생하면 해결해 나가는데 큰 도움이 되었다. 하지만 동기식 SRAM을 사용하면서 Write Cycle과 Read Cycle을 분리할 수 없어서 전체 동작 Cycle을 감소 시키는데에는 큰 어려움이 있었다. 동기식 SRAM을 사용하면서도 Write Enable과 Read Enable을 분리하여 사용한다면 Write와 Read Cycle을 별도로 제어할 수 있다고 생각된다. 따라서 Enable 신호를 사용하면서도 전체 32 cycle 동작 시간을 획기적으로 줄일 수 있을 것 같다.

만약 비동기식 SRAM으로 설계 하였다면 Write Cylce과 Read Cycle을 다르게 둘 수 있어 Readability와 Writability를 만족하는 범위 내로 Cycle을 줄여 전체 시간을 감소할 수 있었다는 생각이 든다.

SRAM의 읽기와 쓰기는 비트라인의 충, 방전 및 인버팅 동작으로 이루어지기 때문에 각 서브셀들을 이어주는 전달 게이트의 사이즈, SRAM 셀 내부의 사이즈 설정이 매우 중요했다.

특히 인버팅으로 작동하는 감지 증폭기의 경우 작은 차이에도 큰 출력을 만들어 Read upset 문제가 빈번하게 발생하였다. 따라서 SAE 신호가 들어오기 전에 BL과 BLB의 방전 속도가 느려 반대의 결과를 나타나는 상황을 겪었다.(Read upset)

프리차지 회로에 의해 BL과 BLB가 VDD 로 모두 충전되어야 하는 상황에서도 감지증폭기 상단, 하단, 워드라인 상단 모두 전압의 차이가 발생하는 것을 보고 단순히 프리차징이 되는 것이 아닌 각 서브셀의 전하가 빠지는 현상, 기생 커패시턴스의 충전 등 다양한 요소를 고려해야 했다.

소자가 정상적으로 동작하는 범위 내에서 설계사양을 맞추기 위하여(동작 속도 및 전력 소비 측면) 설계를 수도 없이 재검토하고 시뮬레이션을 하면서 회로를 디자인할 때 겪을 수 있는 많은 난관을 간접적으로나마 경험할 수 있었다.