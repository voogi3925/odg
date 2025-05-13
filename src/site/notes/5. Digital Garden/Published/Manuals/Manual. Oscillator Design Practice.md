---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-oscillator-design-practice/","created":"2025-05-11T14:57:48.114+09:00"}
---


# Manual. Oscillator Design Practice

> 작성일: 2025-05-11

----
## Purpose of the post
- Oscillator의 design spec.을 이해하고, Cadence 상에서 시뮬레이션을 돌려 확인 할 수 있다.
- Virtuoso 툴이 시뮬레이션 결과에 주는 영향을 안다/이해한다.

- [[5. Digital Garden/Published/Manuals/Manual. FoM of Osc.\|Manual. FoM of Osc.]]

--------------------
## Design Example
- Ring oscillator target
	- $f_{o} \approx 1GHz$
	- Power < 1mW & VDD = 1.8V
	- $FoM_{osc} > 161dBc/Hz \;when\;\Delta f=100MHz$
- LC oscillator: -188dBc/Hz


------------------
## Further Questions
- Q1) Ring oscillator의 1/f corner가 10MHz라 가정해보자. 그렇다면 10MHz 보다 큰 주파수 대역에서 FoMosc는 왜 평평한가? 반대로 10MHz보다 작은 주파수 대역에서는 주파수가 10배 감소하면 ($\Delta f \rightarrow 0.1\cdot \Delta f$) FoMosc는 몇 dB 변화하겠는가? 왜 그렇게 변화하는가?
- Q2) 

--------------
## Understanding simulator
- 

## 
- RC oscillator: -163dBc/Hz

- Osc. 설계
	- Ring 
	- RC <= Prof. 정협리 
	- LC <= Review. [Phase noise suppression in LC oscillators: Tutorial](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cta.3097)
	- Phase noise jitter power start up 
- Jitter 정의
	- Cycle-to-cycle jitter
	- period jitter
	- rms jitter