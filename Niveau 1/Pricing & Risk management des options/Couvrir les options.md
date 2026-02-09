# Couvrir les options

**Antonin Chaix**

---

## Les sensibilités (les « grecques »)

### Delta (Δ)
Sensibilité du prix de l’option au cours du sous-jacent.

### Gamma (Γ)
Sensibilité du delta aux variations du sous-jacent.

### Thêta (θ)
Sensibilité du prix de l’option à l’écoulement du temps.

### Véga (ν)
Sensibilité du prix de l’option à la volatilité du sous-jacent.

### Rhô (ρ)
Sensibilité du prix de l’option au taux d’intérêt sans risque.

---

## Expression des grecques

### Notations
Les grecques sont définies comme des dérivées partielles du prix de l’option par rapport aux variables de marché.

- Delta : $\frac{\partial C}{\partial S}$
- Gamma : $\frac{\partial^2 C}{\partial S^2}$
- Véga : $\frac{\partial C}{\partial \sigma}$
- Thêta : $\frac{\partial C}{\partial t}$
- Rhô : $\frac{\partial C}{\partial r}$

---

## Pense-bête : signes des grecques

| Position | Delta | Gamma | Thêta | Véga | Rhô |
|--------|-------|-------|-------|------|-----|
| Achat Call | > 0 | > 0 | < 0 | > 0 | > 0 |
| Vente Call | < 0 | < 0 | > 0 | < 0 | < 0 |
| Achat Put | < 0 | > 0 | < 0 | > 0 | < 0 |
| Vente Put | > 0 | < 0 | > 0 | < 0 | > 0 |

---

## Delta selon la moneyness

### Call
- OTM : $0 < \Delta < 0.5$
- ATM : $\Delta \approx 0.5$
- ITM : $0.5 < \Delta < 1$

### Put
- OTM : $-0.5 < \Delta < 0$
- ATM : $\Delta \approx -0.5$
- ITM : $-1 < \Delta < -0.5$

---

## Couverture en delta (Delta Hedging)

Objectif :
👉 Neutraliser le risque lié aux variations du sous-jacent.

Principe :
- Acheter ou vendre le sous-jacent en proportion du delta de l’option.
- Réajuster la couverture au fil du temps.

On parle de **gestion delta-neutre**.

---

## Exemple de couverture en delta

Vente d’un call ATM :
- $K = S_0 = 100$
- $T = 1$ an
- Prix du call : $C_0 = 10$
- Delta initial : $\Delta_0 \approx 0.5$

Position :
- Short call → delta = −0.5
- Achat de 0.5 action pour neutraliser le delta

Flux initial :
$$
+10 - 0.5 \times 100 = -40
$$

---

## Réajustement de la couverture

### Cas 1 : le sous-jacent monte à 110

- Delta passe de 0.5 à 0.6
- Sous-couverture → achat de 0.1 action

Coût :
$$
-110 \times 0.1
$$

---

### Cas 2 : le sous-jacent redescend à 105

- Delta passe de 0.6 à 0.55
- Sur-couverture → vente de 0.05 action

Gain :
$$
+105 \times 0.05
$$

---

## Pourquoi le delta hedge fonctionne ?

À maturité :

- Si $S_T < K$ → $\Delta \rightarrow 0$
  - Le call n’est pas exercé
  - On ne détient plus d’actions

- Si $S_T > K$ → $\Delta \rightarrow 1$
  - Le call est exercé
  - On détient l’action à livrer

---

## L’impact du gamma

En vendant des options :

- Gamma négatif
- On achète le sous-jacent après une hausse
- On vend après une baisse

👉 La convexité joue contre le vendeur.

Les pertes augmentent :
- quand la volatilité réalisée est élevée
- quand l’actif évolue proche du strike
- quand la maturité est courte

---

## Gamma vs Thêta

Pour un vendeur d’option delta-couvert :

- Gain certain : **thêta** (érosion du temps)
- Perte incertaine : **gamma** (réajustements en delta)

$$
P\&L = \text{Thêta encaissé} - \text{Pertes liées au gamma}
$$

---

## Acheter vs vendre la volatilité

### Vendre des options
- Encaissement de la prime
- Pari : volatilité réalisée < volatilité implicite

### Acheter des options
- Paiement de la prime
- Pari : volatilité réalisée > volatilité implicite

---

## TP : Delta hedge

Vente d’un call ATM :
- $S_0 = K = 100$
- $T = 1$ an
- $C_0 = 10$
- $r = 0$

### Scénarios
1. L’actif monte à 110 puis reste stable
2. L’actif monte à 110, chute à 90, puis remonte à 110

Calculer le P&L final du trading.

---

## Vision en P&L quotidien

À chaque date $t_i$ :
- Position short call
- Couverture en delta
- Position de prêt / emprunt

La valeur du portefeuille est nulle à chaque instant, mais le P&L dépend :
- des variations du sous-jacent
- du gamma
- du thêta

---

## Volatilité implicite vs volatilité réalisée

Sous Black & Scholes (r = 0) :

- Thêta est lié au gamma
- Le P&L dépend de :
$$
\text{Vol implicite} - \text{Vol réalisée}
$$

👉 Trader des options, c’est avant tout **trader la volatilité**.
