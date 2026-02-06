# Introduction : Méthodes Numériques en Finance

En finance, l’évaluation de produits dérivés amène à calculer des quantités du type $\mathbb{E}_{\mathbb{P}}[f(X_{\cdot})]$, où $X$ est une variable aléatoire ou un processus stochastique. 

L’objectif de ce cours est d’exposer et de mettre en place des méthodes numériques permettant d’estimer ce type de quantités en utilisant le langage **Python**.

---

## Structure du cours

### Partie 1 : La Méthode de Monte-Carlo
* **Chapitre 1 : Principes et Convergence** Exposé de la méthode et des résultats théoriques assurant sa convergence.
* **Chapitre 2 : Simulation de variables aléatoires** Techniques de simulation numérique pour générer des réalisations de v.a.
* **Chapitre 3 : Simulation de processus stochastiques** Extension des méthodes de simulation aux trajectoires de processus.

### Partie 2 : Lien avec les EDP
Lorsqu'un processus $X$ est gouverné par une Équation Différentielle Stochastique (EDS) du type :
$$dX_t = b(X_t)dt + a(X_t)dB_t$$
où $B$ est un mouvement Brownien, on peut établir un lien entre $\mathbb{E}_{\mathbb{P}}[f(X_{\cdot})|X_t = x]$ et la résolution d’Équations aux Dérivées Partielles (EDP).



* **Chapitre 4 : Méthode des différences finies** Résolution numérique du problème de Cauchy associé :
    $$\begin{cases} \frac{\partial u}{\partial t}(t, x) + b(x) \frac{\partial u}{\partial x}(t, x) + \frac{1}{2} a^2(x) \frac{\partial^2 u}{\partial x^2}(t, x) = 0 \\ u(T, x) = f(x) \end{cases}$$

---

## Références bibliographiques
1.  **Paul Glasserman**, *Monte Carlo Methods in Financial Engineering* (2004).
2.  **Cónall Kelly**, *Computation and Simulation for Finance: An introduction with Python*.

# Méthode de Monte-Carlo

Soit $X$ une variable aléatoire sur un espace de probabilité $(\Omega, \mathcal{F}, \mathbb{P})$ dont la loi est notée $\mathbb{P}_X$. 

### Objectif
L'objectif est de calculer ou d'estimer la grandeur $\Theta$ définie par :
$$\Theta := \mathbb{E}_{\mathbb{P}}[f(X)] = \int_{\mathbb{R}^d} f(x) d\mathbb{P}_X(x)$$
où $f : \mathbb{R}^d \to \mathbb{R}$ est une fonction telle que $\int_{\mathbb{R}^d} |f(x)| d\mathbb{P}_X(x) < \infty$ (fonction intégrable).

### Le Principe de Monte-Carlo
Le principe consiste à générer une suite $(X_n)_{1 \leq n \leq N}$ de réalisations indépendantes et identiquement distribuées (i.i.d.) de $X$ pour laquelle une **Loi des Grands Nombres** s'applique.

On définit l'estimateur de Monte-Carlo par la moyenne empirique :
$$\hat{\Theta}_n := \frac{1}{n} \sum_{k=1}^{n} f(X_k)$$

D'après la Loi Forte des Grands Nombres, on a la convergence presque sûre :
$$\hat{\Theta}_n \xrightarrow[n \to +\infty]{\mathbb{P}-p.s.} \mathbb{E}_{\mathbb{P}}[f(X)]$$

Une approximation de $\Theta$ est alors donnée par $\hat{\Theta}_n$ pour un choix de $n$ suffisamment grand.

## 1.1 Théorèmes de Convergence

La validité de l’approximation de Monte Carlo est assurée par la loi des grands nombres (LGN), qui garantit que la moyenne empirique converge vers l'espérance théorique.

### Théorème 1.1.1 : Loi faible et loi forte des grands nombres

Soit $X$ une v.a. de loi $\mathbb{P}_X$ et $f : \mathbb{R} \to \mathbb{R}$ une fonction telle que $\mathbb{E}_{\mathbb{P}}[|f(X)|] < \infty$. Soit $(X_n)_{n \in \mathbb{N}}$ une suite de v.a. réelles i.i.d. de loi $\mathbb{P}_X$. Alors :

1. **Loi faible** : La convergence en probabilité
$$\mathbb{P} \left( \left| \frac{1}{n} \sum_{k=1}^{n} f(X_k) - \mathbb{E}_{\mathbb{P}}[f(X)] \right| > \epsilon \right) \xrightarrow{n \to \infty} 0, \quad \forall \epsilon > 0$$

2. **Loi forte** : La convergence presque sûre ($\mathbb{P}-p.s.$)
$$\frac{1}{n} \sum_{k=1}^{n} f(X_k) \xrightarrow[n \to +\infty]{\mathbb{P}-p.s.} \mathbb{E}_{\mathbb{P}}[f(X)]$$

> [!INFO] Preuve
> La loi faible peut être démontrée via l'inégalité de Bienaymé-Tchebychev (voir exercice 1.3.1). Pour la loi forte, on se réfère généralement à des travaux plus avancés (ex: Kolmogorov).

### Proposition 1.1.2 : Erreur quadratique moyenne (EQM)

En plus des hypothèses de la Loi Forte des Grands Nombres, on suppose que $f(X)$ est de carré intégrable ($\mathbb{E}_{\mathbb{P}}[|f(X)|^2] < \infty$). Alors :

$$\mathbb{E}_{\mathbb{P}} \left[ \left| \frac{1}{n} \sum_{k=1}^{n} f(X_k) - \mathbb{E}_{\mathbb{P}}[f(X)] \right|^2 \right] = \frac{var(f(X))}{n}$$
~={orange}La vitesse de convergence de la méthode Monté Carlo en $O(\frac{𝑛 −1}{2} )$ =~

> [!NOTE] Interprétation
> Cette proposition montre que la précision de l'estimateur dépend directement de la variance de la fonction $f$. Plus la variance est élevée, plus il faut de simulations pour stabiliser l'erreur.

---

### Théorème 1.1.3 : Théorème Central Limite (TCL)

Le TCL précise la vitesse de convergence et la loi de l'erreur. Sous l'hypothèse $\mathbb{E}_{\mathbb{P}}[|f(X)|^2] < \infty$ :

$$\sqrt{n} \left( \hat{\Theta}_n - \mathbb{E}_{\mathbb{P}}[f(X)] \right) \xrightarrow[n \to +\infty]{\text{loi}} \mathcal{N}(0, var(f(X)))$$

Où l'on note l'estimateur de Monte-Carlo : $\hat{\Theta}_n = \frac{1}{n} \sum_{k=1}^{n} f(X_k)$.

---

### Intervalle de confiance

Sous les hypothèses du TCL, pour tout $\varepsilon > 0$ :
$$\mathbb{P} \left( \sqrt{\frac{n}{var(f(X))}} | \hat{\Theta}_n - \mathbb{E}_{\mathbb{P}}[f(X)] | \leq \varepsilon \right) \xrightarrow[n \to +\infty]{} 2\mathcal{N}(\varepsilon) - 1$$

Ceci permet de construire l'**intervalle de confiance bilatéral symétrique** au niveau de confiance asymptotique $1 - \alpha$ pour $\mathbb{E}_{\mathbb{P}}[f(X)]$ :

$$IC_{1-\alpha} := \left[ \hat{\Theta}_n - q_{1-\frac{\alpha}{2}} \sqrt{\frac{\sigma^2}{n}}, \hat{\Theta}_n + q_{1-\frac{\alpha}{2}} \sqrt{\frac{\sigma^2}{n}} \right]$$

**Paramètres :**
- $\sigma^2 = var(f(X))$
- $q_{1-\frac{\alpha}{2}}$ est le quantile de la loi normale centrée réduite tel que $\mathcal{N}(q_{1-\frac{\alpha}{2}}) = 1 - \frac{\alpha}{2}$.

**Valeurs usuelles :**
- Pour $1 - \alpha = 0.95$ (95%), $q_{0.975} \simeq 1.96$.
- Pour $1 - \alpha = 0.99$ (99%), $q_{0.995} \simeq 2.58$.
---

### Estimation de la variance

En pratique, la variance théorique $\sigma^2$ est inconnue. On utilise alors l'estimateur de la variance empirique (non biaisé) calculé sur le même échantillon :

### Proposition 1.1.4
Sous les conditions du TCL, l'estimateur suivant converge presque sûrement vers la variance théorique :

$$\hat{\sigma}^2_{n-1} := \frac{1}{n - 1} \sum_{k=1}^{n} (f(X_k) - \hat{\Theta}_n)^2 \xrightarrow[n \to +\infty]{\mathbb{P}-p.s.} var(f(X))$$

> [!TIP] Pratique Numérique
> Dans un algorithme de Monte-Carlo, on calcule simultanément $\hat{\Theta}_n$ et $\hat{\sigma}^2_{n-1}$ pour fournir non seulement une estimation du prix (en finance), mais aussi une mesure de la fiabilité de ce prix (la largeur de l'intervalle de confiance).
### Comparaison des estimateurs de la variance

Il existe deux estimateurs classiques pour la variance $\sigma^2 = var(f(X))$ dans une simulation de Monte-Carlo :

1.  **L'estimateur sans biais** (corrigé) :
    $$\hat{\sigma}^2_{n-1} := \frac{1}{n - 1} \sum_{k=1}^{n} (f(X_k) - \hat{\Theta}_n)^2$$
    - Il est préféré car son espérance est exactement égale à la variance théorique : $\mathbb{E}_{\mathbb{P}}[\hat{\sigma}^2_{n-1}] = \sigma^2$.

2.  **L'estimateur convergent** (biaisé) :
    $$\hat{\sigma}^2_{n} := \frac{1}{n} \sum_{k=1}^{n} (f(X_k) - \hat{\Theta}_n)^2$$
    - Cet estimateur est légèrement "pessimiste" en moyenne. Son espérance est :
    $$\mathbb{E}_{\mathbb{P}}[\hat{\sigma}^2_{n}] = \frac{n-1}{n} \sigma^2$$

> [!TIP] Pourquoi $n-1$ ?
> En utilisant la moyenne empirique $\hat{\Theta}_n$ (calculée à partir des mêmes données) au lieu de la vraie moyenne $\mathbb{E}[f(X)]$, on réduit artificiellement la variabilité apparente de l'échantillon. La division par $n-1$ compense exactement cette perte de "degré de liberté".

### 1.1.4 Vers un intervalle de confiance pratique

En pratique, comme la vraie variance $\sigma^2$ est inconnue, on utilise le **Théorème de Slutsky** pour la remplacer par son estimateur $\hat{\sigma}^2_{n-1}$ dans le TCL sans changer la loi limite.

#### Théorème 1.1.5 : Théorème de Slutsky
Soit $Y$ une v.a., $c \in \mathbb{R}$ une constante. Si $Y_n \xrightarrow{\mathcal{L}} Y$ et $Z_n \xrightarrow{\mathbb{P}} c$, alors :
- $(Z_n, Y_n) \xrightarrow{\mathcal{L}} (c, Y)$
- En particulier : $Z_n Y_n \xrightarrow{\mathcal{L}} cY$

#### Proposition 1.1.6 : Intervalle de confiance asymptotique
Grâce à Slutsky et au TCL, on peut définir un intervalle où la variance est estimée :
$$\sqrt{\frac{n}{\hat{\sigma}^2_{n-1}}} \left( \hat{\Theta}_n - \mathbb{E}_{\mathbb{P}}[f(X)] \right) \xrightarrow[n \to +\infty]{\mathcal{L}} \mathcal{N}(0, 1)$$

L'intervalle de confiance bilatéral symétrique au niveau $1 - \alpha$ est :
$$IC_{1-\alpha} := \left[ \hat{\Theta}_n - q_{1-\frac{\alpha}{2}} \sqrt{\frac{\hat{\sigma}^2_{n-1}}{n}}, \hat{\Theta}_n + q_{1-\frac{\alpha}{2}} \sqrt{\frac{\hat{\sigma}^2_{n-1}}{n}} \right]$$

---

### 1.1.5 La Méthode Delta

La méthode Delta permet de trouver la loi limite d'une fonction de notre estimateur, si cette fonction est suffisamment régulière.

#### Proposition 1.1.7 : Méthode Delta
Soit $(X_n)$ une suite de v.a. telle que $\sqrt{n}(\bar{X}_n - \theta) \xrightarrow{\mathcal{L}} \mathcal{N}(0, \sigma^2)$.
Soit $\bar X_n = \frac 1n \overset {n}{\underset {k=1}{\sum}}X_k$ la moyenne empirique.
Si $g : \mathbb{R} \to \mathbb{R}$ est de classe $C^1$ avec $g'(\theta) \neq 0$, alors :
$$\sqrt{n} \left( g(\bar{X}_n) - g(\theta) \right) \xrightarrow[n \to +\infty]{\mathcal{L}} \mathcal{N}(0, \sigma^2 |g'(\theta)|^2)$$



#### Exemple 1.1.1 : Loi de Poisson $\mathcal{P}(\lambda)$
Soit $(X_k)$ i.i.d. de loi $\mathcal{P}(\lambda)$. On sait que $\mathbb{E}[X] = Var(X) = \lambda$.
1. **TCL classique** : $\sqrt{n}(\bar{X}_n - \lambda) \xrightarrow{\mathcal{L}} \mathcal{N}(0, \lambda)$.
2. **Application de la méthode Delta** avec $g(x) = \sqrt{x}$ :
   - $g'(\lambda) = \frac{1}{2\sqrt{\lambda}}$.
   - La variance limite devient : $\sigma^2 |g'(\lambda)|^2 = \lambda \times \left(\frac{1}{2\sqrt{\lambda}}\right)^2 = \frac{1}{4}$.
3. **Résultat** : 
$$\sqrt{n} \left( \sqrt{\bar{X}_n} - \sqrt{\lambda} \right) \xrightarrow[n \to +\infty]{\mathcal{L}} \mathcal{N}\left(0, \frac{1}{4}\right)$$

On en déduit un intervalle de confiance asymptotique de niveau $1 - \alpha$ pour $\sqrt{\lambda}$ :
$$\sqrt{\lambda} \in \left[ \sqrt{\bar{X}_n} - \frac{q_{1-\frac{\alpha}{2}}}{2\sqrt{n}} \, , \, \sqrt{\bar{X}_n} + \frac{q_{1-\frac{\alpha}{2}}}{2\sqrt{n}} \right]$$

En élevant au carré, l'intervalle de confiance pour $\lambda$ est donné par :
$$IC_{1-\alpha} := \left[ \left( \sqrt{\frac{1}{n} \sum_{k=1}^{n} X_k} - \frac{q_{1-\frac{\alpha}{2}}}{2\sqrt{n}} \right)^2 \, , \, \left( \sqrt{\frac{1}{n} \sum_{k=1}^{n} X_k} + \frac{q_{1-\frac{\alpha}{2}}}{2\sqrt{n}} \right)^2 \right]$$

Où $q_{1-\frac{\alpha}{2}}$ (noté parfois $\mathcal N^{-1}(1-\frac{\alpha}{2})$) est le quantile de la loi normale centrée réduite.
> [!REMARK] 
> Ici, la variance limite ($1/4$) ne dépend plus de $\lambda$ ! C'est ce qu'on appelle une transformation **stabilisatrice de variance**.

## 1.2 Méthodes de réduction de variance

Dans la méthode Monte Carlo classique, l’erreur quadratique moyenne :
$$\mathbb{E}_{\mathbb{P}} \left[ \left| \frac{1}{n} \sum_{k=1}^{n} f(X_k) - \mathbb{E}_{\mathbb{P}}[f(X)] \right|^2 \right] = \frac{var(f(X))}{n}$$
dépend de la taille de l’échantillon et de la variance $var(f(X))$. L’objectif des méthodes de réduction de variance est de substituer, dans le problème d’approximation, la suite $f(X_n)$ par une suite $(Y_n)$ ayant la même moyenne $\mathbb{E}_{\mathbb{P}}[f(X)]$ mais de variance $\sigma^2_Y < var(f(X))$.

### 1.2.1 Méthode de variable antithétique

La méthodes des variables antithétiques consiste à réduire la variance en introduisant, dans le calcul de l’estimateur, des v.a. négativement corrélées. Elle s’applique lorsque la loi $\mathbb{P}_X$ possède des propriétés d’invariance telle que la symétrie.

**Définition 1.2.1 (Estimateur de variable antithétique)**
Soit $X$ une v.a. à valeurs dans $\mathbb{R}^d$ de loi $\mathbb{P}_X$ et $(X_n)_{n \geq 1}$ est une suite de v.a. i.i.d. de loi $\mathbb{P}_X$. On suppose que :
Il existe $a \in \mathbb{R}^d$ tel que $a - X \stackrel{loi}{=} X$.

La v.a. $(a - X)$ est appelée variable antithétique de $X$ et l’estimateur de variable antithétique est défini par :
$$\hat{\Theta}^A_n := \frac{1}{n} \sum_{k=1}^{n} \frac{f(X_k) + f(a - X_k)}{2}$$

- **Sans biais** : Comme $a - X \stackrel{loi}{=} X$, on vérifie facilement que $\mathbb{E}_{\mathbb{P}}[\hat{\Theta}^A_n] = \mathbb{E}_{\mathbb{P}}[f(X)]$.
- **Convergence** : La loi forte des grands nombres permet de montrer que $\hat{\Theta}^A_n \xrightarrow[n \to +\infty]{\mathbb{P}-p.s.} \mathbb{E}_{\mathbb{P}}[f(X)]$.
- **Variance** : L’inégalité de Cauchy-Schwarz permet de montrer que :
$$var(\hat{\Theta}^A_n) = \frac{var(f(X))}{n} \frac{1 + \rho}{2} \leq \frac{var(f(X))}{n} = var(\hat{\Theta}_n)$$
où $\rho := Cov(f(X), f(a - X)) / var(f(X)) \in [-1, 1]$.
- **TCL** : Si $\mathbb{E}_{\mathbb{P}}[|f(X)|^2] < \infty$, le TLC permet de montrer que :
$$\sqrt{n} \left( \hat{\Theta}^A_n - \mathbb{E}_{\mathbb{P}}[f(X)] \right) \xrightarrow[n \to +\infty]{loi} \mathcal{N} \left( 0, var(f(X)) \frac{1 + \rho}{2} \right)$$

L’estimateur de la variable antithétique a une meilleure performance que la méthode de Monte Carlo Classique ($var(\hat{\Theta}^A_n) \leq var(\hat{\Theta}_n)$), le cas le plus favorable étant celui où $Cov(f(X), f(a - X)) \leq 0$. En effet :
- $var(\hat{\Theta}^A_n) \leq var(\hat{\Theta}_{2n})$ si et seulement si $Cov(f(X), f(a - X)) \leq 0$.

**Proposition 1.2.1**
Si $f$ est monotone alors $Cov(f(X), f(a - X)) < 0$ et $var(\hat{\Theta}^A_n) \leq var(\hat{\Theta}_{2n})$.



**Exemple 1.2.1**
Dans le modèle de Black & Scholes le prix d’une option d’achat de maturité $T$ et de strike $K$ sur une option $S$ est donné par :
$$\Pi = \mathbb{E}_{\mathbb{P}} \left[ e^{-rT} (S_0 e^{(r-\sigma^2/2)T + \sigma\sqrt{T}Z} - K)_+ \right]$$
où $Z \sim \mathcal{N}(0, 1)$.

Ici $r \in \mathbb{R}$ est le taux d’intérêt sans risque, $\sigma \in \mathbb{R}$ est la volatilité de l’option $S$ et $S_0$ est son prix initial. Le prix $\Pi$ est de la forme $\Pi = \mathbb{E}_{\mathbb{P}}[f(Z)]$ où :
$$f : x \mapsto e^{-rT} (S_0 e^{(r-\sigma^2/2)T + \sigma\sqrt{T}x} - K)_+$$

La loi normale est symétrique ($Z \stackrel{loi}{=} -Z$) et la fonction $f$ est monotone. La méthode de variable antithétique peut être appliquée et elle donne un estimateur plus efficace que la Méthode de Monte Carlo classique.
### 1.2.2 Méthode de variable de contrôle

La méthode de variable de contrôle exploite l’information que l’on détient sur des quantités que l’on sait calculer pour réduire l’erreur d’estimation sur des quantités inconnues.

**Définition 1.2.2 (Méthode de la variable de contrôle)**
Soit $X$ une v.a. à valeurs dans $\mathbb{R}^d$ de loi $\mathbb{P}_X$ et $(X_n)_{n \geq 1}$ est une suite de v.a. i.i.d. de loi $\mathbb{P}_X$. Soit $g : \mathbb{R}^d \to \mathbb{R}$ telle que $m := \mathbb{E}_{\mathbb{P}}[g(X)]$ soit facile à calculer et $var(g(X)) < +\infty$. Pour tout réel $\beta \in \mathbb{R}$, on définit :
$$\hat{\Theta}_{C,\beta}^n := \frac{1}{n} \sum_{k=1}^{n} \{ f(X_k) - \beta (g(X_k) - m) \}$$

- **Sans biais** : Comme $\mathbb{E}_{\mathbb{P}}[g(X_k) - m] = 0$, on vérifie facilement que $\mathbb{E}_{\mathbb{P}}[\hat{\Theta}_{C,\beta}^n] = \mathbb{E}_{\mathbb{P}}[f(X)]$.
- **Convergence** : La loi forte des grands nombres permet de montrer que $\hat{\Theta}_{C,\beta}^n \xrightarrow[n \to +\infty]{\mathbb{P}-p.s.} \mathbb{E}_{\mathbb{P}}[f(X)]$.
- **Variance** : La variance de $\hat{\Theta}_{C,\beta}^n$ est donnée par :
$$var(\hat{\Theta}_{C,\beta}^n) = \frac{var(f(X)) + \beta^2 var(g(X)) - 2\beta Cov(f(X), g(X))}{n}$$
$$var(\hat{\Theta}_{C,\beta}^n) = var(\hat{\Theta}_n) + \frac{1}{n} [\beta^2 var(g(X)) - 2\beta Cov(f(X), g(X))]$$
- **TCL** : Les v.a. $Y_k := f(X_k) - \beta(g(X_k) - m)$ étant i.i.d. et de variance $\sigma^2(\beta)$ finie, le TCL donne :
$$\sqrt{n} \left( \hat{\Theta}_{C,\beta}^n - \mathbb{E}_{\mathbb{P}}[f(X)] \right) \xrightarrow[n \to +\infty]{loi} \mathcal{N}(0, \sigma^2(\beta))$$
La variance $\sigma^2(\beta)$ peut être estimée par la variance empirique :
$$\hat{\sigma}^2(\beta) = \frac{1}{n - 1} \sum_{k=1}^{n} (Y_k - \hat{\Theta}_{C,\beta}^n)^2$$

**Proposition 1.2.2 (Choix optimal de $\beta$)**
La plus petite valeur de la variance de $\hat{\Theta}_{C,\beta}^n$ est atteinte pour :
$$\beta^* := \frac{Cov(f(X), g(X))}{var(g(X))}$$
Dans ce cas :
$$var(\hat{\Theta}_{C,\beta^*}^n) = \frac{var(f(X))}{n} (1 - \rho(f, g)^2)$$
où $\rho(f, g) = \frac{Cov(f(X), g(X))}{\sqrt{var(f(X))var(g(X))}}$.

L’estimateur de variance minimale a une variance inférieure à l’estimateur classique $\hat{\Theta}_n$ dès que la corrélation $\rho(f, g) \neq 0$. La méthode est d’autant plus efficace que $|\rho(f, g)|$ est proche de 1.



**Remarque 1.2.1 (Détermination de $\beta^*$)**
En général, $Cov(f(X), g(X))$ ne peut pas être calculée de manière explicite. On peut estimer $\beta^*$ par :
$$\hat{\beta}^*_m = \frac{\sum_{k=1}^m (g(X_k) - m)(f(X_k) - \hat{\Theta}_m)}{\sum_{k=1}^m (g(X_k) - m)^2}$$

Dans la pratique, deux solutions sont possibles :
1. **Échantillons séparés** : On utilise les $m$ premiers termes pour estimer $\hat{\beta}^*_m$ et les $n - m$ restants pour calculer $\hat{\Theta}_{C,\hat{\beta}^*_m}^{n-m}$. Cet estimateur est sans biais.
2. **Échantillon total** : On utilise l'ensemble de l'échantillon $n$ pour estimer $\hat{\beta}^*_n$ et $\hat{\Theta}_{C,\hat{\beta}^*_n}^n$. L'estimation de $\beta^*$ est meilleure, mais l'estimateur devient biaisé (bien que de même variance asymptotique).
### 1.2.3 Méthode de stratification (hors programme)

Soit $(A_i)_{1 \le i \le \ell}$ une partition de $\mathbb{R}^d$ et $Z$ une v.a. à valeurs dans $\mathbb{R}^d$. On a :
$$\mathbb{E}_{\mathbb{P}}[f(X)] = \sum_{i=1}^\ell \mathbb{P}(Z \in A_i) \mathbb{E}_{\mathbb{P}}[f(X) | Z \in A_i]$$

Pour estimer $\mathbb{E}_{\mathbb{P}}[f(X)]$, la méthode de stratification exploite l’information obtenue sur chaque élément de la partition en supposant que :
- Pour chaque $i$, $\mathbb{P}(Z \in A_i) > 0$ et est connue explicitement.
- Pour chaque $i$, on sait simuler la loi conditionnelle $\mathcal{L}(X | Z \in A_i)$.

**Définition 1.2.3**
Pour chaque élément $A_i$ de la partition, on considère une suite $(X_{i,n})_{n_i \in \mathbb{N}}$ de v.a. i.i.d. suivant la loi conditionnelle $\mathcal{L}(X | Z \in A_i)$. Pour tout $n = n_1 + \dots + n_\ell$, on définit l'estimateur stratifié :
$$\hat{\Theta}^S_n(n_1, \dots, n_\ell) := \sum_{i=1}^\ell \mathbb{P}(Z \in A_i) \frac{1}{n_i} \sum_{k=1}^{n_i} f(X_{ik})$$

On appelle :
- **Variable de stratification** : la variable $Z$ (qui peut être $X$).
- **Strates** : les éléments $A_i$ de la partition.
- **Allocation** : le choix des nombres de tirages $n_1, \dots, n_\ell$.



**Propriétés** :
- **Sans biais** : Si pour tout $i, n_i > 0$, l'estimateur est sans biais.
- **Convergence** : La loi forte des grands nombres appliquée à chaque strate implique :
  $$\hat{\Theta}^S_n(n_1, \dots, n_\ell) \xrightarrow[n \to \infty]{\mathbb{P}-p.s.} \mathbb{E}_{\mathbb{P}}[f(X)]$$
- **TCL** : On note $\sigma^2_i = var(f(X) | Z \in A_i)$. L'indépendance entre les strates donne :
  $$\sqrt{n} \left( \hat{\Theta}^S_n(n_1, \dots, n_\ell) - \mathbb{E}_{\mathbb{P}}[f(X)] \right) \xrightarrow[n \to \infty]{loi} \mathcal{N}(0, \sigma^2_A)$$
  Où $\sigma^2_A = \sum_{i=1}^\ell \frac{(\mathbb{P}(Z \in A_i))^2}{n_i/n} \sigma^2_i$.
- **Estimation de la variance** : On estime les variances intra-strates par :
  $$\hat{\sigma}^2_A = \sum_{i=1}^\ell \frac{(\mathbb{P}(Z \in A_i))^2}{n_i/n} \left( \frac{1}{n_i - 1} \sum_{k=1}^{n_i} (f(X_{ik}) - \bar{f}_i)^2 \right)$$

**Proposition 1.2.3 (Allocation optimale)**
Soit $n$ le nombre total de simulations. L'allocation qui minimise la variance est :
$$n^*_i = n \frac{\mathbb{P}(Z \in A_i)\sigma_i}{\sum_{j=1}^\ell \mathbb{P}(Z \in A_j)\sigma_j}$$
Dans ce cas, $var(\hat{\Theta}^S_n(n^*_1, \dots, n^*_\ell)) \le var(\hat{\Theta}_n)$.

**Définition 1.2.4 (Allocation proportionnelle)**
L'allocation est dite proportionnelle si pour tout $i$ : $n_i = n\mathbb{P}(Z \in A_i)$.

**Proposition 1.2.4**
Sous l'hypothèse d'allocation proportionnelle, l'estimateur stratifié $\hat{\Theta}^S_n$ est plus efficace que l'estimateur de Monte Carlo classique :
$$var(\hat{\Theta}^S_n) = \frac{1}{n} \sum_{i=1}^\ell \mathbb{P}(Z \in A_i) \sigma^2_i \le var(\hat{\Theta}_n)$$
### 1.2.4 Méthode Échantillonnage préférentiel

On suppose que la loi $\mathbb{P}_X$ de la v.a. $X$ admet une densité $f_X$. La méthode d’échantillonnage préférentiel (*importance sampling* en anglais) part de l’observation suivante : si $h : \mathbb{R}^d \to \mathbb{R}$ est une densité de probabilité, alors :

$$\mathbb{E}_{\mathbb{P}}[f(X)] = \int_{\mathbb{R}^d} f(x) \frac{f_X(x)}{h(x)} h(x) dx = \mathbb{E}_{\mathbb{P}} \left[ \frac{f(Y)f_X(Y)}{h(Y)} \right]$$

où $Y$ est une v.a. qui a pour densité $h$ pour $\mathbb{P}$. Ainsi, si l’on sait simuler selon la densité $h$ et que $var\left(\frac{f(Y)f_X(Y)}{h(Y)}\right) \leq var(f(X))$, on peut obtenir un estimateur plus efficace que l’estimateur de Monte Carlo classique.

**Définition 1.2.5**
Soit $h : \mathbb{R}^d \to \mathbb{R}$ une densité telle que :
$$Supp(f f_X) := \{x : f(x)f_X(x) \neq 0\} \subset Supp(h) := \{x : h(x) > 0\}$$

Soit $(Y_n)_{n \geq 1}$ une suite de v.a. i.i.d. suivant la densité $h$ sous $\mathbb{P}$. L’estimateur d’échantillonnage préférentiel est :
$$\hat{\Theta}_n(h) := \frac{1}{n} \sum_{k=1}^{n} \frac{f_X(Y_k)}{h(Y_k)} f(Y_k) = \frac{1}{n} \sum_{k=1}^{n} w_k f(Y_k)$$

La densité $h$ est appelée **loi instrumentale** ou **loi d’importance** et la fraction $w_k = f_X(Y_k)/h(Y_k)$ est appelée **poids d’importance**.

- **Sans biais** : Sous l’hypothèse $Supp(f f_X) \subset Supp(h)$, on vérifie facilement que $\hat{\Theta}_n(h)$ est sans biais.
- **Convergence** : La loi forte des grands nombres assure que :
$$\hat{\Theta}_n(h) \xrightarrow[n \to \infty]{\mathbb{P}.p.s} \mathbb{E}_{\mathbb{P}} \left[ \frac{f(Y)f_X(Y)}{h(Y)} \right] = \mathbb{E}_{\mathbb{P}}[f(X)]$$
- **Variance** : Les v.a. $(Y_k)$ étant i.i.d. et de densité $h$, la variance de $\hat{\Theta}_n(h)$ est :
$$var(\hat{\Theta}_n(h)) = \frac{1}{n} \left( \mathbb{E}_{\mathbb{P}} \left[ \frac{f_X^2(Y)f^2(Y)}{h^2(Y)} \right] - (\mathbb{E}_{\mathbb{P}}[f(X)])^2 \right) \quad (1.1)$$
$$var(\hat{\Theta}_n(h)) = \frac{1}{n} \int_{\mathbb{R}^d} \frac{(f(x)f_X(x) - \theta h(x))^2}{h(x)} dx \quad (1.2)$$



- **Estimateur de la variance** : En pratique, un estimateur de $var_{\mathbb{P}}\left[ \frac{f(Y)f_X(Y)}{h(Y)} \right]$ est :
$$\hat{\sigma}^2(h) = \frac{1}{n - 1} \sum_{k=1}^{n} \left( \frac{f(Y_k)f_X(Y_k)}{h(Y_k)} - \hat{\Theta}_n(h) \right)^2$$

**Proposition 1.2.5**
L’estimateur d’échantillonnage préférentiel de variance minimale $\hat{\Theta}_n(h^*)$ est obtenu pour la densité instrumentale :
$$h^*(x) = \frac{|f(x)| f_X(x)}{\int_{\mathbb{R}^d} |f(z)| f_X(z) dz}$$

> [!WARNING] Limite pratique
> Cette proposition a une utilité limitée car le dénominateur $\int |f(z)| f_X(z) dz$ est précisément ce que l'on cherche à estimer (ou une quantité proche).

**Observations sur le choix de $h$ :**
1. Pour garantir une variance finie, on choisit souvent $h$ telle que $f_X/h$ soit bornée (queues de distribution de $h$ plus "lourdes" que celles de $f_X$).
2. L'équation (1.2) suggère de choisir $h$ proportionnelle à $f \cdot f_X$.
3. Un candidat pertinent est tel que $|f| f_X / h$ soit quasi constant.

**Application au calcul d’événement rare**
Cette méthode est utile lors du calcul d’événements rares. On change la loi de sorte que l'événement rare (où $f$ est non nulle) se produise beaucoup plus souvent sous la loi instrumentale $h$.

![[Pasted image 20260206075223.png]]