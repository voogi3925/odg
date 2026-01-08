---
{"dg-publish":true,"permalink":"/5-digital-garden/b4-publish/crystal-less-clock-generation-and-calibration-for-passive-ble-tag-chips-in-io-t-applications/","tags":["relaxation_oscillator","IoT","clock_generation","calibration","passive_BLE","BLE"],"created":"2026-01-08T21:14:14.702+09:00"}
---

--- 
- Motivation & Thought: 
	- 첨언/특이한 점/추가로 찾아볼 점:
		- 페이퍼가 회로적으로 특이한 부분은 없었으나 application 적으로는 실험까지 마친 부분에서 참고할 가치가 충분함.
		- 외부에서 data로 넣어준 신호를 CDR로 clock으로 만드는게 아님에도 불구하고 굳이 CPPLL을 쓴 이유를 모르겠음. => 그냥 FLL 구조로 구현하는게 더 간단하지 않았을까 싶음.
		- ULP와 high precision 조건을 논문에 맞춘 느낌.
			- ULP 조건이 <3uW & high precision이 $< \pm 4000 ppm$ 로 제안함
- Summary: 
	- <mark style="background: #FFB86CA6;">하고자 한 바 (1문장으로)</mark>
		- Passive BLE를 위해서 low power, small size (w/o XTAL), accurate enough한 clock을 만들고자 통신을 위해 (for backscattering) 외부로부터 받은 신호를 demodulation하여 reference로 삼아 on-chip clock을 calibration 하였다.
	- <mark style="background: #FFB86CA6;">왜 쓰여진 논문인가.</mark>
		- Target Application/문제 상황: 
			- Passvie BLE는 backscatter 통신을 하기에 low cost, low power, w/o crystal 구현이 가능하다.
			- 하지만 BLE protocaol과 호환을 위해서는 <1000ppm의 data rate tolerance (4000ppm 이하의 deviation from empirical studies)를 요구한다.
			- 기존 work은,
				- clock deviation이 너무 크거나, power overhead, XTAl을 필요로 하는 문제가 있었다.
	- <mark style="background: #FFB86CA6;">어떻게 해결했지.</mark>
		- Main Idea/제안점: 
			- RX oscillator + CPPLL로 2MHz를 <1.6uW로 달성함. (noise 조건보다 power 조건이 더 까다롭기에 가능한 접근)
				- RxO = Current controlled oscillator (w/ digital IDAC calibration), 저항 대신에 Vref 사용, comparator에 chopper 사용
			- Digital IDAC calibration
				- cal. stability를 위해서 counter를 power-on 시에만 초기화함...?
				- 반대로 cal. ouptut이 제대로 나오지 않는/비교되지 않는 상황을 막기 위한 judge cell 추가
	- <mark style="background: #FFB86CA6;">해결 결과는.</mark>
		- 좋아진 점/수치적으로:
			- key-parameters: power, accuracy, area, frequency, calibration speed/BW(?)
				- Oscillator
					- 20-ppm temperature drift (Temp. range 정보가 없음)
					- 125kHz & 458nW => 0.79nW/kHz
				- 4번의 통신 pulse 만에 calibration 완료

Circuit:
- ![Pasted image 20260108213855.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260108213855.png)
- ![Pasted image 20260108213912.png](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020260108213912.png)

---
