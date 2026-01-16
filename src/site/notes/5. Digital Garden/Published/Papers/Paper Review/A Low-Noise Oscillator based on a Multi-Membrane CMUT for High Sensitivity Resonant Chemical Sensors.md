---
{"dg-publish":true,"permalink":"/5-digital-garden/published/papers/paper-review/a-low-noise-oscillator-based-on-a-multi-membrane-cmut-for-high-sensitivity-resonant-chemical-sensors/","tags":["MEMS","MEMS_resonator","CMUT","Colpitts","resonant_sensor","time_domain"],"created":"2026-01-16T16:27:23.164+09:00"}
---

--- 
- Motivation & Thought: 
	- 첨언/특이한 점/추가로 찾아볼 점:
		- 프로젝트를 진행함에 있어서 CMUT resonator-based oscillator를 설계해야 하여 읽기 시작함.
		- CMUT은 기본적으로 silicon membrane-vacuum-oxide post-silicon substrate으로 구성됨. => AC/DC의 electrostatic force가 capacitor에 가해지면 자체 물성을 결정된 주파수에서 공진하기 시작함. => 이래서 biasing을 해줘야하는구나.
		- <mark style="background: #ADCCFFA6;">고려/기억할 사항</mark>
			- CMUT 자체의 특성으로 한 면은 substarte과 연결되어 있어야 함...! 양쪽 node로 driving할 수 없음
			- 기존에 읽었던 XTAL oscillator의 4-element RLC van Dyke model과는 달리 6-element로 modeling을 해뒀다는 점, Q 값이 200~50 수준으로 비교적 작다는 점에서 차이가 있음.
				- 이는 substarte과 electrode의 parasitic effect에 대한 고려가 같이 되어있음.
			- CMUT resonator를 lossy inductor로 모델링하고 (왜?? 이미 앞에서 6-elements로 모델링을 해뒀으면서 lossy inductor로 분석한 것이지?) Colpitts osc.를 설계함. 이때 1) start-up criteria 2) desired oscillation freq. 3) amp.에 대한 loading을 줄이기 위한 큰 R_biasing 이 고려됨.
		- <mark style="background: #ADCCFFA6;">이해 안되는 점</mark>
			- Q) Biasing (figure 6-a)을 해줄 때 41V, 66V로 biasing을 해줬다는데 이걸 IC에서 구현할 수 가 있나...? 구현해야하나...?
			- Parallelism으로 ESR을 낮춘 것은 알겠고, Series에 비하여 parallel일 때 Q값이 적게 줄어드는 것도 알겠음. 하지만, Q 값 감소 대비 ESR이 얼마나 줄었는지에 대한 이야기가 없어서 해당 방식이 얼마나 좋은지 와닿지 X...
			- TIA-기반 vs Colpitts에서 power: 80mW vs 6mW & Phase noise floor: -130 dBc/Hz vs -148 dBc/Hz 라는데... phase noise floor가 작은게 data conversion하는데 기여를 하나? accumulated jitter 측면에서 봐야하는거 아닌가? thermal floor는 그다지 의미 없어 보임...
- Summary: 
	- <mark style="background: #FFB86CA6;">하고자 한 바 (짧은 문장으로)</mark>
		- CMUT resonator cell들을 병렬로 연결하여 electrically parallel하게 구현하여 motional impedance (ESR)을 줄였음. 이를 통하여 해당 resonator 기반 Colpitts oscillator의 phase noise 성능을 향상 시켜, 센서로 이용하였을 경우 (TIA-based oscillator topology보다) 좋은 resolution 성능을 달성함.
	- <mark style="background: #FFB86CA6;">왜 쓰여진 논문인가.</mark>
		- Target Application/문제 상황: 
			- Micromechnical system에서 resonant sensing은 pressure, acceleration, chemical/biological agents의 측정에 이용됨.
			- Resonator sensor system에서 oscillator의 noise performance는 minimum detectable signal (sensor resolution)의 결정에 직접 연관됨.
				- 이를 위해, 여러 resonator를 series 혹은 parallel로 이용하여 motional resistance를 낮추는 접근이 있었음.
				- 이는 mechanical-coupling을 통해서 주로 진행되었음.
				- Electrically-coupling이 기피된 이유는 resonator-to-resonator Q non-uniformity 때문에 전체 Q 값을 낮추기 때문임. 따라서 아래의 2가지 방향을 달성한다면 electrical-coupling을 사용해도 괜찮음.
					- 1) resonator의 unifomity를 좋게 만듦
					- 2) 하나의 Q만 특별히 더 낮음 (왜지...? 이러면 낮은 쪽 Q에 맞추겠다는 소리인가?)
	- <mark style="background: #FFB86CA6;">어떻게 해결했지.</mark>
		- Main Idea/제안점: 
			- 1000 CMUT w/ electrically connected in parallel => Resolution 향상
				- 1) Massive parallelism (1000개)으로 <100ohm의 motional resistance 달성
				- 2) 분석 결과 series보다 parallel이 동일한 std deviation에 대해서 더 적게 Q 값이 감소하였음. (Figure 5 참조) => parallelism의 장점을 reasonable Q로 챙겼다.
			- MEMS resonator-based oscillator는 transresistance amplifier-based osc.와 single-stage tuned osc. (Pierce, Colpitts)로 나뉨.
				- Transresistance amp.는 R 값으로 open-loop gain이 결정되고 single-stage tuned는 C 값으로 gain이 결정되기에 후자가 noise 측면에서 유리함.
				- CMUT에게는 Colpitts가 Pierce보다 적합함. 왜냐하면,
					- 1) CMUT은 한 쪽 electrode가 ground와 연결되어 있어야만 함.
					- 2) Series resonance 보다 parallel resonace에서 더 높은 Q를 지님.
	- <mark style="background: #FFB86CA6;">해결 결과는.</mark>
		- 좋아진 점/수치적으로:
			- key-parameters: phase noise, power, oscillating freq.
				- 42.7-MHz oscillator: 
					- -105 dBc/Hz at 1kHz offset freq. & -148 dBc/Hz at 1MHz offset freq.
				- 17.5-MHz oscillator: 
					- -97 dBc/Hz at 1kHz offset freq. & -155 dBc/Hz at 1MHz offset freq.
					- Power 80mW(기존 TIA기반) => 6mW & phase noise floor가 19dB 감소
		- Trade-off: 
			- 절대적인 phase noise 측면에서는 그다지 좋지 않음... (Power 소모가 작아졌으니깐)

Circuit:

- ![Pasted image 20260116163124.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116163124.png)  ![Pasted image 20260116165623.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116165623.png)
	- (좌) electrically-coupling한 해당 work. 각 CMUT cell 자체가 연결되어 있지는 않으나 동일하게 voltage가 인가되는 듯.
		- CMUT 자체의 특성으로 한 면은 substarte과 연결되어 있어야 함...! 양쪽 node로 driving할 수 없음
	- (우) mechanically-coupling한 reference (MECHANICALLY CORNER-COUPLED SQUARE MICRORESONATOR ARRAY FOR REDUCED SERIES MOTIONAL RESISTANCE)
- ![Pasted image 20260116163958.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116163958.png)
- ![Pasted image 20260116163146.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116163146.png)
- ![Pasted image 20260116163205.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116163205.png)
- ![Pasted image 20260116163211.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260116163211.png)



---
