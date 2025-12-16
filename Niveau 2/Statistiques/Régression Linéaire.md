# Introduction et cas d'étude
Le terme *regression* vient des travaux de **Francis Galton** (dans le sens, ***regression vers la moyenne***)
C'est le modèle linéaire le plus utilisé.
Le but est de mettre en relation une ***variable quantitative à expliquer*** (nommée *label, étiquette, output*), avec des ***variables explicatives*** (nommées *covariables, features, prédicteurs, inputs*)
## Cas d'étude 1
Étude du lien entre *le pic d'ozone journalier* et des *facteurs potentiellement explicatifs* à des fins de *prévision*
On dispose de 112 données (recueillies à Rennes) et 14 variables (principalement météorologiques)
- Date : Date 
- maxO3 : Teneur maximale en ozone observée dans la journée
- T9, T12, T15 : Température à 9h, 12h, 15h
- Ne9, Ne12, Ne15 : Nébulosité observée à 9h, 12h, 15h
- Vx9, Vx12, Vx15 : Composante Est-Ouest du vent à 9h, 12h, 15h
- maxO3v : Teneur maximale en ozone observée la veille
- vent : Orientation du vent à 12h
- pluie : Occurrence ou non de précipitations
![[Pasted image 20251211204931.png]]
# Régression linéaire simple
## Hypothèses
- On note **Y** la variable à expliquer
- On note **X** la covariable 
- Le modèle de ***régression linéaire simple*** s'écrit :
	- $Y = \beta_0 + \beta_1 X + \epsilon$
	- Où :
		- $\beta_0 \space et \space \beta_1$ sont des paramètres inconnus (non observables)
		- $\epsilon$ est l'erreur du modèle, est centrée (d'espérance nulle) et de variance $\sigma^2$ 
- Dans le cas où $X = 0 \implies Y = 0$ on a :
	- $Y = \beta_1 X + \epsilon$
## L'échantillon

# Régression linéaire multiple
aa
# Sélection de modèles
aa
# Qualité prédictive d'un modèle