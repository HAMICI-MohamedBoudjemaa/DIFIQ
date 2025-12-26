Soit $(\Omega, \mathcal F, \mathbb P)$ un espace de probabilité
Dans le modèle de **BS**, le cours de l'actif risqué est $$\begin{aligned}
&S_t = S_0 e^{(\mu - \frac {\sigma^2}{2})t + \sigma W_t} \\
\text{où} &\left|
\begin{array}{ll}
\mu \in \mathbb R \text{ le drift (la tendance/ dérivée)}\\
\sigma \gt 0 \text{ la volatilité} \\
(W_t)_{t \ge 0} \text{ mouvement brownien}
\end{array}
\right.
\end{aligned}$$
# Mouvement Brownien
## Définition
C'est un processus $(W_t)_{t \ge 0}$ tel que
- $W_0 = 0 \space \mathbb P-p.s.$ 
- $t \rightarrow W_t(\omega) \text{ continue }  \mathbb P-P.s.$
- $W_t - W_s \perp\!\!\!\perp (W_r)_{r \ge s}, \forall s \le t \text{ (accroissements indépendants)}$
- $\underset{\mathbb P(W_t - W_s \le x) = \mathbb P(W_{t-s} \le x) = \int_{-\infty}^x \frac {e^{-y^2/2(t-s)}}{\sqrt{2 \pi (t-s)}}dy}{\underline{W_t - W_s \overset {loi}{=} W_{t-s} \sim \mathcal N(0, t-s)}}, \forall s \le t \text{ (accroissements stationnaires)}$ 
### Propriétés
- $$\begin{aligned}
  \mathbb E[W_t W_s] &= \mathbb E[(W_t - W_s) W_s + W_s^2] \\
  &= \mathbb E[(W_t - W_s) W_s] + \mathbb E[W_s^2] \\
  &= \mathbb E[(W_t - W_s)]\mathbb E[W_s] + \mathbb E[W_s^2]\\
  &= 0*0 + \mathbb E[W_s^2]\\
  &= var(W_s) | \textcolor{red}{\text{ car }\mathbb E(W_s^2) = var(W_s)}\\
  &= s
  \end{aligned}$$
- Soit $Z \sim \mathcal N(0,1)$, alors, $$\begin{aligned}
  \mathbb E[e^{\lambda Z}] &= \int_{-\infty}^{+\infty} e^{\lambda z} \frac {e^{-z^2/2}}{\sqrt{2 \pi}}dz \\
  &= \frac {1}{\sqrt{2\pi}} \int_{-\infty}^{+\infty} e^{-\frac 12(z^2-2\lambda z)}dz\\
  &= e^{\lambda^2/2} \int_{-\infty}^{+\infty} \frac{e^{-\frac 12(z^2-2\lambda z)}}{\sqrt{2\pi}}dz \\
  &= e^{\lambda^2/2}
  \end{aligned}$$
	- d'où $$\begin{aligned}
	  \mathbb E[e^{\lambda W_t}] &= \mathbb E \left[ e^{\lambda \sqrt{t}\frac{W_t}{\sqrt{t}}} \right]\\
	  &= \mathbb E \left[ e^{\lambda \sqrt{t}Z} \right]\\
	  &= e^{(\lambda \sqrt{t})^2/2} \textcolor{yellow}{\text{| comme vu plus haut}}\\
	  &= e^{\lambda^2t/2}
	  \end{aligned}$$ 
-  $$\begin{aligned}
  \mathbb P(|W_T|) \le \lambda \sqrt{t}) &= \mathbb P\left(\left|\frac{W_t}{\sqrt{t}}\right| \le \lambda \right) \\
  &= \mathbb P(|z| \le \lambda) = \mathbb P(-\lambda \le Z \le \lambda) \\
  &= \mathbb P(z \le \lambda) - \mathbb P(z \lt -\lambda) \\
  &= \Phi(\lambda) - \Phi(-\lambda) \\
  &=2 \Phi(\lambda) - 1
  \end{aligned}$$
### Remarque
$\mathbb P(|W_t| \le 3\sqrt{t}) \approx 0.997$ 
De ce fait, l'ordre de grandeur de $W_t - W_s$ est $\sqrt{t-s}$ , i.e., $W_{t-s} = O(\sqrt{t-s})$ 
## Filtration
$$\begin{aligned}
\mathcal F_t &= \sigma(W_s, s \le t) \\
	&= \sigma(S_s, s \le t) \text{ car S et }W_s \text{ sont en bijection}
\end{aligned}$$
## Proposition :
$(W_t)_{t \ge 0}$ est une martingale par rapport à $(F_t)_{t \ge 0}$
### Preuve
$$\begin{aligned}
\mathbb E[W_t |\mathcal F_s] &= \mathbb E[W_t - W_s + W_s | \mathcal F_s] \\
&= \mathbb E[W_t - W_s] + W_s \text{ car } \left|\begin{matrix}W_t - W_s \perp\!\!\!\perp \mathcal F_s \\ W_s, \mathcal F_s-mes \end{matrix}\right. \\
&=W_s
\end{aligned}$$
# Intégrale stochastique
Soit $t_0 = 0 \lt t_1 \lt ... \lt t_n = T$ une grille de temps
La stratégie qui consiste à détenir $\phi_{t_i}$ actifs risqués entre $t_i$ et $t_{i+1}$ conduit au portefeuille $$\tilde V_T = \tilde V_0 + \sum_{i=0}^{n-1} \phi_{t_i}(\tilde S_{t_{i+1}} - \tilde S_{t_i})$$
On souhaite définir la valeur du portefeuille lorsqu'on agit de plus en plus souvent, in fine, continument, sur le marché. Pour cela, on va définir $$\int_0^T \phi_s d \tilde S_s = \underset{n \rightarrow +\infty}{lim} \sum_{i=0}^{n-1} \phi_{t_i} (\tilde S_{t_{i+1}} - \tilde S_{t_i})$$par analogie avec l'intégrale classique $$\int_0^Tf(t)dt = \underset{n \rightarrow + \infty}{lim}\sum_{i=0}^{n-1}f(t_i)(t_{i+1}-t_i)$$
## Processus simples
### Définition
C'est un processus $(\phi_t)_{t \in [0,T]}$ tel que :
- Il existe $0 = t_0 \lt t_1 \lt ... \lt t_n = T$ tel que
	- $\phi_t = \sum_{i=0}^{n-1} \phi_{t_i} \mathbb 1_{]t_i, t_{i+1}]}(t)$ où $\phi_{t_i}$ est $\mathcal F_{t_i}-mesurable$ et $\mathbb E[|\phi_{t_i}|^2] \lt +\infty$ 
On définit l'intégrale stochastique par rapport au Mouvement Brownien $$\begin{aligned}
\int_0^t \phi_s dW_s &= \sum_{i=0}^{j-1} \phi_{t_i} (W_{t_{i+1}} - W_{t_i}) + \phi_{t_j}(W_t - W_{t_j}), \forall t \in ]t_j, t_{j+1}] \\
&= \sum_{i=0}^{n-1} \phi_{t_i}(W_{t_{i+1} \wedge t} - W_{t_{i} \wedge t}) , \forall t \in [0,T]
\end{aligned}$$
N.B. $\wedge$ signifie~={yellow} $min$ =~
### Proposition
1. ~={yellow} **Linéarité** =~ : $\int_0^t (\lambda \phi_s +\mu \psi_s)dW_s = \lambda \int_0^t \phi_s dW_s + \mu \int_0^t \psi_s dW_s, \forall \lambda, \mu \in \mathbb R \text{ et } \phi, \psi \text{ simples}$
2.  ~={yellow}**Espérance Nulle**=~ : $\mathbb E[\int_0^t \phi_s dW_s] = 0$
3.  ~={yellow}**Isométrie**=~ : $\mathbb E[(\int_0^t \phi_s dW_s)^2] = \mathbb E[\int_0^t |\phi_s|^2 dW_s]$
 
#### Preuve
1. Quitte à prendre une grille de temps plus fine, on peut toujours supposer que $\phi$ et $\psi$ sont définis sur la même grille de temps. La linéarité découle alors immédiatement de la définition.
2. Quitte à ajouter t à la grille de temps on peut supposer que $t = t_k$ : $$\begin{aligned}
   \mathbb E\left[\int_0^{t_k} \phi_s dW_s\right] &= \sum_{i=0}^{k-1} \mathbb E[\phi_{t_i}(W_{t_{i+1}} - W_{t_i})] \\
   &= \sum_{i=0}^{k-1} \mathbb E[\phi_{t_i}] \space \underset{=0}{\underline {\mathbb E[W_{t_i+1} - W_{t_i}]}} \textcolor{red}{\text{ car } \phi_{t_i} \perp\!\!\!\perp W_{t_{i+1}}-W_{t_i}} \\
   &= \sum_{i=0}^{k-1}0 \\
   &= 0
   \end{aligned}$$
3. $$\mathbb E[(\int_0^{t_k} \phi_s dW_s)^2] = \sum_{i,j=0}^{k-1} \mathbb E\left[\phi_{t_i}  \phi_{t_j}(W_{t_{i+1}}- W_{t_i})(W_{t_{j+1}}- W_{t_j})\right]$$
	1. Si $i=j$ : $$\begin{aligned}
	   &\mathbb E[|\phi_{t_i}|^2(W_{t_{i+1}}- W_{t_i})^2] \\
	   &= \mathbb E\left[|\phi_{t_i}|^2\right] \mathbb E\left[(W_{t_{i+1}}- W_{t_i})^2\right] \\
	   &= \mathbb E[|\phi_{t_i}|^2 ](t_{i+1} - t_i)
	   \end{aligned}$$
	2. Si $i \ne j$ : *e.g.* $i \lt j$ on a $$\begin{aligned}
	   &\mathbb E\left[\phi_{t_i}  \phi_{t_j}(W_{t_{i+1}}- W_{t_i})(W_{t_{j+1}}- W_{t_j})\right] \\
	   &=\underset{\mathcal F_{t_j-mes}}{\underline{\mathbb E\left[\phi_{t_i}  \phi_{t_j}(W_{t_{i+1}}- W_{t_i})\right]}}\space\space \underset{\perp\!\!\!\!\perp \mathcal F_{t_j}}{\underline{\mathbb E\left[(W_{t_{j+1}}- W_{t_j})\right]}} \\
	   &= 0
	   \end{aligned}$$
#### Conclusion
$$\begin{aligned}
\mathbb E\left[ (\int_0^{t_k} \phi_s dW_s)^2\right] &= \sum_{i=0}^{k-1} \mathbb E[| \phi_{t_i}|^2](t_{i+1} - t_i)  \\
&= \mathbb E\left[ \sum_{i=0}^{k-1} | \phi_{t_i}|^2(t_{i+1} - t_i)\right] \\
&= \mathbb E\left[ \int_{0}^{k-1} | \phi_{s}|^2 ds\right]
\end{aligned}$$
### Proposition 2
$(\int_0^t \phi_s dWs)_{t \in [0,T]}$ est une ~={yellow}**martingale continue**=~
#### Remarque
Si $\phi_s = \lambda \in \mathbb R, \forall s \in [0,T]$ alors $\int_0^t \phi_s dW_s = \lambda W_t$ 
#### Preuve 
$$\begin{aligned}
&\mathbb{E}\!\left[\int_0^{t_k} \phi_s\, dW_s \mid \mathcal{F}_{t_l} \right] \\



&= \sum_{i=0}^{l-1} \phi_{t_i}\,(W_{t_{i+1}} - W_{t_i})
  + \sum_{i=l}^{k-1} \phi_{t_i}\,(W_{t_{i+1}} - W_{t_i}) \\



&= \int_0^{t_l} \phi_s\, dW_s
  + \sum_{i=l}^{k-1} \phi_{t_i}\,(W_{t_{i+1}} - W_{t_i}) \\

&= \int_0^{t_l} \phi_s\, dW_s
  + \sum_{i=l}^{k-1}
    \mathbb{E}\!\left[
      \phi_{t_i}(W_{t_{i+1}} - W_{t_i})
      \mid \mathcal{F}_{t_l}
    \right]\\

&= \int_0^{t_l} \phi_s\, dW_s
  + \sum_{i=l}^{k-1}
    \mathbb{E}\! \underset{=0} {\underline {\left[ \mathbb{E}\! \underset {=\phi_{t_i \mathbb E[W_{t_{i+1}} - W_{t_{i}}]} = 0}{\underline{\left[\phi_{t_i}W_{t_{i+1}} - W_{t_i})  \mid \mathcal{F}_{t_i}\right]}} \mid \mathcal{F}_\tau
    \right]}}\\

&= \int_0^{t_l} \phi_s\, dW_s
\end{aligned}$$
## Processus admissible
On dit qu'un processus $(\phi_t)_{t \in [0,T]}$ est admissible lorsqu'il est ~={yellow}**adapté** **($\mathcal F_t-mes$)**=~ et $\mathbb E\left[ \int_0^T |\phi_t|^2 dt\right] \lt +\infty$ 
On admet qu'on peut prouver l'existence d'une suite $(\phi^n)_{n \in \mathbb N}$ de processus simples tel que $$\mathbb E\left[ \int_0^T |\phi_t - \phi_t^n|^2 dt\right] \underset{n\rightarrow +\infty}{\longrightarrow} 0$$ ==Intuitivement, on approche notre fonction par une suite de fonctions==
Dans ce cas, on peut montrer que la suite $\left(\int_0^t \phi_s^n dW_s \right)_{n \in \mathbb N}$ converge ~={red}(au sens $L^2$)=~ et on définit $$\int_0^t \phi_s dW_s = \underset{n \rightarrow +\infty}{lim}\int_0^T \phi_s^n dW_s$$
La limite hérite des propriétés de l'intégrale stochastique établies sur les processus simples.
Essentiellement; $\left( \int_0^t \phi_s dW_s\right)_{t \in [0,T]}$  est une **martingale continue** telle que $$ \mathbb E\left[(\int_0^t\phi_s dW_s)^2\right] = \mathbb E\left[ \int_0^t |\phi_s|^2ds \right]$$
### Idée de preuve
$\forall t \le T$
$$\begin{aligned}
&\mathbb E\left[\left|\int_0^t\phi_s^n dW_s - \int_0^t\phi_s^m dW_s\right|^2\right] \\
&=\mathbb E\left[\left|\int_0^t(\phi_s^n - \phi_s^m) dW_s\right|^2\right]\\
&=\mathbb E\left[\int_0^t\left|\phi_s^n - \phi_s^m\right|^2 d_s\right] \\
&\le \mathbb E\left[\int_0^T\left|\phi_s^n - \phi_s^m\right|^2 d_s\right] \\
\implies &\left(\int_0^t\phi_s^n dW_s\right)_{n \in \mathbb N}\text{ est une suite de cauchy dans } L^2 \text{, qui converge donc dans }L^2 \text{qui est complet}
\end{aligned}$$
Les propriétés de $\int \phi_s dW_s$ se déduisent alors par passage à la limite.
*e.g.*$$\begin{aligned}
\mathbb E\left[\left(\int_0^t \phi_s dW_s \right)^2\right] &= \mathbb E\left[\underset {n \rightarrow +\infty}{lim}\left(\int_0^t \phi_s^n dW_s \right)^2\right] \\
&= \underset {n \rightarrow +\infty}{lim}\mathbb E\left[\left(\int_0^t \phi_s^n dW_s \right)^2\right] \textcolor{red}{\text{ car }L^2-lim} \\
&=\underset {n \rightarrow +\infty}{lim}\mathbb E\left[\int_0^t |\phi_s^n|^2 ds \right] \\
&=\mathbb E\left[\int_0^t |\phi_s|^2 ds \right]
\end{aligned}$$
# Formule d'itô
Dans le calcul différentiel classique, si $x$ et $f$ sont dérivables, alors $$\begin{aligned} 
\int_0^tf'(x(s))dx(s) &= \int_0^tf'(x(s))x'(s)ds \\
&= \left[ f(x(s)) \right]_0^t \\
&=f(x(t)) - f(x(0)) \\
\iff &f(x(t)) = f(x(0)) + \int_0^t f'(x(s))dx(s)
\end{aligned}$$
Mais le **calcul stochastique** n'est pas le **calcul différentiel classique** et cette formule doit être modifiée
## Cas du Mouvement Brownien
*Exemple* : On va montrer que$$W_t^2 = 2 \int_0^t W_s dW_s + \underset{nouveau terme}{\underline t}$$En effet $$
\begin{aligned}
W_t^2 &= W_t^2 - W_0^2 \\
&= \sum_{i=0}^{n-1} W_{t_{i+1}}^2 - W_{t_i}^2 \\
&= \sum_{i=0}^{n-1} \left( 2W_{t_i}(W_{t_{i+1}} - W_{t_i})+W_{t_{i+1}}^2 + W_{t_i}^2 - 2W_{t_{i+1}} W_{t_i}\right) \\
&= \underset{\int_0^t W_s dW_s}{2\underline{\sum_{i=0}^{n-1} W_{t_i}(W_{t_{i+1}} - W_{t_i})}} + \underset{\langle W\rangle _t \text{ la variation quadratique de } W}{\underline{\sum_{i=0}^{n-1} (W_{t_{i+1}} - W_{t_i})^2}}
\end{aligned}$$Il reste à montrer que $\langle W\rangle_t = t$
- En moyenne :
  $$\begin{aligned}
  \mathbb E\left[\sum_{i=0}^{n-1} (W_{t_{i+1}} - W_{t_i})^2\right] &= \sum_{i=0}^{n-1} \mathbb E\left[(W_{t_{i+1}} - W_{t_i})^2\right] \\
  &=\sum_{i=0}^{n-1} (t_{i+1} - t_i)\\
  &= t
  \end{aligned}$$
- $p.s.$ : $$\sum_{i=0}^{n-1} (W_{t_{i+1}} - W_{t_i})^2 = \frac tn \sum_{i=0}^{n-1} \left(\underset{i.i.d \space \mathcal N(0,1)}{\underline{\frac{W_{t_{i+1}} - W_{t_i}}{\sqrt{t_{i+1}-t_i}}}}\right)^2 \overset{p.s.}{\underset{n \rightarrow +\infty}\longrightarrow} t \mathbb E[Z^2]$$En fait, il y a convergence dans $L^2$ quelle que soit la grille de temps
**Remarque**
Si $x$ est dérivable, alors $$\begin{aligned}
\sum_{i=0}^{n-1} \left(x({t_{i+1}}) - x({t_i})\right)^2 &= \sum_{i=0}^{n-1}\left(x'(t_i)(t_{i+1}-t_i) + o(\frac1n)\right)^2 \\
&=n * o(\frac 1n) \\
&= o(1) \underset{n \rightarrow +\infty}{\longrightarrow} 0
\end{aligned}$$
### Formule d'Itô
$$\begin{aligned}
\forall f, \mathcal C^2,\\
f(W_t) &= f(W_0) + \int_0^tf'(W_s)dWs + \frac 12 \int_0^tf''(W_s)d\langle W\rangle_s \\
&=f(0) + \int_0^tf'(W_s)dWs + \frac 12 \int_0^tf''(W_s)ds
\end{aligned}$$On écrit aussi $$df(W_t) = f'(W_t)dW_t + \frac 12 f''(W_t)dt$$
#### Idée de preuve :
$$\begin{aligned}
f(W_t) - f(W_0) &= \sum_{i=0}^{n-1} f(W_{t_{i+1}}) - f(W_{t_i}) \\
&= \underset{\int_0^tf'(W_s)dWs}{\underline{\sum_{i=0}^{n-1} f'(W_{t_i})(W_{t_{i+1}} - W_{t_i})}} + \frac 12 \sum_{i=0}^{n-1} f''(W_{t_i})\underset{\approx (\langle W\rangle_{t_{i+1}} - \langle W\rangle_{t_{i}})}{\underline{(W_{t_{i+1}} - W_{t_i})^2}} + \underset{\rightarrow 0}{\underline{n * o(\frac 1n)}} \\
&= \int_0^tf'(W_s)dWs + \frac 12 \int_0^tf''(W_s)d\langle W\rangle_s
\end{aligned}$$
#### Exemple 1
$$\begin{aligned}
W_t^2 &= f(W_t) \text{ avec }f(x) = x^2 \rightarrow f'(x) = 2x, f''(x) = 2\\
&= f(W_0) + \int_0^t f'(W_s) dW_s + \frac 12 \int_0^tf''(W_s) d\langle W\rangle_s \\
&= 0 + \int_0^t 2 W_s dW_s + \frac {1} {\enclose{updiagonalstrike}{2}} \int_0^t \enclose{updiagonalstrike}{2} ds \\
&=2 \int_0^t W_s dW_s +t
\end{aligned}$$On peut aisément généraliser la formule d'Itô comme ceci : $$\forall f : \mathbb R^+ \times \mathbb R \underset{t,x \longrightarrow f(t,x)}{\longrightarrow \mathbb R}, C^{1,2}, \text{1 fois dérivable en t, 2 fois en x et }\partial_tf,\partial_xf,\partial_{xx}f,continues$$
$$f(t, W_t) = f(0, W_0) + \int_0^t\partial_tf(s,W_s)ds$$
#### Exemple 2
$$\begin{aligned}
S_t &= f(t,W_t), \text{ où }f(t,x)= S_0e^{(\mu-\frac{\sigma^2}{2})t + \sigma x} \\
&= f(0, W_0) + \int_0^t\partial_tf(s,W_s) ds +\int_0^t \partial_xf(s,W_s)dW_s + \frac 12\int_0^t\partial_{xx}f(s,W_s)d\langle W\rangle_s \\
&= S_0 + \int_0^t(\mu - \enclose{updiagonalstrike}{\frac {\sigma^2}{2}})S_sds + \int_0^t\sigma S_s dW_s + \frac 12 \int_0^t \enclose{updiagonalstrike}{\sigma^2}S_s ds \\
&= S_0 + \int_0^t \mu S_s ds + \int_0^t\sigma S_s dW_s
\end{aligned}$$Autrement dit, $$\underset{\text{Equation Différentielle Stochastique}}{\underline{dS_t = \mu S_t dt + \sigma S_t dW_t}}$$
## Cas général
### Processus d'Itô
C'est un processus $(X_t)_{t \ge 0}$ tel que $$X_t = x + \int_0^t \mu_s ds + \int_0^t \sigma_s dW_s$$où $$\left| \begin{array} xx \in \mathbb R \\ (\mu_s)_{s \ge 0} \text{ adapté tel que } \int_0^t|\mu_s|ds \gt +\infty \\ (\sigma_s)_{s \ge 0}\text{ adapté tel que }\mathbb E[\int_0^t |\sigma_s|ds] \gt +\infty \end{array}\right.$$
On écrit aussi $$dX_t = \mu_t dt + \sigma_t dW_t$$