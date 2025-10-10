---
{"dg-publish":true,"permalink":"/5-digital-garden/published/papers/paper-review/a-sub-0-5-v-crystal-oscillator-timer-xo-timer-combining-16-m-hz-reference-and-32k-hz-sleep-timer-with-a-single-crystal-for-energy-harvesting-radios-in-28nm-cmos/","tags":["SXDO","ULV","dual_mode_XO"],"created":"2025-10-09T14:08:54.258+09:00"}
---

--- 
- Motivation & Thought: 
	- 첨언/특이한 점/추가로 찾아볼 점:
		- Q) 32.768kHz가 아닌 32.258kHz를 만들고 있음. 아마 16MHz를 dividing 쳐서 만들기에 그런 것 같음. <mark style="background: #ADCCFFA6;">허나 정확한 32.768kHz를 만드는게 얼마나 중요한 토픽</mark>이지?
			- 16MHz + 4개의 async. divider + FF으로 된 div-by-31 cell로 구성됨
		- BLE standard
			- HF XO (16MHz)는 $\pm 50ppm$
			- LF XO (32kHz)는 $\pm 500ppm$
		- Sleep timer로 사용하기 위해서 LPM으로 동작시키는 것은 이미 [[1. 임시 메모/그 외 나머지/Circuit Researchers/Danielle Griffith\|Danielle Griffith]]가 했었음... 하지만 HPM에서는 load cap.을 온전히 전부 붙혀서 PN을 낮추고, LPM에서는 CL을 전부 없애는 것은 확인해둘만 함.
		- <mark style="background: #ADCCFFA6;">Q) XTAL을 fully on 시켜둠에도 불구하고 왜 다른 work들에 비하여 temp. coef.가 클까?</mark>
		- 또한 LPM 상태일 때 nominal freq. 자체에 drift가 생김. 아마 load cap.이 없어져서 저항이나 MOSFET 등이 load로 보일텐데, 이를 trimming 하는 회로를 따로 안 넣었지 않을까 싶음...
- Summary: 
	- <mark style="background: #FFB86CA6;">하고자 한 바 (1문장으로)</mark>
		- Energy harvesting BLE application을 위해서, ULV(0.5V)에서 XTAL을 high power와 low power mode 각각으로 동작 가능케 하면서 동시에 single voltage regulation loop을 power efficiency를 챙김
	- <mark style="background: #FFB86CA6;">왜 쓰여진 논문인가.</mark>
		- Target Application/문제 상황: 
			- Energy harvesting 조건(=ULV 상황)에서 digital cell과 amp.가 동작하려면 DC-DC converter가 필요함.
				- 기존 work은 여러 개의 voltage-regulation loop을 돌렸기에 power-inefficient함.
			- MHz XTAL은 sleep timer로는 power 소모가 너무 큼.
				- LPM과 HPM으로 나누고, HPM은 single gm-cell + load cap., LPM은 3-stage gm-cell + pseudo R로 구현.
					- HPM은 Pierce 처럼 동작.
					- LPM은 negative R을 boost하기 위해서 3-stage gm + 작은 load cap. => power에서 이득 (그래프 참조)
	- <mark style="background: #FFB86CA6;">어떻게 해결했지.</mark>
		- Main Idea/제안점: 
			- 하나의 micro-power management (μPM) cell을 통하여 single loop으로 3개의 supply voltage+Vbias 를 unregulated harvested voltage로 부터 만듦
				- Switched Cap. Voltage Adder (SCVA) & Switched Cap. Voltage Doubler (SCVD)를 이용하여 voltage를 키움.
				- kickstart signal로 시작 => 스스로 만든 supply로 ref. & bias generator를 킴. => 생성된 Vref를 기준으로 loop이 control됨.
				- single regulation loop이라서 power가 기존보다 27.5% 감소 & on-chip 주파수 중심이 아니라 regulating voltage를 기준으로 loop을 잡기에 ripple도 작음
			- high power mode (HPM)와 low power mode(LPM)를 오갈 수 있는 ULV core amp.를 gm efficient하게 설계
				- HPM => freq. stability를 위한 것. 16MHz에서 VT-variation이 생겨도 BLE standard인 $\pm 50ppm$을 유지할 수 있도록 함.
				- LPM => divider를 통해서 32.258kHz를 만듦. $\pm 500ppm$ 성능을 유지함
	- <mark style="background: #FFB86CA6;">해결 결과는.</mark>
		- 좋아진 점/수치적으로:
			- key-parameters:
		- Trade-off: 
			- temperature range: ULV이기에 저온과 고온에서 동작을 보장 못함.
			- sleep timer 주파수: 32.768kHz가 아니라 다른 주파수를 선택함.
			- 다른 온도 보상 방식이 없어서 그런가 temp. dep. variation이 상대적으로 크다.

Circuit:
- ![Pasted image 20251009145414.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020251009145414.png)
- ![Pasted image 20251009145424.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020251009145424.png)
- ![Pasted image 20251009145431.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020251009145431.png)
	- 3-stage gm에서 훨씬 current 대비 neg. R이 커진다.
- ![Pasted image 20251009145903.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020251009145903.png)
- ![Pasted image 20251009145516.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020251009145516.png)


---
