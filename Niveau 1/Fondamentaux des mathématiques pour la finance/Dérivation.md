
# 1. Nombre dérivé et Fonction dérivée

## 1.1 Définition théorique
Soit $f$ une fonction définie sur un intervalle $I$ contenant le réel $a$. 
$f$ est dite **dérivable en $a$** si la limite suivante existe et est un nombre réel :

$$\lim_{h \to 0} \frac{f(a+h) - f(a)}{h} = f'(a)$$

> [!abstract] Interprétation géométrique
> Lorsque $h$ tend vers 0, la droite sécante $(AM)$ tend vers une position limite appelée **tangente** à la courbe $\mathcal{C}_f$ au point $A$. Le nombre dérivé $f'(a)$ correspond au **coefficient directeur** de cette tangente.



## 1.2 Exemple : Fonction carré
Soit $f(x) = x^2$ sur $\mathbb{R}$.
Calcul du taux d'accroissement :
$$\frac{f(a+h) - f(a)}{h} = \frac{(a+h)^2 - a^2}{h} = \frac{a^2 + 2ah + h^2 - a^2}{h} = \frac{2ah + h^2}{h} = 2a + h$$
Or, $\lim_{h \to 0} (2a + h) = 2a$. 
Donc, pour $f(x) = x^2$, on a **$f'(x) = 2x$**.

---

# 2. Formulaire des dérivées usuelles

| Fonction $f(x)$ | Dérivée $f'(x)$ | Domaine |
| :--- | :--- | :--- |
| $k$ (constante) | $0$ | $\mathbb{R}$ |
| $x$ | $1$ | $\mathbb{R}$ |
| $x^n$ | $n x^{n-1}$ | $\mathbb{R}$ |
| $\frac{1}{x}$ | $-\frac{1}{x^2}$ | $\mathbb{R}^*$ |
| $\sqrt{x}$ | $\frac{1}{2\sqrt{x}}$ | $]0, +\infty[$ |



---

# 3. Opérations sur les dérivées

Soient $u$ et $v$ deux fonctions dérivables sur $I$ et $k$ un réel :

| Opération | Formule |
| :--- | :--- |
| **Somme** | $(u + v)' = u' + v'$ |
| **Produit par un scalaire** | $(ku)' = k u'$ |
| **Produit** | $(uv)' = u'v + uv'$ |
| **Inverse** | $\left(\frac{1}{v}\right)' = -\frac{v'}{v^2}$ |
| **Quotient** | $\left(\frac{u}{v}\right)' = \frac{u'v - uv'}{v^2}$ |

---

# 4. Équation de la tangente

L'équation de la tangente $T$ à la courbe de $f$ au point d'abscisse $a$ est donnée par :

> [!important] Formule à retenir
> $$y = f'(a)(x - a) + f(a)$$

### Exemple d'application
Soit $f(x) = x^2 - 3x + 1$ au point d'abscisse $a = 2$.
1. **Image :** $f(2) = 2^2 - 3(2) + 1 = 4 - 6 + 1 = -1$
2. **Dérivée :** $f'(x) = 2x - 3$
3. **Pente :** $f'(2) = 2(2) - 3 = 1$
4. **Équation :** $y = 1(x - 2) + (-1) \implies \mathbf{y = x - 3}$

---

# 5. Exercices de mise à niveau

Calculez la dérivée $f'(x)$ pour :
1. $f(x) = x^3 + 5x - 4$
2. $f(x) = \frac{2x - 1}{x + 3}$ (Indice : utiliser $\frac{u}{v}$)
3. $f(x) = x \sqrt{x}$ (Indice : utiliser $uv$)