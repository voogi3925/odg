---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-oscillator-design-practice/","created":"2025-05-11T14:57:48.114+09:00"}
---


# Manual. Oscillator Design Practice

> 작성일: 2025-05-11

----
## Purpose of the post
- Oscillator의 design spec.을 이해하고, Cadence 상에서 시뮬레이션을 돌려 확인 할 수 있다.
- 

--------------------
## 
- Ring oscillator:
	- $f_{o}$
	- FoMosc: -155dBc/Hz
	- 
- RC oscillator: -163dBc/Hz
- LC oscillator: -188dBc/Hz



- Osc. 설계
	- Ring 
	- RC <= Prof. 정협리 
	- LC <= Review. [Phase noise suppression in LC oscillators: Tutorial](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cta.3097)
	- Phase noise jitter power start up 
- Jitter 정의
	- Cycle-to-cycle jitter
	- period jitter
	- rms jitter