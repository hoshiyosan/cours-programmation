# Qu'est ce qu'un programme ?

Un programme peut être vu comme un ensemble d'instructions ou blocs d'instructions qui s'éxécutent séquentiellement (les unes à la suite des autres). Il peut accepter une entrée (les paramètres du programme) et fournir une sortie (le retour du programme).

## Types d'instruction

### Fonctions

La fonction **print** permet d'envoyer du texte vers la `sortie` du programme.

```python
print("hello")
```

### Affectations

L'opération d'**affectation** consiste à attribuer une valeur à une variable

```python
x = 3
prenom = "toto"
```

### Opérations mathématiques

La plupart des langages de programmation permettent d'effectuer des **opérations** mathématiques courrantes
  
```python
x = 5
y = 10 * x + 1
print("y =", y)
```

### Commentaires

Le **commentaire** n'est pas une instruction (il n'affecte pas le fonctionnement du programme). Il permet (dans le code) d'expliquer aux autres développeurs ce que fait un programme sans qu'ils n'aient à en comprendre toute les instructions.
  
Il peut être placé
    - soit sur une ligne seule
    - soit à la fin d'une ligne d'instruction
    - **jamais** au début d'une ligne contenant une instruction

```python
# calcule et affiche le carré de x
x = 3
y = x ** 2
print(x, "au carré vaut", y) # affiche par exemple "3 au carré vaut 9"
```

## Types de blocs d'instructions

### Conditions

Un bloc **conditionnel** permet d'exécuter un ensemble d'instructions si une condition est vérifié.

```python
# affiche "majeur" si la variable age est supérieure ou égal à 18, "mineur" sinon
age = 17

if age >= 18:
    print("majeur")
else:
    print("mineur")
```

### Boucle for

Une boucle for permet de réitérer une série d'instructions autant de fois qu'il y a d'élément dans un itérable.
Une boucle for signifie `execute les instructions suivantes pour chaque element dans la liste`.

Par exemple on peut calculer la somme des nombres de 0 à 4 en faisant
```python
somme = 0
for k in range(5): # range exclus la borne supérieure, range(5) ~ [0,1,2,3,4]
    somme += k
```

**Comprendre la fonction range**
La fonction `range` génère un itérable contenant des nombres. Son comportement diffère selon les paramètres choisis.
Par exemple:

- `range(5) ~ range(0,5) ~ [0,1,2,3,4]` : Génère la liste des nombres entiers entre 0 et 5 (exclus)
- `range(3, 7) ~ [3,4,5,6]` : Génère la liste des nombres entiers entre 3 et 7 (exclus)
- `range(0, 8, 2) ~ [0,2,4,6]` : Génère la liste des nombres entiers entre 0 et 8 avec un intervalle de 2


## Conclusion

Cette compréhension vous permet déjà d'écrire de petits programmes simples.
Mais au fur et à mesure que votre programme se complexifie, il vous faudra le structurer davantage.
Par exemple vous pouvez définir vos propres fonctions qui encapsulent la logique d'un ensemble d'instructions.
