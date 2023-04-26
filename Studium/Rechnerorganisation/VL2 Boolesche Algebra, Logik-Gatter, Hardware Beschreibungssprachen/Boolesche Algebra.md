---
tags: Uni RO
VL-Date: 19.04.23
---
# Boolesche Algebra

### 3 Tupel $(A, +, \cdot )$ 
- A: Menge
- $+, \cdot$: Abbildung aus $A \times A \rightarrow A$
- spezielle Elemente $1, 0 \in A$ erfüllen Axiome der neutralen Elemente
- für jedes $x \in A$ gibt es ein $\overline{x}$ das Axiome des inversen Elements erfüllt
### Axiome
| Kommutativgesetze | Distributivgesetze    | neutrale Elemente | inverse Elemente   |
| ----------------- | --------------------- | ----------------- | ------------------ |
| $x * y = y * x$   | $x*(y+z)=(x*y)+(x*z)$ | $x*1=x$           | $x*\overline{x}=0$ |
| $x+y=y+x$         | $x+(y*z)=(x+y)*(x+z)$ | $x+0=x$           | $x+\overline{x}=1$                   |

## Schaltalgebra vs Mengenalgebra

In dieser Vorlesung behandeln wir ausschließlich die Schaltalgebra

## Theoreme
| Elemination | Absorption  | Assoziativitgesetz | Idempotenz | Doppelnegation                  | DeMorgan                                       |
| ----------- | ----------- | ------------------ | ---------- | ------------------------------- | ---------------------------------------------- |
| $x*0=0$     | $x*(x+y)=x$ | $(x*y)*z=x*(y*z)$  | $x*x=x$    | $\overline{(\overline{x})} = x$ | $\overline{(x+y)}=(\overline{x}*\overline{y})$ |
| $x+1=1$     | $x+(x*y)=x$ | $(x+y)+z=x+(y+z)$  | $x+x=x$    |     -                            | $\overline{(x*y)}=(\overline{x}+\overline{y})$                                               |


