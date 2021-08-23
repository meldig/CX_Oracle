# Connexion à une base oracle via le module cx_oracle de conda

## Présentation :
La connexion présentée ci-dessous est une connexion de type *Standalone*, c'est-à-dire pour un utilisateur seulement (pour plus d'information veuillez consulter la documentation [ici](https://cx-oracle.readthedocs.io/en/latest/user_guide/connection_handling.html)) et se fait en deux temps (à voir plus tard comment la passer en une seule opération) :
1. Création d'un fichier de connexion .py ;
2. Lancement du fichier avec conda ;

## 1. Création d'un fichier de connexion .py

```PY
# 1. Import du module cx_Oracle
import cx_Oracle

# 2. Création de variables contenant les informations de connexion 
user_d = input("Veuillez saisir le schéma de destination : ")
mdp_d = input("Veuillez saisir le mot de passe du schéma de destination : ")
inst_d = input("Veuillez saisir l'instance de destination : ")

# Connexion à oracle
conn_str = user_d + "/" + mdp_d + "@" + inst_d
connexion = cx_Oracle.connect(conn_str, encoding = "UTF-8")

cursor = connexion.cursor()

# Commande permettant de tester votre connexion
cursor.execute("SELECT * FROM MON_SCHEMA.MA_TABLE")
for row in cursor:
    print(row[0], '-', row[1])
```

## 2. Lancement du fichier avec conda

### 2.1. Mettez-vous dans votre environnement python

```PY
conda activate #mon_environnement
```

### 2.2. Vérifiez que le module cx_oracle est bien présent dans voter environnement

```PY
conda list #Cette commande liste tous les éléments de l'environnement actif. Vous devrez donc vérifier par vous-même si le module cx_oracle est bien présent dans cette liste.
```

### 2.3. Lancez le fichier de connexion et remplissez les informations lorsqu'elles vous sont demandées

```PY
python mon_chemin_d_acces\mon_fichier_de_connexion.py
```

## 3. Remarque :
Contrairement à un .bat vous n'obtiendrez aucun message en cas de connexion réussie à la base, d'où l'importance de la tester avec une simple requête de sélection.
Rassurez-vous cependant, en cas d'erreur de connexion, vous recevrez un message d'erreur dans conda.