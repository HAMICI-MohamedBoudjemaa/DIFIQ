# Calcul Stochastique multidimensionnel
## Mouvement Brownien
### Définition
$(W_t^1,....,W_t^m)_{t \ge 0}$ est un mouvement Browien en dimension $m \ge 1$ lorsque
1. $(W_t^i)_{t \ge 0}$ MB en dimension $1, \forall 1 \le i \le m$
2. $(W^1,...,W^m)$ sont indépendants
### Application
**BS** en dimension 2, 2 actifs risqués dont le prix est donné par $$\begin{aligned}
S_t^1 = S_0^1 e^{ \left((\mu_1 - \frac {\sigma_1^2}{2})t + \sigma_1 W_t^1 \right)} \\
S_t^2 = S_0^2 e^{ \left((\mu_2 - \frac {\sigma_2^2}{2})t + \sigma_2 (\rho W_t^1 + \sqrt{1 - \rho^2}W_t^2 \right)}
\end{aligned}$$Où$$\left| \begin{matrix} \mu_1, \mu_2 \in \mathbb R \text{ drifts}\\ \sigma_1, \sigma_2 \gt 0 \text{ volatilité}\\ S_0^1, S_0^2 \gt 0 \text{ volatilité} \\ \rho \in [-1, 1] \text{ paramètre de corrélation}\end{matrix} \right.$$
### Filtration
$\mathcal F_t = \sigma(W_s^1,...,W_s^m, s \le t)$
### Covariation quadratique
$\forall 1\le i,j \le m$,
$$\begin{aligned}
\langle W^i, W^j \rangle_t &= \underset{n \rightarrow +\infty}{lim}\sum_{k=1}^n (W_{t_k}^i - W_{t_{k-1}}^i)(W_{t_k}^j - W_{t_{k-1}}^j) \\ &= \begin{cases} t\text{ si } i = j\\ 0\text{ si } i \ne j\\ \end{cases}
\end{aligned}
$$En effet, en prenant $t_k = k \frac tn$, $$\begin{aligned}
\sum_{k=1}^n (W_{t_k}^i - W_{t_{k-1}}^i)(W_{t_k}^j - W_{t_{k-1}}^j) &= \frac tn \sum_{k=1}^n \frac{W_{t_k}^i - W_{t_{k-1}}^i}{\sqrt{t_k - t_{k-1}}} \frac{W_{t_k}^j - W_{t_{k-1}}^j}{\sqrt{t_k - t_{k-1}}}\\ &\underset{n \rightarrow + \infty}{\longrightarrow} t \mathbb E[ZZ'] = t\mathbb E[Z]\mathbb E[Z'] = 0, \\&\text{Par Loi des Grands Nombres }Z,Z' \text{ i.i.d } \mathcal N(0,1)
\end{aligned}$$
## Formule d'Itô
### Processus d'Itô
C'est un processus de la forme $$X_t  = X_0 + \int_0^t \mu_s ds + \sum_{j=1}^m \int_0^t \sigma_s^j dW_s^j $$
$$où \left|\begin{matrix} (\mu_t)_{t \ge 0} \text{ adapté } \int_0^t |\mu_s|ds \lt + \infty \\
(\sigma_t^j)_{t \ge 0} \text{ adapté } \mathbb E[\int_0^t (\sigma_s^j)^2 ds]
\end{matrix}\right.$$
### Covariation quadratique
$$\begin{aligned}
\langle X, \bar X \rangle_t &= \underset{n \rightarrow + \infty}{lim} \sum_{k=1}^n (X_{t_k} - X_{t_{k-1}})(\bar X_{t_k} - \bar X_{t_{k-1}}) \\
&= \sum_{j=1}^m \int_0^t \sigma_s^j \bar \sigma_s^j ds 
\end{aligned}$$
### Formule d'Itô
$\forall f : \mathbb R_+ \times \mathbb R \rightarrow \mathbb R, C^{1,2}$
$$\begin{aligned}
f(t, X_t) = f(0, X_0) + \int_0^t \partial_t f(s, X_s)ds + \int_0^t \partial_x f(s, X_s)\underset{\mu_s ds + \sum_{j=1}^m \sigma_s^j dW_S^j}{\underline{dXs}} + \frac 12 \int_0^t \partial_{xx} f(s, X_s)\underset{\sum_{j=1}^m (\sigma_s^j)^2 ds}{\underline{d\langle X\rangle s}}
\end{aligned}$$
#### Exemple
$$\begin{aligned}
dS_t^1 &= df(X_t^1) où \left| \begin{matrix} f(x) = e^x \rightarrow f'(x) = f''(x) = e^x \\ X_t^1 = ln(S_0^1) + (\mu_1 - \frac{\sigma_1^2}{2})t + \sigma_1 W_t^1 \end{matrix} \right.\\
&=\underset{\textcolor{green}{S_t^1}}{\underline{f'(X_t^1)}}\space\underset{\textcolor{red}{(\mu-\frac{\sigma_1^2}{2})dt + \sigma_1 dW_t^1}}{\underline{dX_t^1}} + \frac 12 \underset{\textcolor{green}{S_t^1}}{\underline{f''(X_t^1)}}\space \underset{\textcolor{red}{\sigma_1^2 dt}}{\underline{d \langle X^1\rangle_t}} \\
&= \mu_1 S_t^1 dt + \sigma_1 S_t^1 dW_t^1 \textcolor{green}{+ 0*dW_t^2}
\end{aligned}$$
$$\begin{aligned}
dS_t^2 &= df(X_t^2) où \left| \begin{matrix} f(x) = e^x \rightarrow f'(x) = f''(x) = e^x \\ X_t^2 = ln(S_0^2) + (\mu_2 - \frac{\sigma_2^2}{2})t + \sigma_2 (\rho W_t^1 + \sqrt{1-\rho^2}W_t^2) \end{matrix} \right.\\
&=f'(X_t^2)\underset{\textcolor{red}{(\mu-\frac{\sigma_2^2}{2})dt + \sigma_2 \rho dW_t^1 + \sigma_2\sqrt{1-\rho^2}dW_t^2}}{\underline{dX_t^2}} + \frac 22 f''(X_t^2) \underset{\textcolor{red}{\sigma_2^2 \rho^2 dt + \sigma_2^2(1-\rho^2)dt = \sigma_2^2 dt}}{\underline{d \langle X^2\rangle_t}} \\
&= \mu_2 S_t^2 dt + \sigma_2 S_t^2 (\rho dW_t^1 + \sqrt{1-\rho^2}dW_t^2) 
\end{aligned}$$
$$\langle S^1, S^2 \rangle_t = \int_0^t \sigma_1 S_t^1 \sigma_2 S_t^2 \rho dt$$
### Processus d'Itô en dimension $d$
C'est $X_t = (X_t^1,...,X_t^d)$ où $\forall 1 \le i \le d$ $$X_t^i = X_0^i + \int_0^t \mu_s^i ds + \sum_{j=1}^m \int_0^t \sigma_s^{i,j}dW_s^j
$$Est un **processus d'Itô en dimension 1**
#### Formule d'Itô en dimension $d$
$\forall f : \mathbb R_+ \times \mathbb R^d \longrightarrow \mathbb R, C^{1,2}$
$$\begin{aligned}
f(t, X_t) = f(0, X_0) &+ \int_0^t \partial_t f(s, X_s)ds \\
&+ \sum_{i=1}^d \int_0^t \partial_{x_i} f(s, X_s)\underset{\textcolor{red}{\mu_s^i ds + \sum_{k=1}^d \sigma_s^{ik} dW_s^k}}{\underline{dX_s^i}} \\
&+ \frac 12 \sum_{1 \le i\le j \le d}^d \int_0^t \partial_{x_i x_j} f(s, X_s) \underset{\textcolor{red}{\sum_{k=1}^m \sigma_s^{ik} \sigma_s^{jk}ds}}{\underline{d\langle X^i,X^j \rangle_s}}
\end{aligned}
$$
##### Exemple 1
Soit $(X_t)_{t \ge 0}$ et $(Y_t)_{t \ge 0}$ deux **processus d'Itô** en dimension 1$$ \begin{aligned} dX_t Y_t &= df(X_t,Y_t) \quad\text{où } f(x,y)=xy 
\left|\begin{matrix}\partial_x f(x,y) = y \\ \partial_y f(x,y) = x \\ \partial_{xx} f(x,y) = 0 \\ \partial_{yy} f(x,y) = 0 \\ \partial_{xy} f(x,y) = 1 \\ \end{matrix}\right. 
\\\\\\ &= \partial_x f(X_t,Y_t)\,dX_t + \partial_y f(X_t,Y_t)\,dY_t \\ &\quad + \tfrac12\,\partial_{xx}f(X_t,Y_t)\,d\langle X\rangle_t + \tfrac12\,\partial_{yy}f(X_t,Y_t)\,d\langle Y\rangle_t \\ &\quad + \partial_{xy}f(X_t,Y_t)\,d\langle X,Y\rangle_t \\ &= Y_t\,dX_t + X_t\,dY_t + \underset{\textcolor{red}{\text{(nouveau terme)}}}{\underline{d\langle X,Y\rangle_t}} \end{aligned} $$
##### Exemple 2 
$$
\begin{aligned}
df(t, S_t^1, S_t^2) &= \partial_t f(t, S_t^1, S_t^2) dt \\
&\quad + \partial_x f(t, S_t^1, S_t^2) dS_t^1 + \partial_y f(t, S_t^1, S_t^2) dS_t^2 \\
&\quad + \frac{1}{2} \partial_{xx} f(t, S_t^1, S_t^2) \underbrace{d\langle S^1 \rangle_t}_{(\sigma_1 S_t^1)^2 dt} + \frac{1}{2} \partial_{yy} f(t, S_t^1, S_t^2) \underbrace{d\langle S^2 \rangle_t}_{(\sigma_2 S_t^2)^2 dt} \\
&\quad + \partial_{xy} f(t, S_t^1, S_t^2) \underbrace{d\langle S^1, S^2 \rangle_t}_{\rho \sigma_1 \sigma_2 S_t^1 S_t^2 dt} \\
&= \partial_x f(t, S_t^1, S_t^2) dS_t^1 + \partial_y f(t, S_t^1, S_t^2) dS_t^2 \\
&\quad + \left[ \partial_t f(t, S_t^1, S_t^2) + \frac{1}{2} (\sigma_1 S_t^1)^2 \partial_{xx} f(t, S_t^1, S_t^2) \right. \\
&\quad \left. + \frac{1}{2} (\sigma_2 S_t^2)^2 \partial_{yy} f(t, S_t^1, S_t^2) + \rho \sigma_1 \sigma_2 S_t^1 S_t^2 \partial_{xy} f(t, S_t^1, S_t^2) \right] dt
\end{aligned}
$$
## Théorème de Girsanov
### Théorème
Soient $(\lambda_j)_{1 \le j \le m} \in \mathbb R^m$ et  $$H = exp \left(-\frac 12 \sum_{j=1}^m \lambda_j^2 T + \sum_{j=1}^m \lambda_j W_t^j \right)
$$Alors $$W_t^{\mathbb Q,j} = W_t^j - \lambda_j t \text{ avec } t \ge 0, 1 \le j \le m
$$est un MB en dimension $m$ sous la mesure $\mathbb Q$ définie par $\frac{d \mathbb Q}{d \mathbb P} = H$ 
# Modèle de BS en dimension 2
## Présentation
### Marché
- Taux d'intérêt sans risque $r \in \mathbb R$
- 2 actifs risqués
	- $S_t^1 = S_0^1 exp \left( (\mu_1 - \frac {\sigma_1^2}{2})t + \sigma_1 W_t^1 \right)$
	- $S_t^2 = S_0^2 exp \left( (\mu_2 - \frac {\sigma_2^2}{2})t + \sigma_2 (\rho W_t^1 + \sqrt{1 - \rho^2}W_t^2 \right)$ 
### Filtration
$$\begin{aligned}
\mathcal F_t &= \sigma(W_s^1,W_s^2,s \le t)\\
&=\sigma(S_s^1,S_s^2,s \le t) \text{ si }\rho \ne 1
\end{aligned}$$
### Portfolio
La valeur actualisée d'un portefeuille est $$
\tilde V_t^{x, \phi} = x + \int_0^t \phi_s^1 d \tilde S_s^1 + \int_0^t \phi_s^2 d \tilde S_s^2
$$$$où \left|\begin{matrix}x \in \mathbb R \text{ capital initial} \\
\phi = (\phi^1, \phi^2) \begin{cases} \phi_t^1 \text{\# actif de type 1 au temps t} \\ \phi_t^2 \text{\# actif de type 2 au temps t} \end{cases}
\end{matrix}\right.$$
# Taux d'intérêt stochastique
## Modèle de Vasicek (Exercice)
### Modèle
$dr_t = a(b -r_t) dt + \gamma d \bar W_t$
### Actif risqué
$dS_t = \mu_t S_t dt + \sigma S_t dW_t^1$
#### 1)
##### a)
$$\begin{aligned}
d \tilde S_t &= d(\beta_t S_t) \text{ où } \beta_t = e^{-\int_0^t r_s ds} \\
&= \beta_t dS_t + S_t d\beta_t + d\langle B, S \rangle_t\\
&= \beta_t(\mu_t S_t dt + \sigma S_t dW_t^1) - r_t \beta_t S_t dt + 0 \\
&= (\mu_t -r_t) \tilde S_t dt + \sigma \tilde S_t W_t^1
\end{aligned}$$
##### b)
On cherche $(\lambda_1 , \lambda_2) \in \mathbb R^2$ tel que $$\begin{aligned}
&\left|\begin{matrix} 
dS_t = r_t S_t dt + \sigma S_t (dW_t^1 - \lambda_1 dt) \\ 
dr_t = a(\bar b - r_t)dt + \gamma (\rho (dW_t^1 - \lambda_1 dt) + \sqrt{1 - \rho^2}(dW_t^2 - \lambda_2 dt)) 
\end{matrix}\right. \\\\
\iff&\left|\begin{matrix}
r_t-\lambda_1 \sigma = \mu_t \\
a \bar b - \rho \gamma \lambda_1 - \sqrt{1 - \rho^2} \gamma \lambda_2 = ab
\end{matrix}\right.\\\\
\iff&\left|\begin{matrix}
\lambda_1 = \frac{r_t \mu_t}{\sigma} = - \frac{\delta}{\sigma}\\
\lambda_2 = 0
\end{matrix}\right.
\end{aligned}$$
##### c)
Oui, $\mathbb Q$ est une probabilité risque neutre car $\mathbb Q \sim \mathbb P$ et $$d \tilde S_t = \sigma \tilde S_tdW_t^{\mathbb Q,1} \iff dS_t = r_t S_t d_t + \sigma S_t dW_t^{\mathbb Q,1}$$Non, elle n'est pas unique, on peut prendre n'importe quel $\lambda_2 \ne 0$. Cela ne change pas la dynamique $S$, seulement le paramètre $\bar b$
##### Remarque
La non-unicité de la probabilité risque-neutre est caractéristique des marchés incomplets
#### 2)
On admet que $$dB_t = r_t B_t dt - \gamma n_t B_t d\bar W_t^{\mathbb Q}$$
##### a) 
Par le théorème de représentation martingale : $$
\tilde G = \mathbb E^{\mathbb Q}[\tilde G] + \int_0^T \psi_t^1 dW_t^{\mathbb Q,1} + \int_0^T \psi_t^2 dW_t^{\mathbb Q,2}
$$On cherche les stratégies $\phi^1$ et $\phi^2$ telles que $$
\tilde G = \mathbb E^{\mathbb Q}[\tilde G] + \int_0^T \phi_t^1 \underset{\sigma \tilde S_t d W_t^{\mathbb Q,1}}{\underline{d\tilde S_t}} + \int_0^T \phi_t^2 \underset{-\gamma n_t \tilde B_t d\bar W_t^{\mathbb Q}}{\underline{d\tilde B_t}}
$$Donc le marché est complet
##### b) 
On suppose que $G = g(S_t)$
Pour trouver l'EDP, on considère que le prix de l'option est de la forme $v(t, S_t, r_t)$ et on applique Itô
$$
\begin{aligned}
d\left(B_t v(\underset{\color{red}{Z_t}}{\underbrace{t, S_t, r_t}})\right) &= -r_t B_t v(t, Z_t) dt + B_t \underset{\color{red}{\partial_x v(t, Z_t) dS_t + \partial_r v(t, Z_t) dr_t}}{\underline{dv(t, Z_t)}} \\
&\quad + \underset{\color{red}{(\partial_t v + \frac{\sigma^2 S_t^2}{2} \partial_{xx} v + \frac{\gamma^2}{2} \partial_{rr} v + \rho \gamma \sigma S_t \partial_{xr} v)(t, Z_t) dt}}{+} \\
\\
&= \partial_x v(t, Z_t) \underset{\color{blue}{d\tilde{S}_t}}{\underbrace{\color{blue}{\sigma \tilde S_t dW_t^{\mathbb{Q},1}}}} + \partial_r v(t, Z_t) \underset{\color{blue}{-\frac{1}{n_t B_t} d\tilde{B}_t}}{\underline{\gamma B_t d\bar{W}_t^{\mathbb{Q}}}} \\
&\quad + B_t \left( \underset{\color{green}{= 0}}{\underline{\partial_t v + \frac{\sigma^2 S_t^2}{2} \partial_{xx} v + \frac{\gamma^2}{2} \partial_{rr} v + \rho \gamma \sigma S_t \partial_{xr} v + r_t S_t \partial_x v + a(\bar{b} - r_t) \partial_r v - r_t v}} \right)(t, Z_t) dt \\
&= 0
\end{aligned}
$$
Ainsi, si $v$ est la solution de $$ \begin{aligned} \left\{ \begin{aligned} (&\partial_t v + \frac{\sigma^2 x^2}{2}\,\partial_{xx} v + \frac{\gamma^2}{2}\,\partial_{rr} v \\ &\quad + \rho\,\gamma\,\sigma x\,\partial_{xr} v + r x\,\partial_x v \\ &\quad + a(\bar b - r)\,\partial_r v - r v)(t,x,r) = 0, \\[0.3em] &v(T,x,r)=g(x), \end{aligned} \right. \\[0.6em] \text{alors} \\[0.4em] g(S_T)=V_T^{p,\phi} \\[0.6em]  \\[0.4em] \text{où }  \left\{ \begin{aligned}p &=v(0,S_0,r_0)\\ \phi_t^{1} &= \partial_x v(t,S_t,r_t), \\ \phi_t^{2} &= -\frac{1}{n_t B_t}\,\partial_r v(t,S_t,r_t). \end{aligned} \right. \end{aligned} $$
# Modèle a volatilité stochastique
On considère un modèle (**~={yellow}de Heston=~**) de la forme $$\left|\begin{matrix}
dS_t = rS_t dt + \sqrt{v_t}S_t dW_t^{\mathbb Q, 1}\\
dv_t = a(b-v_t)dt + \gamma \sqrt{v_t} d\bar W_t^{\mathbb Q}
\end{matrix}\right.$$
où $(W^{\mathbb Q, 1}, W^{\mathbb Q, 2})$ MB sous une probabilité risque neutre $\mathbb Q$.
Pour compléter le marché, on suppose qu'il existe un marché liquide pour les calls de strike $K$ et maturité $T$ dont le prix est donné par $$
C_t = \mathbb E^{\mathbb Q}[e^{-r(T-t)}(S_t, K)^+ | \mathcal F_t]
$$
Il reste à déterminer la dynamique de $(C_t)_{t \ge 0}$. On peut raisonner comme dans la section précédente et chercher le prix du call sous la forme $$C_t = c(t, S_t, v_t)$$et on voit que c'est solution de $$\left|\begin{matrix} (\partial_tc + rx \partial_x c + a(b-v)\partial_v c + \frac{vx^2}{2}\partial_{xx}c + \frac{\gamma^2 v}{2}\partial_{vv}c + \rho \gamma vx \partial_{xv}c -rc)(t,x,v) = 0\\
c(T,x,v) = (x-K)^+
\end{matrix}\right.$$et$$dC_t = r C_t dt + \partial_x c(t,S_t,v_t)\sqrt{v_t}S_t dW_t^{\mathbb Q,1} +\partial_v c(t, S_t, v_t)\gamma \sqrt{v_t}d \bar W_t^{\mathbb Q} $$