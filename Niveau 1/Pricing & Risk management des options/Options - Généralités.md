# Options – Généralités et premières propriétés

## Plan

### Généralités sur les options européennes
- Définition
- Payoff et stratégie d’exercice
- Utilisations des options
- Vocabulaire

### Premières propriétés
- Hypothèse d’Absence d’Opportunités d’Arbitrage (AOA)
- Inégalités et parité call-put
- Déterminants des prix d’options

---

## Les options européennes (« vanilles »)

### Call européen
Un call européen est une option d’achat.  
Son détenteur a la possibilité, mais pas l’obligation, d’acheter un actif $S$ à une date future (maturité) et à un prix fixé à l’avance appelé prix d’exercice ou strike $K$.

L’actif $S$ est appelé actif sous-jacent.

**Exemple :**
- Call sur action Orange
- Strike : 10 €
- Maturité : 3 mois
- Cours actuel : 10.19 €

---

### Put européen
Un put européen est une option de vente.  
Il donne le droit de vendre l’actif sous-jacent à un prix donné à l’échéance de l’option.

---

## Option vs Forward

- Une option donne un droit sans obligation et nécessite le paiement d’une prime.
- Un forward est un engagement ferme : l’acheteur est tenu d’acheter l’actif au prix convenu, même si cela lui est défavorable.
- Le prix forward est fixé de sorte que le contrat soit équitable, sans paiement initial.

---

## Stratégie d’exercice (Call)

À maturité :
- Si $S_T > K$, j’exerce le call et je gagne $S_T - K$
- Si $S_T < K$, je n’exerce pas et le gain est nul

---

## Payoff

### Call
$$
\max(S_T - K, 0)
$$

### Put
$$
\max(K - S_T, 0)
$$

---

## Physical settlement vs Cash settlement

- **Physical settlement** : achat réel de l’actif au prix $K$
- **Cash settlement** : encaissement direct du payoff

**Exemple :**
- Strike : 100
- Cours à maturité : 120
- Gain : 20

---

## Pourquoi utiliser des options ?

- Instrument de couverture et de gestion des risques
- Instrument spéculatif (effet de levier)
- Moyen de prendre position sur la volatilité

---

## Exemples de couverture

### Options de taux
- Cap : garantit un taux maximal
- Floor : garantit un taux minimal

### Options de change
Protection contre la variation du taux de change tout en conservant un potentiel favorable.

### Options actions
Achat de puts pour se protéger contre une forte baisse des marchés.

---

## Effet de levier des options

Investissement initial : 1000 €

| Cours dans 1 an | Actions | Options |
|---------------|---------|---------|
| 80 | -20 % | -100 % |
| 100 | 0 % | -100 % |
| 130 | +30 % | +200 % |

Les options amplifient les gains mais exposent à une perte totale.

---

## Position sur la volatilité

Une option permet de parier :
- sur le niveau du sous-jacent
- sur la volatilité, notamment via une couverture delta-neutre

---

## Moneyness

- **In the money (ITM)** : exercice immédiatement profitable
- **At the money (ATM)** : strike proche du prix du sous-jacent
- **Out of the money (OTM)** : aucun gain à l’exercice

Plus une option est ITM, plus elle est chère.

---

## Hypothèse d’Absence d’Opportunités d’Arbitrage (AOA)

Il n’est pas possible de réaliser un gain certain sans investissement initial et sans risque.

Formellement :
$$
X_0 = 0,\quad X_T \geq 0,\quad P(X_T > 0) > 0
$$

Sous AOA, deux portefeuilles ayant le même payoff final ont la même valeur aujourd’hui.

---

## Portefeuille de réplication

Si un portefeuille $X$ réplique exactement le payoff d’un call :
$$
X_T = (S_T - K)^+
$$

Alors le prix du call est égal à la valeur actuelle de ce portefeuille.

---

## Inégalités fondamentales

$$
C_0 \leq S_0
$$

$$
P_0 \leq K e^{-rT}
$$

---

## Pricing d’un forward par réplication

Payoff du forward :
$$
V_T = S_T - K
$$

Valeur aujourd’hui :
$$
V_0 = S_0 - K e^{-rT}
$$

Prix forward équitable :
$$
F_0 = S_0 e^{rT}
$$

---

## Forward avec dividendes

Si un dividende $D$ est versé avant maturité :
$$
F_0 = S_0 e^{rT} - D e^{r(T-t)}
$$

---

## Parité Call-Put

Sans dividendes :
$$
C_0 - P_0 = S_0 - K e^{-rT}
$$

Avec dividendes :
$$
C_0 - P_0 = S_0 e^{-dt} - K e^{-rT}
$$

Un call moins un put équivaut à un forward synthétique.

---

## ATM spot vs ATM forward

- **ATM spot** : $K = S_0$
- **ATM forward** : $K = S_0 e^{rT}$

Dans ce cas :
$$
C_0 = P_0
$$

---

## Déterminants du prix d’une option

Par ordre d’importance :
1. Prix du sous-jacent
2. Volatilité
3. Temps jusqu’à maturité
4. Taux d’intérêt
5. Dividendes

---

## Sensibilités (Grecs)

| Facteur | Call | Put |
|------|------|------|
| Delta | > 0 | < 0 |
| Vega | > 0 | > 0 |
| Theta | < 0 | < 0 |
| Rho | > 0 | < 0 |

---

## Exercice

Montrer, en utilisant l’AOA, que le prix d’un call est une fonction convexe du strike :

$$
C_0\left(\frac{K_1 + K_2}{2}\right) \leq \frac{C_0(K_1) + C_0(K_2)}{2}
$$
