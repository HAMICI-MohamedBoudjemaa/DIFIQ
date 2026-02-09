# 1. Définition et exemples : Négligeabilité

Le réel $a$ désigne un nombre réel ou l'infini ($\pm \infty$).

## 1.1 Définition
Soient deux fonctions $f$ et $g$ définies au voisinage de $a$. On dit que **$f$ est négligeable devant $g$** au voisinage de $a$ lorsqu'il existe une fonction $\varepsilon$ définie au voisinage de $a$, de limite nulle en $a$, telle que :
$$f(x) = \varepsilon(x)g(x) \text{ au voisinage de } a$$

On note (notation de Landau) : 
> [!info] Notation
> $$f(x) \underset{a}{=} o(g(x))$$
> *Lire : $f(x)$ est un "petit o" de $g(x)$ au voisinage de $a$.*

### Exemples
- $x^2 \underset{0}{=} o(x)$ (car $x^2 = x \cdot x$ et $\lim_{x \to 0} x = 0$)
- $\sqrt{x} \underset{+\infty}{=} o(x)$ (car $\sqrt{x} = x \cdot \frac{1}{\sqrt{x}}$ et $\lim_{x \to +\infty} \frac{1}{\sqrt{x}} = 0$)

> [!warning] Attention
> La relation $f(x) = o(g(x))$ signifie que $f$ appartient à l'ensemble des fonctions négligeables devant $g$. On ne peut pas manipuler le symbole $=$ comme une égalité classique.

### Remarque
$f(x) \underset{a}{=} o(1)$ signifie simplement que $\lim_{x \to a} f(x) = 0$.

## 1.2 Caractérisation
**Théorème 1 :** Si $g$ ne s'annule pas au voisinage de $a$, alors :
$$f(x) \underset{a}{=} o(g(x)) \iff \lim_{x \to a} \frac{f(x)}{g(x)} = 0$$

## 1.3 Négligeabilités classiques (Croissances comparées)
**Théorème 2 :** Pour tout réel $\alpha > 0$ et $n \in \mathbb{N}$ :
- $\ln(x) \underset{+\infty}{=} o(x^n)$
- $x^\alpha \underset{+\infty}{=} o(e^x)$

*Exemple :* $\ln(x) \underset{+\infty}{=} o(\sqrt{x})$ avec $\alpha = 1/2$.



## 1.4 Propriétés
- **Transitivité (Propriété 1) :** Si $f = o(g)$ et $g = o(h)$, alors $f = o(h)$.
- **Linéarité (Propriété 2) :** Si $f = o(h)$ et $g = o(h)$, alors pour tous réels $\alpha, \beta$ : 
  $$\alpha f(x) + \beta g(x) \underset{a}{=} o(h(x))$$

---

# 2. Équivalence

## 2.1 Définition et exemples
**Définition :** On dit que $f$ et $g$ sont **équivalentes** au voisinage de $a$ s'il existe une fonction $\varepsilon$ telle que $\lim_{x \to a} \varepsilon(x) = 0$ et :
$$f(x) = (1 + \varepsilon(x))g(x) \text{ au voisinage de } a$$

On note :
> [!info] Notation
> $$f(x) \underset{a}{\sim} g(x)$$

### Exemples
- $x + x^2 \underset{0}{\sim} x$
- $e^x + e^{-x} \underset{+\infty}{\sim} e^x$

## 2.2 Caractérisation
**Théorème 3 :** $f(x) \underset{a}{\sim} g(x) \iff f(x) = g(x) + o(g(x))$

**Théorème 4 :** Si $g$ ne s'annule pas au voisinage de $a$, alors :
$$f(x) \underset{a}{\sim} g(x) \iff \lim_{x \to a} \frac{f(x)}{g(x)} = 1$$

## 2.3 Équivalence et opérations
- **Transitivité :** Si $f \sim g$ et $g \sim h$, alors $f \sim h$.
- **Produit / Quotient :** Si $f \sim g$, alors $fh \sim gh$ et $\frac{1}{f} \sim \frac{1}{g}$ (si $f, g \neq 0$).
- **Puissance :** Si $f \sim g$, alors $(f(x))^n \sim (g(x))^n$ pour $n \in \mathbb{N}$.

> [!danger] Attention
> De manière générale, on ne peut **ni additionner**, **ni composer** (par $\ln$ ou $\exp$) des équivalents.

## 2.4 Équivalents classiques
**Théorème 5 (Limites usuelles) :**
- $e^x - 1 \underset{0}{\sim} x$
- $\ln(1 + x) \underset{0}{\sim} x$



**Théorème 6 (Polynômes) :**
- Au voisinage de **0** : un polynôme est équivalent à son monôme de **plus bas degré**.
- Au voisinage de **l'infini** : un polynôme est équivalent à son monôme de **plus haut degré**.

## 2.5 Équivalents et limites
**Théorème 7 :** Si $f(x) \underset{a}{\sim} g(x)$, alors $\lim_{x \to a} f(x) = \lim_{x \to a} g(x)$.

---
# 3. Développements limités

## 3.1 Développement limité d’ordre 1

> [!abstract] Définition
> On dit qu’une fonction $f$ définie au voisinage d’un réel $x_0$ admet un **développement limité d’ordre 1** en $x_0$ lorsqu’il existe deux réels $a_0$ et $a_1$ tels que, au voisinage de $x_0$ :
> $$f(x) = \underbrace{a_0 + a_1 (x - x_0)}_{\text{partie polynomiale}} + o(x - x_0)$$

On peut aussi écrire :
$f(x) = a_0 + a_1 (x - x_0) + (x - x_0) \varepsilon(x)$ avec $\lim_{x \to x_0} \varepsilon(x) = 0$.

* **Exemple :** La relation $f(x) \underset{0}{=} 1 - x + o(x)$ est un DL de $f$ à l'ordre 1 au voisinage de 0.

## 3.2 Développement limité d’ordre $n$

> [!abstract] Définition
> On dit qu’une fonction $f$ admet un **DL d’ordre $n$** en $x_0$ s'il existe $n + 1$ réels $a_0, a_1, \dots, a_n$ tels que :
> $$f(x) = \underbrace{a_0 + a_1 (x - x_0) + \dots + a_n (x - x_0)^n}_{\text{partie polynomiale}} + o((x - x_0)^n)$$

**Théorème 8 :** Si une fonction admet un développement limité, alors celui-ci est **unique**.

---

# 4. Formule de Taylor-Young

> [!important] Théorème 9 (Taylor-Young)
> Si une fonction $f$ est de classe $\mathcal{C}^n$ au voisinage de $x_0$, alors elle admet un DL d'ordre $n$ en $x_0$ donné par :
> $$f(x) = f(x_0) + (x - x_0)f'(x_0) + \frac{(x - x_0)^2}{2!}f''(x_0) + \dots + \frac{(x - x_0)^n}{n!}f^{(n)}(x_0) + o((x - x_0)^n)$$

### DL et Équivalents
**Théorème 10 :** Une fonction est équivalente en 0 au **premier terme non nul** de son développement limité.
* Si $f(x) = a_0 + a_1x + a_2x^2 + o(x^2)$ :
	* Si $a_0 \neq 0$, alors $f(x) \underset{0}{\sim} a_0$.
	* Si $a_0 = 0$ et $a_1 \neq 0$, alors $f(x) \underset{0}{\sim} a_1x$.

### Interprétation géométrique (Ordre 2)
**Théorème 11 :** Soit $f(x) = a + b(x - x_0) + c(x - x_0)^2 + o((x - x_0)^2)$.
- $a = f(x_0)$ : Continuité.
- $y = a + b(x - x_0)$ : Équation de la **tangente** en $x_0$.
- **Position relative :** - Si $c > 0$, la courbe est localement **au-dessus** de sa tangente.
	- Si $c < 0$, la courbe est localement **en-dessous**.



---

# 5. Développements limités usuels (en 0)

| Fonction | Développement Limité à l'ordre $n$ |
| :--- | :--- |
| $e^u$ | $1 + \frac{u}{1!} + \frac{u^2}{2!} + \frac{u^3}{3!} + \dots + \frac{u^n}{n!} + o(u^n)$ |
| $\ln(1 + u)$ | $u - \frac{u^2}{2} + \frac{u^3}{3} - \frac{u^4}{4} + \dots + (-1)^{n-1}\frac{u^n}{n} + o(u^n)$ |
| $(1 + u)^\alpha$ | $1 + \alpha u + \frac{\alpha(\alpha-1)}{2!}u^2 + \dots + \frac{\alpha(\alpha-1)\dots(\alpha-n+1)}{n!}u^n + o(u^n)$ |

### Cas particuliers importants

* **Série géométrique ($\alpha = -1$) :**
	* $\frac{1}{1+u} = 1 - u + u^2 - u^3 + \dots + (-1)^n u^n + o(u^n)$
	* $\frac{1}{1-u} = 1 + u + u^2 + u^3 + \dots + u^n + o(u^n)$

* **Racine carrée ($\alpha = 1/2$) :**
	* $\sqrt{1+u} = 1 + \frac{u}{2} - \frac{u^2}{8} + o(u^2)$
# 6. Utilisation des développements limités

Les développements limités (DL) sont des outils puissants pour toute sorte d’étude locale. Ils permettent de simplifier des fonctions complexes par des polynômes au voisinage d'un point.

Voici les principales applications que nous aborderons dans les exercices :

* **Calcul de limites :** Pour lever des indéterminations (formes $0/0$ ou $\infty/\infty$) en remplaçant les fonctions par leurs approximations polynomiales.
* **Étude locale d'une fonction :**
	* Déterminer l'équation de la **tangente** à la courbe en un point.
	* Étudier la **convexité** et la position relative de la courbe par rapport à sa tangente (au-dessus ou en-dessous).
* **Détermination d'asymptotes :** Pour étudier le comportement d'une courbe représentative aux voisinages de l'infini (recherche d'asymptotes obliques).
* **Étude de séries :** Pour déterminer la nature (convergence ou divergence) d'une série numérique dans les cas où un équivalent simple n'est pas directement accessible.



---
# 7. Entraînement

---

## Exercice 1 : Application de la formule de Taylor-Young
En appliquant la formule de Taylor-Young, calculer le DL en $0$ à l’ordre $3$ des fonctions :

a) $x \mapsto \ln(1 + x)$
b) $x \mapsto e^x$
c) $x \mapsto \frac{1}{1+x}$
d) $x \mapsto \sqrt{1 - x}$

> [!tip] Rappel de la formule
> $f(x) = f(0) + \frac{f'(0)}{1!}x + \frac{f''(0)}{2!}x^2 + \frac{f'''(0)}{3!}x^3 + o(x^3)$

---

## Exercice 2 : DL usuels en 0 et règles de troncature
Déterminer les développements limités suivants :

a) $x \mapsto x \ln(1 + x)$ : DL en $0$ à l’ordre $3$
b) $x \mapsto \ln(1 + x) - x$ : DL en $0$ à l’ordre $3$
c) $x \mapsto e^{-2x}\sqrt{1 + x}$ : DL en $0$ à l’ordre $2$
d) $x \mapsto x\sqrt{1 + \frac{1}{x}}$ : DL en $+\infty$ à l’ordre $2$ (poser $h = 1/x$)

---

## Exercice 3 : Calcul de limites
Utiliser les développements limités pour lever les indéterminations :

a) Calculer la limite en $0$ de :
$$\frac{\sqrt{\frac{1}{1-x^2}}-1}{x^2}$$

b) Calculer la limite en $+\infty$ de :
$$\left(1 + \frac{1}{x}\right)^x$$

c) Calculer la limite en $+\infty$ de :
$$x \times \left[ \left(1 + \frac{1}{x}\right)^x - e \right]$$



---
**Note sur la correction :** Pour l'exercice 3.b, n'oubliez pas d'utiliser la forme exponentielle : $(1 + \frac{1}{x})^x = e^{x \ln(1 + \frac{1}{x})}$.