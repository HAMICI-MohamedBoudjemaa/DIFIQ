La courbe des taux est la courbe à un instant $t$ de l'évolution du taux en fonction de la maturité![[Pasted image 20251126094255.png]]
Il y a autant de courbes des taux que de marchés de taux :
- Courbe Interbancaire (ou "Courbe Swap" ou "Courbe Euribor")
- Courbe des obligations d'état (OAT)
- Courbes obligataires corporates
- Courbes des taux d'emprunt immobiliers
- etc...
La courbe interbancaire (Euribor/Swap) est composite et se compose généralement de **trois compartiments** :
- Court terme (<1 an) : taux de dépôt
- Moyen terme : contrats futures sur Euribor
- Long terme : Swap de taux
Cette courbe permet **d'évaluer et couvrir** un portefeuille, puisqu'elle répertorie les **instruments liquides** (dérivés de l'Euribor) permettant de gérer le **risque de taux**.
![[Pasted image 20251126094942.png]]

**Objectif :** Utiliser la courbe interbancaire pour évaluer un portefeuille de produits de taux
$$Courbe \space Interbancaire\overset {Pricing}{\longrightarrow}MTM \space Portefeuille $$
**Problème :** Impossible directement car les produits en portefeuille ont vieilli dont la valeur n'est plus lisible sur la courbe des taux !

**Solution :** On détermine ***la courbe zéro-coupons*** correspondant à la courbe interbancaire et on l'utilise pour évaluer notre portefeuille.
Afin de déterminer les prix zéro-coupons (ou **Discount Factors**), on utilise un ***bootstrap*** à partir des produits liquides sur le marché.
Formule du Discount Factor :
$$DF(T) = \frac {1}{(1+r(T))^T}$$
Avec :
- $r(T)$ : Taux zéro-coupon de maturité $T$

Formule générale :
$$DF(n) = \frac {P_n - C_n \sum_{i=1}^{n-1}DF(i)}{100+C_n}$$
Avec :
- $P_n$ : Prix de l'obligation de maturité $n$
- $C_n$ : Coupon de l'obligation de maturité $n$
On a donc :![[Pasted image 20251126100550.png]]

***Exemple*** :
![[Pasted image 20251126101200.png]]
**Le prix de la première obligation nous donne DF(1) :**
$$104.25 = 105.5 * DF(1) \implies DF(1) = 104.25/105.5$$
**De DF(1) on passe à DF(2) :**
$$102.73 = 3.2*DF(1) + 103.2*DF(2)$$
$$DF(2) = \frac {102.73-3.2*DF(1)}{103.2}$$
**De DF(1) et DF(2) on passe à DF(3) :**
$$107.47 = 4.8 * DF(1) + 4.8 * DF(2) + 104.8 * DF(3)$$
$$DF(3) = \frac {107.47-4.8*(DF(1)+DF(2))}{104.8}$$
## Notes et informations importantes :
- La courbe zéro-coupon est un intermédiaire de calcul indispensable à une évaluation fine des produits de taux
- Il y a autant de courbe ZC que de courbes de marché. On détermine la courbe ZC **associée à telle ou telle courbe de marché**
- La courbe ZC est déterminée via **boostrap** à partir des produits de marché liquides
- Pour évaluer un produit de taux, il suffit de savoir exprimer sa valeur en fonction des $DFs$ puis d'utiliser la courbe ZC déterminée à partir du marché correspondant