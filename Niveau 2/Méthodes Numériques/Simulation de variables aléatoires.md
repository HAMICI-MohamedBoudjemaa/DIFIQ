# Chapitre 2 : Simulation des variables aléatoires

Pour implémenter une méthode Monte Carlo, il est nécessaire de disposer d’un algorithme qui simule les réalisations d’une variable aléatoire. Ce chapitre présente différentes méthodes de simulation, la Section 2.4 traitant en particulier du cas Gaussien.

---

## 2.1 PRNG de la loi uniforme

Un générateur pseudo-aléatoire, **Pseudo Random Number Generator (PRNG)**, de loi uniforme $\mathcal{U}([0, 1])$ est un algorithme déterministe qui produit des suites périodiques de nombres ayant l’apparence de réalisations indépendantes d’une variable aléatoire suivant la loi $\mathcal{U}([0, 1])$.

> [!NOTE] Commentaire 2.1.1 (Python)
> En Python, la méthode `numpy.random.default_rng()` du package **Numpy** permet de créer une instance d’un générateur de loi $\mathcal{U}([0, 1])$.

---

## 2.2 Méthode d’inversion de la fonction de répartition

La méthode d’inversion est une méthode universelle qui permet de construire un générateur de loi $\mathbb{P}_X$ à partir d’un générateur de loi $\mathcal{U}([0, 1])$.

**Définition 2.2.1 (Inverse généralisée)**
Soit $X$ une v.a., $F_X$ sa fonction de répartition. L’inverse généralisée de $F_X$, appelée également **fonction quantile**, est la fonction $F_X^{\leftarrow}$ définie par :
$$F_X^{\leftarrow}(\alpha) = \inf \{x \in \mathbb{R} : F_X(x) \ge \alpha\} , \quad \alpha \in ]0, 1[$$
*Note : Lorsque $F_X$ est strictement croissante et continue, $F_X^{\leftarrow} = F_X^{-1}$.*

**Proposition 2.2.1**
L’inverse généralisée de $F_X$ vérifie :
$$F_X^{\leftarrow}(\alpha) \le x \iff F_X(x) \ge \alpha, \quad \forall x \in \mathbb{R}, \alpha \in ]0, 1[$$



**Théorème 2.2.2**
Si $U$ suit la loi $\mathcal{U}([0, 1])$, alors la variable aléatoire $F_X^{\leftarrow}(U)$ suit la loi $\mathbb{P}_X$.

> [!ABSTRACT] Preuve
> $\mathbb{P}(F_X^{\leftarrow}(U) \le x) = \mathbb{P}(U \le F_X(x)) = F_X(x)$. (Grâce à la Proposition 2.2.1).

---

### Exemples d'application

**Exemple 2.2.1 (Loi de Bernoulli $\mathcal{B}(p)$)**
La fonction de répartition et son inverse sont :
- $F_{\mathcal{B}(p)}(x) = (1-p)\mathbb{1}_{[0,1[}(x) + \mathbb{1}_{[1,+\infty[}(x)$
- $F_{\mathcal{B}(p)}^{\leftarrow}(\alpha) = \mathbb{1}_{]1-p, 1]}(\alpha)$
**Simulation** : Si $U \sim \mathcal{U}([0, 1])$, alors $X = \mathbb{1}_{\{U > 1-p\}}$ suit une loi $\mathcal{B}(p)$.

**Exemple 2.2.2 (Loi exponentielle $\mathcal{E}(\lambda)$)**
- $F_{\mathcal{E}(\lambda)}(x) = 1 - \exp(-\lambda x)$
- $F_{\mathcal{E}(\lambda)}^{\leftarrow}(\alpha) = -\frac{1}{\lambda} \ln(1 - \alpha)$
**Simulation** : Si $U \sim \mathcal{U}([0, 1])$, alors $1-U$ suit aussi une loi $\mathcal{U}([0, 1])$. On utilise souvent la formule simplifiée :
$$X = -\frac{1}{\lambda} \ln(U) \sim \mathcal{E}(\lambda)$$
## 2.3 Méthode de Rejet
La méthode de rejet, introduite par Von Neumann [6], permet de simuler une loi $\mathbb{P}_X$ à partir d’une autre loi $\mathbb{P}_Y$ dont la simulation est facile. Nous la présentons ici dans le cas où $\mathbb{P}_X$ admet une densité $f$ et $\mathbb{P}_Y$ admet une densité $g$.

### Théorème 2.3.1
Soit $X$ une v.a. dont la loi admet une densité de probabilité $f : \mathbb{R}^d \to \mathbb{R}^+$. On suppose qu’il existe une constante $c \geq 1$ telle que :
$$\forall x \in \mathbb{R}^d, \quad f(x) \leq c \, g(x)$$

Soit $(Y_n, U_n)_{n \geq 1}$ une suite de v.a. i.i.d. où, pour tout $n$, $Y_n$ est de densité $g$ et est indépendant de $U_n$ qui suit une loi $\mathcal{U}([0,1])$. On définit le temps d'arrêt $T$ par :
$$T = \inf \left\{ n \geq 1 : U_n \leq \frac{f(Y_n)}{c \, g(Y_n)} \right\}$$

Alors $T$ suit une loi géométrique de paramètre $p = 1/c$ et $Y_T$ est une variable aléatoire de densité $f$. De plus, la suite des variables acceptées $(Y_{T_n})$ forme une suite i.i.d. de densité $f$.



> [!IMPORTANT] Remarque 2.3.1 (Efficacité)
> Le nombre moyen de tirages nécessaires pour obtenir une réalisation de $X$ est $\mathbb{E}[T] = c$. 
> Plus $c$ est proche de 1, plus la méthode est efficace. Il est donc crucial de choisir une densité auxiliaire $g$ dont la forme est "proche" de $f$.

---

**Exemple 2.3.1 : Simulation de la loi Normale via Laplace**
La loi de Laplace $\mathcal{L}(0, 1)$ a pour densité $g(x) = \frac{1}{2} \exp(-|x|)$. Elle est facile à simuler par inversion de la fonction de répartition. Le rapport avec la densité normale $f_N$ est borné :
$$\frac{f_N(x)}{g(x; 0, 1)} = \sqrt{\frac{2}{\pi}} e^{-x^2/2 + |x|} \leq \sqrt{\frac{2e}{\pi}} \approx 1,32$$
On peut donc simuler une $\mathcal{N}(0, 1)$ avec $c \approx 1,32$.

---

## 2.4 Simulation de la loi Normale

### 2.4.1 Méthode de Box-Muller
L’algorithme de Box-Muller fournit une méthode directe pour simuler un couple de variables normales indépendantes à partir de deux variables uniformes.

### Théorème 2.4.1
Soit $(U, V)$ un vecteur aléatoire de loi uniforme sur $[0,1]^2$. On définit :
$$X := \sqrt{-2 \ln(U)} \cos(2\pi V)$$
$$Y := \sqrt{-2 \ln(U)} \sin(2\pi V)$$

Alors $X$ et $Y$ sont deux variables aléatoires **indépendantes** de loi $\mathcal{N}(0, 1)$.



**Interprétation géométrique :**
1. On génère un rayon $R^2 = -2 \ln(U)$ qui suit une loi exponentielle $\mathcal{E}(1/2)$ (ou une loi du $\chi^2$ à 2 degrés de liberté).
2. On génère un angle $\Theta = 2\pi V$ uniforme sur $[0, 2\pi]$.
3. Le couple $(X, Y)$ correspond aux coordonnées cartésiennes d'un point choisi aléatoirement selon une symétrie polaire gaussienne.
### 2.4.2 Approximation de $\mathcal{N}$ et de son inverse $\mathcal{N}^{-1}$

La fonction de répartition de la loi $\mathcal{N}(0, 1)$, notée $\mathcal{N}(x)$, est définie par :
$$\mathcal{N}(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{t^2}{2}\right) dt$$

Cette fonction est inversible, mais il n'existe pas de formule fermée pour sa fonction inverse $\mathcal{N}^{-1}$. En utilisant des approximations de $\mathcal{N}^{-1}$, on peut appliquer la **méthode d'inversion** pour simuler une loi normale.

Par symétrie de la loi normale :
$$\mathcal{N}^{-1}(1 - u) = -\mathcal{N}^{-1}(u), \quad \forall u \in [0, 1]$$
Il suffit donc d'approcher la fonction sur l'intervalle $[0.5, 1]$.

**Proposition 2.4.2 (Approximation de Beasley et Springer)**
Pour $0.5 \le u \le 0.92$ :
$$\mathcal{N}^{-1}(u) \approx \frac{\sum_{i=0}^3 a_i(u - \frac{1}{2})^{2i+1}}{1 + \sum_{i=0}^3 b_i(u - \frac{1}{2})^{2i}}$$

**Coefficients :**
| $i$ | $a_i$ | $b_i$ |
| :--- | :--- | :--- |
| 0 | 2.50662823884 | -8.47351093090 |
| 1 | -18.61500062529 | 23.0836743743 |
| 2 | 41.39119773534 | -21.062224101826 |
| 3 | -24.44106049637 | 3.13082909833 |

---

### 2.4.3 Loi normale multivariée

Une loi normale de dimension $d$ est caractérisée par sa moyenne $\mu \in \mathbb{R}^d$ et sa matrice de variance-covariance $\Sigma \in \mathbb{M}_{dd}$ (symétrique semi-définie positive). On la note $\mathcal{N}(\mu, \Sigma)$.

**Proposition 2.4.3**
Soit $\mu \in \mathbb{R}^d$ et $A \in \mathbb{M}_{dd}(\mathbb{R})$. 
Si $X \sim \mathcal{N}(0, I_d)$, alors le vecteur aléatoire $Y = \mu + AX$ suit la loi $\mathcal{N}(\mu, \Sigma)$ où $\Sigma = AA^T$.

Pour simuler $\mathcal{N}(\mu, \Sigma)$, on cherche donc une matrice $A$ telle que $AA^T = \Sigma$.



#### Théorème 2.4.4 (Décomposition de Cholesky)
Soit $\Sigma \in \mathbb{M}_{dd}$ une matrice symétrique définie positive. Il existe une unique matrice $B \in \mathbb{M}_{dd}$ **triangulaire inférieure** à coefficients diagonaux strictement positifs telle que :
$$\Sigma = BB^T$$

**Commentaire 2.4.1 : Algorithme de Cholesky**
Pour construire $B = (b_{ij})$ :
1. **Colonne 1** : $b_{11} = \sqrt{\sigma_{11}}$ et $b_{j1} = \frac{\sigma_{1j}}{b_{11}}$ pour $j = 2, \dots, d$.
2. **Colonne $j$** ($2 \le j \le d-1$) :
   - $b_{jj} = \sqrt{\sigma_{jj} - \sum_{k=1}^{j-1} b_{jk}^2}$
   - $b_{ij} = \frac{\sigma_{ij} - \sum_{k=1}^{j-1} b_{ik}b_{jk}}{b_{jj}}$ pour $i = j+1, \dots, d$.
3. **Colonne $d$** : $b_{dd} = \sqrt{\sigma_{dd} - \sum_{k=1}^{d-1} b_{dk}^2}$.

> [!NOTE] Cas semi-définie (rang $k < d$)
> Si $\Sigma$ n'est pas de rang plein, on peut réduire la dimension : il existe un sous-vecteur $\tilde{X}$ de dimension $k$ et une matrice $D \in \mathbb{M}_{dk}$ tels que $D\tilde{X} \sim \mathcal{N}(0, \Sigma)$ avec $\tilde{X} \sim \mathcal{N}(0, \tilde{\Sigma})$ où $\tilde{\Sigma}$ est définie positive.

