
---

### 1. Simulation des Variables Aléatoires

Avant de modéliser des actifs financiers, il est nécessaire de savoir générer du hasard numériquement.

- **Générateurs de nombres pseudo-aléatoires (PRNG) :** Le cours présente des algorithmes (comme le générateur congruentiel linéaire) pour simuler une loi uniforme sur $[0, 1]$.
    
- **Méthode d'inversion :** Utilisation de la fonction de répartition inverse ($F^{-1}$) pour transformer une loi uniforme en n'importe quelle autre loi.
    
- **Simulation de la Loi Normale :** * **Méthode de Box-Muller :** Transforme deux variables uniformes en deux variables normales indépendantes.
    
    - **Algorithme de Marsaglia-Polar :** Une variante plus efficace évitant les fonctions trigonométriques coûteuses.
        
- **Vecteurs Gaussiens :** Utilisation de la **décomposition de Cholesky** ($A = LL^T$) pour simuler des variables corrélées à partir de variables indépendantes.
    

### 2. Méthodes de Monte Carlo

Le principe est d'estimer une espérance (le prix d'une option) par une moyenne empirique sur un grand nombre de simulations ($N$).

- **Convergence :** * **Loi Forte des Grands Nombres :** Garantit que la moyenne converge vers l'espérance quand $N \to \infty$.
    
    - **Théorème Central Limite :** Permet de quantifier l'erreur de calcul et de construire un **intervalle de confiance** proportionnel à $\frac{\sigma}{\sqrt{N}}$.
        
- **Réduction de la variance :** Techniques pour atteindre la même précision avec moins de simulations :
    
    - **Variables antithétiques :** Utiliser la symétrie des lois (ex: simuler $W$ et $-W$).
        
    - **Variables de contrôle :** Utiliser une variable proche dont on connaît l'espérance exacte.
        
    - **Stratification et Échantillonnage préférentiel (Importance Sampling) :** Concentrer les simulations dans les zones "utiles" (ex: quand l'option finit dans la monnaie).
        

### 3. Modélisation et discrétisation des processus

Pour évaluer des options dont le prix dépend du temps (options asiatiques, barrières, etc.), on simule des trajectoires.

- **Mouvement Brownien :** Construction de trajectoires par le schéma d'Euler.
    
- **Modèle de Black-Scholes :** Simulation du prix de l'actif via l'exponentielle du mouvement brownien.
    
- **Options dépendantes du chemin :**
    
    - **Asiatiques :** Dépendent de la moyenne des cours.
        
    - **Lookback :** Dépendent du maximum ou minimum atteint.
        
    - **Barrières :** L'option s'active ou s'éteint si un seuil est franchi.
        

### 4. Méthodes d'Arbres (Cox-Ross-Rubinstein)

Une alternative discrète au modèle de Black-Scholes.

- **Principe :** Le prix de l'actif peut monter ($u$) ou descendre ($d$) à chaque étape.
    
- **Arbitrage et Probabilité Risque-Neutre :** Calcul des probabilités de hausse/baisse pour que le rendement espéré soit le taux sans risque ($r$).
    
- **Évaluation à rebours (Backward Induction) :** On part de la maturité (valeur finale) et on remonte l'arbre jusqu'à aujourd'hui.
    
- **Options Américaines :** Les arbres sont particulièrement adaptés pour ces options car on peut vérifier à chaque nœud s'il est plus rentable d'exercer l'option immédiatement ou de la conserver.
    
Voici l'ajout des théorèmes et formules fondamentales pour compléter le résumé de votre cours de **Méthodes Numériques en Finance**.

---

### 1. Théorèmes de Convergence (Monte Carlo)

L'efficacité de la méthode de Monte Carlo repose sur deux piliers de la théorie des probabilités :

- Loi Forte des Grands Nombres (LFGN) : Elle garantit la convergence presque sûre de l'estimateur. Si $(X_i)_{i \geq 1}$ sont des variables i.i.d. d'espérance $\mu = E[f(X)]$, alors :
    
    $$\bar{I}_N = \frac{1}{N} \sum_{i=1}^N f(X_i) \xrightarrow[N \to \infty]{p.s.} E[f(X)]$$
    
- Théorème Central Limite (TCL) : Il permet de quantifier l'erreur de calcul. Pour $N$ grand, l'erreur de l'estimateur suit une loi normale :
    
    $$\sqrt{N} \left( \bar{I}_N - E[f(X)] \right) \xrightarrow{\mathcal{L}} \mathcal{N}(0, \sigma^2)$$
    
    C'est ce théorème qui impose une vitesse de convergence en $O(1/\sqrt{N})$, indépendante de la dimension du problème.
    

---

### 2. Simulation de la Loi Normale

Deux méthodes clés sont détaillées pour transformer l'aléa uniforme $U \sim \mathcal{U}(0,1)$ :

- Théorème de Box-Muller : Si $U_1, U_2 \sim \mathcal{U}(0,1)$ et sont indépendantes, alors les variables $X$ et $Y$ suivantes sont des normales centrées réduites indépendantes :
    
    $$X = \sqrt{-2\ln(U_1)} \cos(2\pi U_2)$$
    
    $$Y = \sqrt{-2\ln(U_1)} \sin(2\pi U_2)$$
    
- Décomposition de Cholesky (Vecteurs Gaussiens) : Pour simuler un vecteur $X$ de matrice de covariance $\Sigma$, on cherche une matrice triangulaire inférieure $L$ telle que $\Sigma = LL^T$. On obtient alors :
    
    $$X = \mu + L Z$$
    
    où $Z$ est un vecteur de variables normales $\mathcal{N}(0,1)$ indépendantes.
    

---

### 3. Modélisation Continue et Discrétisation

- Schéma d'Euler-Maruyama : Pour simuler une Équation Différentielle Stochastique (EDS) du type $dX_t = b(t, X_t)dt + \sigma(t, X_t)dW_t$ sur un pas de temps $\Delta t$, on utilise l'approximation :
    
    $$X_{t+\Delta t} \approx X_t + b(t, X_t)\Delta t + \sigma(t, X_t)\sqrt{\Delta t} Z$$
    
    (où $Z \sim \mathcal{N}(0,1)$).
    

---

### 4. Modèle Binomial (CRR)

- Formule de la Probabilité Risque-Neutre ($p$) : Dans l'arbre, pour éviter l'arbitrage, la probabilité d'une hausse est fixée par :
    
    $$p = \frac{e^{r\Delta t} - d}{u - d}$$
    
    où $u$ est le facteur de hausse, $d$ de baisse, et $r$ le taux sans risque.
    
- Algorithme de l'Espérance Conditionnelle : Le prix d'une option européenne au nœud $(n, i)$ est calculé par :
    
    $$C_{n,i} = e^{-r\Delta t} \left[ p C_{n+1, i+1} + (1-p) C_{n+1, i} \right]$$
    
    Pour une option américaine, on compare cette valeur à la valeur d'exercice immédiat et on retient le maximum.
    

---

Formulaire examen

---

### 1. Simulation de l'Aléa (Loi Normale)

- **Méthode de Box-Muller** : Pour $U_1, U_2 \sim \mathcal{U}(0,1)$ i.i.d.
    
    - $X = \sqrt{-2\ln(U_1)} \cos(2\pi U_2)$
        
    - $Y = \sqrt{-2\ln(U_1)} \sin(2\pi U_2)$
        
    - _Résultat : $X, Y \sim \mathcal{N}(0,1)$ indépendantes._
        
- **Vecteurs Gaussiens (Cholesky)** : Pour simuler $X \sim \mathcal{N}(\mu, \Sigma)$
    
    - Décomposer $\Sigma = LL^T$ ($L$ triangulaire inférieure).
        
    - $X = \mu + L Z$ avec $Z \sim \mathcal{N}(0, I_d)$.
        

---

### 2. Monte Carlo et Précision

- **Estimateur** : $\bar{I}_N = \frac{1}{N} \sum_{i=1}^N f(X_i)$
    
- Intervalle de Confiance (95%) :
    
    $$\left[ \bar{I}_N - 1.96 \frac{\hat{\sigma}_N}{\sqrt{N}} \ ; \ \bar{I}_N + 1.96 \frac{\hat{\sigma}_N}{\sqrt{N}} \right]$$
    
    Où $\hat{\sigma}_N$ est l'écart-type empirique des simulations.
    

---

### 3. Réduction de la Variance

- **Variables Antithétiques** : On simule $N/2$ couples $(f(U_i), f(1-U_i))$.
    
    - L'estimateur est la moyenne globale. La variance est réduite si $f$ est monotone.
        
- **Variable de Contrôle** : On cherche $Y$ dont $E[Y]$ est connu.
    
    - $Z = X + c(Y - E[Y])$
        
    - $c^* = -\frac{Cov(X,Y)}{Var(Y)}$ (valeur optimale de $c$).
        

---

### 4. Modèle de Black-Scholes (Discret)

- Schéma d'Euler (Prix de l'actif) :
    
    $$S_{t+\Delta t} = S_t \exp\left( (r - \frac{\sigma^2}{2})\Delta t + \sigma \sqrt{\Delta t} Z \right)$$
    
    (Formule exacte pour le modèle log-normal).
    

---

### 5. Arbre de Cox-Ross-Rubinstein (CRR)

- **Paramètres de l'arbre** :
    
    - $u = e^{\sigma \sqrt{\Delta t}}$ (Hausse)
        
    - $d = e^{-\sigma \sqrt{\Delta t}}$ (Baisse)
        
    - $p = \frac{e^{r\Delta t} - d}{u - d}$ (Probabilité risque-neutre)
        
- Valorisation d'une option Américaine (Nœud $n,i$) :
    
    $$V_{n,i} = \max \left( \text{Payoff Immédiat} \ ; \ e^{-r\Delta t} [p V_{n+1, i+1} + (1-p) V_{n+1, i}] \right)$$
    

---

### 6. Rappels Mathématiques Utiles

- **Payoff Call** : $\max(S_T - K, 0)$
    
- **Payoff Put** : $\max(K - S_T, 0)$
    
- **Probabilité risque-neutre** : C'est la probabilité sous laquelle le prix actualisé de l'actif est une martingale.
    

---

**Conseil pour l'examen :** Vérifiez toujours si l'option est **Européenne** (calcul direct à la fin) ou **Américaine** (nécessite l'algorithme de programmation dynamique/arbre pour vérifier l'exercice anticipé à chaque étape).

Bonne chance pour vos révisions !