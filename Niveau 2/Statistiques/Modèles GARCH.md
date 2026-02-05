# Généralités
## Exemple de séries temporelles
Nous pouvons énumérer différents exemples de séries temporelles, pouvant présenter des tendances dans le temps (croissance, saisonnalité, répétition)
Citons par exemple :
- Les bruits blancs![[Pasted image 20260203164809.png]]
- La population US (**courbe croissante, exponentielle ?**)![[Pasted image 20260203164830.png]]
- Nombre mensuel de passages aériens (**tendance haussière et pattern répété**)![[Pasted image 20260203164859.png]]
- Nombre annuel de Lynx capturés au Canada (**saisonnalité**)![[Pasted image 20260203164928.png]]
## Processus stochastiques
## Série temporelle
- Soit $(x_t)_{t \in \mathcal T}$ une famille d'observations d'un phénomène qui peut être physique, économique, biologique
- Chaque observation $x_t$, dans $\mathbb R^d$, a été enregistrée ) à un temps spécifique $t \in \mathcal T$ et on appelle ~={red}**série temporelle**=~ cet ensemble d'observations
## Terminologie
- On considère des séries temporelles sur $\mathcal T$
- Si $\mathcal T$ est dénombrable (en général $\mathcal T  \subset \mathbb Z$), on parle de série temporelle **~={red}à temps discret=~**
- Si $\mathcal T$ n'est pas dénombrable (en général un intervalle de $\mathbb R$), on parle de série temporelle **~={red}à temps continu=~**
## Processus stochastique
- $(X_t)_{t \in \mathcal T}$ est un **processus**, ou **processus aléatoire**, ou encore ***~={red}processus stochastique=~***, si pour tout $t \in \mathcal T$ fixé, $X_t$ est une variable aléatoire
## Hypothèses de travail
- On considère désormais que la série temporelle est la réalisation d'un processus
- On ne s'intéresse pas ici à la loi du processus mais aux relations linéaires qui le sous-tendent
- On considère des processus univariés à temps discret 
## Bruits blancs
- $(\varepsilon_t)_{t \in \mathbb Z}$ est un bruit blanc fort s'il est constitué de ***~={yellow}v.a.r. indépendantes=~***, et si :$$\begin{aligned}
\forall t \in \mathbb Z : &\mathbb E(\varepsilon_t) = 0 \\
&\mathbb E (\varepsilon_t^2) = \sigma^2
\end{aligned}$$$\sigma^2$ sera considéré strictement positif dans la suite
- $(\varepsilon_t)_{t \in \mathbb Z}$ est un bruit blanc gaussien si c'est un bruit blanc fort constitué de v.a.r. de loi $\mathcal N(0, \sigma^2)$
- $(\varepsilon_t)_{t \in \mathbb Z}$ est un bruit blanc faible si :$$\begin{aligned}
\forall t \in \mathbb Z : &\mathbb E(\varepsilon_t) = 0 \\
&\mathbb E (\varepsilon_t^2) = \sigma^2 \\
\forall(t, t') \in \mathbb Z^2 /t \ne t' : &Cov(\varepsilon_t, \varepsilon_{t'})  =0
\end{aligned}$$
## Processus du second ordre
- On dit que $(X_t)_{t \in \mathbb Z}$ est un **~={red}processus du second ordre=~** s'il admet à chaque instant des moments d'ordre 2
## Notion de stationnarité
- Dans de très nombreux cas, on ne peut pas renouveler la suite de mesures dans des conditions identiques
- Pour que le modèle déduit à partir d'une suite d'observations ait un sens, il faut que toute portion de la trajectoire observée fournisse des informations sur la loi du processus et que des ***~={cyan}portions différentes, mais de même longueur, fournissent les mêmes indications=~***
- D'où la notion de stationnarité
## Processus (faiblement) stationnaire
- Un processus $(X_t)_{t \in \mathbb Z}$ du second ordre est **~={red}faiblement stationnaire=~** si son espérance et ses autocovariances sont invariantes par translation dans le temps :
	- $\forall t \in \mathbb Z : \mathbb E (X_t) = \mu$
	- $\forall (s,t) \in \mathbb Z^2, \forall h \in \mathbb Z : Cov (X_s, X_t) = Cov(X_{s+h}, X_{t+h})$ 
## Fonction d'autocovariance
- On appelle fonction d'autocovariance d'un processus $(X_t)_{t \in \mathbb Z}$ stationnaire la fonction $\gamma$ suivante : $\forall h \in \mathbb Z : \gamma (h) = Cov(X_t, X_{t-h})$ 
- $\gamma$ est une fonction symétrique :$$\forall h \in \mathbb Z : \gamma(-h) = \gamma (h)$$On pourra donc calculer la fonction d'autocovariance pour $h \in \mathbb N$
## Autocorrélogramme simple
- On appelle autocorrélogramme simple d'un processus $(X_t)_{t \in \mathbb Z}$ stationnaire la fonction $\rho$ suivante : $$\forall h \in \mathbb Z : \rho (h) = Cov( X_t, X_{t-h}) = \frac {\gamma (h)}{\gamma (0)}$$
- On a $|\rho (h)| \le \rho(0) = 1$ 
## Autocorrélogramme partiel
- On appelle autocorrélogramme partiel d'un processus $(X_t)_{t \in \mathbb Z}$ stationnaire la fonction $r$ suivante :
	- $r(0) = 1$
	- $r(1) = \rho (1)$
	- $\forall h \in \mathbb N \backslash \{0,1\}$ : $$r(h) = Corr (X_t, X_{t-h} / X_{t-1}, \dots, X_{t-h+1})$$
## Estimation des moments pour les processus stationnaires : Espérance
- L'estimateur naturel (consistant et sans biais) de $\mathbb E(X_t) = \mu$ à partir $(X_1, \dots, X_t)$ est la moyenne empirique $\bar X_t$ : $$\hat \mu =\bar X_T$$ avec $\bar X_T = \frac 1T \sum_{i=1}^T X_i$
## Estimation des moments pour les processus stationnaires : Autocorrélations
- A partir de $(X_1, \dots X_T)$, on peut considérer les estimateurs suivants : $$\forall h \in \mathbb N^* : \hat \gamma(h) = \frac {1}{T-h} \overset{T}{\underset{t=h+1}{\sum}}(X_t - \bar X_T)(X_{t-h} - \bar X_T)$$
- On en déduit : $$\forall h \ge 1 : \hat \rho (h) = \frac {T}{T-h} \frac {\sum_{t=h+1}^T (X_t - \bar X_T)(X_{t-h} - \bar X_T)}{\sum_{t=1}^T (X_t - \bar X_T)^2}$$
- Les estimations des autocorrélations partielles se déduisent des estimations des autocorrélations simples grâce à l'algorithme de Durbin-Levinson
## Test de Portmanteau
- On considère le test suivant pour un processus stationnaire $(X_t)_{t \in \mathbb Z}$ :$$\begin{cases} 
  H_0 : \rho(1) = \dots = \rho(k) = 0\\
  H_1 : H_0 \text{ est fausse}
  \end{cases}$$
- Si on dispose de $(X_1, \dots, X_T)$, on considère la statistique de **~={red}Portmanteau=~** (calculée sur les *k premières estimations* des autocorrélations) : $$Q_k = T \overset{k}{\underset{h=1}{\sum}} \hat \rho ^2 (h)$$
- Une trop grande valeur de $Q_k$ indique que les autocorrélations sont trop importantes pour être celles d'un bruit blanc
- Il existe d'autres versions de cette statistique, par exemple la  statistique de **~={red}Ljung-Box=~** : $$Q_k^* = T(T+2) \overset{k}{\underset{h=1}{\sum}} \frac {\hat\rho^2(h)}{T-h}$$
	- Sous $H_0, Q_k$ (ainsi que $Q_k^*$) suit asymptotiquement une loi du Khi-deux à k degrés de liberté : $$Q_k \overset{\mathcal L}{\rightarrow} \mathcal X^2 (k)$$
	- On rejette donc l'hypothèse $H_0$ au niveau de test $\alpha$ si :$$Q_k \gt \mathcal X_{k, 1-\alpha}^2$$où $X_{k, 1-\alpha}^2$ désigne le quantile d'ordre $1- \alpha$ d'une loi du Khi-deux à $k$ degrés de liberté
	- La p-valeur vaut : $$\text{p-valeur} = \mathbb P(\mathcal X_k^2 \ge Q_k)$$
# Modèle GARCH
## Introduction
- De nombreuses séries financières font l'objet d'études : cours d'action, taux d'intérêt, taux de change, etc...
- A partir d'un cours d'action $X_t$, on travaille souvent sur les variations relatives : $$\tau_t = \frac {X_t - X_{t-1}}{X_{t-1}} = \frac {X_t}{X_{t-1}} - 1$$ou le rendement : $$r_t = ln \left( \frac {X_t}{X_{t-1}}\right) = ln( 1 + \tau_t)$$
- La stationnarité de telles séries n'est pas forcément remise en cause, on ut même souvent considérer qu'on a affaire à des bruits blancs (oscillations ponctuellement élevées mais pas sur des périodes longues)
- La densité de telles séries fait souvent apparaitre des queues de distribution épaisses, plus que celles d'une loi normale (hypothèse utilisée lors de l'estimation de processus ARMA)
- L'hypothèse de variance conditionnelle constante est peu compatible avec le comportement de ces séries, on parle là d'hétéroscédasticité conditionnelle
## Processus ARCH et GARCH
### Modèle conditionnellement hétéroscédastique
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus conditionnellement hétéroscédastique si : $$X_t = \sigma_t \varepsilon_t$$où 
	- $(\varepsilon_t)_{t \in \mathbb Z}$ est une suite de v.a.r. i.i.d. centrées et de variance 1
	- $\sigma_t$ est mesurable par rapport à la tribu engendrée par le passé de $X_t$ : $$\mathcal F_{-\infty}^{t-1}(X) = \sigma (X_s, s \in \mathbb Z, s \le t-1)$$
	- $\varepsilon_t$ est indépendant de $\mathcal F_{-\infty}^{t-1}(X)$ 
	- $\sigma_t \gt 0$ ($\sigma_t$ est la volatilité du processus)
- On trouve parfois dans la littérature $h_t$ au lieu de $\sigma_t$ avec $\sigma_t = \sqrt{h_t}$ 
- On trouve parmi les modèles pour les processus conditionnellement hétéroscédastiques : 
	- Les modèles **~={red}ARHC=~** (***autorégressifs conditionnellement hétéroscédastiques***), introduits par Engle (1982)
	- Les modèles **~={red}GARCH=~** (***ARCH Généralisés***), introduits par Bollerslev (1986)
### Modèle ARCH
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d.
- on dit que $(X_t)_{t \in \mathbb Z}$ est un processus **ARCH(q)** (au sens fort) si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &\sigma_t^2 = \omega + \overset {q}{\underset{i=1}{\sum}} \alpha_i X_{t-i}^2
  \end{aligned}$$où $\omega \in \mathbb R^{+*}$ et $(\alpha_1, \dots, \alpha_q) \in \mathbb R^{+^{q}}$ 
- En toute rigueur il faudrait supposer en sus que $\alpha_q \in \mathbb R^{+*}$ pour que l'ordre du ARCH soit bien $q$
### Modèle GARCH
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d.
- on dit que $(X_t)_{t \in \mathbb Z}$ est un processus **GARCH(p,q)** (au sens fort) si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &\sigma_t^2 = \omega + \overset {q}{\underset{i=1}{\sum}} \alpha_i X_{t-i}^2 + \overset {p}{\underset{j=1}{\sum}} \beta_j \sigma_{t-j}^2
  \end{aligned}$$où $\omega \in \mathbb R^{+*}$ et $(\alpha_1, \dots, \alpha_q, \beta_1, \dots, \beta_q) \in \mathbb R^{+^{p+q}}$ 
- On peut également considérer des processus GARCH non centrés : $$\forall t \in \mathbb Z : X_t = \mu + \sigma_t \varepsilon_t$$
### Stationnarité
### Exemple : Processus ARCH(1)
- On considère : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &\sigma_t^2 = \omega + \alpha X_{t-1}^2
  \end{aligned}$$où $\omega \in \mathbb R^{+*}$ et $\alpha \in \mathbb R^+$
- On suppose ici que $(\varepsilon_t)_{t \in \mathbb Z}$ est une suite i.i.d. de loi $\mathcal N(0,1)$
#### Espérance du processus ARCH(1)
- On a : $$\begin{aligned}
  \mathbb E(X_t | \mathcal F_{-\infty}^{t-1}(X)) &= \mathbb E(\sigma_t \varepsilon_t | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \sigma_t \mathbb E(\varepsilon_t) \\
  &= 0
  \end{aligned}$$car $\sigma_t \in \mathcal F_{-\infty}^{t-1}(X)$ et $\varepsilon_t \perp\!\!\!\perp \mathcal F_{-\infty}^{t-1}(X)$
- D'où : $$\mathbb E(X_t) = 0$$
#### Variance du processus ARCH(1)
- On a :$$\begin{aligned}
  Var(X_t | \mathcal F_{-\infty}^{t-1}(X)) &= \mathbb E(X_t^2 | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \mathbb E(\sigma_t^2 \varepsilon_t^2 | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \sigma_t^2 \mathbb E(\varepsilon_t^2 | \mathcal F_{-\infty}^{t-1}(X)) \text{ car } \sigma_t \in \mathcal F_{-\infty}^{t-1}(X) \\
  &= \sigma_t^2 \mathbb E(\varepsilon_t^2) \text{ car } \varepsilon_t \perp\!\!\!\perp \mathcal F_{-\infty}^{t-1}(X)
  \end{aligned}$$
- D'où $$\begin{aligned}
  Var(Xt) &= \mathbb E(X_t^2) \\
  &= \mathbb E \left[\mathbb E (X_t^2 | \mathcal F_{-\infty}^{t-1}(X)) \right] \\
  &= \mathbb E(\omega + \alpha X_{t-1}^2) \\
  &= \omega + \alpha \mathbb E(X_{t-1}^2)
  \end{aligned}$$
- De la stationnarité on déduit : $$Var(X_t) = \frac {\omega}{1 - \alpha}$$
#### Kurtosis du processus ARCH(1)
- On a : $$
  \begin{aligned}
  \mathbb E (X_t^4 | \mathcal F_{-\infty}^{t-1}(X)) &=  \mathbb E (\sigma_t^4 \varepsilon_t^4 | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \sigma_t^4 \mathbb E (\varepsilon_t^4 | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \sigma_t^4 \mathbb E (\varepsilon_t^4) \\
  &= 3(\omega + \alpha X_{t-1}^2)^2
  \end{aligned}$$
- D'où : $$\begin{aligned}
  \mathbb E(X_t^4) &= \mathbb E\left[ \mathbb E \left( X_t^4 | \mathcal F_{-\infty}^{t-1}(X)\right)\right] \\
  &= 3 \mathbb E(\omega^2 + 2 \alpha \omega X_{t-1}^2 + \alpha^2 X_{t-1}^4) \\
  &= 3 \left[ \omega^2 + 2 \alpha \omega \mathbb E(X_{t-1}^2) + \alpha^2 \mathbb E(X_{t-1}^4) \right] \\
  &= 3 \left[ \omega^2 + 2 \alpha \frac {\omega^2}{1- \alpha} + 3 \alpha^2 \mathbb E(X_{t-1}^4) \right] \\
  &= 3 \left[ \omega^2 \frac {1 + \alpha}{1 - \alpha} + 3 \alpha^2 \mathbb E(X_{t-1}^4) \right]
  \end{aligned}$$
- Si on considère que les moments d'ordre 4 existent et se conservent (extension naturelle de la stationnarité au sens faible), on obtient : $$(1 - 3 \alpha^2) \mathbb E(X_t^4) = 3 \omega^2 \frac {1 + \alpha}{1 - \alpha} $$Soit : $$\mathbb E(X_t^4) = 3 \frac {\omega^2 (1 + \alpha)}{(1 - \alpha)(1 - 3\alpha^2)}$$
- Pour que le moment d'ordre 4 existe, il faut que $1 -  3\alpha^2 \gt 0$, c'est à dire que $0 \lt \alpha \lt \frac {\sqrt 3}{3}$ 
- Dans ce cas, le kurtosis vaut : $$\kappa_X = \frac {\mathbb E(X_t^4)}{\mathbb E(X_t^2)} = 3 \frac{\omega^2 (1 + \alpha)}{(1 - \alpha)(1 - 3\alpha^2)} \frac {(1 - \alpha)^2}{\omega^2} = 3 \frac {1 - \alpha^2}{1 - 3\alpha^2} \gt 3$$
#### Kurtosis du processus GARCH(1,1)
- Dans le cas d'un GARCH(1,1), le kurtosis vaut : $$\kappa_X = 3 \frac {1 - (\alpha + \beta)^2}{1 - (\alpha + \beta)^2 - \alpha^2(\mu_4^\varepsilon - 1)} \kappa_\varepsilon$$où $\mu_4^\varepsilon = \mathbb E(\varepsilon_t^4)$ 
### Exemple : Processus AR(1)
#### Espérance du processus AR(1)
- Considérons maintenant un processus AR(1) (centré) : $$\forall t \in \mathbb Z : X_t = \varphi X_{t-1} + \varepsilon_t$$où $(\varepsilon_t)_{t \in \mathbb Z}$ est un brui blanc de variance $\sigma^2$ et $\varphi \lt 1$
- On a : $$\begin{aligned}
  \mathbb E(X_t | \mathcal F_{-\infty}^{t-1}(X)) &= \mathbb E(\varphi X_{t-1} + \varepsilon_t | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= \varphi X_{t-1} \text{ car } \varepsilon_t \perp \mathcal F_{-\infty}^{t-1}(X) 
  \end{aligned}$$
- D'où : $$\mathbb E(X_t) = 0$$

#### Variance du processus AR(1)
- On a : $$\begin{aligned}
  Var(X_t | \mathcal F_{-\infty}^{t-1}(X)) &= Var(\varphi X_{t-1} + \varepsilon_t | \mathcal F_{-\infty}^{t-1}(X)) \\
  &= Var(\varepsilon_t) \\
  &= \sigma^2
  \end{aligned}$$
- D'où : $$\begin{aligned}
	  Var(X_t) &= Var(\varphi X_{t-1} + \varepsilon_t) \\
	  &= \varphi^2 Var(X_{t-1}) + Var(\varepsilon_t) \text{ car } \epsilon_t \perp X_{t-1}
	  \end{aligned}$$
- De la stationnarité, on déduit que :$$Var(X_t) = \frac{\sigma^2}{1-\varphi^2}$$
### Estimation des processus GARCH
#### MV pour les ARCH : Loi normale
- Si on dispose d'un échantillon $(X_1, \dots, X_T)$ et des valeurs initiales $(X_q, \dots, X_1)$, sous hypothèse de normalité de $(\varepsilon_t)_{t \in \mathbb Z}$, la vraisemblance s'écrit : $$
  \begin{aligned}
  &p(x_T, \dots, x_1, \theta) \\
  = &\overset{T}{\underset{t = q + 1}{\Pi}} f_\theta (x_t | \mathcal F_{-\infty}^{t-1}(X)) f_\theta(x_q, \dots, x_1) \\
  = &f_\theta(x_q, \dots, x_1) \overset{T}{\underset{t = q + 1}{\Pi}} \frac{1}{\sigma_t \sqrt{2 \pi}}exp\left[ -\frac 12 \left( \frac {X_t}{\sigma_t} \right) ^2\right]
  \end{aligned}$$
- Si $T$ est suffisamment grand, on utilise la vraisemblance conditionnelle (aux $q$ premières valeurs) : $$\begin{aligned}
  p^* (x_T, \dots, x_{q+1}; \theta) &= p(x_T, \dots, x_1 | x_q, \dots, x_1; \theta) \\
  &= \overset{T}{\underset{t=q+1}{\Pi}} \frac{1}{\sigma_t \sqrt{2 \pi}}exp\left[ - \frac 12 \left( \frac{X_t}{\sigma_t}\right)^2 \right]
  \end{aligned}$$et son logarithme :$$\ell^* (x_T, \dots, x_{q+1}; \theta) = \overset{T}{\underset{t = q + 1}{\sum}} \left( - \frac 12 ln(2 \pi) - \frac 12 ln(\sigma_t^2) - \frac 12 \frac {X_t^2}{\sigma_t^2} \right) $$où la variance cnoditionnelle : $$ \sigma_t^2 = \omega + \overset{q}{\underset{i = 1}{\sum}} \alpha_i X_{t-i}^2$$est estimée itérativement
- On peut estimer un modèle ARCH par **~={red}quasi-maximum de vraisemblance conditionnel=~** : on considère alors que même si le processus $(\varepsilon_t)_{t \in \mathbb Z}$ n'est pas gaussien, a solution obtenue, sous hypothèse gaussienne, reste raisonnable
- On considère néanmoins parfois d'autres distributions
- Si une variable aléatoire $X$ suit une loi $\mathcal T(n)$ alors : $$ \forall n \gt 2 : Var(X) = \frac {n}{n-2}$$
- La vraisemblance conditionnelle vaut alors : $$\begin{aligned}
  &p^*(x_T, \dots, x_{q+1}; \theta) \\
  = &\overset{T}{\underset{t = q + 1}{\Pi}}\frac{1}{\sqrt{n-2}} \frac {1}{\beta(\frac 12, \frac n2)} \left( 1+ \frac{x_t^2}{n-2} \right)^{-\frac{n+1}{2}} \\
  = &\overset{T}{\underset{t = q + 1}{\Pi}}\frac {\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n}{2})\Gamma(\frac 12)}\frac{1}{\sqrt{n-2}} \left( 1+ \frac{x_t^2}{n-2} \right)^{-\frac{n+1}{2}} \\
  = &\overset{T}{\underset{t = q + 1}{\Pi}}\frac {\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n}{2})}\frac{1}{\sqrt{\pi (n-2)}} \left( 1+ \frac{x_t^2}{n-2} \right)^{-\frac{n+1}{2}}
  \end{aligned}$$
- On peut également effectuer les calculs avec la loi de probabilité dite généralisée : $$f(x) = \frac {n \space exp(- \frac 12 |\frac x\lambda|^n)}{\lambda 2 ^{1 + \frac 1n}\Gamma(\frac 1n)}$$où : $$\lambda = \sqrt{2^{- \frac2n} \Gamma \left(\frac 1n \right) \Gamma \left(\frac 3n\right)}$$avec $n \in \mathbb R^{+*}$
- De la même manière que pour un processus ARCH, on estime les paramètres d'un modèle GARCH par (quasi ou non) maximum de vraisemblance conditionnel
- Il existe des résultats de convergence presque sûre et normalité asymptotique des estimateurs du maximum de vraisemblance
### Des processus GARCH alternatifs
#### Modèle IGARCH (GARCH Intégré)
- Un modèle IGARCH(p,q) est un modèle GARCH(p,q) non stationnaire, c'est-à-dire tel que :$$\overset{q}{\underset{i = 1}{\sum}} \alpha_i + \overset{q}{\underset{j = 1}{\sum}} \beta_j = 1$$
- Ce modèle est utilisé dans le cadre des données à haute fréquence en finance
#### Modèle GARCH-M (GARCH in Mean)
- Ce modèle permet d'expliquer la moyenne conditionnelle d'un processus en fonction de sa variance conditionnelle
- Soit $(\eta_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d. centrées et de variance 1
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus GARCH-M(p,q) si : $$\begin{aligned}
  \forall t \in \mathbb Z : X_t &= \mu + \delta g(\sigma_t) + \varepsilon_t \\
  \varepsilon_t &= \sigma_t \eta_t \\
  \sigma_t^2 &= \omega + \overset{q}{\underset{i = 1}{\sum}} \alpha_i^2 \varepsilon_{t-i}^2 + \overset{q}{\underset{j = 1}{\sum}} \beta_j \sigma_{t-j}^2 
  \end{aligned}$$où $(\mu, \delta) \in \mathbb R^2$ et $g$ est une fonction connue
- Par exemple : 
	- $g(\sigma_t^2) =  \sigma_t^2$ (forme linéaire)
	- $g(\sigma_t^2) =  ln(\sigma_t^2)$ (forme log-linéaire)
	- $g(\sigma_t^2) =  \sigma_t$ (forme racine carrée)
#### Modèle EGARCH (GARCH Exponentiel)
On constate sur de nombreuses séries financières une asymétrie des chocs sur la variance conditionnelle, l'impact d'une baisse est plus élevé sur la volatilité que celui d'une hausse.
On utilise donc un modèle EGARCH afin de palier à cette situation
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d. centrées et de variance 1
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus **~={red}E-GARCH=~** si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &ln(\sigma_t^2) = \omega + \overset{q}{\underset{i = 1}{\sum}} \alpha_i[\delta \varepsilon_{t-i} + \gamma g(\varepsilon_{t-i})] + \overset{q}{\underset{j = 1}{\sum}} \beta_j \sigma_{t-j}^2 
  \end{aligned}$$où $(\delta, \gamma) \in \mathbb R^2$ et $g(x) = |x| - \mathbb E(|x|)$ 
#### Modèle TGARCH (GARCH à seuil)
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d. centrées et de variance 1
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus **~={red}TGARCH(p,q)=~** si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &ln(\sigma_t^2) = \omega + \overset{q}{\underset{i = 1}{\sum}} (\alpha_{i+}\varepsilon_{t-i}^+ - \alpha_{i-}\varepsilon_{t-i}^-) + \overset{q}{\underset{j = 1}{\sum}} \beta_j \sigma_{t-j}
  \end{aligned}$$où $(\alpha_{1+}, \dots, \alpha_{q+},\alpha_{1-}, \dots, \alpha_{q-}) \in \mathbb R^{2q}$ et :$$\begin{aligned}
  &\varepsilon_{t-i}^+ = max(\varepsilon_t, 0)\\
  &\varepsilon_{t-i}^- = min(\varepsilon_t, 0)
  \end{aligned}$$
#### Modèle QGARCH (GARCH Quadratique)
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ une suite de v.a.r. i.i.d. centrées et de variance 1
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus **~={red}QGARCH(1,1)=~** si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &\sigma_t^2 = \omega + \delta X_{t-1} + \alpha X_{t-1}^2 + \beta \sigma_{t-1}^2
  \end{aligned}$$où $(\omega, \delta, \alpha, \beta) \in \mathbb R^4$
#### Modèle GJR-GARCH (GARCH Glosten-Jagannathan-Runkle)
- Soit $(\varepsilon_t)_{t \in \mathbb Z}$ un bruit blanc faible de variance 1
- On dit que $(X_t)_{t \in \mathbb Z}$ est un processus **~={red}GJR-GARCH(p,q)=~** si : $$\begin{aligned}
  \forall t \in \mathbb Z : &X_t = \sigma_t \varepsilon_t \\
  &\sigma_t^2 = \omega + \overset{q}{\underset{i = 1}{\sum}} (\alpha_i \varepsilon_{t-i}^2 + \delta_i \varepsilon_{t-i}^2 \mathbb 1_{\epsilon_{t-i} \lt 0}) + \overset{q}{\underset{j = 1}{\sum}} \beta_j \sigma_{t-j}^2
  \end{aligned}$$où $(\delta_1, \dots, \delta_q) \in \mathbb R^{+^q}$ 