# 1 - Primitives

> [!abstract] Définition
> On dit que la fonction $F$ est une **primitive** de la fonction $f$ sur l’intervalle $I$ si $F$ est dérivable sur $I$ et si pour tout $x \in I$ :
> $$F'(x) = f(x)$$

### Exemples
1. La fonction $F : x \mapsto \frac{x^3}{3} + 2x$ est une primitive de $f : x \mapsto x^2 + 2$ sur $\mathbb{R}$.
2. La fonction $F : x \mapsto \ln(x)$ est une primitive de $f : x \mapsto \frac{1}{x}$ sur $\mathbb{R}_{+}^{*}$.
3. La fonction $F : x \mapsto e^x + 5x - 7$ est une primitive de $f : x \mapsto e^x + 5$ sur $\mathbb{R}$.

### Théorème : Existence de primitives
Toute fonction $f$ **continue** sur un intervalle $I$ possède au moins une primitive $F$ sur $I$. Ce théorème peut être prolongé : toute fonction continue par morceaux sur un intervalle $I$ admet au moins une primitive.

### Proposition : Primitives d'une fonction continue sur I
Soit $f$ une fonction continue sur un intervalle $I$ :
- Si $F$ est une primitive de $f$ sur $I$, alors l’ensemble des primitives de $f$ sur $I$ est l’ensemble des fonctions de la forme :
  $$x \mapsto F(x) + k \quad \text{où } k \in \mathbb{R}$$
- Soient $a$ et $b$ deux nombres réels. Alors, il existe une **unique** primitive $F$ de $f$ telle que $F(a) = b$.

> [!example] Exemple
> Déterminer une fonction $G$, définie sur $\mathbb{R}^*$, dérivable sur $\mathbb{R}^*_+$ et $\mathbb{R}^*_-$, telle que $G(1) = 3$, $G(-2) = 1$ et pour tout $x \in \mathbb{R}^*$, $G'(x) = \frac{1}{x^2}$.

### Proposition
Soient $I$ un intervalle et $f : I \to \mathbb{R}$ une fonction continue. Soient $a, b \in I$.
Soit $F_1$ et $F_2$ deux primitives de $f$. Alors $F_1(b) - F_1(a) = F_2(b) - F_2(a)$.

---

# 2 - Définitions de l’intégrale

## 2.1 - Intégrale d’une fonction positive (Aire sous la courbe)

> [!info] Définition
> Soit $f : I \to \mathbb{R}$ une fonction continue et positive ($f(x) \ge 0$).
> Soient $a, b \in I$ avec $a \le b$. On définit l’**intégrale de f entre a et b**, notée
> $$\int_{a}^{b} f(x)dx$$
> comme l’aire de la surface délimitée par les droites d’équation $x = a$, $x = b$, l’axe des abscisses et la courbe de $f$.



### Sommes de Riemann
Soit une fonction $f$ continue sur $[a, b]$ et un entier naturel $n$ non nul. On appelle sommes de Riemann associées à $f$ sur $[a, b]$ :
- $S_n = \frac{b - a}{n} \sum_{k=1}^{n} f\left(a + k \frac{b - a}{n}\right)$
- $T_n = \frac{b - a}{n} \sum_{k=0}^{n-1} f\left(a + k \frac{b - a}{n}\right)$

**Théorème :** Les suites $(S_n)_{n \in \mathbb{N}^*}$ et $(T_n)_{n \in \mathbb{N}^*}$ convergent vers $\int_{a}^{b} f(x)dx$.



### Cas particulier
Si $f$ est une fonction continue sur $[0, 1]$, alors :
$$\lim_{n \to +\infty} \frac{1}{n} \sum_{k=0}^{n-1} f\left(\frac{k}{n}\right) = \lim_{n \to +\infty} \frac{1}{n} \sum_{k=1}^{n} f\left(\frac{k}{n}\right) = \int_{0}^{1} f(t)dt$$

> [!tip] Remarques
> - **Variable muette :** $x$ est une variable muette. On peut écrire $\int_{a}^{b} f(x)dx = \int_{a}^{b} f(t)dt$.
> - **Relation nulle :** $\int_{a}^{a} f(t)dt = 0$.
> - **Inversion des bornes :** Si $a > b$, on pose $\int_{a}^{b} f(t)dt = -\int_{b}^{a} f(t)dt$.

---

## 2.2 - Intégrale d’une fonction continue et primitives

> [!abstract] Définition
> Soient $I$ un intervalle et $f : I \to \mathbb{R}$ une fonction continue. Soient $a, b \in I$.
> L'intégrale de $f$ entre $a$ et $b$ est le réel :
> $$\int_{a}^{b} f(x)dx = F(b) - F(a)$$
> où $F$ est une primitive quelconque de $f$ sur $I$.

### Notation
On utilise la notation crochet pour le calcul :
$$[g]_a^b = g(b) - g(a)$$
D'où :
$$\int_{a}^{b} f(x)dx = [F(x)]_a^b$$

### Exemples de calcul
1. $\int_{0}^{1} x dx = \left[\frac{x^2}{2}\right]_0^1 = \frac{1}{2} - 0 = \frac{1}{2}$
2. $\int_{1/2}^{1} \frac{1}{t^2} dt$
3. $\int_{-1}^{1} x^3 dx$

---

### Propriété : Relation de Chasles
Soient $I$ un intervalle, $f : I \to \mathbb{R}$ une fonction continue, et $(a, b, c) \in I^3$ :
$$\int_{a}^{c} f(x)dx = \int_{a}^{b} f(x)dx + \int_{b}^{c} f(x)dx$$

### Proposition
Soit $f : [a, b] \to \mathbb{R}$ une fonction continue. Alors, la fonction $F$ définie sur $[a, b]$ par :
$$F(x) = \int_{a}^{x} f(t)dt$$
est dérivable sur $]a, b[$ et, pour tout $x \in ]a, b[$, $F'(x) = f(x)$.
## 2.2 - Intégrale d’une fonction continue et primitives

> [!abstract] Définition
> Soient $I$ un intervalle et $f : I \to \mathbb{R}$ une fonction continue. Soient $a, b \in I$. 
> On appelle **intégrale de $f$ entre $a$ et $b$**, le réel :
> $$\int_{a}^{b} f(x)dx = F(b) - F(a)$$
> où $F$ est une primitive quelconque de $f$ sur $I$.

### Notation
Pour toute fonction $g : [a, b] \to \mathbb{R}$, on pose la notation des crochets :
$$[g]_{a}^{b} = g(b) - g(a)$$
On écrira donc :
$$\int_{a}^{b} f(x)dx = [F(x)]_{a}^{b}$$

> [!example] Exemple de calcul simple
> $$\int_{0}^{1} x dx = \left[ \frac{x^2}{2} \right]_{0}^{1} = \frac{1^2}{2} - \frac{0^2}{2} = \frac{1}{2}$$

---

# 3 - Quelques propriétés de l’intégrale

## 3.1 - Linéarité de l’intégrale
L'intégration, comme la dérivation, est une opération linéaire.

> [!important] Proposition : Linéarité
> Soient $f, g$ deux fonctions continues sur $I$ et $\lambda \in \mathbb{R}$ :
> 1. $\int_{a}^{b} (f(x) + g(x))dx = \int_{a}^{b} f(x)dx + \int_{a}^{b} g(x)dx$
> 2. $\int_{a}^{b} \lambda f(x)dx = \lambda \int_{a}^{b} f(x)dx$

## 3.2 - Positivité de l’intégrale

> [!info] Proposition : Positivité
> Soit $f$ une fonction continue et **positive** ($f \ge 0$) sur $I$. 
> Pour tout $a, b \in I$ avec $a \le b$ :
> $$\int_{a}^{b} f(t)dt \ge 0$$

### Corollaires
- **Ordre :** Si $f(x) \ge g(x)$, alors $\int_{a}^{b} f(t)dt \ge \int_{a}^{b} g(t)dt$.
- **Intégrale nulle :** Pour $a \le b$, $\int_{a}^{b} |f(t)|dt = 0 \iff \forall x \in [a, b], f(x) = 0$.

---

# 4 - Comment calculer les intégrales

## 4.1 - Catalogue des primitives usuelles
Pour trouver une primitive, on lit généralement le tableau des dérivées à l'envers. $c$ désigne la constante d'intégration (souvent prise égale à 0 pour les calculs d'intégrales).

| Fonction $f(x)$ | Intervalle | Primitives $F(x)$ |
| :--- | :--- | :--- |
| $1$ | $\mathbb{R}$ | $x + c$ |
| $x$ | $\mathbb{R}$ | $\frac{x^2}{2} + c$ |
| $x^n$ ($n \in \mathbb{N}$) | $\mathbb{R}$ | $\frac{x^{n+1}}{n+1} + c$ |
| $x^a$ ($a \neq -1$) | $\mathbb{R}_{+}^*$ | $\frac{1}{a+1}x^{a+1} + c$ |
| $\frac{1}{x}$ | $\mathbb{R}_{+}^*$ | $\ln(x) + c$ |
| $e^x$ | $\mathbb{R}$ | $e^x + c$ |

> [!tip] Astuce pour $x^a$
> Cette formule fonctionne pour les racines et les puissances inverses. 
> *Exemple :* $\sqrt{x} = x^{1/2}$ donc une primitive est $\frac{x^{3/2}}{3/2} = \frac{2}{3}x\sqrt{x}$.

---

## 4.2 - Reconnaître une dérivée

Si $u$ est une fonction dérivable, on peut utiliser les règles de dérivation "à l'envers" pour identifier des primitives de fonctions composées.

| Fonction à intégrer | Primitive $F(x)$ | Remarques |
| --- | --- | --- |
| $\frac{u'}{u}$ | $\ln(u) + c$ | $u$ doit être strictement positive |
| $u' e^u$ | $e^u + c$ | |
| $u' u^a$ | $\frac{1}{a+1}u^{a+1} + c$ | $u > 0$ et $a \neq -1$ |

### Exemples de calcul
* **(i)** $\int_{0}^{1} \frac{2x}{(x^2+1)^4} dx$ : Forme $u' u^a$ avec $u = x^2+1$ et $a = -4$.
* **(ii)** $\int_{e}^{3} \frac{dx}{x \ln(x)}$ : Forme $\frac{u'}{u}$ avec $u = \ln(x)$.
* **(iii)** $\int_{1}^{2} \frac{e^{\sqrt{x}}}{2\sqrt{x}} dx$ : Forme $u' e^u$ avec $u = \sqrt{x}$.

---

## 4.3 - Intégration par parties (IPP)

Cette méthode permet de transformer l'intégrale d'un produit de fonctions.

> [!abstract] Proposition : Formule d'IPP
> Soient $u$ et $v$ deux fonctions de classe $C^1$ sur un intervalle $I$ :
> $$\int_{a}^{b} u(x)v'(x)dx = [u(x)v(x)]_{a}^{b} - \int_{a}^{b} u'(x)v(x)dx$$
> **Forme abrégée :** $\int uv' = [uv] - \int u'v$



### Exemple d'application
Calculer une primitive de $x \mapsto xe^x$.
1. On pose $u(x) = x$ donc $u'(x) = 1$.
2. On pose $v'(x) = e^x$ donc $v(x) = e^x$.
3. Par IPP :
$$\int_{0}^{t} xe^x dx = [xe^x]_{0}^{t} - \int_{0}^{t} 1 \cdot e^x dx = te^t - [e^x]_{0}^{t} = te^t - e^t + 1$$

> [!example] Exercices d'IPP
> Calculer pour $n \in \mathbb{N}$ :
> - $I = \int_{1}^{e} t^n \ln(t) dt$
> - $K = \int_{0}^{1} (x^2 + x) e^x dx$

---

# 5. Entraînement

Testez vos connaissances avec ces calculs d'intégrales :

1.  **Exponentielle :** $I = \int_{0}^{2} 3e^x dx$
2.  **Puissance :** $J = \int_{-1}^{1} x^3 dx$
3.  **Forme $u'/u$ :** $K = \int_{1}^{2} \frac{\ln(x)}{x} dx$
4.  **Logarithme composé :** $L = \int_{2}^{3} \frac{1}{x \ln(x)} dx$
5.  **Fraction rationnelle :** $M = \int_{1}^{2} \frac{4x+6}{x^2+3x+12} dx$
6.  **Composée complexe :** $N = \int_{0}^{3} (x^2+1)e^{x^3+3x} dx$
