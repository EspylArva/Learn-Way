---
aliases: [SOLID, SOLID principles, SRP, OCP, LSP, ISP, DIP]
---
# Principes SOLID (SOLID Principles)
> All systems change during their life cycles. This must be borne in mind when developing systems expected to last longer than the first version.
> - Ivar Jacobson

Lorsqu'un système est conçu, son changement est à prendre en compte. Ce changement peut être une amélioration, l'ajout de fonctionnalité, la correction de bug...
Peu importe la nature de la modification, tout système est amené à changer.

Pour simplifier et accompagner ces amendements, les principes SOLID sont des lignes directives de conception logicielle, des bonnes pratiques à mettre en place pour éviter un système obscur et impossible à maintenir.

## Qu'est ce que sont les principes SOLID ?
| Principe | Acronyme | Explication |
|-|-|-|
| Responsabilité Unique | SRP (Single Responsibility Principle) | Une classe n'a qu'une raison de changer |
| Ouvert/Fermé | OCP (Open Closed Principle) | |
| Substitution de Liskov | LSP (Liskov Substitution Principle) | |
| Segrégation des Interfaces | ISP (Interface Segregation Principle) | |
| Inversion des Dépendances | DIP (Dependency Inversion Principle) | |

### SRP (Single Responsibility Principle)
> A class should have one, and only one, reason to change.
> - Uncle Bob

Le principe de responsabilité unique indique que chaque "responsabilité" doit être séparée.
Ainsi, dans cet esprit, chaque classe ou interface ne doit avoir qu'une raison de changer.

#### Qu'est ce qu'une responsabilité ?
Une responsabilité est une raison de changer le code : c'est une fonctionnalité qui pourrait, potentiellement, être amenée à changer.

![[SRP_fig_8_1.png]]

Par exemple, dans l'exemple donné dans les [[SRP_fig_8_1.png|figure 8-1]] et [[SRP_fig_8_2.png|figure 8-2]], la situation est la suivante : on a des formes géométriques (rectangle, cercle, triangle...), qui :
- Ont une réalité mathématique, avec des valeurs, des algorithmes qui leur sont liées : par exemple une aire, calculée par une formule
- Ont une possibilité d'être affichées à l'écran, via un moteur GUI

On a donc deux fonctionnalités, avec une décorrelation entre ces deux fonctionnalités, ces deux *responsabilités*.
Ces fonctionnalités pourraient être amenées à changer :
- Pour la réalité mathématique des formes, on pourrait imaginer un calcul du volume du solide régulier associé, ou le calcul de la position de l'isobarycentre de la forme
- Pour la réalité graphique des formes, on pourrait imaginer différents moteurs de rendu
Dans cet exemple, on a donc deux *responsabilités*.

![[SRP_fig_8_2.png]]

#### Pourquoi délier les responsabilités ?
La raison principale pour décorréler les responsabilités est que si les responsabilités sont liées, une modification sur l'une a une possibilité d'influer sur l'autre -- alors que ce n'est pas l'intention.

Par exemple, si l'on a 100 tests pour chaque fonctionnalité A et B, et que l'on décide de changer l'une d'elle (la B), il ne suffira pas de relancer les 100 tests associés (à la B) pour s'assurer de la fiabilité du code : on sera obligés de relancer l'entièreté des tests.

#### Dangers de la SRP
C'est en particulier dans la phase de design que le principe d'unicité de responsabilité intervient : il s'agit de séparer les fonctionnalités du produit. Cependant, il est très souvent possible de pousser cette séparation des fonctionnalités à outrance. Dans ce cas, le risque est de créer de la [[Needless Complexity|complexité inutile]].

Par exemple, dans la [[SRP_fig_8_3.png|figure 8-3]], la situation est la suivante :
- L'application est une implémentation de modem (téléphone)
- L'application peut recevoir des appels et les transmettre

![[SRP_fig_8_3.png]]

Il y a donc deux fonctionnalités principales : une fonctionnalité de connexion entre deux appareils (le fait de composer un numéro, d'accepter l'appel ou de raccrocher) et une fonctionnalité de gestion de données (le fait de transmettre ou réceptionner les bytes qui composent le signal).
En s'attardant sur cette dernière fonctionnalité, on pourrait se demander s'il est judicieux de séparer cette fonctionnalité en deux : le fait de transmettre les données d'une part, et le fait de les réceptionner d'autre part.
On pourrait le choix de séparer transmission et réception des données si l'une des deux est amenée à changer ou à évoluer, mais, dans le cas où ces deux fonctionnalités ne seraient pas spécialement amenées à changer, ou qu'elles changeraient conjointement (en s'appuyant par exemple sur le même protocole de transmission de données), cela amènerait cette fameuse [[Needless Complexity]].

Il n'y a pas de règle absolue pour savoir quand et où s'arrêter dans la décomposition des fonctionnalités : c'est le rôle de l'architecte de déterminer la séparation optimale.

Le corolaire est le suivant : un axe de changement n'est un axe de changement que dans le cas où le changement arrive.

### OCP (Open Closed Principle)
> You should be able to extend a classes behaviour, without modifying it
> - Uncle Bob 

Le principe Ouvert-Fermé indique qu'une fonctionnalité doit être "Ouverte à l'extension" et "Fermée à la modification".

#### Ouverture à l'extension
Un module doit pouvoir être étendu : on doit pouvoir avoir la possibilité d'ajouter des nouveaux comportements via des interfaces pour répondre à de nouvelles spécifications, ou à une modification des requis.

#### Fermeture à la modification
Un module doit être hermétique : personne ne doit pouvoir ou avoir le besoin de changer le code. Dans l'idéal, seules les interfaces doivent changer.

Il est cependant généralement impossible d'avoir une fermeture à la modification complète : il y a toujours des cas où la modification des spécifications amènent à la modification d'une classe.

C'est pourquoi on parle de "fermeture stratégique" (strategic closure) : l'architecte doit faire le choix de quels types de modifications seront acceptées ou rejetées. C'est là également que sont les limites de ce principe : il ne s'agit pas d'une règle absolue, mais d'axe de conception, parallèlement à l'expérience de l'architecte.

#### Utiliser l'[[Abstraction]]
L'abstraction est un outil de choix pour réduire le risque de modification et permettre l'extension de manière fluide. L'exemple suivant montre la force de l'abstraction :

Dans une implémentation naïve d'une relation client-serveur, où le client et le serveur communique, on serait tenté de créer deux classes `Client` et `Server`, où `Client` peut envoyer des données vers un objet de type `Server`. Dans cet exemple, `Client` et `Server `sont des classes concrètes. Cette implémentation est illustrée par la [[OCP_fig_1.png|figure 1]].

![[OCP_fig_1.png]]

Cependant, imaginons maintenant que pour les besoins du projet, on doive implémenter à présent un serveur gérant la redondance. Ce type de serveur aura les mêmes fonctionnalités, mais pourra aussi répartir la charge entre les différents nœuds du réseau de redondance. Le problème est qu'à présent, pour relier un objet `Client` à la nouvelle classe `RedundancyServer`, il faut modifier le type de l'attribut `server`, ou ajouter une clause `if` dans `sendToServer(data)` gérant le type de `server` (en passant, voir [[RunTime Type Identification|RTTI]] à ce sujet).
Cette situation est représentée par la [[OCP_fig_2.png|figure 2]].

![[OCP_fig_2.png]]

La solution élégante consiste à utiliser une [[abstraction]] : la classe `AbstractServer` est utilisée par `Client` et défini un squelette à respecter par `Server` et `RedundancyServer`, qui sont les implémentations de `AbstractServer`.
A présent, les futures améliorations et modifications de `Server` ou `RedundancyServer` seront localisées uniquement là où le changement est nécessaire, est non du côté de `Client`, dont le fonctionnement reste le même.
De même, toute future implémentation d'`AbstractServer` sera simplifiée, puisqu'il suffira de créer une nouvelle classe héritant d'`AbstractServer`. `Client` sera également capable d'interagir avec, puisqu'il s'agira d'une classe héritant d'`AbstractServer`, faisant ainsi usage du [[Polymorphisme]].
Cette situation est représentée par la [[OCP_fig_3.png|figure 3]].

![[OCP_fig_3.png]]

Il faut cependant également à utiliser l'abstraction correctement : utiliser un objet `AbstractServer` dans `Client` ne suffit pas à respecter le principe Ouvert-Fermé. Si le comportement de `sendToServer(data)` est toujours géré par [[RunTime Type Identification|Runtime Type Identification]], l'effort d'abstraction est perdu, car `Client` reste ouvert à la modification (et non fermé). 

#### Heuristiques et Conventions
En Programmation Orientée Objet, il y a un certain nombre de conventions à respecter. Certaines ont un lien plus ou moins direct avec le principe Ouvert-Fermé :

| Règle | Raison |
|-|-|
| Toutes les variables du membre doivent être privées | Un changement de la variable changera potentiellement le comportement des implémentations de fonctions de toutes les classes dérivées. |
| Ne jamais utiliser de variables globales | Similairement à la règle de rendre les variables privées, la présence d'argument global ouvre de manière permanente le module dépendant de la variable globale. Cela implique que tout module modifiant cette variable peut casser le fonctionnement des autres modules s'appuyant sur la même variable. |
| Eviter l'[[RunTime Type Identification\|identification du type au runtime]] | Comme vu précédemment, l'usage de [[RunTime Type Identification|RTTI]] peut briser le principe d'OCP. Cependant, certains cas nécessitent le [[RunTime Type Identification|RTTI]] pour un usage ne brisant pas le principe Ouvert-Fermé. |

Ces règles sont, encore une fois, des directives qui ne sont pas absolues. Il existe des cas où il est acceptable de transgresser ces règles, et le style de l'architecte intervient également : certains refuseront catégoriquement de transgresser ces règles pour assurer la maintenabilité, d'autre préfèreront la concision d'une variable globale.

### LSP (Liskov Substitution Principle)
### ISP (Interface Segregation Principle)
### DIP (Dependency Inversion Principle)

## Sources
Robert C. Martin, Micah Martin. (2006). *Agile Principles, Patterns, and Practices in C#*. [URL](https://drive.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/view?resourcekey=0-AbuGpXQzwZcUGExkktKt0g)
Robert C. Martin. (1996). *OCP: The Open-Closed Principle*. [URL](https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view?resourcekey=0-FsS837CGML599A_o5D-nAw)
Robert C. Martin. *Principles of OOD*. butUncleBob.com. [URL](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)
