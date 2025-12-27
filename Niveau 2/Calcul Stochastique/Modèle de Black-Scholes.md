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
### Variation quadratique :
$$\langle W\rangle_t = \int_0^t \sigma_s^2ds = \underset{n \rightarrow +\infty }{lim}\sum_{i=0}^{n-1}(X_{t_{i+1} - X_{t_i}})^2$$En effet $$\begin{aligned}
\sum_{i=0}^{n-1}(X_{t_{i+1}} - X_{t_i})^2 &= \sum_{i=0}^{n-1}\left(\sigma_{t_i}^2 (W_{t_{i+1}} - W_{t_i})^2 + o(\frac 1n)\right) \\
&= \sum_{i=0}^{n-1}\sigma_{t_i}^2 (W_{t_{i+1}} - W_{t_i})^2 + \underset{=0}{\underline{n*o(\frac 1n)}} \\
&= \int_0^t \sigma_s^2d\langle W\rangle s
\end{aligned}$$
### Formule d'Itô
$$\forall f: [0,T] \times \mathbb R \rightarrow \mathbb R, \mathcal C^{1,2}$$
$$\begin{aligned}
f(t, X_t) &= f(0, X_0) + \int_0^t \partial_t f(s, X_s)ds + \int_0^t \partial_xf(s,X_s)\underset{=\mu_s ds + \sigma_s dW_s}{\underline{dX_s}} + \frac 12 \int_0^t \partial_{xx}f(s, X_s)\underset{\sigma_s^2ds}{\underline{d\langle X \rangle_s}} \\
&= f(0,x) + \int_0^t \partial_xf(s, X_s)\sigma_sdW_s + \int_0^t\left(\partial_t f(s, X_s) + \mu_s \partial_xf(s, X_s) + \frac{\sigma_s^2}{2}\partial_{xx}f(s,X_s)\right)ds
\end{aligned}$$
*Exemple* : 
- On note $\tilde X_t = e^{-rt} X_t$ et on a $$\begin{aligned}
  d\tilde X_t &= df(t, X_t) \space où \space f(t,x)=e^{-rt}x \left| \begin{array}{}\partial_t f(t,x) = -rf(t,x) \\\partial_xf(t,x) = e^{-rt} \\\partial_{xx}f(t,x) = 0 \end{array} \right. \\
  &=\partial_t f(t,X_t)dt + \partial_x f(t,X_t)dX_t + \frac 12 \partial_{xx} f(t,X_t)d\langle X\rangle_t \\
  &= -r \tilde X_t dt + e^{-rt}dX_t + 0 \\
  &= (\tilde \mu_t - r \tilde X_t)dt + \tilde \sigma_t dW_t
  \end{aligned}$$
- $$\begin{aligned}
  df(t, S_t) &= \partial_tf(t,S_t)dt + \partial_xf(t,S_t)\underset{=\mu S_t dt + \sigma S_t dW_t}{\underline{dS_t}}+\frac 12 \partial_{xx}f(t,S_t) \underset{=\sigma^2 S_t^2 dt}{\underline{d\langle S \rangle_t}} \\
  &= \partial_xf(t,S_t) \sigma S_t dW_t + \left( \partial_tf(t,S_t) + \mu S_t \partial_xf(t,S_t) + \frac{\sigma^2 S_t^2}{2}\partial_{xx}f(t,S_t) \right)dt
  \end{aligned}$$
# Couverture d'options
## Portefeuille
En temps discret, on avait $$\begin{aligned}
V_{t+1} &= \phi_t S_{t+1} + (V_t - \phi_t S_t)(1+r) \\
&=V_t + \underset{\text{Gain trading risqué}}{\underline{\phi_t(S_{t+1} - S_t)}} + \underset{\text{Gain trading sans risque}}{\underline{(V_t - \phi_tS_t)r}} \\
\iff V_{t+1} - V_t &= \phi_t(S_{t+1} - S_t) + (V_t - \phi_tS_t)r
\end{aligned}$$
Par analogie, en temps continue, on a$$dV_t = \phi_tdS_t + (V_t - \phi_t S_t)rdt$$
C'est une ***équation différentielle stochastique*** (**EDS**).
Pour vérifier si c'est bien défini, on actualise le portefeuille : $$\begin{aligned}
d \tilde V_t &= -r \tilde V_t dt + e^{-rt} dV_t \\
&= -r\tilde V_t dt + e^{-rt} \phi_t dS_t + (\tilde V_t - \phi_t \tilde S_t)rdt \\
&= \phi_t(-r \tilde S_t dt + e^{-rt}dS_t) \\
&= \phi_t d \tilde S_t
\end{aligned}$$Ainsi, on peut définir $$\begin{aligned}
&\tilde V_t^{x,\phi} = x + \int_0^t \phi_s \underset{(\mu - r)\tilde S_s ds + \sigma \tilde S_s dWs}{\underline{d \tilde S_s}} \text{ et } V_t^{x, \phi} = e^{rt}\tilde V_t^{x,\phi} \\ 
\text{où } &\left| \begin{array}{} x \in \mathbb R \text{ capital initial} \\ \phi \text{ stratégie admissible, i.e., adapté et }\mathbb E[\int_0^t |\phi_s S_s|^2ds] \le +\infty\end{array} \right.
\end{aligned}$$
***Remarque*** :
Si $\phi = 0$, alors $V_t^{x, \phi} = e^{rt}x \rightarrow$ ~={red} **taux d'intérêt continu** =~ 
## Options européennes
On considère une option de payoff $g(S_t)$.
Soit alors $v:[0,T] \times \mathbb R_+ \rightarrow \mathbb R$ une fonction satisfaisant l'équation aux dérivées partielles (EDP) suivante :$$\begin{cases}
\partial_tv(t,x) + rx \partial_xv(t,x) + \frac{\sigma^2 x^2}{2} \partial_{xx}v(t,x)  - r v(t,x) = 0, \forall t \in [0,T[, x \gt 0 \\
v(T,x) = g(x)
\end{cases}$$Alors $$V_T^{p, \phi} = g(S_t)$$
Où $\underset{\text{Prime de l'option}}{\underline{p = v(0,S_0)}}$ et $\underset{\text{Delta Hedging}}{\underline{\phi_t = \partial_x v(t,S_t)}}$ 
Autrement dit, on peut répliquer l'option en utilisant la stratégie $\phi$ à partir d'un capital $p$
### Preuve
On applique la formule d'Itô à $(e^{-rt}v(t, S_t))_t$ : $$\begin{aligned}
d(e^{-rt}v(t, S_t)) &= -re^{-rt}v(t, S_t)dt + e^{-rt}dv(t, S_t) \\
&=e^{-rt}\partial_x v(t, S_t)\sigma S_t dW_t + e^{-rt}(\underset{\mu S_t \partial_x v(t, S_t) - rS_t\partial_x v(t, S_t)}{\underline{\partial_t v(t, S_t) + \mu S_t \partial_x v(t, S_t) + \frac{\sigma^2 x^2}{2}\partial_{xx} v(t, S_t) - r v(t, S_t)}})dt \\
&=\partial_x v(t, S_t) \left( (\mu - r)\tilde S_t dt + \sigma \tilde S_t dW_t \right) \\
&=\partial_x v(t, S_t)d \tilde S_t
\end{aligned}$$
On intègre entre $0$ et $T$ : $$\begin{aligned}
e^{-rt}v(T,S_T) &= v(0, S_0) + \int_0^T \partial_x v(t, S_t)d \tilde S_t \\
&= \tilde V_T^{p, \phi} \\
\iff g(S_t) &= e^{rt} \tilde V_T^{p,\phi} = V_T^{p, \phi}
\end{aligned}$$
### Remarque
Ce calcul nous dit aussi que $V_t^{p, \phi} = v(t, S_t)$, c'est la valeur de l'option au temps $t$ 
## Options américaines
On considère une option américaine de payoff $(g(S_t))_{t \in [0,T]}$ 
Soit alors $v : [0,T] \times \mathbb R_+ \longrightarrow \mathbb R$ satisfaisant l'inéquation variationnelle suivante :$$\begin{cases}
max \left( \underset{\le 0 \textcolor{yellow}{(1)}}{\underline{\mathcal Lv(t,x)}}, \underset{\le 0 \textcolor{yellow}{(1)}}{\underline{g(x) - v(t,x)}} \right) = 0, \forall t \in [0,T[, x \gt 0 \\
v(T,x) = g(x) \space\space\space \textcolor{red}{\underset{\text{Continuation \textcolor{yellow}{(2)}}}{\underline{\begin{cases}\mathcal Lv(t,x) = 0 \\ v(t,x) \gt g(x) \end{cases}}}\space\space\space \underset{\text{Exercice \textcolor{yellow}{(3)}}}{\underline{\begin{cases}\mathcal Lv(t,x) \le 0 \\ v(t,x) = g(x) \end{cases}}}}
\end{cases}$$Alors $$V_t^{p, \phi} \ge g(S_t), \forall t \in [0,T]$$et$$V_{\hat \tau}^{p, \phi} = g(S_t), \text{ où } \hat \tau = inf\{t \ge 0, v(t, S_t) = g(S_t)\}$$avec $p = v(0, S_0)$ et $\phi_t = \partial_x v(t, S_t)$ 
Autrement dit, on peut se couvrir en utilisant la stratégie $\phi$ à partir du capital $p$ quelle que soit la date d'exercice, et cette couverture et parfaite si la stratégie d'exercice est $\hat \tau$ (**~={yellow}stratégie optimale de l'acheteur=~**)
### Preuve
On suppose $r=0$ pour simplifier.
En particulier :$$
\mathcal Lv(t,x) = \partial_tv(t,x) + \frac{\sigma^2 x^2}{2}\partial_{xx} v(t,x) \textcolor{green}{\le 0}
$$
Par Itô, $$\begin{aligned}
\underset{\ge g(S_t) \textcolor{yellow}{\text{ par (1)}}}{\underline{v(t, S_t)}} &= v(0, S_0) + \int_0^t \partial_x v(s, S_s) \sigma S_s dW_s + \int_0^t \left( \underset{\le 0 \textcolor{yellow}{\text{ par (1)}}}{\underline{\partial_t v(s, S_s) + \frac{\sigma^2 S_s^2}{2}\partial_{xx} v(s, S_s)}} + \mu S_s \partial_x v(s, S_s) \right)ds \\
&\le \underset{p}{\underline{v(0, S_0)}} + \int_0^t \underset{\phi_s}{\underline{\partial_x v(s, S_s)}} \space\space\underset{dS_s}{\underline{(\sigma S_s dW_s + \mu S_s ds)}} \\
&=V_t^{p, \phi} \\
\iff g(S_t) &\le V_t^{p,\phi}
\end{aligned}$$On refait les calculs avec $\hat \tau$ :$$\begin{aligned}
\underset{= g(S_t)}{\underline{v(\hat \tau, S_{\hat \tau})}} &= v(0, S_0) + \int_0^{\hat\tau}\partial_x v(t,S_t) \sigma S_t dW_t + \int_0^{\hat\tau} \left( \underset{= 0 \textcolor{yellow}{\text{ par (2) car } g(S_t) \lt v(t,S_t), \forall t \lt \hat\tau}}{\underline{\partial_t v(t, S_t) + \frac{\sigma^2 S_t^2}{2} \partial_{xx} v(t, S_t)}} + \mu S_t \partial_x v(t, S_t) \right)dt \\
\iff g(S_{\hat\tau}) &= V_{\hat\tau}^{p, \phi}
\end{aligned}$$
### Remarque
En général, la fonction valeur n'est pas de classe $\mathcal C^{1,2} \textcolor{yellow}{\text{[c.f. (3) si g n'est pas } \mathcal C^2]}$ mais on peut raisonner de manière analogue avec des notions de dérivées faibles.
# Mesures martingales et pricing d'option
## Changement de mesure
### Définition
On dit qu'une mesure de probabilité $\mathbb Q$ est équivalente à $\mathbb P$ lorsque $$\forall A \in \mathcal F,\begin{matrix} \space\space\space\space\space\mathbb P(A) \gt 0 \iff \mathbb Q(A) \gt 0 \\ \text{ou }\mathbb P(A) = 0 \iff \mathbb Q(A) = 0 \\ \text{ou }\mathbb P(A) = 1 \iff \mathbb Q(A) = 1 \end{matrix}
$$
### Propriété
Si $\mathbb Q \sim \mathbb P$, alors $\exists H \gt 0$ v.a. tel que$$\mathbb E^{\mathbb Q}[X] = \mathbb E^{\mathbb P}[HX]$$On note $H = \frac{d \mathbb Q}{d \mathbb P}$
Réciproquement, si $H$ est une v.a. $\gt 0$ tel que $\mathbb E^{\mathbb P}[H] = 1$, alors $\mathbb Q: A \in \mathcal F \rightarrow \mathbb E^{\mathbb P}[H \mathbb 1_A]$ est une mesure de probabilité équivalente à $\mathbb P$ et $\frac {d \mathbb Q}{d \mathbb P} = H$ 
#### Preuve de la réciproque
$$ \begin{aligned} \text{(i)}\;& Q(\Omega) = \mathbb{E}^{\mathbb{P}}\!\left[ H \mathbb{1}_{\Omega} \right] = \mathbb{E}^{\mathbb{P}}[H] = 1. \\[0.6em] \text{(ii)}\;& Q(A \cup B) = \mathbb{E}^{\mathbb{P}}\!\left[ H \mathbb{1}_{A \cup B} \right] = \mathbb{E}^{\mathbb{P}}\!\left[ H(\mathbb{1}_A + \mathbb{1}_B) \right] \quad \text{si } A \cap B = \varnothing \\[0.4em] &= \mathbb{E}^{\mathbb{P}}\!\left[ H \mathbb{1}_A \right] + \mathbb{E}^{\mathbb{P}}\!\left[ H \mathbb{1}_B \right] = Q(A) + Q(B). \\[0.6em] \text{(iii)}\;& \mathbb{P}(A) = 0 \;\iff\; \mathbb{1}_A = 0 \quad \mathbb{P}\text{-p.s.} \;\iff\; H \mathbb{1}_A = 0 \quad \mathbb{P}\text{-p.s.} \\[0.4em] &\iff\; \mathbb{E}^{\mathbb{P}}\!\left[ H \mathbb{1}_A \right] = 0 \;\iff\; Q(A) = 0. \end{aligned} $$

### Théorème de Girsanov
Soient $\lambda \gt 0$ et $$H = e^{-\frac 12 \lambda^2 T +\lambda W_T}$$ Alors le processus $$ W_t^{\mathbb Q} = W_t - \lambda t, t \in [0,T] $$est un MB sous $\mathbb Q$ définie par $\frac {d \mathbb Q}{d \mathbb P} = H$ 
#### Remarque
On a bien $H \gt 0$ et $$\mathbb E^{\mathbb P}[H] = e^{- \frac{\lambda^2}{2}T} \mathbb E[e^{\lambda W_T}] = 1 $$
#### Preuve
Il est clair que $W_0^{\mathbb Q} = 0$ et $t \rightarrow W_t^{\mathbb Q}$ est continue
Il reste à montrer que $\forall 0 \le r \le s \le t \le T$, $$\mathbb E^{\mathbb Q}[g(W_r^{\mathbb Q})h(W_t^{\mathbb Q} - W_s^{\mathbb Q})] = \int \frac {e^{-\frac {x^2}{2r}}}{\sqrt{2 \pi r}} g(x)dx \int \frac {e^{-\frac {y^2}{2(t-s)}}}{\sqrt{2 \pi (t-s)}} h(y)dy $$ qui nous dit que, sous $\mathbb Q$ $$ W_r^{\mathbb Q} \sim \mathcal N(0,r), W_t^{\mathbb Q}-W_s^{\mathbb Q} \sim \mathcal N(0,t-s), W_r^{\mathbb Q} \perp\!\!\!\perp W_t^{\mathbb Q}-W_s^{\mathbb Q} $$
$$ \begin{aligned} \mathbb{E}^{\mathbb{Q}}\!\big[g(W_r^{\mathbb{Q}})\,h(W_t^{\mathbb{Q}}-W_s^{\mathbb{Q}})\big] &= \mathbb{E}^{\mathbb{P}}\!\Big[e^{-\frac12\lambda^2T+\lambda W_T}\, g(W_r^{\mathbb{Q}})\,h(W_t^{\mathbb{Q}}-W_s^{\mathbb{Q}})\Big] \\[0.6em] &= \mathbb{E}^{\mathbb{P}}\!\Big[ e^{-\frac12\lambda^2 r+\lambda W_r}\, g(W_r^{\mathbb Q})\, e^{-\frac12\lambda^2(s-r)+\lambda(W_s-W_r)} \\ &\hspace{4.2em}\times e^{-\frac12\lambda^2(t-s)+\lambda(W_t-W_s)}\, h(W_t^{\mathbb Q}-W_s^{\mathbb Q}) \\ &\hspace{4.2em}\times e^{-\frac12\lambda^2(T-t)+\lambda(W_T-W_t)} \Big] \\[0.8em] &= \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2 r+\lambda W_r}\, g(W_r-\lambda r)\big]\, \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2(t-s)+\lambda(W_t-W_s)} \\ &\hspace{7.5em}\times h(W_t-W_s-\lambda(t-s))\big] \\[0.6em] &\hspace{1em}\times \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2(s-r)+\lambda(W_s-W_r)}\big]\, \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2(T-t)+\lambda(W_T-W_t)}\big] \\[0.8em] &= \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2 r+\lambda W_r}\, g(W_r-\lambda r)\big]\, \mathbb{E}^{\mathbb{P}}\!\big[e^{-\frac12\lambda^2(t-s)+\lambda(W_t-W_s)} \\ &\hspace{7.5em}\times h(W_t-W_s-\lambda(t-s))\big] \\[0.8em] &= \int_{\mathbb{R}} e^{-\frac12\lambda^2 r+\lambda x}\, g(x-\lambda r)\,\frac{e^{-\frac{x^2}{2r}}}{\sqrt{2\pi r}}\,dx \\[0.6em] &= \int_{\mathbb{R}} g(x-\lambda r)\, \frac{e^{-\frac{(x-\lambda r)^2}{2r}}}{\sqrt{2\pi r}}\,dx \\[0.6em] &= \int_{\mathbb{R}} g(y)\, \frac{e^{-\frac{y^2}{2r}}}{\sqrt{2\pi r}}\,dy . \end{aligned} $$
## Probabilité risque neutre
On **construit** la ***probabilité risque neutre*** dans le **modèle de BS** par **Girsanov** en prenant $$\lambda = \frac{r-\mu}{\sigma}$$En effet $$\left. \begin{aligned}
S_t &= S_0 e^{(\mu - \frac{\sigma^2}{2})t + \sigma W_t} \\
&= S_0 e^{(\enclose{updiagonalstrike}{\mu} - \frac{\sigma^2}{2})t + \sigma(W_t^{\mathbb Q} + \frac{r - \enclose{updiagonalstrike}{\mu}}{\sigma}t)} \\
&=S_0 e^{(r - \frac{\sigma^2}{2})t + \sigma W_t^{\mathbb Q}} \\
\implies \tilde S_t &= e^{-rt}S_t \\
&=S_0e^{-\frac{\sigma^2}{2}t + \sigma W_t^{\mathbb Q}}
\end{aligned}\right|
\begin{aligned}
dS_t &= \mu S_t dt + \sigma S_t \underset{dW_t^{\mathbb Q} + \frac{r -\mu}{\sigma}dt}{\underline{dW_t}} \\
&=rS_t dt + \sigma S_t dW_t^{\mathbb Q} \\
\implies d \tilde S_t &=-r \tilde S_t dt + \underset{r \tilde S_t dt + \sigma \tilde S_t dW_t^{\mathbb Q}}{\underline{e^{-rt}dS_t}} \\
&=\sigma \tilde S_t dW_t^{\mathbb Q}
\end{aligned}$$Donc $(\tilde S_t)$ martingale sous $\mathbb Q$
### Remarque
En particulier $$ \mathbb E^{\mathbb Q}[S_t] = e^{rt}\mathbb E^{\mathbb Q}[\tilde S_t] =e^{rt}\tilde S_0 = e^{rt}S_0 $$i.e.,**~={yellow}les rendements de l'actif risqué sont identiques au placement sans-risques=~**
Plus généralement, $(\tilde V_t^{x, \phi})_{t \in [0,T]}$ est une martingale sous $\mathbb Q$. En effet $$ \tilde V_t^{x, \phi} = x + \int_0^t \phi_s d \tilde S_s = x + \int_0^t \phi_s \sigma \tilde S_s d W_s^{\mathbb Q} $$
### Application
On considère un payoff $G=g((S_t)_{t \le T}), \mathcal F_T-mesurable$ et on suppose que $G$ est réplicable, i.e., $\exists p \in \mathbb R$ et $\phi$ stratégie admissible tel que $$ G = V_T^{p, \phi} $$alors $$ p = \mathbb E^{\mathbb Q}[\tilde G] $$En effet, $$ \mathbb E^{\mathbb Q}[\tilde G] = \mathbb E^{\mathbb Q}[\tilde V_T^{p,\phi}] = \tilde V_0^{p, \phi} = p $$En particulier, si $G = g(S_t)$, on a vu que l'option est réplicable (par les EDP) et donc $$\begin{aligned}p = \mathbb E^{\mathbb Q}[e^{-rt}g(S_t)] \color{red}\underset{\text{forume de Feynman-Kac}}{=}v(0,S_0)  &\color{green}\longrightarrow \mathbb E^{\mathbb Q}[e^{-rT}g(S_T) | \mathcal F_t] = e^{-rT}v(t,S_t) \\&\color{green}\iff v(t,S_t) = E^{\mathbb Q}[e^{-r(T-t)}g(S_T) | \mathcal F_t]\end{aligned} $$
Pour pricer, nous utilisons du **Monte Carlo**
## Représentation Martingale
On peut montrer que toute martingale $(M_t)_{t \ge 0}$ par rapport à la filtration du MB est de la forme $$M_t = M_0 + \int_0^t \psi_s dW_s$$où $(\psi_s)$ adapté.
On en déduit que tout payoff $G, \mathcal F_t-mesurable$ satisfait $$\begin{aligned}
\tilde G &= \mathbb E^{\mathbb Q}[\tilde G] + \int_0^T \psi_s dW_s^{\mathbb Q} \\
&=\mathbb E^{\mathbb Q}[\tilde G] + \int_0^T \frac{\psi_s}{\sigma \tilde S_s}\underset{d \tilde S_s}{\underline{\sigma \tilde S_sdW_s^{\mathbb Q}}}\\
&=V_T^{p, \phi} \text{ où }\left|\begin{matrix}p = \mathbb E^{\mathbb Q}[\tilde G] \\ \phi_s = \frac{\psi_s}{\sigma \tilde S_s} \end{matrix} \right.
\end{aligned}$$On en conclut que le marché est complet et les prix des options est $$p = \mathbb E^{\mathbb Q}[\tilde G]$$Mais cela ne nous dit pas comment calculer la stratégie de couverture $\phi$ 
### Remarque
On peut étendre ces arguments pour les options américaines et prouver l'existence d'une stratégie $\phi$ telle que $$V_t^{p, \phi} \ge G_t, \forall t \in [0,T]$$où $$p = \underset{\tau \text{ temps d'arrêt }}{sup} \mathbb E^{\mathbb Q}[\tilde G_\tau] = \mathbb E^{\mathbb Q}[\tilde G_{\hat\tau}]$$avec $$\hat\tau = inf\{t \ge 0, V_t^{p, \phi} = G_t\}$$