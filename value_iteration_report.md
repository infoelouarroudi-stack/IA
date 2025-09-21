# Rapport - Value Iteration (BookGrid)

## Itération 0
- Toutes les valeurs initiales des états non terminaux sont **0**.
- États terminaux :  
  - `V(4,3) = +1` (case verte, sortie positive)  
  - `V(4,2) = -1` (case rouge, sortie négative)  

---

## Itération 1

### Calcul de `V₁(<4,3>)`
Action `EXIT` :  
\[ Q(Exit) = +1 \]  
Donc :  
\[ V₁(<4,3>) = 1.00 \]

### Calcul de `V₁(<4,2>)`
Action `EXIT` :  
\[ Q(Exit) = -1 \]  
Donc :  
\[ V₁(<4,2>) = -1.00 \]

---

## Itération 2

### Calcul de `V₂(<3,3>)`
Action optimale = `RIGHT` vers `<4,3>` :  

\[ Q₂(RIGHT) = 0.8(0 + 0.9 \times V₁(4,3)) + 0.1(0 + 0.9 \times V₁(3,3)) + 0.1(0 + 0.9 \times V₁(3,2)) \]

En remplaçant :  
- 0.9 × V₁(4,3) = 0.9 × 1 = 0.90 → 0.8 × 0.90 = 0.72  
- Les deux autres termes valent 0  

Donc :  
\[ V₂(<3,3>) = 0.72 \]

---

## Itération 3

### Calcul de `V₃(<3,3>)`

\[ Q₃(RIGHT) = 0.8(0 + 0.9 \times V₂(4,3)) + 0.1(0 + 0.9 \times V₂(3,3)) + 0.1(0 + 0.9 \times V₂(3,2)) \]

- 0.9 × V₂(4,3) = 0.9 × 1.00 = 0.900 → 0.8 × 0.900 = 0.7200  
- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648 → 0.1 × 0.648 = 0.0648  
- 0.9 × V₂(3,2) = 0.9 × 0.00 = 0.000 → 0.1 × 0.000 = 0.0000  

Somme = 0.7200 + 0.0648 + 0.0000 = 0.7848  

Donc :  
\[ V₃(<3,3>) = 0.78 \]

---

### Calcul de `V₃(<2,3>)`

Action optimale = `RIGHT` vers `<3,3>` :  

\[ Q₃(RIGHT) = 0.8(0 + 0.9 \times V₂(3,3)) \]

- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648  
- 0.8 × 0.648 = 0.5184  

Donc :  
\[ V₃(<2,3>) = 0.52 \]

---

### Calcul de `V₃(<3,2>)`

Action optimale = `UP` (vers `<3,3>` avec risque de déviation vers `<4,2>`) :  

\[ Q₃(UP) = 0.8(0 + 0.9 \times V₂(3,3)) + 0.1(0 + 0.9 \times V₂(4,2)) + 0.1(0 + 0.9 \times 0) \]

- 0.9 × V₂(3,3) = 0.9 × 0.72 = 0.648 → 0.8 × 0.648 = 0.5184  
- 0.9 × V₂(4,2) = 0.9 × (-1.00) = -0.900 → 0.1 × -0.900 = -0.0900  
- 0.1 × 0 = 0  

Somme = 0.5184 - 0.0900 + 0 = 0.4284  

Donc :  
\[ V₃(<3,2>) = 0.43 \]

---

## Conclusion
Après avoir fait les calculs **manuels** étape par étape :  
- `V₃(<3,3>) = 0.78`  
- `V₃(<2,3>) = 0.52`  
- `V₃(<3,2>) = 0.43`  

👉 Ces valeurs correspondent exactement aux résultats obtenus par notre code lors de l’exécution des tests.
