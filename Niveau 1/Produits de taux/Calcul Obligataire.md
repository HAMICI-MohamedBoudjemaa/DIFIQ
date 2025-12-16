# Obligation
Une obligation est une **part de dette**.
C'est une **valeur mobilière** dont le titre dépend de l'offre et de la demande (comme les actions).
Elle peut être émise par :
- Les états
- Les organismes supra-nationaux (Banque Mondiale, BERD etc...)
- Les entreprises publiques, para-publiques, privées
- Les banques
- Les collectivités locales et territoriales
C'est un titre à revenus fixe (d'où l'appellation ***Fixed Income***)

## Obligation vs Actions
![[Pasted image 20251126185709.png]]

## Principales Caractéristiques d'une obligation :
- Valeur Nominale
- Date d'échéance
- Fréquence des coupons
- Taux nominal (taux facial, taux de coupon)
- Prix d'émission
- Prix de remboursement

Exemple : Obligation 5ans, coupons annuels, taux facial 3%, émise au pair
![[Pasted image 20251126190352.png]]
## Taux de rendement d'une obligation (TRA)
Soit $c$ le taux facial d'une obligation, ses flux sont :
$$F_1=F_2=...=F_{n-1}=100*c \space et \space F_n=100*(1+c)$$Définissons : $$P(r) = \sum_{i=1}^{n} \frac {F_i}{(1+r)^T_i}$$
Le **taux de rendement actuariel (TRA ou Yield to Maturity YTM in English)** de l'obligation est le taux $r$ tel que $P(r)$ coïncide avec le prix de marché de l'obligation.
### Cas d'une obligation au pair
Si on évalue une obligation au pair à sa date anniversaire, nous avons :
$$P(r) = 100 = \frac {100}{(1+r)^n}+\sum_{i=1}^{n} \frac {100*c}{(1+r)^i}$$
d'où $$c = \frac {1 - \frac {1}{(1+r)^n}}{\sum_{i=1}^{n} \frac {1}{(1+r)^i}} = r$$
***En effet, une obligation au pair à sa date d'anniversaire, a un TRA égal à son taux facial*** 
![[Pasted image 20251126193424.png]]

### Relation entre TRA et Courbe ZC
Si on bootstrap la courbe ZC sur le marché obligataire, une obligation de flux $F_i$ payés aux dates $T_i$ aura un prix égal :
$$\sum_{i=1}^{n} \frac {F_i}{(1+r(T_i))^{T_i}}$$
D'où la relation avec le TRA :
$$\sum_{i=1}^{n} \frac {F_i}{(1+r(T_i))^{T_i}} = \sum_{i=1}^{n} \frac {F_i}{(1+r)^{T_i}}$$
Or le flux $F_n$ est bien plus important que les autres flux $F_i$ pour $i<n$, on constate donc souvent que :$$r \approx r(T_n)$$
## Déterminants du prix obligataire
Deux principaux facteurs de marchés influent sur le prix d'une obligation :
- Le niveau des **taux d'intérêts**
	- $\nearrow \space Taux \implies Prix \space Obligation \searrow$   
	- $\searrow \space Taux \implies Prix \space Obligation \nearrow$  
	- Car le prix est une fonction décroissante de r$$P(r) = \sum_{i=1}^{n} \frac {F_i}{(1+r)^{T_i}}$$
	- ==Financièrement parlant, si les taux montent, les obligations précédentes avec un taux inférieur deviennent moins intéressantes, leur prix baisse donc mécaniquement.==
 
- La **qualité de la signature** de l'émetteur, autrement dit son **risque de crédit** (évalué par son **rating** et quantifié par son **spread de crédit**)
	- $\nearrow \space Risque \space de \space crédit \implies Prix \space Obligation \searrow$   
	- $\searrow \space Risque \space de \space crédit \implies Prix \space Obligation \nearrow$  
	- Le spread de crédit, étant une partie du taux de rendement de l'obligation, le spread est une fonction croissante du risque de crédit, si le risque monte, le spread augmente et mécaniquement le $r$, ce qui rend le prix, une fonction décroissante du risque de crédit (comme pour $r$), on peut écrire : 
		- $\nearrow \space Risque \space de \space crédit \implies \nearrow \space Taux \implies Prix \space Obligation \searrow$
		- $\searrow \space Risque \space de \space crédit \implies \searrow \space Taux \implies Prix \space Obligation \nearrow$
	- ==Financièrement parlant, l'explication est la même que la précédente, l'augmentation du risque génère de nouvelles obligations avec un $r$ supérieur, les premières sont donc moins intéressantes et leur prix baisse mécaniquement.==
	- ==Vu autrement, le risque de crédit de l'obligation ayant augmenté, l'investisseur requiert un rendement plus élevé, ne pouvant agir sur le taux facial, le prix baisse afin que le rendement soit cohérent avec l'évolution du risque.==
	
## Sensibilité d'une obligation
La **sensibilité** (ou ***modified duration*** in English) est une grandeur que calculée pour appréhender la dépendance du prix d'une obligation vis à vis des taux d'intérêts.
***C'est la variation relative du prix de l'obligation lorsque le TRA bouge de 1%***
- Par exemple : Une sensibilité de 4 signifie qu'une **baisse** du TRA de **1% augmente** le prix de **4%**

### La sensibilité mathématiquement
$$P(r) = \sum_{i=1}^{n} \frac {F_i}{(1+r)^{T_i}}$$
La variation du prix $P(r)$ est donc égale à la $dérivée*pas$  (avec dérivée = $P'(r)$ et pas = $\delta TRA = 0.01$)
$$\implies \Delta P(r) = P'(r) * 0.01$$
Or, la sensibilité est la variation ***relative*** du prix (soit $\frac {\Delta P(r)}{P(r)}$), on devrait donc obtenir :
$$\implies  \frac {P'(r) * 0.01}{P(r)} < 0 \space$$
Le résultat est négatif à cause de la relation décroissante entre $P(r)$ et le **TRA**, nous le corrigerons donc en ajoutant un $-$ pour obtenir une sensibilité positive, et afin d'obtenir un résultat en pourcentage directement, nous supprimons le pas $0.01$:
$$S(r) = - \frac {P'(r)}{P(r)} =\frac {1}{P(r)} \sum_{i=1}^{n} \frac {F_i*T_i}{(1+r)^{{T_i}+1}}$$
La somme apparaît par dérivation de $P(r)$ comme suit : $$P(r) = \sum_{i=1}^{n} \frac {F_i}{(1+r)^{T_i}} $$
$$\implies P'(r) = \sum_{i=1}^{n}  {F_i} * \frac {d}{dr}{(1+r)^{-T_i}} = \sum_{i=1}^{n}  {F_i} * -{T_i}*{(1+r)^{-{T_i}-1}}  = -\sum_{i=1}^{n} \frac {{F_i} * {T_i}} {(1+r)^{{T_i}+1}}$$
## Duration d'une obligation
La duration d'une obligation est définie comme le produit de la sensibilité par $(1+TRA)$ :
$$D(r) = S(r)*(1+r) = \frac {1}{P(r)} \sum_{i=1}^{n} \frac {F_i*T_i}{(1+r)^{T_i}}$$
Ou, en remplaçant $P(r)$ par son expression $$D(r) = \frac {\sum_{i=1}^{n}T_i*{\frac {F_i}{(1+r)^{T_i}}}}{\sum_{i=1}^{n} \frac {F_i}{(1+r)^{T_i}}}$$
**La duration est la moyenne des dates de paiements des flux de l'obligation, pondérée par les valeurs actuelles des flux**
==On peut interpréter la duration comme le temps moyen nécessaire pour récupérer son investissement ou encore comme un **point d'équilibre temporel** des maturités pondérés par le temps==
![[Pasted image 20251127113200.png]]

### Convexité du prix de l'obligation
La courbe de prix d'une obligation est convexe, ce qui signifie que l'impact d'une **hausse des taux** est **inférieur** à l'impact d'une **baisse des taux** sur le prix de l'obligation (voir graphique ci-dessous).

| TRA    | Prix       | Variation |
| ------ | ---------- | --------- |
| **4%** | **119.79** | **-**     |
| 3%     | 146.23     | 26.44     |
| 5%     | 100        | -19.79    |
Mathématiquement on a : $$C(r) = \frac {P''(r)}{P(r)} = \sum_{i=1}^{n} \frac {F_i*T_i*(T_i+1)}{(1+r)^{T_i+2}}$$
![[Pasted image 20251127113654.png]]

## Propriétés importantes
- $\nearrow$ maturité $\implies$ Sensibilité $\nearrow$
- $\searrow$ coupon $\implies$ Sensibilité $\nearrow$
- Obligation ZC $\implies$ Duration = Maturité
- Obligation ZC $\implies$ Sensibilité $\approx$ Maturité
- $\searrow$ Taux $\implies$ Sensibilité $\nearrow$
## Cotation de l'obligation
La valeur actuelle de l'obligation contient le montant coupon, plus la date de détachement se rapproche plus le montant du coupon est intégré dans la valeur actuelle de l'obligation. Une fois le coupon détaché, la valeur actuelle de l'obligation perd brusquement cette valeur. **Cela explique pourquoi le prix des obligations montre un saut lors du détachement des coupons.**
On décompose donc usuellement le prix d'une obligation en deux :
- Le **Cours** (ou **Pied de coupon**) \[***Clean Price***]
	- $$Clean \space Price = Valeur \space Actuelle \space(Dirty \space Price) \space - \space Coupon \space Couru$$
- **Coupon Couru**
	- $$Coupon \space Couru = Taux \space Nominal * (n/N)$$
	- Avec :
		- $n$ : ***nombre jours écoulés depuis le début de la période d'intérêts***
		- $N$ : ***nombre de jours de la période d'intérêts***
On obtient le prix **pied de coupon** en soustrayant de la valeur actuelle le **coupon couru**, on obtient alors un **cours** plus régulier facilitant les comparaisons de prix entre obligations.

![[Pasted image 20251127172006.png]]

## Notes et informations importantes :
- L'obligation est **cotée** via son ***prix pied de coupon*** appelé aussi ***Cours ou Clean Price***
- L'obligation est **échangée** à sa ***Valeur Actuelle*** appelée aussi ***Dirty Price***