# Introduction
## Qu'est-ce qu'une option exotique
Pour définir une option comme exotique, on se base sur deux critères :
- **Complexité** :
	- Si elle ne s'apparente pas à un/une combinaison de call/put européens
	- Donc pas de *straddle, strangle, collar...*
- Liquidité
	- Une option avec très peu de liquidité, rare dans le marché, est considérée comme exotique.

## Risques 
Il y a **3 grands types de risques** sur les *exotiques* :
- **Risque Digital** (de discontinuité)
- **Risque de volatilité forward**
- **Risque de correlation**
Un modèle d'évaluation de produit exotique doit avoir :
- **Une dynamique adéquate**
- **Une calibration adéquate**
## Exotiques populaires par marché
### Exotiques de change
- Barrières simples / doubles (Up/Down, In/Out)
- Digitales Américaines (No touch, One touch)
- Digitales Européennes
- Asiatiques (strike ou actif moyenné)
### Exotiques equity
- Autocalls
- Variance swaps
- Etc...
### Exotiques de taux d'intérêt
- Digitales et corridors
- CMS et CMS spread options (steepeners)
- Callable : Bermuda, Callable R, spread options, corridors
- Path-dependent : ratchet, TARN, snowball, vol bond etc...

# Panorama (non exhaustif) des produits exotiques
## Options Américaines
Même payoff que les européennes mais exercice possible à tout moment entre l'émission et la maturité.

### Evaluation
- Pas de formule analytique exacte
- Formules analytiques approchées (Barone Adesi, Whaley)
- Méthodes numériques backward (arbre, différences finies)
### Variantes
- Exercice limité à une période donnée (notamment "*no call period*")
- Exercice possible uniquement à certaines dates (options bermudas associées aux produits callable)

### Pricing
Le prix des **options américaines** est supérieur ou égal aux **options européennes** correspondantes.
***NB*** : Avec $r \ge 0$
- Le prix du call américain est égal au prix du call européen
	- $C_t^{US} \ge C_t^{EUR} \gt VI_t = (S_t - Ke^{-r(T-t)})^+ \gt (S_t - K)$
	- Il n'est donc jamais optimal d'exercer un call américain avant maturité
	- Or, comme $C_t^{US} = max(C_t^{EUR}, (S_t-K))$ on a $C_t^{US} =C_t^{EUR}$
- C'est faux pour le put
==Si $r \le 0$ c'est l'inverse, cela deviendra faux pour le call et vrai pour le put, la démonstration est la même que précédemment==

### Evolution prix du put selon maturité et strike
![[Pasted image 20251204211804.png]]

==In the money : Plus la maturité est proche, plus le prix est élevé
Out of the money : Plus la maturité est éloignée, plus le prix est élevé==

## Options digitales

### Digitales fixes (*"Cash-or-nothing"*)
#### Définition
Appelées également options binaires
- **Payoff call** : 
	- 1€ si $S_t \gt K$
	- 0€ sinon
- **Payoff put** :
	- 1€ si $S_t \lt K$
	- 0€ sinon
	![[Pasted image 20251204212307.png]]

#### Evaluation dans le cadre de B&S
 - **Prix call** : 
	- $e^{-rT} \mathcal N(d2)$
- **Payoff put** :
	- $e^{-rT} \mathcal N(-d2)$
==**NB** : $CallDigital + PutDigital = e^{-rT}$, ce qui correspond au payoff (1€) actualisé==

### Digitales variables (*"asset-or-nothing"*)
#### Définition
Les options binaires précédentes sont dites *"cash-or-nothing"*
La version *"asset-or-nothing"*
- **Payoff call** : 
	- $S_t$ si $S_t \gt K$
	- 0€ sinon
- **Payoff put** :
	- $S_t$ si $S_t \lt K$
	- 0€ sinon
![[Pasted image 20251204212845.png]]

#### Evaluation dans le cadre de B&S
 - **Prix call** : 
	- $S_0 \mathcal N(d1)$
- **Payoff put** :
	- $S_0 \mathcal N(-d1)$
**NB** : $CallDigital + PutDigital = S_0$, ce qui correspond au payoff ($S_0$) actualisé

### Limites du pricing B&S
On approche le prix d'une option digitale par un **call spread** (*différence entre deux calls européens*).
![[Pasted image 20251204214327.png]]
$$Digitale = \frac {(C_0(T, K - \epsilon) - C_0(T, K + \epsilon))}{2 \epsilon} = -\frac {\partial \{C_0(T,K)\}}{\partial K}$$ ***Néanmoins, en la présence de *skew* de volatilité, l'évaluation via B&S devient très approximatif.***

### Cas de la double digitale
La double digitale est une digitale entre $K_1$ et $K_2$
![[Pasted image 20251204214405.png]]

On la réplique facilement à partir de deux digitales simples.

***Application*** : **Corridor Range Accrual**
C'est un produit dérivé de taux qui permet d'obtenir un taux d'intérêt défini (généralement attractif), ne s'accumulant que les jours où le taux de référence (Euribor, Libor ou autre) reste dans un corridor défini.
*Exemple* : *Sur Euribor*
- Corridor : 2-4%
- Taux offert : 6%
- Dans notre cas, supposons que l'*Euribor* est resté entre 2% et 4% durant 200 jours
	- On reçoit : $6\% * \frac {200}{360}$ 

## Options à Barrières
### Définition
Payoff d'un call ou put européen mais paiement conditionné par le franchissement (ou non) d'une barrière par l'actif sous-jacent tout au long de la vie de l'option
### Caractéristiques
***Type*** : Call/Put
***Barrière*** : Up/Down
***Activation*** : In/Out
***Variantes*** : Avec rebate/Double Barrière/Digitale à barrière("one touche", "no touch")
***Exemple*** : *Call down & out*
- Payoff en $T$: $(S_t - K)^+ \mathbb 1_{\{min_{[0,T]}S_t \gt H\}}$
***Intérêt du produit*** : *Premium (prix)* réduit, donc effet de levier supérieur
### Evaluation des options barrières
- Formules fermées dans le cas B&S
- Mais vu le risque digital $\implies$ B&S est à proscrire
	- Il faut calibrer le modèle sur la surface de volatilité
	- **Standard du marché** : *Modèle à volatilité locale (Dupire)*
## Options forward start
### Définition 
Call/Put européen dont le strike est déterminé par le niveau de l'actif sous-jacent à une date ultérieure
***Strike*** : $K = S(T_1)$
***Payoff*** en $T_2$ : $Payoff = (S(T_2) - K)^+ = (S(T_2) - S(T_1))^+$
***Intérêt du produit*** :
- Fixer le niveau de volatilité tout en laissant le strike s'établir plus tard
***Exemple*** : Fonds à capital garanti avec période de souscription
### Evaluation des options forward start
==On livre en $T_1$ un call ATM de maturité $T_2$, on s'engage donc sur le niveau futur de vol ATM==
On a donc un risque majeur de **volatilité forward**
Le **Payoff en $T_1$** $\approx 0.4 \space S(T_1) \space \sigma \space (T_2 - T_1)^{0.5}$
- Nécessite de connaitre $\sigma$ vol implicite en $T_1$
*Le modèle à **volatilité stochastique** est donc **obligatoire***.
Cela est encore plus flagrant dans le cas :
- Forward start sur performance
- Payoff :
	- En $T_2$ = $(\frac {S(T_2)}{S(T_1)} - 1)^+$
	- En $T_1$ = $\approx 0.4 \space \sigma \space (T_2 - T_1)^{0.5}$
- On obtient un **pur produit de vol forward** (*pas de delta !*)
- *Exemple* : **EMTN** versant annuellement la performance positive de l'$EUROSTOXX$

## Spread options
### Définition
Option sur la différence entre deux sous-jacents X et Y
**Payoff** : $(X_T - Y_T)^+$

## Evaluation du spread option
- **Gaussien** : Immediat
- **B&S** : Utilisation comme numéraire d'un des deux sous-jacents pour retomber sur une évaluation simple
- **Risque de corrélation** : $\searrow \space Correlation \implies Prix \space spread \space Option \nearrow$   

## Options panier "best-of" et "Worst of"
### Définition 
- ***Best of*** : $max(X_T,Y_T)$
- ***Worst Of*** : : $min(X_T,Y_T)$
- Se généralise aussi à $N$ actifs

### Evaluation du panier
En utilisant la spread option
$$max(X_T,Y_T) = Y_T + max(0,X_t-Y_T)$$
$$min(X_T,Y_T) = Y_T - max(0,Y_t-X_T)$$
## Options "lookback"
### Definition
Ce sont des options dont le payoff dépend du chemin
- Payoff ***hautement rémunérateur***
- Hautement ***path dependent***
- **Payoff**
	- Call *lookback* : $(S_T - min_{[0,T]} S_t)$
	- Put *lookback* :  $(max_{[0,T]} S_t - S_T)$
### Evaluation des options lookback
- Formule fermée en B&S
- Monte Carlo
## Options asiatiques
### Définition
Options faisant intervenir une moyenne de valeurs du sous-jacent (soit à la place de $S_T$, soit à la place de $K$)

|                   | Call                     | Put                      |
| ----------------- | ------------------------ | ------------------------ |
| Sous-jacent moyen | $(M_S(T_1,T_2) - K)^+$   | $(K - M_S(T_1,T_2))^+$   |
| K moyen           | $(S_T - M_S(T_1,T_2))^+$ | $(M_S(T_1,T_2) - S_T)^+$ |
**Intérêt** : Le cours moyen est souvent plus pertinent
### Evaluation
#### Sous B&S
- **Moyenne géométrique** : Formule Fermée 
- **Moyenne Arithmétique** : Monte Carlo avec variable de contrôle
## Produits quantos
### Définition
Un produit quanto est un produit sur un sous-jacent libellé dans une devise étrangère dont le payoff est converti en devise locale via un ***taux de change défini dans le contrat***.
**Intérêt** : Prendre position sur un marché étranger sans subir le risque de change
***Exemple*** : 
- *Forward Quanto*
	- Payoff : $X_0(S_T^f - K^f)$
	- Avec :
		- $X_0$ : Taux de change spécifié dans le contrat
		- $S_T^f$ : Sous-jacent libellé en devise étrangère
		- $K^f$ : Strike libellé en devise étrangère
### Evaluation du quanto
On ajuste la convexité dépendamment de la covariance entre l'actif étranger et le taux de change.

# Notes et astuces importantes
- Si $r>0$ :
	- $C^{Us}=C^{Eur}$ 
	- $P^{Us}>P^{Eur}$ 
- Si $r<0$ :
	- $C^{Us}>C^{Eur}$
	- $P^{Us}=P^{Eur}$
- Si $r=0$ :
	- $P^{Us}=P^{Eur}=C^{Us}=C^{Eur}$
