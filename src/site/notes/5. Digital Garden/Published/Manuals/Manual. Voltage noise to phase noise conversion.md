---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-voltage-noise-to-phase-noise-conversion/","tags":["phase_noise","voltage_noise","oscillator"],"created":"2025-09-11T13:46:44.353+09:00"}
---


# Manual. Voltage noise to phase noise conversion

> 작성일: 2025-04-07

----
## Purpose of the post
본 글은 간단한 시뮬레이션을 통해 voltage noise가 어떻게 phase noise로 변환되는지 확인해보고자 작성하였다.


---------
## Simulation Setting
### Testbench
![Pasted image 20250407104522.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407104522.png)
- idc Current source는 thermal noise를 넣어주는 용도로 추가하였다. 아래와 같이 설정한다.
	- Number of noise/freq pairs: 1
	- Freq 1: 1e6
	- Noise 1: 2e-15
	- DC current: 0
- vdc
	- 500mV
- vcvs
	- gain: 1
- ahdLib의 vcd cell
	- amp: 1
	- center_freq: 25e6
	- vco_gain: -KVCO
- resistor(우측 끝)
	- r: 1n (작게 해야 simulation이 converge가 잘 되었다.)


---------
### ADE L Setting
![Pasted image 20250407105001.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407105001.png)
- 세부적인 analyses의 세팅
![Pasted image 20250407105158.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407105158.png)
- pnoise는 fo/2까지만 유의미한 값이지만 일단 저렇게 세팅한다.

---------
## Simulation Result
- pnoise 결과를 같이 plot한다.
![Pasted image 20250407105400.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407105400.png)
- voltage noise의 PSD와 함께 plot하면 아래와 같이 얻을 수 있다.
![Pasted image 20250407105610.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407105610.png)

---------
### Practice
- Q1) VCO_IN node의 voltage noise PSD는 어떻게 VCO_OUT1 node의 phase noise로 수식적으로 변환할 수 있는가?

- Q2) 그렇다면 Calculator를 이용하여 VCO_IN node의 값을 VCO_OUT1 node의 phase noise로 변환할 수 있는가?

- Hints
	- Calculator에서 VAR 함수를 사용하면 design variable을 이용하여 수식을 세울 수 있다.
		- ex) $K_{VCO}^{2} \Rightarrow VAR("KVCO")**2)$
	- Calculator에서 xval 함수를 사용하면 원래 data의 x축 값을 뽑을 수 있다.
		- ex) xval(VN2("어쩌구저쩌구 결과")) $\Rightarrow$ VN2()의 x축에 해당하는 값인 frequency 정보를 calculator에 넣을 수 있음.

---------
### Solution
- A1)
	- $S_{v}=2f \; [V^{2}/Hz]$ (f: femto)
	- $S_{f}=K_{VCO}^{2} f_{v} \; [Hz^{2}/Hz]$
	- $S_{\phi}=\frac{S_{f}}{f^{2}}\; [rad^{2}/Hz]$
	- $PN=10\cdot log_{10}(\frac{S_{\phi}(f)}{2})\; [dBc/Hz]$
- A2) 
	- $10*log10(VN2(something)*VAR("KVCO")**2/(xval(VN2(something))**2)/2)$
	- 축이 다르기에 달라 보일 수 있음 $\Rightarrow$ 축 값을 수정하면 딱 맞는다.
	- 앞에서 언급했듯이 oscillating freq.인 10MHz의 절반 5MHz를 넘어서부터는 의미가 없는 phase noise 값이 나온다.
![Pasted image 20250407123922.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250407123922.png)


---------
### TOGO
- Q) 만약 VCO의 input으로 flicker noise와 thermal noise가 동시에 들어간다면 phase noise가 어떻게 integration될까?

---------
## References
- 1998 JSSC, [[A general theory of phase noise\|A general theory of phase noise]] - Ali Hajimiri
- 1999 JSSC, [[1. 임시 메모/Summary-임시/Jitter and Phase Noise in Ring Oscillator\|Jitter and Phase Noise in Ring Oscillator]] - Ali Hajimiri