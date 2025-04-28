---
{"dg-publish":true,"permalink":"/5-digital-garden/published/papers/papers-list-pll-fll-basic/","created":"2025-04-28T19:56:57.869+09:00"}
---


# Papers List - PLL FLL Basic

> 작성일: 2025-04-28

----
## Purpose of the post
- PLL/FLL의 loop analysis에 관한 기본을 안다.
- PLL/FLL의 특성을 이용하는 여러 application들을 이해한다.


----
## Loop Analysis
- A Low Noise Sub-Sampling PLL in Which Divider Noise is Eliminated and PD/CP Noise is Not Multiplied by $N^{2}$
	- 2009, JSSC
	- Xiang Gao & Bram Nauta
	- 목적
		- Sub-sampling PLL에 관한 내용 자체에 대해 안다.
		- 기존의 PFD에서 Sampling PFD로 변화하면서 transfer function이 어떻게 변화하였는지 이해한다.
		- PLL의 loop modeling에 대해 안다.

- A 32-MHz, 34-μW Temperature-Compensated RC Oscillator Using Pulse Density Modulated Resistors
	- 2022, JSSC
	- Amr Khashaba & Pavan Kumar Hanumolu
	- 목적
		- Temperature Compensation된 FLL의 동작에 대해 안다.
		- 어떤 식으로 온도에 따라 frequency를 보상하는지 이해한다.
		- FLL의 loop modeling에 대해 안다.

----------------
## 다양한 Application 
- 아래의 사항들을 유념하며 읽어보자.
	- 왜 쓰여진 논문인가? 논문의 핵심 질문이 뭐지?
	- 어떤 방법으로 해결하였지?
	- 해당 방법으로 얼마나 수치적으로 향상되었지?
	- 다른 previous work들과 비교하면 어떻지?
- Realtime clock generation
	- 5.8 A 4.7nW 13.8ppm/°C self-biased wakeup timer using a switched-resistor scheme
		- 2016, ISSCC
		- Taekwang Jang & Dennis Sylvester
- Temperature sensor
	- A 0.9-V 6400-μm2 Resistor-Based Temperature Sensor With a One-Point Trimmed 3σ Inaccuracy of ±0.64 ◦C from −50 ◦C to 125 ◦C
		- 2023, TCAS-2
		- Yongtae Lee & Youngcheol Chae

---------------------------------
- 그 후에는.... ISSCC 2025 PLL/FLL이 내용적으로 쓰인 work들 전부 리뷰하자.