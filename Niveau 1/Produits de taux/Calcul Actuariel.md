# Taux d'intérêt
Le taux d'intérêt est le "loyer" de l'argent, la rémunération qu'on obtient en contrepartie de l'utilisation de cette ressource.
Le risque (Crédit/Contrepartie) peut jouer sur le niveau de taux d'intérêt, mais n'en est pas la raison d'existence.

## Cas sur une période
Le calcul d'un placement $S$ à taux $r$ se fait :
$$S*(1+r*\delta t) = S+S*r*\delta t$$
$\delta t$ est la durée du placement, selon la convention choisie (_ACT/360, ACT/365, ACT/ACT etc..._)

## Capitalisation (sur plusieurs périodes)
**Formule générale de capitalisation annuelle** : $$V_n = V_0 * (1+r)^n$$
- Avec :
	- **$V_0$** : Capital initial
	- **$r$** : Taux d'intérêt
	- **$n$** : Durée du placement en années

**Formule générale de capitalisation pluri-annuelle** : $$V_n = V_0 * (1+ \frac {r}{m})^{n*m}$$
- Avec :
	- **$V_0$** : Capital initial
	- **$r$** : Taux d'intérêt
	- **$n$** : Durée du placement en années
	- **$m$** : Nombre de périodes dans l'année

**Capitalisation Continue** :$$V_n = V_0 * e^{n*m}$$
# Actualisation
La **valeur actuelle** d'un flux F reçu ou payé à une date future (dans n années) est la somme d'argent que je dois placer aujourd'hui pour obtenir le montant F dans n années.
$$VA = \frac {F}{(1+r)^n}$$
## Cas d'une série de flux
Pour actualiser une série de flux $C_i$ , il suffit de faire la somme des valeurs actuelles des flux en fonction de leurs dates de paiement respectives $t_i$:
$$ VA = \frac {C_1}{(1+r)^{t_1}} + \frac {C_2}{(1+r)^{t_2}} + ... + \frac {C_n}{(1+r)^{t_n}}$$
# Zéro-coupon:
Une **obligation zéro-coupon** (ou "zéro-coupon" tout court) est un titre financier qui verse 1 (ou 100%) à sa maturité T (exprimée en années)

![[Pasted image 20251125110805.png]]

La valeur du ZC à $t=0$ est la suivante :$$V_{zc} = \frac {1}{(1+r)^T} $$
Ce prix nécessite l'hypothèse d'_**absence d'opportunité d'arbitrage**_ afin d'assurer cette unicité de prix et les cas d'arbitrage, démontrons le :
***Considérons un prix $V_{zc}=\frac {1}{(1+r^T)}-\epsilon$ avec $\epsilon >0$***
- Alors, nous avons l'arbitrage suivant :
	- $t=0$
		- Emprunt du montant $V_{zc}$ au taux $r$
		- Achat du ZC avec le montant emprunté
		- Flux initial $F_0=0$
	- $t=T$
		- Remboursement de l'emprunt
		- Obtention du paiement du ZC
		- Flux final $F_T = 1 - (\frac {1}{(1+r)^T}-\epsilon)(1+r)^T = \epsilon (1+r)^T > 0$
- Nous obtenons donc une valeur finale de $F_T=\epsilon (1+r)^T$ avec un investissement initial $F_0=0$
# Intérêts
## Intérêts simples vs actuariels
Un intérêt est simple lorsqu'il est payé en une fois et proportionnel à la durée du placement :
$$Intérêt = C * r * n$$
- Avec :
	- **C** : Le capital (ou Nominal)
	- **n** : La durée du placement
	- **r** : Le taux d'intérêt
==L'intérêt simple est en général pratiqué lorsque les durées sont inférieures à 1 an.==

- **Intérêt simple** : $100 \overset {6 mois}{\longrightarrow} 100 *(1+r*0.5)$ 
- **Intérêt actuariel** : $100 \overset {6 mois}{\longrightarrow} 100 *(1+r)^{0.5}$ 
### Intérêts précomptés / postcomptés :
Il existe deux méthodes de paiement des intérêts :
![[Pasted image 20251125114847.png]]

Dans le cas d'un emprunt de 1M€ sur une période de 1 mois à un taux d'intérêt de 5%, le montant d'intérêt sera : 1 000 000 * 5% = 50 000€.![[Pasted image 20251125115340.png]]
- Pour passer de l'un à l'autre :
	- $(1+r_{post})(1-r_{pre}) = 1$ 
	- $r_{post} = \frac {r_{pre}}{1-r_{pre}}$ 
	- $r_{pre} = \frac {r_{post}}{1+r_{post}}$  
# Valeur Actuelle Nette (VAN)
C'est la valeur actuelle (vue plus haut) nette des investissement, donc la somme des flux (positifs et négatifs) actualisés. 
$$VAN = \sum_{i=0}^{n} \frac {F_i}{(1+r)^i}$$
## Taux de Rendement Interne (TRI)
Le TRI est le taux d'actualisation $R$ qui rend la VAN nulle $$VAN = \sum_{i=0}^{n} \frac {F_i}{(1+R)^i} = 0$$Autrement dit, c'est le taux qui égalise les valeurs actualisées des dépenses et des recettes $$\sum_{i=0}^{n} \frac {Dépenses_i}{(1+R)^i} = \sum_{i=0}^{n} \frac {Recettes_i}{(1+R)^i}$$

## Taux de Rendement Actuariel (TRA)
C'est l'équivalent du TRI pour les obligations, c'est ce qui permet donc d'avoir une VAN de l'obligation nulle, autrement dit, ça égalise les flux reçus de l'obligation avec son prix de marché 
C'est donc le taux R qui permet 
$$P=\sum_{i=0}^{n} \frac {F_i}{(1+R)^i}$$
![[Pasted image 20251125162835.png]]

# Les amortissements
## Amortissement "In Fine"
 Le remboursement du capital se fait à la fin.
 L'intérêt est payé à chaque échéance prévue.![[Pasted image 20251125171300.png]]
## Amortissement par annuités constantes
Chaque versement contient des intérêts et une part du capital.
Les remboursements sont identiques à chaque échéance.
![[Pasted image 20251125171355.png]]
$$K = \frac {a}{1+r} + \frac {a}{(1+r)^2} + ... +\frac {a}{(1+r)^n} = \sum_{j=1}^{n} \frac {a}{(1+r)^j}$$
D'où l'annuité constante $$a = \frac {K}{\sum_{j=1}^{n} \frac {1}{}(1+r)^j} = \frac {K*r}{1-(1+r)^{-n}}$$
## Amortissement par tranches égales (amortissement constant)
Dans ce cas, c'est le montant du ***capital remboursé*** qui est constant![[Pasted image 20251125173107.png]]
$$I_j = i*K*\frac {n-j+1}{n}$$

# TP
![[TP cours 1.xlsx]]