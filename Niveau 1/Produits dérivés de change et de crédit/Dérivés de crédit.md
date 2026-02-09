
# Credit Default Swaps (CDS)

## 1. Fondamentaux du Risque de Crédit
Le taux d'intérêt risqué ($r$) se décompose en : $r = r_{REF} + CS$ (où $CS$ est le **Credit Spread**).

### Quantification de la Perte Attendue (Expected Loss)
L'**Expected Loss (EL)** est le coût moyen du risque :
> **$EL = EaD \times CPD \times LGD$**

* **EaD (Exposure at Default) :** Montant exposé au moment du défaut.
* **CPD (Cumulative Probability of Default) :** Probabilité que l'émetteur fasse défaut.
* **LGD (Loss Given Default) :** Pourcentage de perte réelle après recouvrement ($1 - \text{Taux de Recouvrement}$).

---

## 2. Fonctionnement du CDS
Un CDS est un contrat d'assurance contre le défaut d'un émetteur (entité de référence).

### Les deux jambes du contrat :
1. **Premium Leg (Jambe de prime) :** L'acheteur de protection paie une prime périodique (le spread de CDS) au vendeur.
2. **Protection Leg (Jambe de protection) :** En cas d'événement de crédit, le vendeur paie la perte subie (souvent $100\% - \text{Recouvrement}$) à l'acheteur.



### Événements de Crédit (ISDA) :
Le déclenchement de la protection nécessite un événement officiel :
* Faillite (*Bankruptcy*).
* Défaut de paiement (*Failure to Pay*).
* Restructuration de la dette.

---

## 3. Aspects Opérationnels et Standardisation
Depuis le "Big Bang" de 2009, le marché est très standardisé :
* **Coupons fixes :** Généralement 100 bps (Investment Grade) ou 500 bps (High Yield).
* **Upfront :** Soulte payée à l'initiation du contrat pour compenser l'écart entre le coupon fixe et le spread de marché.
* **Dates d'échéance :** Standards (20 mars, 20 juin, 20 sept, 20 déc).

---

## 4. Pricing et Courbes de Défaut

### Valeur de Marché (MtM)
La valeur d'un CDS dépend de la probabilité de défaut survie de l'entité.
* Si le risque de crédit augmente, le prix du CDS (spread) monte.
* La **Sensibilité (Risky PV01)** mesure la variation de la valeur du CDS pour un décalage de 1 bp du spread de crédit.

### Bootstrapping et Probabilités de Défaut
Le marché utilise les prix des CDS de différentes maturités (1 an, 2 ans, 5 ans...) pour construire une **Courbe de Probabilité de Défaut**.



> [!info] Spread vs Probabilité
> Les probabilités de défaut implicites du marché sont généralement **2 à 3 fois supérieures** aux taux de défaut historiques car elles incluent une **prime de risque** et une **prime de liquidité**.

---

## 5. Cas Particulier : Le CDS Souverain
Contrairement aux entreprises, le défaut d'un État est plus complexe (souvent traité via la restructuration). Le CDS souverain est un indicateur clé de la santé budgétaire d'un pays.

---
**Points clés pour l'examen :**
- Savoir calculer l'Upfront (différence entre spread de marché et coupon fixe $\times$ Risky PV01).
- Comprendre que l'acheteur de CDS est "Short Crédit" (il profite si la signature se dégrade).
- Relation inverse : Si le taux de recouvrement (*Recovery*) baisse, le spread de CDS augmente.