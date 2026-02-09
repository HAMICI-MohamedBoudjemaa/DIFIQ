# Gestion de Portefeuille - Synthèse Complète

## 1. Rendement des Actifs Financiers
Le rendement mesure la performance d'un investissement sur une période.

* **Rendement Arithmétique :** $R_{T} = \frac{W_{T}}{W_{0}} - 1$
* **Log-rendement (continu) :** $R_{T}^{c} = \ln\left(\frac{W_{T}}{W_{0}}\right)$
* **Propriété d'additivité :** Le log-rendement sur $[0, T]$ est la somme des log-rendements intermédiaires.
* **Rendement d'un portefeuille :** $R_p = \sum_{i=1}^n w_i R_i$ (moyenne pondérée des rendements des actifs).

---

## 2. Markowitz : Analyse Risque-Rendement
L'objectif est de minimiser la variance pour un niveau d'espérance donné.

* **Espérance du portefeuille :** $E(R_p) = w^T \mu$
* **Variance du portefeuille :** $\sigma_p^2 = w^T \Sigma w$
  * Où $w$ est le vecteur des poids et $\Sigma$ la matrice de variance-covariance.
* **Frontière Efficiente :** Ensemble des portefeuilles qui maximisent l'espérance pour un risque donné. Elle est représentée par une hyperbole dans le plan $(\sigma, \mu)$.

---

## 3. Optimisation de Markowitz
### Sans actif sans risque
On cherche à minimiser $\frac{1}{2} w^T \Sigma w$ sous les contraintes $w^T \mathbf{1} = 1$ et $w^T \mu = \mu_p$.
* **Portefeuille de Variance Minimale (MVP) :** $w_{mvp} = \frac{\Sigma^{-1} \mathbf{1}}{\mathbf{1}^T \Sigma^{-1} \mathbf{1}}$

### Avec un actif sans risque ($r_f$)
La frontière devient une droite appelée **Capital Allocation Line (CAL)**.
* **Portefeuille de Tangence ($w_T$) :** C'est le portefeuille risqué qui maximise le ratio de Sharpe.
* **Théorème de Séparation :** Tout investisseur efficient détient une combinaison de l'actif sans risque et du portefeuille de tangence.

---

## 4. Modèle d'Équilibre (CAPM / MEDAF)
À l'équilibre, le portefeuille de tangence est le **Portefeuille de Marché ($M$)**.

* **Capital Market Line (CML) :** $E(R_p) = r_f + \frac{E(R_M) - r_f}{\sigma_M} \sigma_p$
* **Security Market Line (SML) :** $E(R_i) = r_f + \beta_i (E(R_M) - r_f)$
* **Le Bêta ($\beta_i$) :** Mesure le risque systématique.
  $$\beta_i = \frac{Cov(R_i, R_M)}{Var(R_M)}$$

---

## 5. Indicateurs de Performance
Ils permettent d'évaluer la qualité de la gestion (ajustée au risque).

* **Ratio de Sharpe :** $S_p = \frac{E(R_p) - r_f}{\sigma_p}$ (Risque total)
* **Ratio de Treynor :** $T_p = \frac{E(R_p) - r_f}{\beta_p}$ (Risque de marché)
* **Alpha de Jensen ($\alpha_p$) :** Performance anormale par rapport au CAPM.
  $$\alpha_p = E(R_p) - [r_f + \beta_p (E(R_M) - r_f)]$$
* **Ratio d'Information :** $IR = \frac{\alpha_p}{\sigma(\epsilon_p)}$ (où $\sigma(\epsilon_p)$ est la Tracking Error).

---

## 6. Risque Systématique vs Spécifique
La variance d'un actif peut être décomposée comme suit :
$$\sigma_i^2 = \beta_i^2 \sigma_M^2 + \sigma^2(\epsilon_i)$$
* **Risque Systématique :** $\beta_i^2 \sigma_M^2$ (Non diversifiable).
* **Risque Spécifique (Idiosyncratique) :** $\sigma^2(\epsilon_i)$ (Éliminé par la diversification).

---

## 7. Modèles à Facteurs
Ils expliquent les rendements par plusieurs sources de risque.

* **Modèle à un facteur :** $R_i = \alpha_i + \beta_i F + \epsilon_i$
* **Modèles Multi-facteurs :** $R_i = E(R_i) + \sum_{k=1}^K \beta_{ik} F_k + \epsilon_i$
  * Les facteurs peuvent être macroéconomiques ou basés sur des caractéristiques de titres (ex: Fama-French).

---

## 8. Modèle APT (Arbitrage Pricing Theory)
L'APT repose sur l'absence d'opportunité d'arbitrage.

* **Formule de l'APT :** $E(R_i) = \lambda_0 + \sum_{k=1}^K \beta_{ik} \lambda_k$
  * $\lambda_0$ est généralement le taux sans risque.
  * $\lambda_k$ est la prime de risque associée au facteur $k$.
* Contrairement au CAPM, l'APT ne nécessite pas d'identifier le portefeuille de marché, mais nécessite d'identifier les facteurs sources de risque systématique.

---
**Points clés pour l'examen :**
1. Savoir passer d'un rendement arithmétique à un log-rendement.
2. Calculer le poids du portefeuille de variance minimale.
3. Interpréter le Bêta (si $\beta > 1$, l'actif est plus risqué que le marché).
4. Calculer l'Alpha de Jensen pour juger un gérant.