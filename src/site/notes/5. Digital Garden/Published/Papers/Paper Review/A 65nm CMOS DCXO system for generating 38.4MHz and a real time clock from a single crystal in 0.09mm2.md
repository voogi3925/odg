---
{"dg-publish":true,"permalink":"/5-digital-garden/published/papers/paper-review/a-65nm-cmos-dcxo-system-for-generating-38-4-m-hz-and-a-real-time-clock-from-a-single-crystal-in-0-09mm2/","tags":["DCXO","RTC","low_power_XO","mobile_device_clock_generation","CMIC","paper_review"],"created":"2025-09-11T13:46:29.524+09:00"}
---

--- 
- Motivation & Thought: 
	- 첨언/특이한 점/추가로 찾아볼 점:
		- Mobile의 경우와 IoT의 경우 각각의 application에 대해 이해하기 위해서 더 많은, 일반적인 work들을 읽어볼 필요가 있다.
			- 이 경우는 mobile device이기에 가능한게 아닌가? 라는 생각이 듦.
		- Q) 내가 만들고자 하는 system에서도 1171.875배 차이 (38.4MHz and 32.768kHz)를 만들 수 있을까?
- Summary: 
	- <mark style="background: #FFB86CA6;">하고자 한 바 (1문장으로)</mark>
		- 통신을 위한 PLL reference clock과 wkae-up timing을 위한 reference clock 모두를 만들고자 하였으며, 이는 평소에는 high-power mode로 DCXO를 38.4MHz 동작시키고 wake-up timer는 동일 XO를 analog하게 low VDD, low-power로 동작+dividing으로 32.76kHz 출력을 만들게 하여 달성함.
	- <mark style="background: #FFB86CA6;">왜 쓰여진 논문인가.</mark>
		- Target Application/문제 상황: 
			- Cellular phone에는 RTC (Real-time clock)가 필요. 이는 핸드폰이 booting될 때 바로 켜져서 동작함. => Always on 상태로 동작하므로 low power consumption이 무척 중요함.
				- 32.768kHz의 RTC를 그냥 XTAL을 사용해서 만든다면 cost + PCB area가 소모됨.
				- =>해당 work은 32.768kHz의 주파수를 38.4MHz DCXO output을 dividing 시켜서 만듦.
	- <mark style="background: #FFB86CA6;">어떻게 해결했지.</mark>
		- Main Idea/제안점: 
			- Digital 하게 XTAL의 load를 조정하기 위해서 Coarse Frequency Adjust (CFA) array & Fome Frequnecy Adjust (FFA) array 2개를 만듬
				- CFA는 6 bit binary weighted로 1 time factory calibration
					- 107ppm tuning
				- FFA는 thermometer coded array로 two-dimensional matrix로 480 unit cell과 64 half size cell로 구성 + DSM
					- Unit cell당 130-200ppb 주파수 tuning 가능
					- DSM으로 2ppb까지 trim 가능
					- 173ppm tuning
			- Peak detector 를 SAR ADC로 conversion한 값 vs oscilalting하는 voltage replica를 SAR ADC로 conversion한 값을 비교하여 oscillator amplitude를 얻음. => 이걸로 amplitude control loop을 돌림.
			- RTC는 DCXO를 analog하게 동작시켜서 얻음
				- LDO 자체도 10% 정도의 low-power로 설정
				- XTAL도 20%의 current로 동작
				- Fractional dividing해서 32.768kHz를 만듦.
				- DCXO가 켜질 때 seamless하게 analog하게 동작하던 XO가 digital operation으로 넘어감.
	- <mark style="background: #FFB86CA6;">해결 결과는.</mark>
		- 좋아진 점/수치적으로:
			- key-parameters:, power, FoM...?, tuning range, step size, die area
				- Power: 9mW w/ LDO and analog output buffer
				- Tuning range: 280ppm w/ step size of 2ppb
				- Die area: 0.09mm^2
		- Trade-off: 
			- 

Circuit:
- ![Pasted image 20250723184247.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250723184247.png)
- ![Pasted image 20250723184304.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250723184304.png)
- ![Pasted image 20250723184320.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250723184320.png)



---
