# RAPPORT - Calculs Value Iteration

## Partie 1 : Value Iteration manuelle

Nous détaillons ici les trois premières itérations de Value Iteration dans l’environnement **BookGrid**.

---

### Itération 0
On initialise toutes les valeurs des états non terminaux à **0**.

\[ V_0(s) = 0 \]

---

### Itération 1

- **État <4,3> (case verte, +1)**  
  L’action *exit* donne directement la récompense **+1** :  
  \[ V_1(\langle4,3\rangle) = 1.0 \]

- **État <4,2> (case rouge, -1)**  
  L’action *exit* donne directement la récompense **-1** :  
  \[ V_1(\langle4,2\rangle) = -1.0 \]

- Les autres états restent à 0.

---

### Itération 2

- **État <3,3>**  
  Action optimale : *RIGHT*.  
  \[ Q_2(RIGHT) = 0.8(0 + \gamma V_1(4,3)) + 0.1(0 + \gamma V_1(3,3)) + 0.1(0 + \gamma V_1(3,2)) \]

  Substitution :  
  \[ Q_2(RIGHT) = 0.8(0.9 \times 1) + 0.1(0.9 \times 0) + 0.1(0.9 \times 0) = 0.72 \]

  Donc :  
  \[ V_2(\langle3,3\rangle) = 0.72 \]

---

### Itération 3

- **État <3,3>**  
  \[ Q_3(RIGHT) = 0.8(0.9 \times V_2(4,3)) + 0.1(0.9 \times V_2(3,3)) + 0.1(0.9 \times V_2(3,2)) \]

  Substitution :  
  \[ Q_3(RIGHT) = 0.8(0.9 \times 1) + 0.1(0.9 \times 0.72) + 0.1(0.9 \times 0) \]  
  \[ = 0.720 + 0.0648 + 0.000 = 0.7848 \]

  Donc :  
  \[ V_3(\langle3,3\rangle) \approx 0.78 \]

- **État <2,3>**  
  Action optimale : *RIGHT* vers <3,3>.  
  \[ Q_3(RIGHT) = 0.8(0.9 \times V_2(3,3)) = 0.8(0.9 \times 0.72) = 0.5184 \]

  Donc :  
  \[ V_3(\langle2,3\rangle) \approx 0.52 \]

- **État <3,2>**  
  Action optimale : *UP* vers <3,3>, avec risque d’aller à <4,2>.  
  \[ Q_3(UP) = 0.8(0.9 \times V_2(3,3)) + 0.1(0.9 \times V_2(4,2)) + 0.1(0.9 \times 0) \]

  Substitution :  
  \[ Q_3(UP) = 0.8(0.648) + 0.1(-0.9) + 0 = 0.5184 - 0.09 = 0.4284 \]

  Donc :  
  \[ V_3(\langle3,2\rangle) \approx 0.43 \]

---

## Conclusion

Après calcul manuel des trois premières itérations, nous obtenons :

- \(V_3(\langle3,3\rangle) = 0.78\)  
- \(V_3(\langle2,3\rangle) = 0.52\)  
- \(V_3(\langle3,2\rangle) = 0.43\)

Ces résultats correspondent exactement aux valeurs observées lors de l’exécution du code (`python gridworld.py -a value -i ...`).

---
