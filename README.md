# Documentation OriLang pour les utilisateurs
>[!note] Note du développeur
>
>Pour le moment, OriLang est un programme 'mono-instruction', càd qu'il n'exécute qu'un *Statement* constitué d'une ou plusieurs *Expressions* et ne retourne qu'un seul résultat.
>
>Il n'est pas encore possible d'exécuter plusieurs *Statements* consécutifs
## Types de valeurs
### Valeurs numériques
Il est possible d'exprimer des valeurs numériques entières, décimales et en notation scientifique.

Exemple:
- `1`
- `5.2`
- `1.2e15`

### Chaînes de caractère
> Temporaire
> 
> Ce type de valeur est encore peu utilisé dans les usages de OriLang

Une chaîne de caractère est un ensemble de caractères encadrés par des apostraophes (*Single quotes*).
Exemple `'Ma chaîne de caractère'`;

### Références d'objet
Il existe deux types de référence d'objet:
- Valeur: c'est une référence à la valeur de l'objet

>[!note]
>
>Exemple: `"Mon objet 1" + "Mon objet 2"`
>Cette opération retournera l'addition des valeurs de ces deux objets
- Absolue: c'est une référence qui pointe directement sur le nom de l'objet en question, une chaine de caractère. Elle se démarque par le préfix `$`

>[!note]
>
>Exemple: `CumulExercice($"Mon objet 1")`
>Cette fonction nécessite un objet en paramètre donc on lui passe sa référence absolue. Il serait également possible d'utiliser les apostrophes `''` plutôt que la notation `$""` mais le support de cette fonctionnalité n'est pas garanti.

>[!warning]
>
>Alors que `"Mon objet 1" + "Mon objet 2"` retournera une valeur numérique correspondant à la somme des valeurs des deux objets, `$"Mon objet 1" + $"Mon objet 2"` retournera une valeur chaine de caractère correspondant à la concaténation des deux noms: `"Mon objet 1Mon objet 2"`
### Valeurs spéciales
`true` et `false` sont des valeurs réservées représentant les deux valeurs booléennes.
### Références spéciales
Dans certains contextes, il est possible d'accéder à des références spéciales pour effectuer certaines opérations liées au contexte global d'exécution. Ces références sont très souvent utilisées de paire avec des `fonctions` pour récupérer une information du contexte.
Ces références sont précédées du symbole `@`.

|Nom|Description|Contexte|
|--|--|--|
|`@FOLDER`|qui correspond au dossier dans lequel s'exécute le programme|Règles de calcul|
|`@USER`|correspond à l'utilisateur qui exécute le programme|Règles de calcul|
|`@ELEMENT`|correspond à l'élément auquel appartient le programme|Règles de calcul|
|`@CLIENT`|correspond au client dans lequel s'exécute le programme|Règles de calcul|
|`@NOW`|correspond à la représentation en chaîne de caractère de la date à laquelle s'exécute le programme|Règles de calcul|
|`@PERIOD`|correspond à la période utilisée pour résoudre certains objets référencés|Règles de calcul|
|`@TRIES`|correspond au nombre de tentatives d'exécution d'un programme donné, principalement dans le cas de références cycliques|Règles de calcul|
## Opérations
### Opérations arithmétiques
Les opérations arithmétiques de base sont disponibles et respectent la précédence des opérations et de droite à gauche:
|Opération|Symbole|Exemple|Précédence|
|--|--|--|--|
|Addition|`+`|`a+b`|
|Soustraction|`-`|`a-b`|
|Multiplication|`*`|`a*b`|
|Division|`/`|`a/b`|
|Division euclidienne |`//`|`a//b`|
|Factorielle|`!`|`a!`|
|Exponentiation|`^`|`a^b`|
|Incrémentation|`++`|`++a` ou `a++`|
|Décrémentation|`--`|`--a` ou `a--`|
|Négation|`-`|`-a`|
|Pourcentage|`%`|`a%`|
|Parenthèses|`()`, `[]`, `{}`| `(a+b)`|
### Opérations booléennes
Les opérations booléennes de base sont disponibles et respectent une précédence spécifique. De la plus haute à la plus basse précédence:
|Opération|Symbole|Exemple|
|--|--|--|
|Non logique|`!`|`!a`|
|Comparaisons relatives|`<`, `>`, `<=`, `>=`, `==`, `!=`, `<>`|`a<b` Notons que `!=` et `<>` ont la même signification 'différent'.|
|Comparaisons logiques| `AND`,`OR`,`XOR`|`a OR b`|
## Fonctions
Les fonctions dépendent du contexte d'exécution.
De manière classique, elles s'utilisent avec des paramètres séparées par un délimiteur `,`.

>[!note]
>
> `,` et `;` sont actuellements indifférenciés mais pourrait à l'avenir avoir des usages différents.
### Fonctions comptable
|Fonction|Arguments|Description|Contexte|
|--|--|--|--|
|`CumulExercice`|`1`: référence d'objet|Cumule toutes les données de l'objet entre le début de l'exercice et la période donnée|Règles de calcul|
|`CumulM-12`|`1`: référence d'objet|Cumule toutes les données de l'objet entre la période donnée un an auparavant et la période donnée|Règles de calcul|
|`M-12`|`1`: référence d'objet|Récupère la donnée d'un objet un an précédent la période donnée|Règles de calcul|
|`M-1`|`1`: référence d'objet|Récupère la donnée d'un objet un mois précédent la période donnée|Règles de calcul|
|`SommeCumulM-12`|**à venir**|||
|`SommeCumulM-1`|**à venir**|||
|`SommeM-12`|**à venir**|||
|`SommeM-1`|**à venir**|||
### Fonctions mathématiques
|Fonction|Arguments|Description|Contexte|
|--|--|--|--|
|`Moyenne`|`+`: une liste de valeurs| Calcule la moyenne réelle d'une liste de valeurs.|Partout|
|`Clamp`|`3`: min, valeur, max|Borne une valeur entre un minimum et un maximum, retournant l'un de ces derniers en cas de dépassement ou la valeur elle même si bornée.|Partout|
|`PGCD`|`2`: a et b|Plus Grand Commun Diviseur.|Partout|
|`PPCM`|`2`: a et b|Plus Petit Commun Multiple.|Partout|
|`Max`|`+`: une liste de valeurs|La valeur la plus élevée parmi une liste de valeurs.|Partout|
|`Min`|`+`: une liste de valeurs|La valeur la plus basse parmi une liste de valeurs.|Partout|
|`Modulo`|`2`: a et b|Le reste de la division euclidenne `a/b` annotée `a%b`.|Partout|
|`Aléatoire`|`0\|2`: optionnellement min et max|Une valeur aléatoire entre 0 et 1 ou entre les bornes données.|Partout|
|`SommeCarrés`|`+`: une liste de valeurs|Calcule la somme des carrées des valeurs données.|Partout|
|`Somme`|**à venir**|||
|`SommeSi`|**à venir**|||
|`SommeCarrésSi`|**à venir**|||
|`MoyenneSi`|**à venir**|||
### Fonctions générales
|Fonction|Arguments|Description|Contexte|
|--|--|--|--|
|`Si`|`3`: condition,conséquent,alternatif|Retourne l'évaluation du conséquent si la condition est vraie, l'alternatif sinon|Partout|
## Coming soon
Les prochaines évolutions sont l'assignation et déclaration de variables pendant l'exécution.
