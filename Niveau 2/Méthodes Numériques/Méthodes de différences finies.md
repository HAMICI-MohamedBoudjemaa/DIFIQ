# Chapitre 4 : Lien entre EDS et EDP

Soit $W$ un mouvement Brownien standard, on considère l’EDS :
$$X_s = x + \int_t^s b(u, X_u)du + \int_t^s \sigma(u, X_u)dW_u, \quad s \geq t \quad (4.1)$$

Sous les conditions de Lipschitz et de croissance linéaire habituelles :
- L’EDS (4.1) admet une unique **solution forte** $X^{t,x} = \{X^{t,x}_s, s \geq t\}$.
- On a l’inégalité des moments : $\forall p \geq 2, \forall T > t, \exists C_T$ :
  $$\mathbb{E}_{\mathbb{P}} \left[ \sup_{s \in [t,T]} |X^{t,x}_s|^p \right] \leq C_T (1 + |x|^p) e^{C_T T}$$

**Objectif** : Estimer numériquement des quantités du type :
$$\mathbb{E}_{\mathbb{P}} \left[ e^{-\int_t^T k(u,X_u^{t,x})du} g(X_T^{t,x}) + \int_t^T e^{-\int_t^u k(s,X_s^{t,x})ds} f(u, X_u)du \right]$$
en exploitant le lien avec le **problème de Cauchy**.

---

### Générateur Infinitésimal
On désigne ainsi l’opérateur différentiel $\mathcal{L} : \mathcal{C}^{1,2}([0, T] \times \mathbb{R}) \to \mathcal{C}^0([0, T] \times \mathbb{R})$ défini par :
$$\mathcal{L}u(t, x) = b(t, x) \frac{\partial u}{\partial x}(t, x) + \frac{1}{2} \sigma^2(t, x) \frac{\partial^2 u}{\partial x^2}(t, x)$$

C’est l’opérateur qui apparaît quand on applique la **formule d’Itô** :
$$\Phi(s, X_s^{t,x}) = \Phi(t, x) + \int_t^s \left[ \frac{\partial \Phi}{\partial t} + \mathcal{L}\Phi \right](u, X_u^{t,x}) du + \int_t^s \frac{\partial \Phi}{\partial x}(u, X_u^{t,x}) \sigma(u, X_u^{t,x}) dW_u$$

Le problème de Cauchy (4.2) s'écrit alors :
$$
\begin{cases}
\frac{\partial u}{\partial t}(t, x) + \mathcal{L}u(t, x) - k(t, x)u(t, x) + f(t, x) = 0, & (t, x) \in [0, T[ \times \mathbb{R} \\
u(T, x) = g(x), & x \in \mathbb{R}
\end{cases}
$$

---

## 4.1 Formule de Feynman-Kac

**Théorème 4.1.1 (Formule de Feynman-Kac)**
Soit $g$ une fonction à croissance au plus polynomiale, $k$ une fonction positive et $f$ mesurable. On suppose qu'il existe une fonction $u$ de classe $\mathcal{C}^{1,2}$ sur $[0, T[ \times \mathbb{R}$, solution du problème (4.2) et à croissance au plus polynomiale. Alors :
$$u(t, x) = \mathbb{E}_{\mathbb{P}} \left[ e^{-\int_t^T k(u,X_u^{t,x})du} g(X_T^{t,x}) + \int_t^T e^{-\int_t^u k(s,X_s^{t,x})ds} f(u, X_u)du \right]$$



> [!ABSTRACT] Preuve (cas où le terme de diffusion est borné)
> Soit $(t, x)$ fixé. On introduit le processus d'actualisation $Y_s = e^{-\int_t^s k(\tau, X_\tau)d\tau}$.
> Par Itô et intégration par parties :
> 1. $dY_s = -Y_s k(X_s) ds$
> 2. $du(s, X_s) = \left[ \frac{\partial u}{\partial t} + \mathcal{L}u \right](s, X_s) ds + H_s dW_s$
> 3. $d(Y_s u(s, X_s)) = Y_s \left[ \frac{\partial u}{\partial t} + \mathcal{L}u - ku \right](s, X_s) ds + Y_s H_s dW_s$
>
> En intégrant entre $t$ et $T$ et en utilisant le fait que $u$ est solution de l'EDP :
> $$Y_T u(T, X_T) = u(t, x) - \int_t^T Y_s f(s, X_s) ds + \int_t^T Y_s H_s dW_s$$
> En prenant l'espérance, l'intégrale stochastique s'annule (martingale) et on obtient le résultat grâce à la condition terminale $u(T, X_T) = g(X_T)$.

## 4.2 Schémas de discrétisation

### 4.2.1 Grille et différences finies
Pour résoudre numériquement le problème de Cauchy (4.2), une première étape consiste à introduire une grille discrète :
$$\text{Grid} = \{ (t_i, x_j), 0 \le i \le N, 0 \le j \le M \}$$
Le but étant de calculer une estimation $U_{ij} \simeq u(t_i, x_j)$ de la valeur de la fonction $u$ en chacun des points de la grille.

* **Maillage du temps** : on peut choisir un pas de temps constant $dt = T/N$ et définir $t_i = i \cdot dt$.
* **Maillage de l'espace** : même si le domaine initial n'est pas borné, on est tenu de considérer un intervalle borné $[L, H] \subset \mathbb{R}$. Après avoir choisi les bornes $L$ et $H$, on peut fixer un pas constant $\Delta x = (H - L)/M$ et définir $x_j := L + j \Delta x$.
* **Bornes artificielles** : Le choix des bornes $L$ et $H$ et des conditions de bord associées est crucial. L'enjeu est de garantir un système de différences finies bien posé dont la solution reste une bonne approximation de $u$.

L'opérateur différentiel $\mathcal{L}$ est approché par un opérateur de différences finies via les formules de **Taylor** :
$$\Phi(y + h) = \Phi(y) + h \frac{\partial\Phi}{\partial y}(y) + \frac{h^2}{2!} \frac{\partial^2\Phi}{\partial y^2}(y) + \dots + \frac{h^n}{n!} \frac{\partial^n\Phi}{\partial y^n}(y) + O(h^{n+1})$$

On introduit les approximations suivantes :
* **Dérivée temporelle** : $\partial_{dt}u(t, x) := \frac{u(t + dt, x) - u(t, x)}{dt} \simeq \frac{\partial u}{\partial t}(t, x) + O(dt)$
* **Dérivée spatiale (avant)** : $\partial_{\Delta x}^+ u(t, x) := \frac{u(t, x + \Delta x) - u(t, x)}{\Delta x} \simeq \frac{\partial u}{\partial x}(t, x) + O(\Delta x)$
* **Dérivée spatiale (arrière)** : $\partial_{\Delta x}^- u(t, x) := \frac{u(t, x) - u(t, x - \Delta x)}{\Delta x} \simeq \frac{\partial u}{\partial x}(t, x) + O(\Delta x)$
* **Dérivée seconde** : $\partial_{\Delta x}^2 u(t, x) := \frac{u(t, x + \Delta x) - 2u(t, x) + u(t, x - \Delta x)}{\Delta x^2} \simeq \frac{\partial^2 u}{\partial x^2}(t, x) + O(\Delta x)$

---

### 4.2.2 Schéma explicite
Le schéma explicite pour le problème (4.2) est obtenu en approximant l'opérateur $\mathcal{L}$ par :
$$\partial_{dt}u(t, x) + \mu(t, x)\partial_{\Delta x}u(t + dt, x) + \frac{1}{2}\sigma^2(t, x)\partial_{\Delta x}^2 u(t + dt, x) - k(t, x)u(t + dt, x) + f(t, x) = 0$$

Où le terme de transport $\mu$ est discrétisé selon son signe (schéma *upwind*) :
$$\mu(t, x)\partial_{\Delta x}u(t + dt, x) = \begin{cases} \mu(t, x)\partial_{\Delta x}^+ u(t + dt, x) & \text{si } \mu(t, x) \ge 0 \\ \mu(t, x)\partial_{\Delta x}^- u(t + dt, x) & \text{si } \mu(t, x) < 0 \end{cases}$$

> [!abstract] Définition 4.2.1 : Schéma explicite par différences finies
> On construit $\{U_j^n\}$ selon l'algorithme suivant :
> 1.  **Condition terminale** : $U_j^N = g(T, x_j), \forall j \in \{0, \dots, M\}$
> 2.  **Récurrence** :
> $$U_j^n = \left[ 1 - \frac{\sigma^2(t_n, x_j)dt}{(\Delta x)^2} - \frac{|\mu(t_n, x_j)|dt}{\Delta x} - k(t, x)dt \right] U_j^{n+1} + \left[ \frac{\sigma^2(t_n, x_j)dt}{(\Delta x)^2} + \frac{\mu^+(t_n, x_j)dt}{\Delta x} \right] U_{j+1}^{n+1} + \left[ \frac{\sigma^2(t_n, x_j)dt}{(\Delta x)^2} + \frac{\mu^-(t_n, x_j)dt}{\Delta x} \right] U_{j-1}^{n+1} + f(t_n, x_j)dt$$



> [!info] Définition 4.2.2 : Condition de monotonie
> On dit que le schéma satisfait la condition de monotonie si, en tout point $(t, x)$ :
> $$1 - \frac{\sigma^2(t_n, x_j)dt}{(\Delta x)^2} - \frac{|\mu(t_n, x_j)|dt}{\Delta x} - k(t, x)dt \ge 0$$

> [!success] Proposition 4.2.1 : Convergence
> Si $(dt, \Delta x) \to 0$ et que la condition de monotonie est satisfaite pour des pas suffisamment petits, alors le schéma est convergent :
> $$\lim_{(dt, \Delta x) \to 0} |U_j^n - u(t_n, x_j)| = 0$$

### 4.2.3 Schéma implicite

Le schéma implicite pour le problème (4.2) consiste à évaluer les opérateurs de transport et de diffusion à l'instant $t_n$ (celui que l'on cherche) plutôt qu'à l'instant $t_{n+1}$. L'approximation de l'opérateur $\mathcal{L}$ s'écrit :
$$\partial_{dt}u(t, x) + \mu(t, x)\partial_{\Delta x}u(t, x) + \frac{1}{2}\sigma^2(t, x)\partial_{\Delta x}^2 u(t, x) - k(t, x)u(t, x) + f(t, x) = 0$$

En réorganisant les termes pour isoler $U^{n+1}$ et les sources, on obtient :
$$U^{n+1}_j + f(t_n, x_j)dt = \left[ 1 + \frac{\sigma^2 dt}{(\Delta x)^2} + \frac{|\mu| dt}{\Delta x} + k dt \right] U^n_j - \left[ \frac{\sigma^2 dt}{2(\Delta x)^2} + \frac{\mu^+ dt}{\Delta x} \right] U^n_{j+1} - \left[ \frac{\sigma^2 dt}{2(\Delta x)^2} + \frac{\mu^- dt}{\Delta x} \right] U^n_{j-1}$$

Contrairement au schéma explicite, $U^n$ ne peut pas être déduit directement de $U^{n+1}$. Il nécessite la résolution d'un **système linéaire** :
$$(I - A(n)) U^n = U^{n+1} + f(n, \cdot)dt$$

Où $A(n)$ est une **matrice tridiagonale** définie par les coefficients $d$, $d^+$ et $d^-$ :



$$A(n) = \begin{pmatrix} 
d(n,1) & d^+(n,1) & 0 & \cdots & 0 \\ 
d^-(n,2) & d(n,2) & d^+(n,2) & \ddots & \vdots \\ 
0 & d^-(n,3) & d(n,3) & \ddots & 0 \\ 
\vdots & \ddots & \ddots & \ddots & d^+(n, M-1) \\ 
0 & \cdots & 0 & d^-(n, M) & d(n, M) 
\end{pmatrix}$$

> [!TIP] Avantage du schéma implicite
> Ce schéma est **inconditionnellement stable**. Il ne nécessite pas de respecter une condition de type CFL sur le pas de temps $dt$, ce qui permet d'utiliser des pas de temps plus larges qu'en explicite.

---

### 4.2.4 $\theta$-Schéma

Le $\theta$-Schéma est une combinaison convexe des schémas explicite et implicite. On fixe un paramètre $\theta \in [0, 1]$ pour pondérer les deux approches :

$$\partial_{dt}u(t, x) + \theta \left[ \mathcal{L}u - ku \right](t+dt, x) + (1-\theta) \left[ \mathcal{L}u - ku \right](t, x) + f(t, x) = 0$$

Cela conduit au système matriciel suivant :
$$(I - (1 - \theta)A(n))U^n = (I + \theta A(n))U^{n+1} + f(n, \cdot)dt$$

D'où la solution :
$$U^n = (I - (1 - \theta)A(n))^{-1} \left[ (I + \theta A(n))U^{n+1} + f(n, \cdot)dt \right]$$



#### Cas particuliers notables :
* **$\theta = 0$** : On retrouve le schéma **implicite** pur.
* **$\theta = 1$** : On retrouve le schéma **explicite** pur.
* **$\theta = 1/2$** : Correspond au schéma de **Crank-Nicolson**.

> [!IMPORTANT] Schéma de Crank-Nicolson
> En choisissant $\theta = 1/2$, le schéma devient d'ordre 2 en temps ($O(dt^2)$), offrant une bien meilleure précision pour un coût de calcul similaire au schéma implicite.

