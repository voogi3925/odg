---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-fo-m-of-osc/","created":"2025-09-11T13:47:04.949+09:00"}
---


# Untitled

> 작성일: 2025-05-12

----
## Purpose of the post
- Oscillator의 FoM을 이해한다.


---
### FoM1
- Operation freq, offset freq., PN, power만을 고려.
- PN와 power dissipation은 작을수록 좋다.
- 동일한 PN를 지닌다면(*operation이나 offset freq.에 따라 PN가 달라짐* ), 높은 operation freq.($f_{o}$)일수록 동일한 offset freq.($\Delta f$)에서 그 크기의 PN를 지니기 어렵다.
- 클수록 좋다
$$
FoM1=-L(\Delta f)+20log(\frac{f_{o}}{\Delta f})-10log(\frac{P_{DC}}{1mW})
$$

---
### FoM2
- FoM1에서 TR(Tunning Range)을 % 단위로 고려할 경우.
$$
FoM2=-L(\Delta f)+20log((\frac{f_{o}}{\Delta f})(\frac{TR(\%)}{10}))-10log(\frac{P_{DC}}{1mW})
$$

---
### FoM3
- $1/f^3$ 영역 에서의 osc. performance에 대한 지표이다.
- $f_{m}$은 carrier 로부터의 freq. offset으로 대개 10 KHz보다 작다.
$$
FoM3=-L(\Delta f)+20log((\frac{f_{o}}{f_{m}^{1.5}})(\frac{TR(\%)}{10}))-10log(\frac{P_{DC}}{1mW})
$$

---
### FoM4
- Tank의 Q factor를 제외하고 osc. core만의 performance를 보여준다.
- FoMmax 는 tank의 thermal noise만이 PN에 영향을 끼친다 가정하므로 FoMmax - FoM1을 통해 얻어낼 수 있다.

$$
FoM4=[176.8+20log_{10}Q]-FoM_{1}
$$
---
