# Attaque-DPA

# Implémentation simple d'une attaque DPA sur AES

Ce projet propose une petite implémentation (non optimisée) d'une **attaque par analyse de puissance différentielle (DPA)** appliquée sur l’algorithme AES.  
L’objectif est purement pédagogique : montrer concrètement comment une attaque DPA fonctionne sur des traces réelles.

---

## 🔍 Qu’est-ce qu’une attaque DPA ?
L’attaque **Differential Power Analysis (DPA)** exploite les fuites d’information contenues dans la consommation électrique d’un dispositif cryptographique.  
En analysant un grand nombre de traces de puissance mesurées pendant l’exécution d’AES, on peut corréler certaines hypothèses sur des sous-clés avec les fuites observées, et ainsi retrouver la clé secrète.

---

## 📂 Dataset : `AES_traces_set_1st_round.ets`

Le dataset utilisé est `AES_traces_set_1st_round.ets`, qui contient :

- **Traces de puissance** mesurées lors de l’exécution du **premier round d’AES**.  
- **Taille** : chaque trace correspond à l’évolution de la consommation électrique pendant une exécution d’AES.  
- **Labels** : les données sont annotées avec les informations nécessaires pour tester les hypothèses de clé (par exemple les valeurs intermédiaires issues de la SBox).  
- **Format `.ets`** : il s’agit d’un format binaire couramment utilisé dans les bases de traces pour Side-Channel Analysis 

En résumé, le dataset contient :  
- Un ensemble de **traces de consommation électrique** (mesures expérimentales).  
- Les **textes clairs (plaintexts)** utilisés lors du chiffrement.  
- La **clé secrète réelle** (pour pouvoir vérifier la réussite de l’attaque).  

---

## ⚙️ Fonctionnement du projet

1. Chargement du dataset `AES_traces_set_1st_round.ets`.  
2. Sélection des hypothèses de clé pour un **byte** du premier round.  
3. Calcul des valeurs intermédiaires (sortie de la SBox).  
4. Partitionnement des traces selon les hypothèses (0 ou 1 sur un bit).  
5. Calcul des moyennes différentielles → récupération de la clé la plus probable.  

---
