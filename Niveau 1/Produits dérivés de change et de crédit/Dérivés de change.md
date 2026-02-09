# Marché des Changes et Dérivés (FX)

## 1. Bases du marché du FX
Le marché des changes est le premier marché mondial en termes de volume (plus de 5 000 milliards $ par jour).
* **Cotation :** Une paire de devises se note **Devise Directrice / Devise Cotée** (ex: EUR/USD).
* **Spot :** Transaction immédiate (livraison à $J+2$).
* **Pip (Percentage in Point) :** La 4ème décimale d'une cotation (sauf pour le JPY où c'est la 2ème).

---

## 2. Le Change à Terme (Forward)
Le prix d'un forward n'est pas une prédiction du futur, mais le résultat d'un **arbitrage de taux**.

### Points de Swap (Report / Déport)
Le cours à terme est déterminé par le différentiel de taux d'intérêt entre les deux devises.
> **Formule simplifiée :** $F = S \times \frac{1 + r_{cotée} \times T}{1 + r_{dir} \times T}$

* **Report :** La devise directrice est plus "chère" à terme car son taux est plus bas que celui de la devise cotée.
* **Déport :** La devise directrice est plus "bon marché" à terme (taux plus élevé).



---

## 3. FX Swaps et Cross Currency Swaps
* **FX Swap :** Combinaison d'un spot et d'un forward inverse. Utilisé pour gérer la liquidité ou décaler une échéance (Rollover).
* **NDF (Non-Deliverable Forward) :** Contrat à terme sur des devises non convertibles (ex: BRL, CNY, INR). Pas de livraison physique, règlement de la différence en USD.

---

## 4. Options de Change

### Stratégies Vanille
* **Achat de Call :** Droit d'acheter la devise à un prix fixé (protection contre la hausse).
* **Achat de Put :** Droit de vendre la devise à un prix fixé (protection contre la baisse).

### Options Exotiques et Barrières
* **Digitales :** Payent un montant fixe si une condition est remplie.
* **Barrières :**
  - **Knock-In :** L'option s'active si la barrière est touchée.
  - **Knock-Out :** L'option disparaît si la barrière est touchée.



---

## 5. Produits Structurés de Change
Ils permettent de réduire le coût de la prime ou d'améliorer le rendement d'un dépôt.

* **Cylinder (Tunnel) :** Achat d'un Call et vente d'un Put (souvent à prime nulle). Permet de fixer une fourchette de cours pour le futur.
* **Accumulateurs :** Permettent d'acheter des devises à un cours préférentiel tant qu'une barrière n'est pas touchée.
* **Range Accrual :** Dépôt dont le taux dépend du temps passé par le spot à l'intérieur d'un range prédéfini.



---
**Points clés pour l'examen :**
- Calculer un cours Forward à partir du Spot et des taux (ou des points de swap).
- Comprendre l'impact des taux : la devise avec le taux le plus élevé est celle qui est en **déport** (se vend moins cher à terme).
- Maîtriser le vocabulaire : *Strike*, *Barrier*, *Premium*, *Expiry*.