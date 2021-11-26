# Programmation orientée objet

La programmation orientée objet (POO ou OOP en anglais) permet de structurer son code autour de concepts.
Elle apporte une abstration supplémentaire (par rapport aux fonctions) qui permet d'organiser son code et gagner en lisibilité.

## Vocabulaire et exemples

### Classes
Une classe représente une categorie d'objets. Elle définit des propriétés qui sont communes à chacun des objets de cette catégorie.

On peut par exemple définir une classe `Vehicule` qui precise le nombre de roues d'un vehicule, sa vitesse maximale ainsi que sa couleur

```python
class Vehicule:
    def __init__(self, nombre_de_roues, vitesse_max_kmh, couleur):
        self.nombre_de_roues = nombre_de_roues
        self.vitesse_max_kmh = vitesse_max_kmh
        self.couleur = couleur
```


### Instances

On peut ensuite créer un objet de cette classe (~synonyme de catégorie). 

```python
ma_voiture = Vehicule(4, "250", "jaune")
```

L'object obtenu lorsque l'on appelle (ou instancie) la classe est appelé une **instance**.

Pour bien comprendre la différence entre classe et instance

- une classe défini une catégorie d'objets (ex: Un véhicule)
- une instance décrit un objet de cette catégorie (ex: Un véhicule jaune à 4 roues qui peut rouler à 250 km/h)

!!! danger "A retenir"

    Dans la vie de tous les jours la phrase **ma_voiture est une instance de la classe Voiture** signifie **ma_voiture est une voiture** (on oublie trop souvent de le préciser d'ailleurs). Dans le monde de la programmation, on préfère être précis pour éviter toute ambiguité entre une classe et une instance de cette même classe.

### Attributs

Un attribut d'une classe est une variable qui est lié à une instance d'une classe. C'est à dire que sa valeur est connue au moment où on instancie (~crée) un objet de cette classe.

En reprenant notre classe véhicule de l'exmple précédent

```python
ma_voiture = Vehicule(4, "250", "jaune") # on instancie un véhicule
print(ma_voiture.couleur) # affiche l'attribut "couleur" du véhicule qui ici est "jaune"
```

**Pourquoi utiliser un attribut de l'objet plutôt qu'une variable globale?**

Imaginez un programme qui doit afficher la couleur d'un grand nombre de véhicules.
Vous pourriez écrire
```python
couleur_voitures = [
    "rouge", "jaune", "bleu"
]
for couleur in couleur_voitures:
    print(couleur)
```

On peut l'écrire, ce qui parait plus long. Toutefois, la lecture en est plus simple (on comprend que pour chaque voiture, on affiche sa couleur).

```python
voitures = [
    Vehicule(4, "250", "jaune"),
    Vehicule(4, "250", "jaune"),
    ...,
    Vehicule(4, "250", "jaune")
]
for voiture in voitures:
    print(voiture.couleur)
```

Mais l'intérêt vient surtout quand le code se complexifie. Imaginons qu'on veuille maintenant afficher la couleur la vitesse et le nombre de roues.

Avec le premier exemple cela donne
```python
couleur_voitures = [
    "rouge", "jaune", "bleu"
]
nombre_de_roues_voitures = [
    4, 4, 4
]
vitesse_max_voitures = [
    200, 250, 50
]
for k in range(len(voitures)):
    print(couleur_voitures[k], nombre_de_roues_voitures[k], vitesse_max_voitures[k])
```

La même chose en utilisant la POO donne
```python
voitures = [
    Vehicule(4, "250", "jaune"),
    Vehicule(4, "250", "jaune"),
    ...,
    Vehicule(4, "250", "jaune")
]
for voiture in voitures:
    print(voiture.couleur, voiture.nombre_de_roues, voiture.vitesse_max_kmh)
```

On voit ici plus clairement l'amélioration dans la lisibilité.

!!! danger "Pourquoi ne pas utiliser un dictionnaire?"

    Si on veut représenter un objet rapidement, on peut également utiliser un dictionnaire plutôt que de définir une classe.
    C'est une structure de données propre à python qui correspondrait dans d'autres langages à une HashMap.
    
    `voitures = [{"couleur": "jaune", "nombre_de_roues": 4, "vitesse_max_kmh": 250}]`

    L'approche est similaire puisqu'un dictionnaire est une instance de la classe dict.
    L'avantage de définir votre propre classe est que vous pouvez valider ses attributs (par exemple vérifier que la vitesse est bien un nombre) en effectuant des vérifications dans le constructeur par exemple. Mais également définir des méthodes qui sont des fonctions d'une classe. (cf. section suivante)


### Méthodes 

Une méthode est une fonction qui est liée à une une classe. Le principal intérêt d'une méthode, est qu'on peut accéder à l'instance de la classe à laquelle cette méthode est liée.

On pourrait par exemple reprendre notre exemple précédent et lui ajouter une méthode `Vehicule.peut_rouler_a(vitesse)` qui détermine si un véhicule peut rouler à une vitesse donnée. C.à.D si la vitesse max du véhicule est supérieure à la vitesse souhaitée.

```python
class Vehicule:
    def __init__(self, nombre_de_roues, vitesse_max_kmh, couleur):
        self.nombre_de_roues = nombre_de_roues
        self.vitesse_max_kmh = vitesse_max_kmh
        self.couleur = couleur

    def peut_rouler_a(self, vitesse_kmh):
        return vitesse_kmh <= self.vitesse_max_kmh

ma_voiture = Vehicule(4, 250, "jaune")
if not ma_voiture.peut_rouler_a(90):
    print("Vous ne devriez pas emprunter l'autoroute")
```

En Python, à la différence d'une fonction une méthode d'une instance a nécessairement comme premier argument une variable qui contient l'instance courante de l'objet.

!!! note "Note"
    Par convention on l'appelle souvent `self` qui en anglais signifie soi-même, dans d'autres langages on trouvera plus souvent `this`.


Dans cet exemple, quand je fais `ma_voiture.peut_rouler_a(50)`, la variable `self` passée en paramètre a exactement la même valeur que l'objet `ma_voiture` dans le contexte global.

!!! note "Quel est l'intérêt de cette variable `self`?"

    Rappelez vous qu'une classe définit un type d'objet (abstrait). C'est au moment de l'instanciation que les attributs prennent une valeur. Dans la méthode, il faut donc pouvoir accéder à l'instance pour connaître la valeur de ses attributs.

A noter que dans l'expression...

```python
ma_voiture.peut_rouler_a(50)
```

...on ne passe pas le premier argument `self` de manière explicite. Python le passe automatiquement pour nous quand on appelle une méthode d'une instance.
Par contre, on peut très bien choisir d'appeler directement la méthode de la classe, et non la méthode d'une instance. Dans ce cas la méthode se comporte comme une fonction et c'est au développeur de passer l'instance en paramètre de cette fonction.

```python
ma_voiture = Vehicule(4, 250, "jaune")
Vehicule.peut_rouler_a(ma_voiture, 50)
```

!!! danger "A retenir"

    **En python, une méthode est une fonction comme une autre**. La seule différence est que lorsque la méthode est appelée depuis une instance d'une classe, l'instance courante est passée comme premier paramètre sans que le développeur ne s'en soucie.

### Héritage

L'héritage permet de spécialiser une classe. C'est à dire de créer un sous-type du type (= de la classe) dont on hérite.
En reprenant notre exemple, on se rend compte que notre classe `Vehicule` est très générique. On trouverait plus simple de manipuler des voitures, sans avoir spécifier leur nombre de roues puisqu'elles en ont toujours 4 (admettons).

Nous allons donc créer une classe voiture, dont le constructeur prend uniquement les paramètres qui nous intéressent. Ici tous sauf le nombre de roues. Et nous allons faire appel au constructeur de la classe Parent (ici `Voiture`), en spécifiant toujours 4 pour le nombre de roues, et en passant les autres paramètres tels quels.

```python
class Voiture(Vehicule):
    def __init__(self, vitesse_max_kmh, couleur):
        super().__init__(4, vitesse_max_kmh, couleur)
```

Nous pouvons désormais instancier une `Voiture`.

```python
ma_voiture = Voiture(250, "jaune")
```

**Quel est le sens de toute cela?** 

`ma_voiture` est une `Voiture`, donc un type de `Véhicule` par héritage.

Par conséquent, elle hérite possède les attributs et méthodes d'une `Voiture`, mais aussi ceux d'un `Vehicule` par extension.

On peut donc écrire
```python
ma_voiture.peut_rouler_a(50)
# ou
print(ma_voiture.nombre_de_roues)
```

**A quoi bon faire de l'héritage ?**

Imaginons maintenant qu'on veuille ajouter des motos, ces motos ont un nombre de roues différents de celui des voitures, et des capacités que les voitures n'ont pas. Par exemple faire une roue arrière.

```python
class Moto(Vehicule):
    def __init__(self, vitesse_max_kmh, couleur):
        super().__init__(2, vitesse_max_kmh, couleur)

    def faire_une_roue_arriere(self):
        print("Bam! Roue arrière!")
```

On peut maintenant instancier une moto, et lui demander de faire une roue arrière.

```python
ma_moto = Moto(300, "vert")
ma_moto.faire_une_roue_arriere()
```

*Ici ça affiche simplement que la moto fait une roue arrière. Il faut croire le programme sur parole.*

Mais si vous instanciez une voiture, vous ne pourrez pas faire de roue arrière car la voiture n'a pas de méthode `faire_une_roue_arriere` (dommage).
```python
ma_voiture = Voiture(250, "jaune")
ma_voiture.faire_une_roue_arriere()
```

Vous aurez l'erreur suivante qui vous indique qu'une voiture n'a pas d'attribut `faire_une_roue_arriere`
```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Voiture' object has no attribute 'faire_une_roue_arriere'
```

!!! danger "Pourquoi l'erreur indique `no attribute` et pas `no method` ?"

    Pas de panique, en python les fonctions sont des variables. Par conséquent les méthodes d'une instance, sont également des attributs de cette instance. (méthode et attributs sont des attributs) Ce qui explique pourquoi le message d'erreur ne dit pas ` 'Voiture' object has no method 'faire_une_roue_arriere'`


!!! warning "Conseil"

    A tout moment si ces notions vous paraissent floues, **n'hésitez pas à revenir sur ce mémo**. Rare sont ceux qui ont assimilés toutes ces notions du premier coup d'oeil. La programmation orienté objet n'est pas intuitive au premier abord. Pourtant une fois maîtrisé, structurer votre code et manipuler des notions complexes devient un jeu d'enfant. La meilleure manière de bien comprendre ces concepts est d'essayer de les utiliser sur un projet concret.
