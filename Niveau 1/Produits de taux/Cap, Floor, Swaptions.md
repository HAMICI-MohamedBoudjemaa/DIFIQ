# Cap
## Qu'est-ce qu'un Cap
Contrairement à un **Swap** qui permet de transformer sa dette **variable** en dette **fixe**.
Un **Cap** permet de *Capper* sa dette (lui donner une borne max).
![[Pasted image 20251203200606.png]]
## Comment ça marche
Un **Swap** va compenser la différence entre taux fixe et variable, et de ce fait, ma dette variable devient fixe.
- Je paie ma dette à **Euribor**
- Je reçois ma jambe variable **Euribor**
- Je paie ma jambe fixe à **$x\%$**
- Je paie donc $Euribor-(Euribor-x\%) = x\%$
Un **Cap** versera à contrario, $(Euribor-x\%)^+$, et dans ce cas :
- Si $Euribor \gt x\%$ : Je suis compensé (*comme pour le swap*) et je paie le fixe de $x\%$
- Si $Euribor \lt x\%$ : Le Cap donne 0 et je paie $Euribor$ ($\lt x\%$)
- Je paie donc au **Maximum** $x\%$
## Flux du Cap
Chaque flux s'appelle **un Caplet** et sa valeur n'est rien de plus qu'un **call sur $Euribor$**
![[Pasted image 20251203200626.png]]
==A noter le sens du caplet, dans la direction contraire de la dette, il vient compenser le cash-flow sortant==
Ici :
- $2\%$ est le strike du Cap
- Ce Cap est dit **à la monnaie** car le strike ($2\%$) est égal au taux Euribor actuel
# Floor
## Qu'est-ce qu'un Floor
Le **Floor** permet de *floorer* (donner un minimum) à un **placement variable**.

## Comment ça marche
J'ai un placement Euribor, je reçoit donc un flux $Euribor$.
Un **Floor** versera à contrario, $(x\% - Euribor)^+$, et dans ce cas :
- Si $x\% \gt Euribor$ : Je suis compensé (*comme pour le swap*) et je reçoit le fixe de $x\%$
- Si $x\% \lt Euribor$ : Le Floor donne 0 et je reçoit $Euribor$ ($\gt x\%$)
- Je reçoit donc au **Minimum** $x\%$ ($Euribor + (x\% - Euribor)^+$)
## Flux du Floor
![[Pasted image 20251203203330.png]]
==A noter le sens du floorlet, dans la même direction que le placement, il vient enrichir le placement==

# Tunnel

## Qu'est-ce qu'un Tunnel
Le **tunnel** permet  de **réduire (voir annuler) le coût de la couverture** en achetant et vendant simultanément un *Cap* et un *Floor*. Ce qui va encadrer la position entre un *minimum* et un *maximum*.

## Comment ça marche ?
Je suis **endetté** à taux variable. 
Pour couvrir ma position
- J'**achète un CAP** ($3\%$ pour l'exemple).
- Le coût est élevé, je **vends un floor en parallèle** ($1\%$ pour l'exemple).
- J'obtiens : $-Euribor + (Euribor - 3\%)^+ - (1\% - Euribor)^+$
	- Si $Euribor \gt 3\%$ : Le **Cap** *s'active*, le **Floor** *s'annule* et je paie $3\%$
	- Si $Euribor \lt 1\%$ :  Le **Floor** *s'active*, le **Cap** *s'annule* et je paie $1\%$
	- Si $1\% \lt Euribor \lt 3\%$ : Les deux options s'annulent et je paie $Euribor$
- Ma dette est donc bien restreinte entre $1\%$ et $3\%$
![[Pasted image 20251203205552.png]]

## Flux du tunnel 
C'est la différence des flux des Caps et Floors vus précédemment

# Evaluation des Caps et Floors
Un cap(floor) est une série de caplets(floorlets), chacun étant un call(put) sur $Euribor$
Pour évaluer un **Cap(Floor)** il suffit d'évaluer la $PV$ de chacun des *caplets(floorlets)* avec les méthodes classiques de pricing d'options.
La $PV$ d'un **Cap(Floor)** est donc la somme des $PV$ de ses *caplets(floorlets)*
$$PV_{CAP} = \sum_{i=1}^{n} PV_{Caplet}^{i}$$
$$PV_{FLOOR} = \sum_{i=1}^{n} PV_{Floorlet}^{i}$$
# Pricing d'un caplet
Historiquement, nous utilisions Black and Scholes pour l'évaluer :$$PV_{Caplet} = DF(T_2) BSCall(T_f,K,TauxFRA,\sigma)$$
Mais depuis l'apparition des taux négatifs, on passe au modèle gaussien :$$PV_{Caplet} = DF(T_2) NORMCall(T_f,K,TauxFRA,\sigma_n)$$
# Volatilité implicite des caps/floors
![[Pasted image 20251203210620.png]]

# Swaptions
Une **Swaption** est l'*option* de rentrer dans un swap à une date future.
Le sous-jacent d'une **swaption** est un **swap-forward**
*Exemple :*
- Un swap 5Y /10Y payeur 2% traité aujourd'hui est :
	- L'obligation dans 5 ans de rentrer dans un swap payeur 2% pour 10 ans.
	- Dans 5 ans, je peux être gagnant (si le taux swap augmente) ou perdant (sinon)
- Comment éviter ce problème ?
	- On passe donc du **swap-forward 5Y/10Y payeur 2%** à la **swaption 5Y/10Y payeur 2%**.
	- Dans 5 ans, j'aurai le choix de rentrer ou non dans le swap, et on ***n'exerce que si le MtM du swap sous-jacent est positif, i.e. si le taux swap 10ans est supérieur au strike de 2% de la  swaption***
Le MtM du swap sous-jacent en $T_f$ s'écrit :$$LVL(T_f)(S(T_f)-K)$$
Le payoff de la swaption en $T_f$ s'écrit :$$LVL(T_f)(S(T_f)-K)^+$$
==Qui peut se comprendre comme un **call** sur le **taux swap**==
## Evaluation d'une swaption
Historiquement, nous utilisions Black and Scholes pour l'évaluer :$$PV_{Swaption}^P = LVL(0) BSCall(T_f,K,S(0),\sigma)$$
Mais depuis l'apparition des taux négatifs, on passe au modèle gaussien :$$PV_{Swaption}^P = LVL(0) NORMCall(T_f,K,S(0),\sigma_n)$$
Avec :$$LVL(0) = N \sum_{i=1}^{n} \delta_i^F DF(T_i^F)$$$$S(0) = \frac {\sum_{j=1}^{m} \delta_j^V * TauxFRA_j * DF(T_j^V)}{\sum_{i=1}^{n}\delta_i^F DF(T_i^F)}$$
## Volatilité implicite des swaptions

![[Pasted image 20251203212617.png]]

## Utilité des swaptions
- On peut utiliser une swaption simplement pour avoir une *option* sur la conversion d'un flux (variable vs fixe)
- Cela sert aussi à structurer des ***produits annulables*** 
	- $$Swap \space 15y \space receveur \space 2\% \space + \space swaption \space 5y/10y \space payeuse \space 2\% \space = \space swap \space 15y \space receveur \space 2\% \space annulable \space dans \space 5ans$$
## Cas de la Bermuda
La **swaption Bermuda** est une swaption à plusieurs dates d'exercices.
On peut l'utiliser pour structurer un produit *callable*. 
Si on reprend l'exemple précédent, en **version Bermuda** on pourrait avoir par exemple :
- Une swaption annulable dans 2ans, 3ans ....., 14ans
Ce type de swaption exotique est plus difficile à évaluer

# EMTN (Euro Medium Term Notes)
Un **EMTN** (Euro Medium Term Notes) est un **programme d'émission de titres de dettes** qui permet à un emetteur (entreprise, banque, état) de lever des fonds de manière *flexible* sur les marchés financiers.
Ses caractéristiques principales sont :
- **Flexibilité** :
	- Emissions multiples pour un même programme cadre
	- Montants, maturités et devises variables selon le besoin
	- Possibilité d'émettre rapidement (parfois en quelques heures)
- **Documentation** : 
	- Prospectus de base approuvé **une seule fois**
	- Des suppléments (*final terms*) ajoutés pour chaque émission spécifique
	- Réduit les coûts et les délais par rapport à des émissions isolées
- **Durée** :
	- *Medium term* : 1-10ans en général
	- Peut aller de quelques mois jusqu'à 30ans en pratique
![[Pasted image 20251203214013.png]]
