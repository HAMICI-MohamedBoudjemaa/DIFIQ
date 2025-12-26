# Une première présentation
On suppose que $T = 2$ périodes
## Marché
- Taux d'intérêt sans risque $r \gt 0$ sur chaque période
- Actif risqué
```mermaid
 graph LR
 subgraph A["S"]
 direction LR
 S0(""$$S_0$$"") --> uS0("$$uS_0$$")
 S0 --> dS0("$$dS_0$$")
 uS0 --> uuS0("$$u^2S_0$$")
 uS0 --> udS0("$$udS_0$$")
 dS0 --> ddS0("$$d^2S_0$$")
 dS0 --> udS0("$$udS_0$$")
 end
 
 subgraph B["C"]
 direction LR
 C0(""$$C_0$$"") --> C1uS0("$$C_1(uS_0)$$")
 C0 --> C1dS0("$$C_1(dS_0)$$")
 C1uS0 --> guuS0("$$g(u^2S_0)$$")
 C1uS0 --> gudS0("$$g(udS_0)$$")
 C1dS0 --> gddS0("$$g(d^2S_0)$$")
 C1dS0 --> gudS0("$$g(udS_0)$$")
 end
  A --- B
 ```
## Hypothèse
~={yellow} $d \lt 1+r \lt u$ =~
## Option
On considère une option de payoff $g(S_2)$ et on cherche à déterminer un portefeuille de couverture.
On peut raisonner par récurrence rétrograde :
- $t = 2$ : le prix de l'option correspond à son payoff $g(S_2)$
- $t=1$ : Il s'agit d'une option expirant dans une période et donc on peut raisonner comme dans le **chapitre 1**, étant donné $S_1$, on a :
	- $C_1(S_1) = \frac {1}{1+r}(q \space g(uS_1) + (1-q) \space g(dS_1))$
	- $\phi_1 = \frac {g(uS_1) - g(dS_1)}{uS_1 - dS_1}$
- $t = 0$ : Il s'agit d'un produit dérivée de payoff $C_1(S_1)$ dans une période :
	- $C_0 = \frac {1}{1+r}(q \space C_1(uS_0)  + (1-q) \space C_1(dS_0)) = \frac {1}{(1+r)^2}(q^2 g(u^2S_0) + 2q(1-q) g(udS_0) + (1-q)^2 g(d^2S_0)$
	- $\phi_0 = \frac {C_1(uS_0) - C_1(dS_0)}{uS_0 - dS_0}$
	
# Notions de probabilité
## Processus stochastique
C'est une famille $X = (X_0,X_1,...,X_T)$ *(qu'on écrit aussi $(X_t)_{t \in \{0,...,T\}}$)* de v.a. décrivant l'évolution d'un phénomène aléatoire au cours du temps, e.g., le cours d'une action
## Filtration de $X$
C'est le flux d'information $\mathcal (F_t)_{t \in \{0,..,T\}}$ associé à l'évolution $X$, i.e., $\mathcal F_t = \sigma(X_0,...,X_t)$ correspond ç l'ensemble des évènements qui ne dépendent que de la réalisation de $(X_0,...,X_t)$
## Adapté
On dit qu'un processus $Y$ est adapté à la filtration lorsque $Y_t$ est $\mathcal F_t-mesurable \space \forall t \in \{0,...,T\}$, i.e., $Y_t = f(X_0,...,X_t)$.
~={yellow}Connaitre $(X_0,...,X_t)$ c'est connaître $Y_t$ =~
## Martingales
On dit qu'un processus $Y$ est ***martingale par rapport à la filtration*** lorsque $$\mathbb E[Y_{t+1} | \mathcal F_t] = Y_t, \forall t \in \{0,...,T-1\}$$
Ou de manière équivalente :$$\mathbb E[Y_s | \mathcal F_t] = Y_t, \forall 0 \le t \le s \le T$$
## Espérance conditionnelle
Soit $B \subset \Omega$ tel que $\mathbb P(B) \gt 0$, on rappelle que $$\mathbb P(A|B) = \frac {\mathbb P(A \cap B)}{\mathbb P(B)}, \forall A \subset \Omega$$
Soient $X,Y$ v.a. on peut définir $$\mathbb E[X |Y=y] = \sum_{x \in X(\Omega)} x \space \mathbb P(X=x | Y=y), \forall y \in Y(\Omega)$$
Et également $$\begin{aligned} 
\mathbb E[X|\sigma(Y)](\omega) &= \mathbb E[X | Y](\omega) \\
&= \mathbb E[X|Y=y] \space si \space Y(\omega) = y
\end{aligned}$$
En particulier, $\mathbb E[X|Y]$ est une **Variable Aléatoire** $\sigma(Y)-mesurable$ (~={yellow} $\mathbb E[X|Y]$ est connue si $Y$ est connue=~)
*Exemple* : $X \sim U(\{1,..,6\})$ le résultat d'un dé
$$Y = \begin{cases}
1 \space si \space X \space pair \\
0 \space sinon
\end{cases}$$
$$\begin{aligned}
\mathbb E[X | Y=1] &= \sum_{x=1}^6 x &\underline{\mathbb P(X = x | Y = 1)} \\
&&= \frac {\mathbb P(X=x, Y=1)}{\mathbb P(Y=1)}\\
&&= \begin{cases} 0 \space si \space x \space est \space impair \\ \frac {\mathbb P(X=x)}{\mathbb P(Y=1)} = \frac {1/6}{1/2} = \frac 13\end{cases} \\
&= 2 * \frac 13 + 4* \frac 13 + 6 * \frac 13 \\
&= 4
\end{aligned}$$
$$\mathbb E[X | Y=0] = 1 * \frac 13 + 3 * \frac 13 + 5 * \frac 13 = 3$$
$$\mathbb E[X|Y](\omega) = \begin{cases} 4 \space si \space Y(\omega) = 1 \\ 3 \space si \space Y(\omega) = 0\end{cases}$$
### Propriétés
1. Si $X \perp\!\!\!\perp Y$, alors $\mathbb E[X|Y] = \mathbb E[X]$
2. Si $X$ est $\sigma(Y) - mesurable$, alors $\mathbb E[X|Y] = X$
3. $\mathbb E[\mathbb E[X|Y]]= \mathbb E[X]$ 
### Preuve
1. Si $X \perp\!\!\!\perp Y$, alors $$\begin{aligned}
   \mathbb E[X|Y=y] &= \sum_{x \in X(\Omega)} x \space \mathbb P(X=x|Y=y) \\
   &= \sum_{x \in X(\Omega)} x \space \mathbb P(X=x) \\
   &= \mathbb E[X]
   \end{aligned}$$
2. Si X est $\sigma(Y)-mesurable$, alors $X = f(Y)$ et $$\begin{aligned}
   \mathbb E[X|Y=y] &= \sum_{x \in X(\Omega)} x \space \mathbb P(X=x|Y=y) \\
   &= \sum_{x \in X(\Omega)} x \space \mathbb P(f(Y)=x|Y=y) \\
   &= \sum_{x \in X(\Omega)} x \times \space \begin{cases} 1 \space si \space x=f(y) \\ 0 \space sinon\end{cases} \\
   &=f(y)
   \end{aligned}$$
   $$\mathbb E[X|Y](\omega) = f(Y(\omega)) = X(\omega)$$
3. $$\begin{aligned}
   \mathbb E[\mathbb E[X|Y]] &= \sum_{y \in Y(\Omega)} \mathbb E[X|Y=y] \mathbb P(Y=y) \\
   &= \sum_y \sum_x x \space \mathbb P(X=x|Y=y) \mathbb P(Y=y) \\
   &= \sum_y \sum_x x \space \frac {\mathbb P(X=x,Y=y)}{\enclose{updiagonalstrike}{\mathbb P(Y=y)}} \enclose{updiagonalstrike}{\mathbb P(Y=y)} \\
   &= \sum_x x \sum_y \mathbb P(X=x, Y=y) \\
  par \space proba \space totale &= \sum_x x\mathbb P(X=x) \\
   &= \mathbb E[X]
   \end{aligned}$$
## Conséquence
Une martingale est nécessairement un processus adapté et d'espérance constante.
En effet $$\mathbb E[Y_t] = \mathbb E[\mathbb E[Y_t | \mathcal F_0]] = \mathbb E[Y_0]$$
# Le modèle revisité
## Description
### Espace de Probabilité
- $\Omega = \{\omega_u, \omega_d\}^T$, i.e., $\omega = (\omega_1,...,\omega_T)$ avec $\omega_t \in \{\omega_u, \omega_d\}$
- $\mathcal F = \mathcal P(\Omega)$
- $\mathbb P(\omega) \gt 0, \forall \omega \in \Omega$
### Marché
- Taux d'intérêt sans risque $r \gt 0$ fixé sur chaque période
- Actif risqué $S_0 \gt 0$ fixé et $$S_{t+1}(\omega) = \begin{cases}uS_t(\omega) \space si \space \omega_{t+1} = \omega_u \\ dS_t(\omega) \space si \space \omega_{t+1} = \omega_d\end{cases}$$*Ex* :~={green} $\omega = (\omega_u, \omega_u, \omega_d)$ =~ou~={red} $\omega = (\omega_d, \omega_u, \omega_d)$ =~
```mermaid
 graph LR
 S0(""$$S_0$$"") --> uS0("$$uS_0$$"):::green
 S0 --> dS0("$$dS_0$$"):::red
 uS0 --> uuS0("$$u^2S_0$$"):::green
 uS0 --> udS0("$$udS_0$$")
 dS0 --> ddS0("$$d^2S_0$$")
 dS0 --> udS0("$$udS_0$$"):::red
 uuS0 --> uuuS0("$$u^3S_0$$")
 uuS0 --> uudS0("$$u^2dS_0$$"):::green
 udS0 --> uudS0("$$u^2dS_0$$")
 udS0 --> uddS0("$$ud^2S_0$$"):::red
 ddS0 --> uddS0("$$ud^2S_0$$")
 ddS0 --> dddS0("$$d^3S_0$$")
 classDef red stroke:#f00
 classDef green stroke:#0f0
```
- $\mathcal F_t = \sigma(\enclose{updiagonalstrike}{S_0}, S_1,.....,S_t)$ filtration de S
### Portefeuille
- $x \in \mathbb R$ capital initial
- $(\phi_t)_{t \in \{0,....,T-1\}}$ stratégie, i.e. $\phi_t$ $\#$ **actif risqué entre** $t$ et $t+1$ ($\phi$ processus adapté, i.e., $\phi_t \space \mathcal F_t-mesurable$)
- Valeur $$\begin{aligned}
  &V_t^{x,\phi} = \underset{risqué}{\phi_t S_t} + \underset{sansRisque}{(V_t^{x,\phi} - \phi_t S_t)} \\ 
  &V_{t+1}^{x,\phi} = \underset{risqué}{\phi_t S_{t+1}} + \underset{sansRisque}{(V_{t}^{x,\phi} - \phi_t S_t)(1+r)} \\
  \implies &\frac {V_{t+1}^{x,\phi}}{(1+r)^{t+1}} = \frac {\phi_t S_{t+1} + (V_{t}^{x,\phi} - \phi_t S_t)\enclose{updiagonalstrike}{(1+r)}}{(1+r)^{t+\enclose{updiagonalstrike}{1}}} \\
  \implies &\tilde V_{t+1}^{x,\phi} = \phi_t \tilde S_{t+1} + \tilde V_t^{x,\phi} - \phi_t \tilde S_t \\
  \implies &\tilde V_{t+1}^{x,\phi} = \tilde V_t^{x,\phi} +\phi_t (\tilde S_{t+1}  -\tilde S_t) \\
  mais \space puisque \space &\tilde V_{t}^{x,\phi} = \tilde V_0^{x,\phi} + \sum_{s=0}^{t-1}(\tilde V_{s+1}^{x,\phi} - \tilde V_{s}^{x,\phi}) \\
  \implies &\tilde V_{t}^{x,\phi} = x + \sum_{s=0}^{t-1}\phi_s(\tilde S_{s+1}^{x,\phi} - \tilde S_{s}^{x,\phi})
  \end{aligned}$$où $\tilde X_t = \frac {X_t}{(1+r^t)}$ ~={yellow}**valeur actualisée**=~
## Arbitrage et Martingale
### Arbitrage
C'est une stratégie $\phi$ tq $$V_t^{0,\phi} \ge 0, \forall \omega \in \Omega \space \text{et} \space \exists \omega \in \Omega, V_t^{0,\phi}(\omega) \gt 0$$ Autrement dit : $$\mathbb P(V_t^{0,\phi} \ge 0) = 1 \text{ et } \mathbb P(V_t^{0,\phi} \gt 0) \gt 0$$
### Hypothèse
On suppose $d \lt 1+r \lt u$
### Probabilité risque neutre
On considère la probabilité $\mathbb Q$ tel que les rendements $\left( \frac {S_t}{S_{t+1}}\right)_{t \in \{1,...,T\}}$ sont indépendants et de même loi $$\begin{aligned}
\mathbb Q(\frac {S_t}{S_{t+1}} = u) &= 1 - \mathbb Q(\frac {S_t}{S_{t+1}} = d) \\
&= q = \frac {1+r-d}{u-d} \in ]0,1[
\end{aligned}$$
### Martingales
On observe que $(\tilde S_t)_{t \in \{0,...,T\}}$ est une $\mathbb Q-martingale$. En effet $$\begin{aligned}
\mathbb E^{\mathbb Q}[\tilde S_{t+1} | \mathcal F_t] &= \mathbb E^{\mathbb Q} \left[\tilde S_t \frac {S_{t+1}}{S_t}| \mathcal F_t \right] \\
&= \tilde S_t \mathbb E\left[\frac {\tilde S_{t+1}}{\tilde S_t}\right] \Bigg| \color{yellow}{ \text{ car } \tilde S_t \space \mathcal F_t-mes \text{ et } \frac {\tilde S_{t+1}}{\tilde S_t} \perp\!\!\!\perp \mathcal F_t \text { sous } \mathbb Q}\\
&= \tilde S_t \space \underset{\color{yellow}{=1}}{\underline{(q\frac {u}{1+r} + (1-q) \frac {d}{1+r})}} \\
&=\tilde S_t \\
\iff \mathbb E^{\mathbb Q}[S_{t+1} | \mathcal F_t] &= (1+r)S_t
\end{aligned}$$
De plus, $(\tilde V_t^{x,\phi})_{t  \in \{0,...,T\}}$ est une $\mathbb Q-martingale$ 
En effet $$\begin{aligned}
\mathbb E^{\mathbb Q}[\tilde V_{t+1}^{x,\phi} | \mathcal F_t] &= \mathbb E^{\mathbb Q}[\tilde V_{t}^{x,\phi} + \phi_t(\tilde S_{t+1}^{x,\phi} - \tilde S_{t}^{x,\phi})|\mathcal F_t) \\
&=\tilde V_{t}^{x,\phi} + \phi_t \mathbb E^{\mathbb Q}[\tilde S_{t+1}^{x,\phi} - \tilde S_{t}^{x,\phi} | \mathcal F_t] \\
&=\tilde V_{t}^{x,\phi} + \phi_t (\mathbb E^{\mathbb Q}[\tilde S_{t+1}^{x,\phi} | \mathcal F_t] - \tilde S_{t}^{x,\phi}) \\
&=\tilde V_{t}^{x,\phi} + \phi_t (\tilde S_{t}^{x,\phi} - \tilde S_{t}^{x,\phi}) \\
&= \tilde V_{t}^{x,\phi}
\end{aligned}$$
En particulier $$\begin{aligned}
\mathbb E^{\mathbb  Q}[\tilde V_{t}^{x,\phi}] = \mathbb E^{\mathbb  Q}[\tilde V_{0}^{x,\phi}] = \tilde V_{0}^{x,\phi} = x \\ 
\iff \mathbb E^{\mathbb  Q}[ V_{t}^{x,\phi}] = (1+r)^T x
\end{aligned}$$
### Conséquence
On peut en déduire l'AOA. En effet, soit $\phi$ stratégie tel que $\forall \omega, V_t^{0,\phi}(\omega) \ge 0$, on a donc$$\begin{aligned}
\mathbb E^{\mathbb Q}[V_T^{0,\phi}] &= 0 =(1+r)^T*0 \color{yellow}{\text{ comme vu plus haut}} \\
&=\sum_{\omega \in \Omega}\underset{\ge 0}{\underline{V_T^{0,\phi}(\omega)}} \space \space \underset{\gt 0}{\underline{\mathbb Q(\omega)}} \\
\implies &V_T^{0,\phi}(\omega) = 0, \forall \omega \in \Omega \\
\implies &\enclose{updiagonalstrike}{\exists}\omega, V_T^{0,\phi}(\omega) = 0 \\
\implies &\color{green}{\text{pas d'arbitrage}}
\end{aligned}$$
## Option Européenne
On considère un payoff de la forme $g(S_t)$ et on cherche à construire un portefeuille de couverture, i.e., trouver $x \in \mathbb R$ et une stratégie $(\phi_t)$ tel que $$V_t^{x,\phi} = g(S_t)$$
### Remarque
Si on a trouvé ce portefeuille de couverture, alors le prix de réplication de l'option est~={yellow} l'espérance actualisée sous $\mathbb Q$  de $g(S_t)$ =~$$\begin{aligned}
\mathbb E^{\mathbb Q}\left[\frac {g(S_t)}{(1+r)^T} \right] &= \mathbb E^{\mathbb Q}\left[\tilde V_T^{x,\phi} \right] = \color{lightgreen}{x} \\
&= \sum_{k=0}^T\left( \begin{matrix}T \\ k \end{matrix} \right)q^k(1-q)^{T-k}\frac {g(u^kd^{T-k}S_0)}{(1+r)^T}
\end{aligned}$$
L'idée est de déterminer le prix $Y_t$ de l'option et la stratégie $\phi_t$ par récurrence rétrograde
- $t=T$ : $Y_T = g(S_T) \color{red}{= C_T(S_T)}$
- $t = T-1$ : $$\begin{aligned}
  &\phi_{T-1}S_t + (Y_{T-1} - \phi_{T-1} S_{T-1})(1+r) = g(S_T) = Y_T \\
  \iff &\begin{cases}
	  \phi_{T-1}uS_{T-1} + (Y_{T-1} - \phi_{T-1} S_{T-1})(1+r) = g(uS_{T-1}) \\
	  \phi_{T-1}dS_{T-1} + (Y_{T-1} - \phi_{T-1} S_{T-1})(1+r) = g(dS_{T-1})
	  \end{cases} \\
  \iff &\begin{cases}
	  \phi_{T-1} = \frac {g(uS_{T-1}) - g(dS_{T-1})}{uS_{T-1} - dS_{T-1}} \Bigg| \color{red}{\mathcal F_{T-1}-mesurable}\\
	  Y_{T-1} = \frac{1}{1+r}\big(q*g(uS_{T-1}) + (1-q) * g(dS_{T-1})\big) \color{red}{= C_{T-1}(S_{T-1})}
	  \end{cases}
  \end{aligned}$$
- $t \rightarrow t-1$ : Nous utilisons la même méthode, mais en passant par $C_t$ au lieu de $g$  $$\begin{aligned}
  &\phi_{t-1}S_t + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = Y_t \color{green}{= C_t(S_t)} \\
  \iff &\begin{cases}
	  \phi_{t-1}uS_{t-1} + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = C_t(uS_{t-1}) \\
	  \phi_{t-1}dS_{t-1} + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = C_t(dS_{t-1})
	  \end{cases} \\
  \iff &\begin{cases}
	  \phi_{t-1} = \frac {C_t(uS_{t-1}) - C_t(dS_{t-1})}{uS_{t-1} - dS_{t-1}} \Bigg| \color{red}{\mathcal F_{t-1}-mesurable} \\
	  \begin{aligned}Y_{t-1} &= \frac{1}{1+r} \textcolor{yellow}{\big(q*C_t(uS_{t-1}) + (1-q) * C_t(dS_{t-1}) \big)}\\
	  &= \frac {1}{1+r} \textcolor{yellow}{\mathbb E^{\mathbb Q}[Y_t | \mathcal F_{t-1}]}\end{aligned}
	  \end{cases}
  \end{aligned}$$
  Ceci permet de déterminer $Y_0 \in \mathbb R$ et la stratégie $(\phi_t)_{t \in \{0,...,T-1\}}$. On peut vérifier que $$V_t^{Y_0, \phi} = Y_t$$ et on a bien ~={yellow}construit un portefeuille de couverture=~
### Remarque 2
$(\tilde Y_t)_{t \in \{0,...,T\}}$ est une $\mathbb Q-martingale$ donc $$\begin{aligned}
&\tilde Y_t = \mathbb E^{\mathbb Q}[\tilde Y_{t+1} |\mathcal F_t] \iff Y_t = \frac {1}{1+r} \mathbb E^{\mathbb Q}[Y_{t+1}|\mathcal F_t] \\ &et \\
&\tilde Y_t = \mathbb E^{\mathbb Q}[\tilde Y_T | \mathcal F_t] \iff Y_t = \frac {1}{(1+r)^{T-t}} \mathbb E^{\mathbb Q}[g(S_T) | \mathcal F_t]
\end{aligned}$$
Plus généralement, on considère un payoff de la forme $g(S_1,...,S_T)$ et on peut de la même manière construire un portefeuille de réplication.
- $t=T$ : $Y_T = g(S_1,...,S_T) \color{red}{= C_T(S_1,...,S_T)}$
- $t \rightarrow t-1$ :   $$\begin{aligned}
  &\phi_{t-1}S_t + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = Y_t \color{green}{= C_t(S_1,...,S_t)} \\
  \iff &\begin{cases}
	  \phi_{t-1}uS_{t-1} + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = C_t(S1,...,uS_{t-1}) \\
	  \phi_{t-1}dS_{t-1} + (Y_{t-1} - \phi_{t-1} S_{t-1})(1+r) = C_t(S1,...,dS_{t-1})
	  \end{cases} \\
  \iff &\begin{cases}
	  \phi_{t-1} = \frac {C_t(S1,...,S_{t-1},uS_{t-1}) - C_t(S1,...,S_{t-1},dS_{t-1})}{uS_{t-1} - dS_{t-1}} \Bigg| \color{red}{\mathcal F_{t-1}-mesurable} \\
	  \begin{aligned}Y_{t-1} &= \frac{1}{1+r} \textcolor{yellow}{\big(q*C_t(S1,...,S_{t-1},uS_{t-1}) + (1-q) * C_t(S1,...,S_{t-1},dS_{t-1})) \big)}\\
	  &= \frac {1}{1+r} \textcolor{yellow}{\mathbb E^{\mathbb Q}[Y_t | \mathcal F_{t-1}]} \end{aligned}
	  \end{cases}
  \end{aligned}$$
==Le marché est complet==
## Option Américaine
### Couverture
#### Payoff
$G_t$ si l'option est exercé à l'instant $t$ ($\color{red} (G_t)_{t \in \{0,...,T\}} adapté, i.e., \mathcal F_t-mes$) 
#### Réplication
On cherche à construire un portefeuille de réplication. On raisonne par récurrence rétrograde sur $Y_t$, ~={yellow}prix de l'option américaine au temps t, si pas exercée avant=~ \~={green}[autrement dit, émise en $t$]=~
	- $t = T$ : $Y_t = G_t = C_t^{US}(S_1,....,S_t)$
	- $t+1 \rightarrow t$  : 
		- <u><b>Si exercice en  t :</u></b>   $Y_t = G_t$ et on n'a plus besoin de couvrir
		- <u><b>Sinon, si continuation :</u></b> On cherche $Y_t$ et $\phi_t$ tel que $$
		  \begin{aligned}
		  &\phi_t S_{t+1} + (Y_t - \phi_t S_t)(1+r) = Y_{t+1} = C_{t+1}^{US}(S_1,...,S_t+1) \\
		  \iff &\begin{cases} \phi_t uS_{t} + (Y_t - \phi_t S_t)(1+r) = C_{t+1}^{US}(S_1,...,uS_t) \\\phi_t dS_{t} + (Y_t - \phi_t S_t)(1+r) = C_{t+1}^{US}(S_1,...,dS_t) \end{cases} \\
		  \iff &\begin{cases} 
			  \phi_t = \frac {C_{t+1}^{US}(S_1,...,uS_t) - C_{t+1}^{US}(S_1,...,dS_t)}{uS_t - dS_t} \\ 
			  \begin{aligned}  
			  Y_t &= \frac {1}{1+r}  \textcolor{yellow}{\big(q*C_{t+1}^{US}(S1,...,S_{t},uS_{t}) + (1-q) * C_{t+1}^{US}(S1,...,S_{t},dS_{t})) \big)} \\
			   &= \frac {1}{1+r} \textcolor{yellow}{\mathbb E^{\mathbb Q}[Y_{t+1} | \mathcal F_{t}]}
			   \end{aligned} \end{cases}
		  \end{aligned}$$
#### Conclusion
$Y_t = \textcolor{yellow}{max(G_t, \frac {1}{1+r} \mathbb E^{\mathbb Q}[Y_{t+1} | \mathcal F_{t}])}$
#### Remarque
Si $G_t = g(S_t)$ (*à comprendre, $G_t$ fonction de $S_t$*) alors $$Y_t =  max\bigg(g(S_t), \Big(q*C_{t+1}^{US}(uS_{t}) + (1-q) * C_{t+1}^{US}(dS_{t}) \Big)\bigg)$$
### Temps d'arrêt et exercice
#### Temps d'arrêt
C'est une v.a. $\tau : \Omega \rightarrow \{0,1,...,T\}$ telle que $\{\tau \le t\} \in \mathcal F_t$, i.e. on sait si $\tau \le t$ au temps $t$
Dans ce cas, on a aussi $$\begin{aligned} \{\tau \ge t+1\} 
= &\{\tau \gt t\}  = \{\tau \le t\}^C \in {\mathcal F_t} \\
&\{\tau = t\}  = \{\tau \le t\} \cap \{\tau \gt t-1\} \in {\mathcal F_t}
\end{aligned}$$
- *Exemple* :
	- $\tau = 2$ temps d'arrêt *(t.a.)*
	- $\tau = min\{t \in \{0,...,T\}, S_t \ge 100\}$ t.a. car $$\{\tau \le t\} = \{S_0 \ge 100\} \cup \{S_1 \ge 100\} \cup ....\cup \{S_t \ge 100\} \in \mathcal F_t$$
	- $\tau = max\{t \in \{0,...,T\}, S_t \ge 100\}$ t.a. car $$\{\tau \le t\} = \{S_0 \lt 100\} \cap \{S_1 \lt 100\} \cap ....\cap \{S_t \lt 100\} \enclose{updiagonalstrike}{\in} \mathcal F_t$$
- On va montrer que l'option US est $$Y_0 = \underset {\tau \space t.a.}{max} \space \mathbb E^{\mathbb Q}[\tilde G_\tau] = \mathbb E^{\mathbb Q}[\tilde G_{\hat \tau}]$$ ou $\hat \tau = min\{t \in \{0,...,T\}, Y_t = G_t \}$ $\color{yellow}\text{(minimum des temps t, où le payoff }G_t \text{ coincide avec le prix } Y_t )$ 
#### Remarque
$\tau$ correspond à une stratégie d'exercice pour l'acheteur et $\hat \tau$ est la stratégie optimale
#### Preuve
On suppose $r=0$, sinon on travaille avec $\tilde Y$.
$\underline Cas\ge$ : Par définition $$\begin{aligned}
&Y_t = max(G_t, \mathbb E^{\mathbb Q}[Y_{t+1}|\mathcal F_t]) \ge G_t, \forall t \in \{0,...,T\} \\
\implies & Y_\tau \ge G\tau, \forall \tau \space t.a. \\
\implies & \mathbb E^{\mathbb Q}[Y_\tau] \ge \mathbb E^{\mathbb Q}[G\tau] \\
\text{il reste à montrer que } &\mathbb E^{\mathbb Q}[Y_\tau] \ge Y_0 : \\
&\begin{aligned}\mathbb E^{\mathbb Q}[Y_\tau] &= \mathbb E^{\mathbb Q}[Y_\tau \mathbb 1_{\tau \le T-1} + Y_T \mathbb 1_{\tau = T}] \\
&= \mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-1} + \mathbb E^{\mathbb Q}[Y_T \mathbb 1_{\tau \gt T-1}|\mathcal F_{T-1}]\right] \textcolor{red}{\text{| car } \mathbb E^{\mathbb Q}[\mathbb E^{\mathbb Q}[-|\mathcal F_t]] = \mathbb E^{\mathbb Q}[-]}\\
&= \mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-1} + \mathbb 1_{\tau \gt T-1}\mathbb E^{\mathbb Q}[Y_T |\mathcal F_{T-1}]\right] \\
&\le \mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-1} + Y_{T-1} \mathbb 1_{\tau \gt T-1}\right]\textcolor{red}{\text{| car } Y_{T-1} = max(G_{T-1},\mathbb E^{\mathbb Q}[Y_T |\mathcal F_{T-1}] )} \\
&=\mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-2} + Y_{T-1} \mathbb 1_{\tau \ge T-1}\right] \end{aligned}\\
\text{on réitère comme avec t-1}
&\begin{aligned}
\space\space\space\space\space\space\space\space\space\space\space\space &=\mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-2} + \mathbb E^{\mathbb Q}[Y_{T-1} |\mathcal F_{T-2}]\mathbb 1_{\tau \gt T-2} \right] \\
&\le \mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le T-2} + Y_{T-2} \mathbb 1_{\tau \gt T-2}\right] \\.\\.\\.\\.
&\le \mathbb E^{\mathbb Q}\left[Y_\tau \mathbb 1_{\tau \le 0} + Y_{0} \mathbb 1_{\tau \gt 0}\right] \\
&\le \mathbb E^{\mathbb Q}\left[Y_0 \mathbb 1_{\tau \le 0} + Y_{0} \mathbb 1_{\tau \gt 0}\right] \\
&= Y_0
\end{aligned}
\end{aligned}$$Ce qui montre que $$\begin{aligned}
&Y_0 \ge \mathbb E^{\mathbb Q}[Y_\tau] \ge \mathbb E^{\mathbb Q}[G_\tau], \forall \tau \space t.a.\\
\implies &Y_0 \ge \underset{\tau \space t.a}{max} \space \mathbb E^{\mathbb Q}[G_\tau]
\end{aligned}$$
$\underline Cas\le$ : Pour l'inégalité réciproque, on refait les calculs avec $\tilde \tau = min\{t \in \{0,...,T-1\}, Y_t = G_t\}$ $$\begin{aligned}
\mathbb E^{\mathbb Q}[G_{\hat \tau}] &= \mathbb E^{\mathbb Q}[Y_{\hat \tau}] \textcolor{red}{\text{|car }G_{\hat \tau} = Y_{\hat \tau} \text{ par définition}}\\
&=\mathbb E^{\mathbb Q}\left[Y_{\hat \tau} \mathbb 1_{\hat \tau \le T-1} + \mathbb E^{\mathbb Q}[Y_T|\mathcal F_{T-1}]\mathbb 1_{\hat \tau \gt T-1}\right]\\
&=\mathbb E^{\mathbb Q}\left[Y_{\hat \tau} \mathbb 1_{\hat \tau \le T-2} + Y_{T-1}\mathbb 1_{\hat \tau \ge T-1}\right]\\&.\\&.\\&.\\
&= Y_0
\end{aligned}$$ Donc $Y_0 = \mathbb E^{\mathbb Q}[G_{\hat \tau}]$ 
#### Conclusion
$$\begin{aligned}
&\underset{\tau \space t.a}{max}\space \mathbb E^{\mathbb Q}[G_{\tau}] \le Y_0 = \mathbb E^{\mathbb Q}[G_{\hat \tau}] \le \underset{\tau \space t.a}{max}\space \mathbb E^{\mathbb Q}[G_{\tau}] \\
\implies &Y_0 = \underset{\tau \space t.a}{max}\space \mathbb E^{\mathbb Q}[G_{\tau}] = \mathbb E^{\mathbb Q}[G_{\hat \tau}]
\end{aligned}$$
## Option à barrières
On considère un payoff de la forme $$g(S_t) \mathbb 1_{max\{S_t\}\lt B}$$avec $t \in \{0,...,T\} \space et \space B>0$ 
*Ex* : $g(S_t) = (S_t-K)^+$ 
On va construire un portefeuille de couverture en calculant de manière rétrograde le prix $Y_t$ de l'option à barrière issue à la date $t$
- $t = T$ : $Y_T = g(S_T) \mathbb 1_{S_T<B} = \color{red} C_T^B(S_T)$ 
- $t+1 \rightarrow t$ : 
	- si $S_t \ge B$ : $Y_t = 0$
	- si $S_t < B$ : On cherche $Y_t$ et $\phi_t$ tel que $$\begin{aligned}
	  &Y_{t+1} =\phi_tS_{t+1} + (Y_t-\phi_t S_t) = \color{red} C_{t+1}^B(S_{t+1})\\
	  \implies Y_t &= \frac {1}{1+r} \mathbb E^{\mathbb Q}[Y_{t+1}|\mathcal F_t]\\
	  &= \frac {1}{1+r} (q \space C_{t+1}^B(uS_{t})+ (1-q) \space C_{t+1}^B(dS_{t}))\\
	  \end{aligned}$$ On a donc $$\begin{cases}\phi_t = \frac {C_{t+1}^B(uS_{t}) - C_{t+1}^B(dS_{t})}{uS_{t} - dS_{t}} \\
	  Y_t = \frac {1}{1+r} \mathbb E^{\mathbb Q}[Y_{t+1} | \mathcal F_t] \mathbb 1_{S_t \lt B}
	  \end{cases}$$
### Remarque
On écrit aussi le payoff sous la forme $$\begin{aligned}
g(S_t) \mathbb 1_{\tau \gt T}\\\\
avec \space \tau = inf\{t \ge 0, S_t \ge B\}
\end{aligned}$$
