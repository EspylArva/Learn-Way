# You Aren't Gonna Need It (Yet)
![[YAGNI_comics.png]]

YAGNI(Y) est un principe permettant d'éviter les codes trop complexes. Il consiste à se poser la question suivante :

**Le code que je souhaite écrire aura t-il une plus-value ?**

## Analyse plus poussée
Au-delà de la question simpliste posée précédemment, il s'agit de creuser le besoin en amont du développement afin d'éviter :
- Un coût de production trop important pendant le développement
- Un refactoring trop important en aval du développement

La logique est la suivante : [[TODO]]

Wrong build -> +Cost of build +Cost of repair +Cost of carry +Cost of delay
Right feature, wrong build ->  +Cost of repair +Cost of carry +Cost of delay
Right feature, right build -> +Cost of carry +Cost of delay

Il y a donc quatre types de coût principaux dans ce principe : [todo](https://www.acronymat.com/2021/01/05/yagni/)

## Conclusion
YAGNI(Y) est un principe à appliquer en contre-mesure d'autres principes de Clean Coding : il ne s'agit pas d'un principe de bas niveau, mais plutôt d'architecture, et vise à réduire la complexité d'un projet.

Il vient donc en complément d'autres principes, comme les principes [[SOLID]].