# 5주차 : NAND 및 NOR Gate의 구조 및 동작

 

논리설계자들은 NAND 와 NOR 게이트를 자주 사용하는데 AND 혹은 OR 게이트보다는 일반적으로 더 빠르고 더 적은 부품을 사용하기 때문이다.

이러한 NAND, NOR 게이트는 CMOS 구조로 설계가 된다.

그 이유는, 기본적으로 인버터를 설계할 때 CMOS 구조로 설계가 되는데, 여기에서 확장된 것 이라고 생각할 수 있다.

![img](https://blog.kakaocdn.net/dn/JaOJ9/btqMqCNbPkx/gZDTPolv0tYocHSZZJXkM0/img.png)

논리게이트를 만들기위해 CMOS 로 설계하는 이유는 NMOS와 PMOS 의 특성이 다르기 때문이다.

NMOS에서 게이트에 를 걸면, 트랜지스터는 turn on 되고 출력단에서 최대 만큼의 전압만 나온다. 게이트에 0V를 걸면 트랜지스터는 turn off 가 되고 출력단에서 0V 가 나온다. 즉 NMOS 는 낮은 전압은 정확하게 뱉어내지만 높은 전압은 Threshold Voltage 만큼 차감된 전압이 출력된다.

PMOS에서 게이트에 를 걸면, 트랜지스터는 turn off 되고 출력단에서는 가 나오고, 게이트에 0V를 걸면, 트랜지스터는 turn on 되고 출력단에서는 가 나오게 된다. 즉 PMOS 는 높은 전압은 정확하게 뱉어내지만 낮은 전압은 Threshold Voltage 만큼은 최소한 가지고 출력이 된다.

이 둘의 특징을 조합하여 출력에서 정확하게 , 0V 로 뱉어내는 것이다.

 

NAND Gate 과 NOR Gate 의 동작 방식을 알기 전에 CMOS 인버터의 동작방식을 먼저 알 필요가 있다.

![img](https://blog.kakaocdn.net/dn/dYyacH/btqMrj0WWGO/jO9lFG91txdXeUXgNo12G1/img.png)

왼쪽 그림과 같은 전압 특성을 가지게 된다.

처음 일 땐 채널이 형성되지 않아서 NMOS 가 꺼져있다.

 일 땐 가 보다는 크다.

NMOS 는 포화상태, PMOS 는 선형상태를 이루게 된다.

 가 되면 가 보다 낮아졌으므로, 가 보다 큰 상황이 되어 NMOS 가 선형조건을 만족하게 된다.

NMOS나 PMOS 나 정상 동작을 하기 위해선 이나 중 큰 값보다 가 크면 된다.

Logic threshold voltage 인 부분은 인 부분이며 이 부분에서 NMOS 와 PMOS가 둘다 포화돼 가 가장 잘 흐른다.

CMOS 로 만든 회로의 장점은 파워 소모가 적고 에서 0V 까지 Full Swing을 하므로 노이즈에 강하다.

최소 동작 파워 서플라이 전압도 이나 중 큰 값보다 가 크면 되므로 낮게 잡을 수 있다.

심지어 비율을 완벽하게 맞추지 않아도 동작은 한다.

![img](https://blog.kakaocdn.net/dn/cYU8Tn/btqMvLomLnV/CYKCabyIIr68kQjSzmFSA1/img.png)

각각의 소자에 대해 3가지 상황으로 해석이 가능하다.

NMOS에서 Gate가 0V 일 때 Turn off 이므로 은 Floating 된 상태이다.

Gate가 일 때 Turn on 이 되고, 가 라면 이다.

Gate가 일 때 Turn on 이 되고, 가 0V 라면 이다.

PMOS에서 Gate가 일 때 Turn off 이므로 은 Floating 된 상태이다.

Gate가 0V 일 때 Turn on 이 되고, 가 라면 이다.

![img](https://blog.kakaocdn.net/dn/ACYFF/btqMrj0WWFF/4BvQPppltHLCaYMiB2I3uK/img.png)

Gate가 0V 일 때 Turn on 이 되고, 가 0V 라면 이다.

 

위의 특성을 고려하여 논리회로처럼 간단하게 왼쪽 그림처럼 생각할 수 있다.

 

 

 

 

① NAND Gate

![img](https://blog.kakaocdn.net/dn/bxqv76/btqMtyQPYqu/Ej4POCZTWtn8NcmqFwugCK/img.png)

왼쪽 그림은 n 개의 입력을 가진 NAND Gate 이다.

| A    | B    | F    |
| ---- | ---- | ---- |
| 0    | 0    | 1    |
| 0    | 1    | 1    |
| 1    | 0    | 1    |
| 1    | 1    | 0    |

출력은 이다.

NAND Gate 의 출력은 입력들 중에서 하나 혹은 그 이상이 0 일때만 1이 된다.

만약, 2 입력 NAND Gate 라면 다음과 같은 Truth Table을 가지게 될 것이다.

 

2 개의 입력을 가진 NAND Gate를 설계하기 위해선 우선 NMOS 에서는 반전출력 을 구해야 하고, PMOS 에서는 출력 를 구해야한다.

NAND Gate 이므로 이 된다. 이는 PMOS 에 적용이 된다.

 이며 이는 NMOS 에 적용이 된다.

OR의 경우 MOSFET을 병렬로, AND의 경우 직렬로 연결하면 되므로 다음과 같은 회로도가 완성이 된다.

![img](https://blog.kakaocdn.net/dn/kLe06/btqMtyJ5boc/jwAH7kUANNJsNRD36VB4vk/img.png)

이때 PMOS 와 NMOS 의 전자이동도가 다르다는 것을 인식하고 사이즈를 매칭해줄 필요성이 있다.

이므로 와 비교했을 때 나머지 조건은 다 똑같다고 보고,

 를 만족하면 될 것이다.

일반적으로 로 매칭할 수 있다.

매칭할때에는 최악의 상황인 Worst Case 로 고려해야 한다

Worst Case 의 경우 병렬로된 트랜지스터는 다 꺼졌다고 생각하면 된다.

 

만약 PMOS 의 소자 길이가 였다면, 이 되므로, NMOS 전체의 이 된다.

2개의 NMOS 가 직렬로 연결되어 있으면 그 개수만큼 값을 곱한 값이 NMOS 각각의 사이즈가 된다.

즉, NMOS 각각은 . PMOS 각각은 가 된다.

![img](https://blog.kakaocdn.net/dn/mRCuE/btqMuQwTMIm/u3yOceAAODxmCLJslDocxK/img.png)

동작이 어떻게 하는지 확인하기 위해서 , 라고 가정을 해본다.

이때, 밑에 커패시터 을 달아준다.

NMOS 기준에서 위에 있는 트랜지스터는 turn on 이 되고, 아래에 있는 트랜지스터는 turn off 가 된다.

PMOS 기준에서 왼쪽이 있는 트랜지스터는 turn on, 오른쪽에 있는 트랜지스터는 turn off 가 된다.

오른쪽 PMOS 가 켜져 있으므로 가 에 충전될 것이다.

, 인 상황이거나 , 인 상황도 마찬가지 일 것이다.

하지만, , 라면 다른 상황이 일어난다.

 

![img](https://blog.kakaocdn.net/dn/bvNCow/btqMtza9A1K/9hNVVkV7qKWPTwRoFhJe50/img.png)

왼쪽 그림처럼 PMOS 는 모두 turn off 되고, NMOS 는 turn on 이 되어 있으므로 에 충전된 전압이 NMOS 2개를 통해 방전이 될 것이다.

결국 에 걸리는 전압은 0V 가 된다.

| A    | B    |      |
| ---- | ---- | ---- |
| 0V   | 0V   |      |
| 0V   |      |      |
|      | 0V   |      |
|      |      | 0V   |

이를 표로 정리하면 다음과 같이 NAND Gate로 동작함을 확인할 수 있다.

 

 

 

 

 

 

 

 

② NOR Gate

![img](https://blog.kakaocdn.net/dn/r2VOJ/btqMtzPKiPL/GaS3sBjXevnzLLvZfpV0bK/img.png)

왼쪽 그림은 n 개의 입력을 가진 NOR Gate 이다.

출력은 이다.

만약, 2 입력 NOR Gate 라면 다음과 같은 Truth Table을 가지게 될 것이다.

| A    | B    | F    |
| ---- | ---- | ---- |
| 0    | 0    | 1    |
| 0    | 1    | 0    |
| 1    | 0    | 0    |
| 1    | 1    | 0    |

![img](https://blog.kakaocdn.net/dn/mR7b5/btqMrkeuPS8/i41Z7PgDy0EVKY2TvX88n1/img.png)

2 개의 입력을 가진 NOR 를 설계하기 위해선 우선 NMOS 에서는 반전출력 을 구해야 하고, PMOS 에서는 출력 를 구해야한다.

NAND Gate 이므로 이 된다. 이는 PMOS 에 적용이 된다.

 이며 이는 NMOS 에 적용이 된다.

 

NAND Gate를 설계할 때처럼 전자이동도를 고려하여 사이징을 해주기 위해

 를 만족하면 될 것이다.

일반적으로 로 매칭할 수 있다.

만약 NMOS 의 소자 길이가 였다면, 에서 이 되므로, 가 되고, PMOS 전체의 이 된다.

2개의 PMOS 가 직렬로 연결되어 있으면 그 개수만큼 값을 곱한 값이 NMOS 각각의 사이즈가 된다.

즉, NMOS 각각은 . PMOS 각각은 가 된다.

동작이 어떻게 하는지 확인하기 위해서 , 라고 가정을 해본다.

![img](https://blog.kakaocdn.net/dn/sN6Te/btqMtz3huAK/BGJ1k5b25DDX13aP6PNL7K/img.png)

이때, 밑에 커패시터 을 달아준다.

NMOS 기준에서 왼쪽에 있는 있는 트랜지스터는 turn off 가 되고, 오른쪽에 있는 트랜지스터는 turn on 된다.

PMOS 기준에서 위쪽이 있는 트랜지스터는 turn off, 아래쪽에 있는 트랜지스터는 turn on 된다.

직렬로 연결된 PMOS 중 한 개 라도 OFF 되어 있으므로 에 충전된 전압이 오른쪽 NMOS 통해 방전이 될 것이다. 즉 0V 가 출력된다.

, 인 상황이거나 , 인 상황도 마찬가지 일 것이다.

하지만, , 라면 다른 상황이 일어난다.

 

![img](https://blog.kakaocdn.net/dn/nlm1V/btqMuPLwK5f/IWpRc0c2B3yhSd8eiY3No1/img.png)

왼쪽 그림처럼 NMOS 는 모두 turn on 되고, PMOS 는 turn off 되어 있으므로 에 가 걸리게 된다.

결국 에 걸리는 전압은 가 된다.

| A    | B    |      |
| ---- | ---- | ---- |
| 0V   | 0V   |      |
| 0V   |      | 0V   |
|      | 0V   | 0V   |
|      |      | 0V   |

이를 표로 정리하면 다음과 같이 NOR Gate 로 동작함을 확인할 수 있다.