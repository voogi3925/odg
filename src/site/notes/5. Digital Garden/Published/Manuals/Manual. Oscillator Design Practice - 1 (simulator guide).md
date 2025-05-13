---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-oscillator-design-practice-1-simulator-guide/","created":"2025-05-11T14:57:48.114+09:00"}
---


# Manual. Oscillator Design Practice - 1 (simulator guide)

> 작성일: 2025-05-11

----
## Purpose of the post
- Oscillator의 design spec.을 이해하고, Cadence 상에서 시뮬레이션을 돌려 확인 할 수 있다.
	- [[5. Digital Garden/Published/Manuals/Manual. FoM of Osc.\|Manual. FoM of Osc.]]
- Virtuoso 툴이 시뮬레이션 결과에 주는 영향을 안다/이해한다.
	- liberate, moderate, conservative 옵션을 안다.
	- Simulator option 중 tolerance와 gmin을 수정하여 simulator의 accuracy를 조정할 수 있다.
	- High performance simulation 중 APS simulation을 이용할 수 있다.



--------------------
## Design Example

- 해당 예제에서 phase noise 분석 방법:
	- vcvs와 같은 ideal buffer를 통하여 oscillating 하는 output node를 뽑아내어, 해당 노드의 phase noise를 살펴본다.
### Ring oscillator target
- $f_{o} \approx 1GHz$
- Power < 1mW & VDD = 1.8V
- $FoM_{osc} > 161dBc/Hz \;when\;\Delta f=100MHz$

### LC oscillator target
- $f_{o} \approx 2.4GHz$
- Power < 10mW & VDD = 1.8V
- $PN < -108 \;when\;\Delta f=1MHz$ & $PN < -131 \;when\;\Delta f=25MHz$
- $FoM_{osc} > 180dBc/Hz \;when\;\Delta f=1MHz$
- Inductor는 아래의 스펙으로 이용
	- ![Pasted image 20250513142055.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250513142055.png)



--------------
## Understanding simulator

- 앞서 설계한 ring oscillator를 기반으로 진행한다.

### Simulator option - transient simulation
- Transient simulation을 liberate, moderate, conservative 각 옵션으로 돌리고 average frequency & power & FoM을 비교하자.

### Simulator option result  - transient simulation

| option      | liberate      | moderate      | conservative  |
| ----------- | ------------- | ------------- | ------------- |
| AVG freq.   | 1.040GHz      | 1.051GHz      | 1.052GHz      |
| AVG Current | 813.76uA      | 817.54uA      | 817.122uA     |
| PN @10MHz   | -118.93dBc/Hz | -118.93dBc/Hz | -118.93dBc/Hz |
| FoM @10MHz  | 157.616dBc/Hz | 157.688dBc/Hz | 157.695dBc/Hz |

### Simulator option - tolerance setting
- Simulator의 option을 변경하여 tolerance와 gmin을 1/10 씩만 낮춰서 시뮬레이션을 돌려보자.
	- ![Pasted image 20250513151948.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250513151948.png)
	- Main 창에서 reltol, vabstol, iabstol & Algorithm 창에서 gmin 값을 전부 1/10 씩 줄인다.
	- <mark style="background: #FFB86CA6;">자칫 시뮬레이션의 용량이 과도하게 커질 수 있으니 allpub이 아닌지 확인하고 시뮬 돌린다.</mark>
	- 시뮬레이션 시간, 결과를 비교해보자.

### Simulator option result - tolerance setting

| option      | conservative - nominal | conservative - 1/10 tolerance |
| ----------- | ---------------------- | ----------------------------- |
| AVG freq.   | 1.052GHz               | 1.0534GHz                     |
| AVG Current | 817.122uA              | 817.28uA                      |
| PN @10MHz   | -118.93dBc/Hz          | -118.93dBc/Hz                 |
| FoM @10MHz  | 157.695dBc/Hz          | 157.707dBc/Hz                 |


### Simulator option - Spectre APS simulator
- APS simulator setting 
	- ![Pasted image 20250513154329.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250513154329.png)
	- Multi-threading의 경우, 크기가 작은 cell은 시뮬레이터가 코어를 1개만 할당하기에 실제로 적용되지 않으며, 또 크기가 작은 cell은 병렬화로 인한 연산 코스트가 존재하기에 multi-threading으로 인한 속도 차이가 크지 않다.
	- Auto로 multi-thread 개수를 설정하면 지나치게 서버의 코어를 많이 쓸 수 있으니 manual하게 이용하자.
	- ![Pasted image 20250513154344.png|center](/img/user/0.%20TOOLS/00.%20Attechments/Pasted%20image%2020250513154344.png)
### Simulator option result - Spectre APS simulator

| option      | conservative - nominal | conservative - 1/10 tolerance | conservative - ++aps |
| ----------- | ---------------------- | ----------------------------- | -------------------- |
| AVG freq.   | 1.052GHz               | 1.0534GHz                     | 1.0632GHz            |
| AVG Current | 817.122uA              | 817.28uA                      | 817.92uA             |
| PN @10MHz   | -118.93dBc/Hz          | -118.93dBc/Hz                 | -119.15dBc/Hz        |
| FoM @10MHz  | 157.695dBc/Hz          | 157.707dBc/Hz                 | 158.0dBc/Hz          |


-------------------------------
## Questions
- Q1) Ring oscillator의 1/f corner가 10MHz라 가정해보자. 그렇다면 10MHz 보다 큰 주파수 대역에서 FoMosc는 왜 평평한가? 반대로 10MHz보다 작은 주파수 대역에서는 주파수가 10배 감소하면 ($\Delta f \rightarrow 0.1\cdot \Delta f$) FoMosc는 몇 dB 변화하겠는가? 왜 그렇게 변화하는가?
- Q2) Off-chip inductor를 이용한다면 어떤 요소가 설계에서 고려되어야 하는가?
- Q3) 어떤 회로를 시뮬레이션 할 때 tolerance를 낮춰서 더 정확하게 시뮬레이션을 돌려야 하는가?
- Q4) aps를 썼을 때와 안 썼을 때 성능에 차이가 존재한다. 그렇다면 어떤 결과를 golden reference로 삼을 수 있는가? 아니면 golden reference의 의미가 없는가?

### Example directory
- Nas 상의 개인 디렉토리 중 ..../t180/40k_tsmc18/2410_TEST/TB_FOMOSC_LC 와 ..../t180/40k_tsmc18/2410_TEST/TB_FOMOSC_RING

### Appendix
- LC oscillator tutorial paper
	- [Phase noise suppression in LC oscillators: Tutorial](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cta.3097)

