# Formulation
## Marché :
- $1$ actif sans risque :$$dS_t^0 = r S_t^0 dt \text{ où } r \gt 0 \iff S_t^0 = S_0^0 e^{rt}$$
- 1 actif risqué :$$dS_t = \mu S_t dt + \sigma S_t dW_t \text{ où } \mu \in \mathbb R, \sigma \gt 0 \iff S_t = S_0 e^{((\mu - \frac {\sigma^2}{2})t + \sigma W_t)}$$
- Stratégie : $\alpha_t$ (**~={orange}processus adapté=~**) proportion de richesse investie dans l'actif risqué au temps $t$ $$(\alpha_t)_{t \ge 0} \text {processus adapté à valeurs dans } \begin{aligned} &\mathbb R (\text {vente à découvert possible}) \\ &\text{ ou } \\ &[0,1] (\text{ pas de vente à découvert })\end{aligned}$$
- Portefeuille / Richesse $X_t$: $$\begin{aligned} d X_t &= \frac{\alpha_t X_t}{S_t} dS_t + \frac {(1-\alpha_t)_t}{S_t^0}dS_t^0 \\
  &= \alpha_t X_t(\mu dt + \sigma dW_t) + (1-\alpha_t) X_t rdt \\
  &= (r + (\mu -r) \alpha_t)X_t dt + \sigma \alpha_t X_t dW_t
  \end{aligned}$$
- But : Déterminer une stratégie d'investissement optimale au sens où $(\alpha_t)_{t \ge 0}$ maximise $$\mathbb E [U( X_T)]$$où U est une **~={yellow}fonction d'utilité=~**, ie, $U' \ge 0$ 
	 - $U$ **~={yellow}croissante=~** $\iff U' \ge 0$
	 - $U$ **~={yellow}concave=~** $\iff U' décroissante \iff U'' \le 0$ 
## Formule d'Itô
Pour $f : [0,T] \times \mathbb R_+ \longrightarrow \mathbb R$ **régulière** $$\begin{aligned}f(T, X_T) &= f(t, X_t) + \int_t^T \partial_t f(s, X_s) ds + \int_t^T \partial_x f(s, X_s) \underset{(r+(\mu-r)ds)X_s ds + \sigma \alpha_s X_s dW_s}{dX_s} + \frac 12 \int_t^T \partial_{xx} f(s,X_s) \underset{\sigma^2 \alpha_s^2X_s^2ds}{d \langle X \rangle_s} \\
&= f(t,X_t) + \int_t^T \partial_x f(s, X_s) \sigma \alpha_s X_s dW_s + \int_t^T\left[ \partial_t f(s, X_s) + (r+(\mu -r)\alpha_s)X_s \partial_x f(s,X_s) + \frac 12 \sigma^2 \alpha_s^2 X_s^2 \partial_{xx} f(s,X_s) \right]
\end{aligned}$$ où pourtant $s \in [0,T], x \in \mathbb R_+, a \in A$ $$\mathcal L^a f(s,x) = \partial_t f(s,x) + (r + (\mu -r)a)x \partial_x f(s,x) + \frac 12 \sigma^2 a^2 x^2 \partial_{xx} f(s,x)$$
Ex : $$f(t,x) = ln(x) \longrightarrow \begin{aligned} &\partial_t f(t,x) = 0 \\ &\partial_x f(t,x) = \frac 1x \\ &\partial_{xx} f(t,x) = -\frac {1}{x^2}\end{aligned}$$
$$\begin{aligned}
\mathcal L^a f(t,x) &= 0 + (r+(\mu-r)a)x * \frac 1x +\frac 12 \sigma^2 a^2 x^2 * \left( -\frac {1}{x^2}\right) \\
&= r+(\mu -r) a - \frac 12 \sigma^2 a^2
\end{aligned}$$
$$\begin{aligned}ln(X_T) &= f(T,X_T) \\
&=f(t,X_t) + \int_t^T \mathcal L^{\alpha_s} f(s,X_s)ds + \int _t^T \underset{=\frac {1}{X_s}}{\underline{\partial_x f(s,X_s)}} \sigma \alpha_s X_s dW_s \\
&= ln(X_t) + \int_t^T(r+(\mu-r)\alpha_s - \frac 12 \sigma^2\alpha_s^2)ds + \int_t^T\sigma \alpha_s dW_s
\end{aligned}$$
En passant à exp $$X_t = X_t \space exp \left( \int_t^T(r+(\mu - r) \alpha_s - \frac 12 \sigma^2 \alpha_s^2)ds + \int_t^T \sigma \alpha_s dW_s\right)$$
## Fonction valeur
### Definition
Pour tout $t \in [0,T], x \in \mathbb R_+$ $$v(t,x) = \underset{\alpha \text{ stratégie}}{sup} \mathbb E \left[U\left(X_T^{t,x,\alpha}\right)\right]$$où $$X_t^{t,x,\alpha} = x \space exp\left(\int_t^T \left(r + (\mu - r)\alpha_s  - \frac 12 \sigma^2 \alpha_s^2\right)ds + \int_t^T \sigma \alpha_s dW_s\right)$$
$v(t,x)$ **~={green}est la performance de la stratégie optimale=~**
#### Remarque
- $v(T,x) = U(x)$
- $v(t, 0) = U(0)$
#### Idée
C'est l'***~={cyan}analyse de la fonction valeur=~*** qui est la clé de la résolution du problème. Par exemple :
- si $v(t,x) \gt v(t,y)$ on préfère être en $x$ qu'en $y$ à l'instant $t$
- On peut aussi comparer  $v(t,x)$ avec $v(t+h, xe^{rh})$ 
	- Si $v(t,x) \gt v(t+h, xe^{rh})$ on aurait du investir dans l'actif risqué (car la fonction valeur est supérieure en $t$ qu'en $t+h$) et ce, d'autant plus que l'écart est grand
	- $v(t,x) \le v(t+h, xe^{rh})$, on doit tout investir dans l'actif sans risque
## Equation de Hamilton-Jacobi-Bellman
### Théorème
On suppose qu'il existe $u : [0,T]  \times  \mathbb R_+ \longrightarrow \mathbb R$ régulière satisfaisant :$$\begin{cases}\underset{a \in A}{sup} \left\{ \mathcal L_u^a(t,x)\right\} =0  &\forall t \in [0,T], x \in \mathbb R_+ \\u(T,x) = U(x) & \forall x \in \mathbb R_+
\end{cases}$$et $$\begin{aligned} &â : [0,T] \times \mathbb R_+ \longrightarrow \mathbb R \\
\text{tq} : &â(t,x) = \underset{a \in A}{argmax} \left\{\mathcal L^a u(t,x)\right\}\end{aligned}$$
Alors $u = v$ et $\hat\alpha_t = â(t,X_t)$ **~={green}est la stratégie optimale=~**
#### Preuve
1. On commence par appliquer Itô avec la fonction $u$ pour une stratégie $\alpha$ :$$\mathbb E \left[u(T, X_T^{t,x,\alpha})\right] = u(t,x) + 0 + \mathbb E \left[\int_t^T \mathcal L^{\alpha_s}u(s,X_s^{t,x,\alpha}) ds\right]$$d'où $$u(t,x) \ge \underset{\alpha}{sup} \space \mathbb E\left[ U(X_T^{t,x,\alpha})\right] = v(t,x)$$
2. On refait les calculs avec $\hat\alpha_t = \hat\alpha(t,X_t)$ : $$\mathbb E \left[u(T, X_T^{t,x,\hat\alpha})\right] = u(t,x) + \mathbb E \left[\underset{\underset{a \in A}{sup} \space \mathcal L^a u(s,X_s^{t,x,\alpha}) = 0}{\underline{\int_t^T \mathcal L^{\hat\alpha_s}u(s,X_s^{t,x,\hat\alpha}) ds}}\right]$$d'où $$u(t,x) = \mathbb E\left[U(X_T^{t,x,\hat\alpha})\right] \le \underset{\alpha}{sup} \space \mathbb E \left[ U(X_T^{t,x,\alpha})\right] = v(t,x=)$$
3. On conclut que $$v(t,x) = u(t,x) = \mathbb E\left[U(X_T^{t,x,\hat\alpha}) \right]$$
#### Remarque
On peut montrer que la fonction valeur est solution de l'équation de HJB en utilisant le principe de la programmation dynamique $$v(t,x) = \underset{\alpha}{sup} \space \mathbb E \left[v(t+h,X_{t+h}^{t,x,\alpha}) \right]$$
## Exemple
On considère une fonction d'utilité CRRA (**~={cyan}Constant relative risk aversion=~**) de la forme $$U(x) = x^\gamma$$où $0 \lt \gamma \lt 1$ est le paramètre d'aversion au risque (**~={red}Plus $\gamma$ es petit, plus la courbe est concave, plus on est averse au risque=~**)
Et on suppose que $A = \mathbb R$
On cherche une solution de HJB sous la forme $$u(t,x) = x^\gamma f(t)$$où $f : [0,T] \longrightarrow \mathbb R_+$ à déterminer
On a $$\begin{aligned} &\partial_t u(t,x) = x^\gamma f'(t) \\
&\partial_x u(t,x) = \gamma x^{\gamma-1} f(t) \\
&\partial_xx u(t,x) = -\gamma(1-\gamma)x^{\gamma-2} f(t)
\end{aligned}$$
$$\begin{aligned}
\mathcal L^a u(t,x) &= x^\gamma f'(t) + (r+(\mu -r) a)x * \gamma x^{\gamma-1}f(t) + \frac 12 \sigma^2 \alpha^2 x^2 * (-\gamma(1-\gamma)x^{\gamma-2}f(t)) \\ 
&= x^\gamma\left[ f'(t) + (r\gamma + (\mu -r) \gamma a - \frac 12 \sigma^2 \gamma (1-\gamma) a^2) f(t)\right]
\end{aligned}$$
On cherche $f$ tel que : $$\begin{aligned}&\underset{a \in \mathbb R}{sup} \left\{\mathcal L^a u(t,x) \right\} = 0 \\
&\iff \underset{a \in \mathbb R}{sup} \left\{ f'(t) + r\gamma + (\mu-r) \gamma a - \frac 12 \sigma^2 \gamma(1-\gamma) f(t)\right\} = 0 \\
&\iff f'(t) + \underset{a \in \mathbb R}{sup}\left\{ r\gamma + (\mu-r)\gamma a - \frac 12 \sigma^2 \gamma(1-\gamma) a^2\right\}f(t) = 0 \\
&\iff f'(t) + Kf(t) = 0 \\
&\iff f(t) = f(0)e^{-Kt}
\end{aligned} $$
#### Rappel 
Le maximum d'un polynôme de la forme $$P(x) = ax^2 + bx + c$$où $a \lt 0$, est atteint au sommet $\hat x = - \frac {b}{2a}$
C'est aussi la solution de $P'(x) = 0$

**~={yellow}On en déduit que =~**:
Le maximum est atteint en$$\hat a = - \frac {(\mu -r)\gamma}{2(-\frac 12 \sigma^2 \gamma (1-\gamma))} = \frac {\mu-r}{\sigma^2(1-\gamma)}$$Et vaut : $$r \gamma + \frac {(\mu - r)^2 \gamma}{2\sigma^2(1-\gamma)}$$
On veut aussi que $$\begin{aligned}
u(T,x) = x^\gamma &\iff f(T) = 1 \\
&\iff f(0) = e^{KT} | \text{ car } f(T)=f(0)e^{-KT}
\end{aligned}$$
On  vient de montrer que $u(t,x) = x^\gamma e^{K(T-t)}$ est solution de HJB. On en déduit que $$v(t,x) = u(t,x) = x^\gamma e^{K(T-t)}$$et la stratégie optimale consiste à investir une proportion de richesse $$\hat \alpha = \frac {\mu - r}{\sigma^2(1-\gamma)}$$
dans l'actif risqué à chaque instant quelque soit le niveau de richesse