# Généralités
- Les méthodes de régularisation, ou méthodes de pénalisation, permettent de répondre à plusieurs problématiques :
	- Sélection (ou **pondération**) de **variables**
	- Traitement de la **colinéarité** dans les modèles linéaires
	- Traitement des "**fat matrix**" : $n \lt p$ (méthodes "**sparses**")
## Données et modèle
- On dispose d'un échantillon de $(X_1, \dots, X_p, Y)$ : $$d_n = (x_{i1}, \dots, x_{ip}, y_i)_{i \in \{1, \dots, n\}}$$
- On considère le modèle de régression linéaire suivant : $$Y = \beta_0 + \beta_1 X_1 + \dots + \beta_p X_p + \varepsilon $$où $\varepsilon$ désigne l'erreur du modèle de régression
# Régression Ridge
- On appelle ~={red}**estimateur Ridge**=~ de $\beta = (\beta_0, \dots, \beta_p)^\top$ le vecteur $\hat \beta^{Ridge}$ solution de : $$\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 + \lambda \overset{p}{\underset {j=1}{\sum}} \beta_j^2$$ où $\lambda \ge 0$ est un **hyperparamètre de régularisation** (à déterminer)
- On considère ici une pénalité $\mathcal l^2$
- On peut également voir cet estimateur comme solution du problème d'optimisation suivant : $$\begin{aligned}
  &\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 \\
  &\text{sous contrainte} \overset{p}{\underset {j=1}{\sum}} \beta_j^2 \le c
  \end{aligned}$$
## Remarques
- Au préalable on **centre et réduit** les covariables $(X_1, \dots, X_p)$
- On **exclut la constante de pénalisation** (si elle est présente)
- Par simplification d'écriture, on considère que $\beta_0 = 0$ dans la suite
- **L'hyperparamètre optimal $\lambda$ est obtenu par validation croisée**
## Illustration
![[Pasted image 20260202201809.png]]
## Explicitation de la solution
- On peut réécrire ce problème sous forme matricielle : $$\underset{\beta}{min}(y - X\beta)^\top(y-X\beta) + \lambda \beta^\top \beta$$ où $$y = \left(\begin{matrix}y_1 \\ . \\ . \\ . \\y_n\end{matrix}\right), X = \left[\begin{matrix}x_{11} &\dots &x_{1p} \\ .&&. \\ .&&. \\ .&&. \\x_{n1} &\dots &x_{np}\end{matrix}\right], \beta = \left(\begin{matrix}\beta_1 \\ . \\ . \\ . \\\beta_p\end{matrix}\right)$$
- La solution est :$$\hat \beta^{Ridge} = \left( X^\top X + \lambda I_p\right)^{-1}X^\top y$$
- L'estimateur Ridge est **~={red}linéaire=~** en y
# Régression LASSO
- On appelle **~={red}estimateur LASSO=~** (Least Absolute Shrinkage and Selection Operator) de $\beta = (\beta_0, \dots, \beta_p)^\top$ le vecteur $\hat \beta^{LASSO}$ solution de : $$\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 + \lambda \overset{p}{\underset {j=1}{\sum}} |\beta_j|$$ où $\lambda \ge 0$ est un paramètre de régularisation (à déterminer)
- On considère ici une pénalité $\mathcal l^1$
- On peut également voir cet estimateur comme solution du problème d'optimisation suivant :$$\begin{aligned}
  &\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 \\
  &\text{sous contrainte} \overset{p}{\underset {j=1}{\sum}} |\beta_j| \le c
  \end{aligned}$$
## Remarques
- On centre au préalable les covariables $\left( X_1, \dots, X_p\right)$
- On exclut la constante e la pénalisation (si elle est présente)
- Par simplification d'écriture, on considère que $\beta_0 = 0$ dans la suite
- L'hyperparamètre optimal $\lambda$ est obtenu par validation croisée
## Illustration
![[Pasted image 20260202203516.png]]
## Propriétés
- L'estimateur LASSO **~={red}n'est pas linéaire en y=~**
- En toute généralité, on ne dispose pas d'expression explicite de l'estimateur LASSO (non-dérivabilité du critère $\mathcal l^1$)
- Si $\lambda \rightarrow +\infty$, on tend à annuler tous les paramètres $(\beta_j)_{j \in \{1, \dots, p\}}$ 
## Cas particulier
- On considère le cas où la matrice $X$ est orthogonale :  $$X^\top X = I_p$$
- On considère le problème : $$\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 + 2\lambda \overset{p}{\underset {j=1}{\sum}} |\beta_j|$$
- Pour $j \in \{1, \dots, p\}$, on obtient la solution explicite suivante : $$\hat \beta_j^{LASSO} = signe\left(\hat \beta_j^{MCO} \right) \left( \left|\hat \beta_j^{MCO}\right| - \lambda\right) \mathbb 1_{\left|\hat \beta_j^{MCO}\right|\ge \lambda}$$
- On parle de "**~={red}seuillage doux=~**" (***soft thresholding***) de l'estimateur des MCO
## Seuillage doux
![[Pasted image 20260202204416.png]]
## Critère $\mathcal l^q$
- Les estimateurs Ridge et LASSO sont des cas particulier du problème d'optimisation suivant :$$\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 + \lambda \overset{p}{\underset {j=1}{\sum}} |\beta_j|^q$$ où $\lambda \ge 0$ est un paramètre de régularisation (à déterminer par validation croisée) et $q \in \mathbb R^+$
# Méthode Elastic Net
- La méthode **~={red}Elastic Net=~** combine les régressions Ridge et LASSO via le problème d'optimisation suivant : $$\underset{\beta}{min} \overset{n}{\underset {i=1}{\sum}}\left( y_i - \beta_0 - \overset{p}{\underset {j=1}{\sum}} \beta_j x_{ij}\right)^2 + \lambda \left(\alpha\overset{p}{\underset {j=1}{\sum}} |\beta_j| + (1-\alpha) \overset{p}{\underset {j=1}{\sum}} \beta_j^2 \right)$$où $\lambda \ge 0$ et $\alpha \in ]0, 1]$ sont des paramètres de régularisation (à déterminer par validation croisée)