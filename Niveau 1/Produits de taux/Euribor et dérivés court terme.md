# Risque de taux
Le risque de taux peut être vu de deux façons différentes

## Risque de variation de la valeur de marché
**Je suis endetté à taux fixe :**
- La **valeur** de ma dette **est** **sensible au niveau des taux** : **Risque de taux**
- Les cash-flows déboursés (intérêts payés) sont **fixes** : **Pas de risque de cash-flows**
- Selon les normes *IFRS* je subis un risque de **juste valeur** (ou **fair value**)
- Pour **Couvrir** ce risque, j'utilise un ***fair value hedge*** qui consiste a entrer dans un **swap receveur** *(Je paie le taux variable et je reçois le fixe)*
	- Le risque se transforme en **risque de cash-flows**
## Risque de variation des cash-flows
**Je suis endetté à taux variable :**
- La **valeur** de ma dette **n'est** **pas sensible au niveau des taux** : **Pas de risque de taux**
- Les cash-flows déboursés (intérêts payés) sont **variables** : **Risque de cash-flows**
- Selon les normes *IFRS* je subis un risque de **cash-flows**
- Pour **Couvrir** ce risque, j'utilise un ***fair value hedge*** qui consiste a entrer dans un **swap payeur** *(Je paie le taux fixe et je reçois le variable)*
	-  Le risque se transforme en **risque de juste valeur**

# Marché des taux
![[Pasted image 20251128160052.png]]

# Taux Euribor
 Les taux **Euribor** sont les taux interbancaires de la zone Euro :
* Les maturités sont : **1W, 1M, 3M, 6M, 12M**
- Ils sont fixés par l'**European Money Markets** Institute (EMMI) à partir de données déclaratives d'un panel de banques de la zone Euro
- Depuis 2020, la méthodologie hybride permet d'inclure les transactions réelles dans son calcul
- ***NB : Pour les autres devises (USD, JPY, GPB, CHF) : Taux Libor***
- *Néanmoins, l'activité interbancaire est très limitée depuis 2008, les banques se finançant directement auprès de la BCE*
## Fonctionnement d'un emprunt Euribor
Le fonctionnement est le suivant :
1. Fixing du taux Euribor (à la date J)
2. Début de la période d'intérêt $T_1$ (à J+2)
3. Fin de la période d'intérêt à $T_2$ (à J+$\delta$)
4. $\delta$  = $(T_2 - T_1) / 360$ (base Exact/360)
5. $Intérêt = M*Euribor*\delta$
Exemple avec un Emprunt de **100 M€** à Euribor 6 mois.![[Pasted image 20251128162203.png]]

## Relation Euribor / Zéro-Coupons
Pour faire le bootstrap ZC de la courbe interbancaire, il faut savoir calculer les différents *Discount Factors* de l'Euribor.
Dans un emprunt Euribor, nous avons deux flux :
1. $+N$ en $T_1$ 
2. $-N(1+\delta*Euribor)$ en $T_2$
On a donc :
$$N*DF(T_1) + -N(1+\delta*Euribor)*DF(T_2) = 0$$
Soit :$$DF(T_2) = \frac {DF(T_1)}{1+\delta*Euribor} \approx \frac {1}{1+\delta*Euribor}$$
Et : $$Euribor = \frac {1}{\delta}(\frac {DF(T_1)}{DF(T_2)}-1)$$
# Taux JJ : EONIA (devenu €STR)
**EONIA** = ***Euro Overnight Index Average***
- Taux de référence quotidien des prêts interbancaires en blanc effectués au jour-le-jour dans la zone Euro.
- *Ce taux n'existe plus depuis Janvier 2022*
Il est remplacé par l'**€STR** : ***European Short Term Rate***
- L'**€STR** reflète le taux d'emprunt au jour-le-jour (JJ) sur le marché monétaire Européen
L'**EONIA** était défini en spread par rapport à l'**€STR**
- **EONIA =  €STR + 8.5BP**

| **Caractéristique**      | **EONIA (Euro OverNight Index Average) (Obsolète)**                                                                          | **€STR (Euro Short-Term Rate) (Actuel)**                                                                                                 |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Administrateur**       | European Money Market Institute (EMMI)                                                                                       | **Banque Centrale Européenne (BCE)**                                                                                                     |
| **Définition**           | Taux moyen pondéré des prêts interbancaires **non garantis** **déposés** au jour le jour par un **panel de banques**.        | Taux d'intérêt des emprunts au jour le jour **non garantis** que les banques **contractent** auprès d'institutions financières.          |
| **Méthode de Calcul**    | Basé sur les **déclarations** d'un **panel restreint** de banques. Susceptible de biais ou de manipulations (moins robuste). | Basé sur les **transactions réelles et effectives** collectées par la BCE (plus large et plus fiable). Calcul **pondéré par le volume**. |
| **Heure de Publication** | Fin de journée (historiquement 19h00 CET).                                                                                   | Tôt le matin (8h00 CET) à **J+1** (sur les transactions de la veille).                                                                   |
## Fonctionnement de l'€STR
Le fonctionnement est le suivant :
1. Début de la période d'intérêt $T_1$ (à J)
2. Fin de la période d'intérêt à $T_2$ (à J+$1$)
3. $\delta$  = $(T_2 - T_1) / 360$ (base Exact/360) \[ $= 1/360$ ou $= 3/360$ (si week-end)]
4. $Intérêt = M*Euribor*\delta$
Exemple avec un Emprunt de **1 Md€** à **€STR**![[Pasted image 20251128170304.png]]

# FRA
FRA = ***Forward Rate Agreement***
- C'est un **contrat forward** spécifiant à terme l'échange d'un taux fixe déterminé à l'avance et d'un taux variable (EURIBOR/LIBOR)
- Comme tout **Forward**, c'est un contrat de **gré à gré (OTC)**
- C'est un produit dérivé permettant de se garantir **aujourd'hui** un taux de prêt/emprunt pour une période future, il **permet donc de se prémunir contre un risque de cash-flows**
- Il peut être vu comme un ***Swap Forward*** à une période d'intérêt
## Flux d'un FRA
**Achat d'un FRA 12x18** : FRA de maturité 1 an portant sur l'Euribor 6 mois (nominal N).
![[Pasted image 20251130175426.png]]
Ou vu autrement :![[Pasted image 20251130175630.png]]

## Utilisation du FRA comme couverture
Un trésorier anticipe un emprunt de **100M€** sur **6 mois** dans **1 an** et veut couvrir son *risque de cash-flows*.
Pour cela, il va :
1. **Aujourd'hui** : Acheter un **FRA 12x18**
2. **Dans 1 an** : Emprunter **100M€ à Euribor**
Les flux seront donc :
3. En $T_1$ (dans 1 an) : Il reçoit 100M€
4. En $T_2$ (dans 18 mois) : Il donne $100M * (1+ \delta * Euribor)$ et reçoit $100M * \delta *(Euribor - TauxFRA)$
	- Ce qui donne en net $100M * (1+ \delta * TauxFRA)$

On passe donc de (Emprunt Euribor simple): ![[Pasted image 20251130182545.png]]
A (Emprunt Euribor + FRA):
![[Pasted image 20251130182604.png]]

## Relation Taux FRA et Zéro-Coupons
L'actualisation des flux doit donner 0 : $$100 * DF(T_1) - 100 * (1 + \delta * TauxFRA) * DF(T_2) = 0$$
La relation entre Taux FRA et les $DFs$ est donc la même que pour l'Euribor :$$DF(T_2) = \frac {DF(T_1)}{1 + \delta * TauxFRA}$$
$$TauxFRA = \frac {1}{\delta} (\frac {DF(T_1)}{DF(T_2)} - 1)$$

# Forward
On appelle **taux forward** le taux qu'on peut se garantir **aujourd'hui** pour une **période d'intérêt future**.
On a vu précédemment que le ***FRA*** peut être considéré comme un ***taux Euribor forward***.
En convention actuarielle on a :![[Pasted image 20251130191032.png]]

## Calcul du taux forward
L'idée derrière le calcul du taux forward, est la suivante :
- La capitalisation entre $t=0$ et $T_2$ à $r(T_2)$est égale aux capitalisations entre $t=0$ et $T_1$ à $r(T_1)$ puis entre $T_1$ et $T_2$ à $r_{fwd}$ 
- Sinon, il y aurait arbitrage
$$(1+r(T_1))^{T_1}*(1+r_{fwd})^{T_2-T_1}=(1+r(T_2))^{T_2}$$![[Pasted image 20251130192804.png]]

# Futures sur Euribor
En opposition aux **FRA**, les futures sur Euribor se traitent sur un marché organisé. Les échanges passant par *La Chambre de Compensation* (avec appels de marge quotidiens).

|                        | Forward (OTC)         | Future (Marché Organisé |
| ---------------------- | --------------------- | ----------------------- |
| Personnalisation       | ~={green}Importante=~ | ~={red}Nulle=~          |
| Liquidité              | ~={red}Faible=~       | ~={green}Grande=~       |
| Coût de transaction    | ~={red}Elevés=~       | ~={green}Faibles=~      |
| Risque de Contrepartie | ~={red}Important(*)=~ | ~={green}Faible=~       |
*(\*) C’est nativement le cas, mais de plus en plus, les accords de collatéral se systématisent sur les dérivés OTC, éliminant ainsi le risque de contrepartie de ces transactions*
## Specs d'un future sur Euribor
- **Maturité** : 2J ouvrés avant le $3^{ème}$ mercredi du mois de la maturité
- **Prix côté** : $100 * (1 - TauxFuture)$
- **Valeur du contrat** : $1,000,000 \texteuro * (1 - 0.25 * TauxFuture)$
- Et à maturité : **Taux Future** = Fixing de l'**Euribor 3 mois** 
	- *Fin du contrat. Plus de spéculation. Le taux future devient égal à l'Euribor du jour. C'est ce qui garantit la convergence du prix du contrat vers la réalité économique.*
## Payoff d'un contrat future
La valeur du contrat n’a pas de sens en tant que telle, ce sont juste les variations de valeur du contrat qui importent, et la variation.

Supposons l'**achat d'un contrat future** le gain/perte correspond à la différence entre la valeur du contrat à la date d'achat vs date de vente.
$$\Delta V = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t_{achat}}-TauxFuture_{t_{vente}})$$
Ce qui donne à maturité :$$\Delta V = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t_{achat}} -Euribor)$$
## Future vs FRA
Les payoff des Futures et des FRA sont similaires (mais en **sens inversé**):
**Future** : $$\Delta V = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t_{achat}} -Euribor)$$
**FRA** : $$N * \delta *(Euribor - TauxFRA_{t_{achat}})$$
## Appels de marge
Le payoff d'un future, néanmoins, ne se perçoit pas en one-shot à la fin du contrat, mais via des appels de marge quotidiens :
$$\Delta V_{t+1j} = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t} -TauxFuture_{t+1j})$$
$$\Delta V_{t+2j} = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t+1j} -TauxFuture_{t+2j})$$
$$...$$
$$\Delta V_{T-1j} = 1,000,000 \texteuro * 0.25 * (TauxFuture_{T-2j} -TauxFuture_{T-j})$$
$$\Delta V_{T} = 1,000,000 \texteuro * 0.25 * (TauxFuture_{T-1j} - Euribor_{T})$$

La somme des $\Delta V_{t_i}$ donne bien : $$\Delta V = \Delta V_{t+1j} + \Delta V_{t+2j}...+\Delta V_{T-1j}+\Delta V_{T} = 1,000,000 \texteuro * 0.25 * (TauxFuture_{t_{achat}} -Euribor)$$Néanmoins, ces appels de marge ne sont pas sans effets, ils expliquent le fameux biais de convexité entre taux future et taux FRA.
## Biais de convexité future / FRA
Le biais est le suivant (quand on est **acheteur d'un Future**):
- Les taux baissent $\implies$ On reçoit l'appel de marge dans un contexte défavorable de taux bas
- Les taux montent $\implies$ On paie l'appel de marge avec un emprunt dans un contexte défavorable à taux élevés
**En conséquence** : 
- En prix : Le prix d'un Future est inférieur au prix d'un FRA de mêmes caractéristiques
- En taux : $TauxFuture > TauxFRA$
	- $TauxFuture = TauxFRA + Ajustement \space Convexité$
