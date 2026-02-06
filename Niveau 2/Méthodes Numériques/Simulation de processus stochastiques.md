# Chapitre 3 : Simulation de processus et Schémas de discrétisation

En finance, l’évaluation de produits dérivés amène à calculer des quantités du type $\mathbb{E}_{\mathbb{P}}[f(X_{\cdot})]$ où $X$ est un processus stochastique en temps continu dont l’évolution est décrite par une Équation Différentielle Stochastique (EDS) du type :
$$dX_t = b(t, X_t)dt + \sigma(t, X_t)dW_t \quad (3.1)$$

L’approximation Monte Carlo nécessite la simulation de trajectoires de $X$. Cela passe par une **discrétisation du temps** :
1. On considère un maillage $\mathcal{T} = \{t_0 = 0 < \dots < t_N = T\}$ de l’intervalle $[0, T]$.
2. L'objectif est de simuler des réalisations du vecteur $(X_{t_0}, \dots, X_{t_N})$.

**Définition 3.0.1 (Discrétisation exacte)**
On dit que le processus $\tilde{X}^N = \{\tilde{X}^N_{t_k}, 0 \le k \le N\}$ est une discrétisation exacte de $X$ si :
$$(\tilde{X}^N_{t_0}, \dots, \tilde{X}^N_{t_N}) \stackrel{\text{loi}}{=} (X_{t_0}, \dots, X_{t_N})$$

---

## 3.1 Simulation exacte de processus

Cette section traite des cas où l'EDS admet une solution explicite permettant une simulation sans erreur de discrétisation.

### 3.1.1 Mouvement Brownien standard

**Définition 3.1.1 (Mouvement Brownien)**
Un processus $W = \{W_t, t \in [0, T]\}$ est un mouvement Brownien standard si :
1. $W_0 = 0$ $\mathbb{P}$-p.s.
2. La trajectoire $t \mapsto W_t$ est continue $\mathbb{P}$-p.s.
3. **Incréments indépendants** : $W_t - W_s \perp \mathcal{F}_s$ pour tout $t \ge s$.
4. **Incréments gaussiens** : $W_t - W_s \sim \mathcal{N}(0, t - s)$ pour tout $t \ge s$.



**Commentaire 3.1.1 : Algorithme de simulation**
Grâce à l'indépendance et à la normalité des incréments, on simule le mouvement Brownien aux dates du maillage ainsi :
1. Soit $(Z_1, \dots, Z_N)$ une suite de v.a. $\mathcal{N}(0, 1)$ i.i.d.
2. On pose $\tilde{W}^N_0 = 0$.
3. Pour chaque pas de temps :
$$\tilde{W}^N_{t_{k+1}} := \tilde{W}^N_{t_k} + \sqrt{t_{k+1} - t_k} Z_{k+1}$$

Le processus $\tilde{W}^N$ ainsi construit est une **discrétisation exacte** du mouvement Brownien.

Dans de nombreux cas financiers, l'EDS n'a pas de solution explicite. On utilise alors :
- **Le schéma d'Euler-Maruyama**
- **Le schéma de Milstein**
### 3.1.2 Processus Gaussiens

Le mouvement Brownien est un cas particulier de processus Gaussien.

**Définition 3.1.2 (Processus Gaussien)**
Un processus $X = \{X_t, t \in [0, T]\}$ est dit gaussien si et seulement si : pour tout $n \in \mathbb{N}$ et pour tout ensemble fini $\{s_1, \dots, s_n\} \subset [0, T]$, le vecteur $(X_{s_1}, \dots, X_{s_n})$ est gaussien.
Sa loi est complètement décrite par :
- Sa fonction moyenne : $m(t) = \mathbb{E}_{\mathbb{P}}[X_t]$
- Sa fonction covariance : $v(t, s) = cov(X_t, X_s)$

**Commentaire 3.1.2 (Simulation par Cholesky)**
Si $(X_{t_1}, \dots, X_{t_N}) \sim \mathcal{N}(\mu, \Sigma)$, on utilise la décomposition $\Sigma = AA^T$. Pour une suite $Z \sim \mathcal{N}(0, I_N)$, on pose :
$$(\tilde{X}_{t_1}, \dots, \tilde{X}_{t_N})^T = \mu + A(Z_1, \dots, Z_N)^T$$
C'est une discrétisation exacte.

---

#### Processus Gaussien Markovien
Si $X$ est à la fois Gaussien et Markovien, on peut générer $X_{t_{k+1}}$ conditionnellement à $X_{t_k}$.

**Lemme 3.1.1**
Si $\begin{pmatrix} X_{t_k} \\ X_{t_{k+1}} \end{pmatrix} \sim \mathcal{N} \left( \begin{pmatrix} \mu_k \\ \mu_{k+1} \end{pmatrix} , \begin{pmatrix} \sigma_{k,k} & \sigma_{k,k+1} \\ \sigma_{k,k+1} & \sigma_{k+1,k+1} \end{pmatrix} \right)$, alors :
$$X_{t_{k+1}} | X_{t_k} = x_k \sim \mathcal{N} \left( \mu_{k+1} + \frac{\sigma_{k,k+1}}{\sigma_{k,k}}(x_k - \mu_k) \, , \, \sigma_{k+1,k+1} - \frac{\sigma_{k,k+1}^2}{\sigma_{k,k}} \right)$$

**Commentaire 3.1.3 (Algorithme récursif)**
1. $\tilde{X}_{t_1} = \mu_1 + \sqrt{\sigma_{1,1}}Z_1$
2. $\tilde{X}_{t_{k+1}} = \mu_{k+1} + \frac{\sigma_{k,k+1}}{\sigma_{k,k}}(\tilde{X}_{t_k} - \mu_k) + \sqrt{\sigma_{k+1,k+1} - \frac{\sigma_{k,k+1}^2}{\sigma_{k,k}}} Z_{k+1}$

#### EDS Linéaires
Les processus solutions de $dX_t = (b(t) + a(t)X_t)dt + \sigma(t)dW_t$ sont gaussiens et markoviens. Leur solution explicite est :
$$X_t = e^{\alpha(0,t)}X_0 + \int_0^t e^{\alpha(s,t)}b(s)ds + \int_0^t e^{\alpha(s,t)}\sigma(s)dW_s$$
avec $\alpha(s,t) = \int_s^t a(u)du$.

---

**Exemple 3.1.1 (Modèles de taux courts)**
Sous la mesure risque-neutre $\mathbb{Q}$, le taux court $r_t$ suit souvent une EDS linéaire :
- **Ho & Lee** : $dr_t = b(t)dt + \sigma dW_t^{\mathbb{Q}}$
- **Vasicek** : $dr_t = \kappa(\beta - r_t)dt + \sigma dW_t^{\mathbb{Q}}$ (Retour à la moyenne)
- **Hull & White** : $dr_t = \kappa(t)(\beta(t) - r_t)dt + \sigma(t)dW_t^{\mathbb{Q}}$



---

#### Interpolation d'un processus Gaussien
Pour affiner un maillage entre $t_i$ et $t_{i+1}$, on utilise les propriétés du conditionnement gaussien.

**Théorème 3.1.2**
Soit $X = \begin{pmatrix} X_1 \\ X_2 \end{pmatrix} \sim \mathcal{N} \left( \begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix} , \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{pmatrix} \right)$. 
La loi conditionnelle est :
$$X_2 | X_1 \sim \mathcal{N}(\mu_2 + \Sigma_{21}\Sigma_{11}^{-1}(X_1 - \mu_1) \, , \, \Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12})$$

**Exemple 3.1.2 (Pont Brownien)**
Pour un mouvement Brownien standard, si l'on connaît $W_{t_i} = x_i$ et $W_{t_{i+1}} = x_{i+1}$, la valeur à un instant intermédiaire $s \in ]t_i, t_{i+1}[$ suit :
$$W_s | (W_{t_i}, W_{t_{i+1}}) \sim \mathcal{N} \left( \frac{(t_{i+1}-s)x_i + (s-t_i)x_{i+1}}{t_{i+1}-t_i} \, , \, \frac{(t_{i+1}-s)(s-t_i)}{t_{i+1}-t_i} \right)$$
### 3.1.3 Application au modèle de Vasicek

Dans le modèle de Vasicek, la dynamique du taux court est donnée par l'EDS :
$$dr_t = \kappa (\beta - r_t) dt + \sigma dW^{\mathbb{Q}}_t$$
où $\kappa, \beta, \sigma \in \mathbb{R}$ sont des constantes. Ce modèle est un cas particulier d'EDS linéaire (3.2).

#### Solution explicite
La solution de cette EDS est donnée par :
$$r_t = \beta + (r_0 - \beta)e^{-\kappa t} + \sigma e^{-\kappa t} \int_{0}^{t} e^{\kappa s} dW^{\mathbb{Q}}_s$$

De manière plus générale, pour tout $t \geq s$, on a la relation de récurrence :
$$r_t = \beta + e^{-\kappa(t-s)}(r_s - \beta) + \sigma e^{-\kappa t} \int_{s}^{t} e^{\kappa u} dW^{\mathbb{Q}}_u$$

#### Propriétés de la loi conditionnelle
Par les propriétés de l'intégrale de Wiener, les incréments sont gaussiens. Pour tout $s < t$ :
$$r_t | r_s \sim \mathcal{N}\left( r_s e^{-\kappa(t-s)} + \mu(s, t) \, , \, \sigma^2(s, t) \right)$$

Avec les paramètres suivants :
- **Espérance conditionnelle** : $\mu(s, t) = \beta(1 - e^{-\kappa(t-s)})$
- **Variance conditionnelle** : $\sigma^2(s, t) = \frac{\sigma^2}{2\kappa}(1 - e^{-2\kappa(t-s)})$



**Commentaire 3.1.4 : Algorithme de simulation exacte**
Puisque la loi conditionnelle est connue, on peut simuler exactement les trajectoires sur un maillage $\{t_0, \dots, t_N\}$ sans erreur de discrétisation :

1. Soit $(Z_1, \dots, Z_{N-1})$ une suite de v.a. i.i.d. $\mathcal{N}(0, 1)$.
2. On utilise la formule de récurrence :
$$r_{t_{k+1}} = r_{t_k} e^{-\kappa(t_{k+1}-t_k)} + \mu(t_k, t_{k+1}) + \sqrt{\sigma^2(t_k, t_{k+1})} Z_k$$

> [!TIP] Analyse du modèle
> - Si $r_t > \beta$, le terme $\kappa(\beta - r_t)$ est négatif, ce qui tend à faire baisser le taux.
> - Si $r_t < \beta$, ce terme est positif, ce qui tend à le faire monter.
> - C'est la propriété de **retour à la moyenne** vers le niveau de long terme $\beta$.

## 3.2 Schémas de discrétisation d’EDS

Soit $W$ un mouvement Brownien standard, et $X$ la solution de l’EDS :
$$X_t = x + \int_0^t b(u, X_u)du + \int_0^t \sigma(u, X_u)dW_u$$

On suppose que les fonctions $b$ (dérive) et $\sigma$ (diffusion) sont Lipschitziennes et à croissance linéaire en la seconde variable :
1. **Condition de Lipschitz** : $|b(t, x) - b(t, y)| + |\sigma(t, x) - \sigma(t, y)| \leq K|x - y|$
2. **Croissance linéaire** : $|b(t, x)| + |\sigma(t, x)| \leq K(1 + |x|)$

### 3.2.1 Schéma d’Euler-Maruyama

Le principe repose sur l'approximation de l'intégrale sur un petit intervalle $h$ :
$$X_{t+h} \simeq X_t + b(t, X_t)h + \sigma(t, X_t)(W_{t+h} - W_t)$$

On considère un maillage $\mathcal{T}_m = \{t^m_0 = 0 < \dots < t^m_N = T\}$ et on définit le processus discret $X^m$ par :
- $X^m_0 = x$
- $X^m_{t^m_{j+1}} = X^m_{t^m_j} + b(t^m_j, X^m_{t^m_j})(t^m_{j+1} - t^m_j) + \sigma(t^m_j, X^m_{t^m_j})(W_{t^m_{j+1}} - W_{t^m_j})$



#### Prolongement continu
Le processus peut être prolongé sur tout l'intervalle $[0, T]$ par interpolation linéaire :
$$X^m_s = X^m_{t^m_j} + \frac{s - t^m_j}{t^m_{j+1} - t^m_j}(X^m_{t^m_{j+1}} - X^m_{t^m_j}), \quad s \in [t^m_j, t^m_{j+1}]$$

**Proposition 3.2.1 (Convergence)**
Pour un pas constant $\Delta t = T/m$, il existe $C_p$ tel que :
$$\mathbb{E}_{\mathbb{P}} \left[ \sup_{0 \le j \le m} |X^m_{t^m_j} - X_{t^m_j}|^{2p} \right] \leq \frac{C_p}{m^p}$$
De plus, pour tout $\beta < 1/2$ : $\lim_{m \to \infty} m^\beta \sup_{0 \le t \le T} |X^m_t - X_t| = 0$.

> [!NOTE] Vitesse de convergence
> Le schéma d'Euler possède une **vitesse de convergence forte de $0.5$** (en $\sqrt{\Delta t}$) et une **vitesse de convergence faible de $1$** (en $\Delta t$) pour des fonctions de test assez régulières.

---

**Commentaire 3.2.1 : Simulation pratique**
Pour simuler une trajectoire de $X$ selon Euler :
1. Soit $(Z_1, \dots, Z_N)$ une suite i.i.d. $\mathcal{N}(0, 1)$.
2. On itère :
$$X^m_{t^m_{j+1}} = X^m_{t^m_j} + b(t^m_j, X^m_{t^m_j})\Delta t + \sigma(t^m_j, X^m_{t^m_j})\sqrt{\Delta t} Z_{j+1}$$
### 3.2.2 Schéma de Milstein

L’idée du schéma de Milstein est d’établir une « meilleure » approximation de $\int_{t}^{t+h} \sigma(u, X_u)dW_u$ en exploitant la régularité de la fonction $\sigma$. Supposons que $\sigma$ soit de classe $\mathcal{C}^{1,2}$, alors en appliquant la **formule d’Itô** :

$$d\sigma(u, X_u) = \left[ \frac{\partial \sigma}{\partial t} + b \frac{\partial \sigma}{\partial x} + \frac{\sigma^2}{2} \frac{\partial^2 \sigma}{\partial x^2} \right](u, X_u) du + \left[ \sigma \frac{\partial \sigma}{\partial x} \right](u, X_u) dW_u$$

En intégrant et en itérant dans l'intégrale stochastique, on obtient :
$$\int_{t}^{t+h} \sigma(s, X_s) dW_s = \sigma(t, X_t) \int_{t}^{t+h} dW_s + \int_{t}^{t+h} \int_{t}^{s} \sigma(u, X_u) \frac{\partial \sigma}{\partial x}(u, X_u) dW_u dW_s + \dots$$

En négligeant les termes d'ordre supérieur en $du$ et $dudW_s$, on obtient l'approximation :
$$\int_{t}^{t+h} \sigma(s, X_s) dW_s \simeq \sigma(t, X_t)(W_{t+h} - W_t) + \sigma \frac{\partial \sigma}{\partial x}(t, X_t) \int_{t}^{t+h} \int_{t}^{s} dW_u dW_s$$

Or, par l'intégrale d'Itô, $\int_{t}^{t+h} (W_s - W_t) dW_s = \frac{1}{2} \left[ (W_{t+h} - W_t)^2 - h \right]$. On considère alors le maillage $\mathcal{T}_m = \{t^m_0 = 0 < \dots < t^m_N = T\}$ et on définit le processus $X^m$ par :

**Définition du Schéma de Milstein** :
- $X^m_0 = x$
- $X^m_{t^m_{j+1}} = X^m_{t^m_j} + b(t^m_j, X^m_{t^m_j}) \Delta t + \sigma(t^m_j, X^m_{t^m_j}) \Delta W_j + \frac{1}{2} \sigma \sigma'(t^m_j, X^m_{t^m_j}) \left[ (\Delta W_j)^2 - \Delta t \right]$

où $\Delta t = t^m_{j+1} - t^m_j$ et $\Delta W_j = W_{t^m_{j+1}} - W_{t^m_j}$.



#### Prolongement continu
Comme pour Euler, le processus est prolongé par interpolation linéaire sur chaque intervalle $[t^m_j, t^m_{j+1}]$ :
$$X^m_s = X^m_{t^m_j} + \frac{s - t^m_j}{t^m_{j+1} - t^m_j} (X^m_{t^m_{j+1}} - X^m_{t^m_j})$$

**Proposition 3.2.2 (Convergence forte)**
On suppose que le pas de discrétisation est $\Delta t = T/m$. Alors pour tout $p \geq 1$, il existe une constante $C_p$ telle que :
$$\mathbb{E}_{\mathbb{P}} \left[ \sup_{0 \le j \le m} |X^m_{t^m_j} - X_{t^m_j}|^{p} \right] \leq \frac{C_p}{m^p}$$

De plus, pour tout $\beta < 1$ : $\lim_{m \to \infty} m^\beta \sup_{0 \le t \le T} |X^m_t - X_t| = 0$.

> [!IMPORTANT] Avantage de Milstein
> Contrairement au schéma d'Euler (vitesse forte $0.5$), le schéma de Milstein atteint une **vitesse de convergence forte de $1$** (en $\Delta t$). Cela est dû à la prise en compte du terme de dérivée de la diffusion $\sigma \sigma'$.

---

**Commentaire 3.2.2 : Simulation pratique**
Si $Z_{j+1} \sim \mathcal{N}(0, 1)$, alors $\Delta W_j = \sqrt{\Delta t} Z_{j+1}$ et $(\Delta W_j)^2 - \Delta t = \Delta t (Z_{j+1}^2 - 1)$. 
L'itération devient :
$$X^m_{t^m_{j+1}} = X^m_{t^m_j} + b \Delta t + \sigma \sqrt{\Delta t} Z_{j+1} + \frac{1}{2} \sigma \sigma' \Delta t (Z_{j+1}^2 - 1)$$

![[Pasted image 20260206075317.png]]