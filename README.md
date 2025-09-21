# Rapport - Value Iteration (BookGrid)

## Question 1 : Calculs Value Iteration

### Itération 0 - États Initiaux
- **États non terminaux** : Valeurs initiales = 0
- **États terminaux** :
  - `V(4,3) = +1` (case verte, sortie positive)
  - `V(4,2) = -1` (case rouge, sortie négative)

**Résultat de test :**

<img src="https://github.com/user-attachments/assets/13298067-5ad8-413a-8366-72b663cef271" width="50%" alt="Itération 0"/>

---

### Itération 1

#### Calcul de V₁(4,3)
- Action `EXIT` : Q(Exit) = +1
- **Résultat** : V₁(4,3) = 1.00

#### Calcul de V₁(4,2)
- Action `EXIT` : Q(Exit) = -1
- **Résultat** : V₁(4,2) = -1.00

**Résultat de test :**

<img src="https://github.com/user-attachments/assets/05f4f65e-dc2b-48f2-bf4d-b055ec810859" width="50%" alt="Itération 1"/>

---

### Itération 2

#### Calcul de V₂(3,3)
**Action optimale** : `RIGHT` vers (4,3)

**Formule** :
```
Q₂(RIGHT) = 0.8(0 + 0.9 × V₁(4,3)) + 0.1(0 + 0.9 × V₁(3,3)) + 0.1(0 + 0.9 × V₁(3,2))
```

**Calcul détaillé** :
- 0.9 × V₁(4,3) = 0.9 × 1 = 0.90 → 0.8 × 0.90 = 0.72
- Les deux autres termes = 0

**Résultat** : V₂(3,3) = 0.72

**Résultat de test :**

<img src="https://github.com/user-attachments/assets/5f87ca33-5971-483b-831f-c73fc4142dba" width="50%" alt="Itération 2"/>

---

### Itération 3

#### Calcul de V₃(3,3)
**Formule** :
```
Q₃(RIGHT) = 0.8(0 + 0.9 × V₂(4,3)) + 0.1(0 + 0.9 × V₂(3,3)) + 0.1(0 + 0.9 × V₂(3,2))
```

**Calcul détaillé** :
- 0.9 × V₂(4,3) = 0.9 × 1.00 = 0.900 → 0.8 × 0.900 = 0.7200
- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648 → 0.1 × 0.648 = 0.0648
- 0.9 × V₂(3,2) = 0.9 × 0.00 = 0.000 → 0.1 × 0.000 = 0.0000

**Somme** : 0.7200 + 0.0648 + 0.0000 = 0.7848  
**Résultat** : V₃(3,3) = 0.78

#### Calcul de V₃(2,3)
**Action optimale** : `RIGHT` vers (3,3)

**Formule** :
```
Q₃(RIGHT) = 0.8(0 + 0.9 × V₂(3,3))
```

**Calcul détaillé** :
- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648
- 0.8 × 0.648 = 0.5184

**Résultat** : V₃(2,3) = 0.52

#### Calcul de V₃(3,2)
**Action optimale** : `UP` vers (3,3) avec risque de déviation vers (4,2)

**Formule** :
```
Q₃(UP) = 0.8(0 + 0.9 × V₂(3,3)) + 0.1(0 + 0.9 × V₂(4,2)) + 0.1(0 + 0.9 × 0)
```

**Calcul détaillé** :
- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648 → 0.8 × 0.648 = 0.5184
- 0.9 × V₂(4,2) = 0.9 × (-1.00) = -0.900 → 0.1 × -0.900 = -0.0900
- 0.1 × 0 = 0

**Somme** : 0.5184 - 0.0900 + 0 = 0.4284  
**Résultat** : V₃(3,2) = 0.43

#### Résultats Finaux Itération 3
- V₃(3,3) = 0.78
- V₃(2,3) = 0.52
- V₃(3,2) = 0.43

**Résultat de test :**

<img src="https://github.com/user-attachments/assets/c32fee71-02cd-442b-a957-7776117f4056" width="50%" alt="Itération 3"/>

**Conclusion** : Les valeurs calculées manuellement correspondent exactement aux résultats obtenus par le code lors des tests.

---

## Question 2 : Modification BridgeGrid

### Commande Utilisée
```bash
python gridworld.py -g BridgeGrid -a value -k 1 --noise 0.01
```

### Résultats
![BridgeGrid 1](https://github.com/user-attachments/assets/5da404b0-15ed-4569-840b-2cca688d0859)
![BridgeGrid 2](https://github.com/user-attachments/assets/003d19c2-80a3-4d6c-85cb-819f866451cc)

### Solution
**Paramètre modifié** : noise = 0.01 (au lieu de 0.2)

### Justification
J'ai choisi de réduire le bruit car avec noise = 0.2, il y a 20% de chance que l'agent dévie de sa trajectoire, rendant le passage du pont trop risqué (déviation probable dans les cases à -100).

En réduisant le noise à 0.01, l'agent a 99% de chance d'aller dans la direction souhaitée. Cela rend le passage du pont suffisamment sûr pour que la récompense espérée de +10 compense le risque minimal de chute.

**Comparaison des espérances** :
- Espérance avec pont : 0.99 × 10 + 0.01 × (-100) = 8.9
- Alternative sans pont : récompense de 1

Le discount factor n'était pas le bon choix car même avec γ = 1, le risque de 20% reste trop élevé.

---

## Question 3 : Modification DiscountGrid

### 1. Chemin Risqué pour Atteindre +1

#### Commande
```bash
python gridworld.py -g DiscountGrid -a value -d 0.1
```

#### Résultats
![Discount 1a](https://github.com/user-attachments/assets/0c1e6561-d36f-40ac-a839-a283e9f008c7)
![Discount 1b](https://github.com/user-attachments/assets/c20b734d-7e0e-4532-9e8e-4f3da4945d9b)

#### Solution
**Paramètre modifié** : discount = 0.1

**Justification** : Avec un faible discount, l'agent valorise peu les récompenses futures. Il préfère le chemin court et direct vers +1, même s'il passe près du précipice, car les pénalités futures sont fortement dévaluées.

---

### 2. Chemin Risqué pour Atteindre +10

#### Commande
```bash
python gridworld.py -g DiscountGrid -a value -n 0.01
```

#### Résultats
![Discount 2a](https://github.com/user-attachments/assets/4241e4e6-e7e4-4fdc-b69b-dd25af74da4f)
![Discount 2b](https://github.com/user-attachments/assets/a3b5e1e9-28ac-4dfd-8d99-d474eb07af4d)

#### Solution
**Paramètre modifié** : noise = 0.01

**Justification** : En réduisant drastiquement le bruit, l'agent peut emprunter le chemin dangereux près du précipice. La récompense de +10 justifie le risque minimal, et l'agent choisit le chemin le plus court.

---

### 3. Chemin Sûr pour Atteindre +1

#### Commande
```bash
python gridworld.py -g DiscountGrid -a value -n 0.5
```

#### Résultats
![Discount 3a](https://github.com/user-attachments/assets/dc3e3f92-baee-43e8-8779-7114d5aef700)
![Discount 3b](https://github.com/user-attachments/assets/fb923afa-156c-4757-b12b-5d09f7299959)

#### Solution
**Paramètre modifié** : noise = 0.5

**Justification** : Avec un bruit très élevé, l'agent devient très prudent. Il évite complètement les chemins près du précipice car la probabilité de tomber est trop grande. Il préfère le chemin long mais sûr par le haut pour atteindre +1.

---

### 4. Éviter les États Absorbants

#### Commande
```bash
python gridworld.py -g DiscountGrid -a value -r 0.5
```

#### Résultats
![Discount 4a](https://github.com/user-attachments/assets/5b39846b-74fa-49e8-8cb2-deb145c460bd)
![Discount 4b](https://github.com/user-attachments/assets/034996d9-5398-42f6-bfbd-397b40263847)

#### Solution
**Paramètre modifié** : livingReward = 0.5

**Justification** : Avec une récompense positive à chaque pas, l'agent préfère continuer à se déplacer indéfiniment plutôt que d'atteindre un état terminal. Même la récompense de +10 ne compense pas la perte du livingReward constant. L'agent développe une politique qui évite tous les états absorbants pour maximiser la somme des récompenses sur le long terme.
