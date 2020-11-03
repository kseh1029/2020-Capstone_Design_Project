# 7주차 : Inverter

Consider the following inverter circuit. The channel lengths of nmos1v and pmos1v devices are all 45 nm. For the capacitor, use the ‘cap’ device from ‘analogLib’.

> 

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image0.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image0.bmp)

(a) The channel width of nmos1v is 120 nm. Let the channel width of pmos1v is pr×120 nm. Plot the DC transfer curves (*VO* vs. *VI*) changing pr from 1 to 2 with a step size of 0.1. What is the value of pr that makes Vo closest to 0.5 V when VI = 0.5 V? pr = 1.2

**pr = 1.2 일 때 input 499.872mV, output 499.9237mV 로 가장 적합하다.**

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image1.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image1.bmp)

**회로구성**

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image2.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image2.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image3.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image3.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image4.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image4.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image5.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image5.bmp)

*VO* /*VI* **출력 그래프**

**Inverter 내부**

**Virtuoso Simulation 설정**

(b) Find the minimum channel width of nmos1v that makes trise and tfall are both less than 10 ps. Use the pr value obtained in (a). Make sure that the rise/fall time of VI is less than 1 ps when run the ‘tran’ simulations. Width = 620nm

pr 은 (a)에서 구한 1.2를 그대로 사용하였다.

일반적으로 rise time *tr* 은 출력 신호 전압의 10%에서 90% 까지 올라가는데 걸리는 시간이다. 즉 0.1V ~ 0.9V 사이 동안 걸리는 시간을 뜻한다.

마찬가지로 fall time *tf* 은 출력 신호 전압의 90%에서 10% 까지 내려가는데 걸리는 시간이다. 즉 0.1V ~ 0.9V 사이 동안 걸리는 시간을 뜻한다.

만약 Propagation Delay를 구하는 것 이라면 입력이 rising 할 때 전압의 50%, 출력이 falling 할 때 전압의 50% 사이 동안의 걸리는 시간이 *t*pHL 이며

입력이 falling 할 때 전압의 50%, 출력이 rising 할 때 전압의 50% 사이 동안의 걸리는 시간이 *t*pLH

이다.

*tf*, *t*pHL 은 NMOS 특성에 영향을 받고, *tr*와 *t*pLH 는 PMOS 특성에 영향을 받는다.

nmos1v 소자의 채널을 조절해서 *tf* 을 줄일 수 있고, pmos1v 소자의 채널을 조절해서 *tr* 을 줄일 수 있다.

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image6.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image6.bmp)

위 그림은 PMOS, NMOS의 Channel Width를 120nm~520nm 까지 10nm 씩 증가시킨 plot 이다.

단, PMOS 는 pr (1.2) 가 곱해진 Channel Width 이다.

예상했던대로 Channel Width 가 증가할수록 *tf*, *tr* 에 큰 영향을 주고 있다.

Channel Width 가 증가할수록 *tf*, *tr* 가 단축되고 있다.

< 과제에서 제안한 trise (*t*pLH), tfall (*t*pHL) 를 10 ps 이내로 맞추기 >

**120nm 일 때** *t*pLH **= 30.9ps,** *t*pHL **= 26.448ps**

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image7.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image7.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image8.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image8.bmp)

**290nm 일 때** *t*pLH **= 16.45ps,** *t*pHL **= 13.71ps**

**400nm 일 때** *t*pLH **= 13.29ps,** *t*pHL **= 11.17ps**

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image9.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image9.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image10.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image10.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image11.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image11.bmp)

**620nm 일 때** *t*pLH **= 10.00ps,** *t*pHL **= 8.65ps**

**vpulse 설정 값**

*t*pHL 은 *t*pLH 에 비해 상대적으로 빠르게 단축되었다.

620nm에서 10ps 이내로 작동이 가능하다.

**120nm 일 때** *tr* **= 58.51ps,** *tf* **= 50.3ps**

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image12.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image12.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image13.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image13.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image14.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image14.bmp)

![HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image15.bmp](HW7%20e4a4dcb4f24443b8a9aaa2e049b3a8fe/image15.bmp)

*t*

*r*

, tfall을

*t*

*f*

라고 가정시 >

**520nm 일 때** *tr* **= 18.768ps,** *tf* **= 15.763ps**

**1350nm 일 때** *tr* **= 10ps,** *tf* **= 8.85ps**

**1200nm 일 때** *tr* **= 10.52ps,** *tf* **= 9.41ps**

*tf* 은 *tr* 에 비해 상대적으로 빠르게 단축되었다.

처음 120nm를 기준으로 시작한거에 비하면 엄청나게 Width 가 커졌다.

1350nm에서 10ps 이내로 작동이 가능하다.

IC 소자에서 Dynamic Power 소모가 커지고, 집적도 측면에서 불리할 것으로 판단된다.