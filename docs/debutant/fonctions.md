# Définir des fonctions

## Qu'est-ce qu'une fonction ?

Une fonction peut être considérée comme un sous-programme. Elle prend en entrée des paramètres et fourni une valeur de retour.
Le but d'une fonction est de définir une abstraction pour un ensemble d'instructions. Cela permet une meilleure réutilisabilité du code ainsi qu'une meilleur lisibilité.

## Exemple

Supposez que vous ayez le programme suivant

```python
age_pierre = 17
age_paul = 18

if age_pierre >= 18:
    print("pierre est majeur")
else:
    print("pierre est mineur")

if age_paul >= 18:
    print("paul est majeur")
else:
    print("paul est mineur")
```

On remarque que la logique permettant de vérifier l'age et d'afficher si la personne est majeure est la même quelle que soit la personne concernée. On peut donc factoriser ce code en utilisant une fonction.

Nous allons donc créer une fonction `affiche_si_majeur`. Cette fonction prend en paramètre le nom d'une personne ainsi que son age et affiche si la personne est majeure. Ainsi, notre programme précédent devient :

```python
def affiche_si_majeur(nom, age):
    if age >= 18:
        print(nom, "est majeur")
    else:
        print(nom, "est mineur")

affiche_si_majeur("pierre", 17)
affiche_si_majeur("paul", 18)
```

Dans cette approche notre fonction fait 2 choses:

- elle calcule si un utilisateur est majeur ou mineur 
- et affiche en fonction une phrase indiquant le résultat

## Portée des variables

TODO:
