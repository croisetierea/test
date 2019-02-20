# Remise du premier livrable

## Identification
- Cours      : Outils et pratiques de développement logiciel
- Sigle      : INF2050
- Session    : Hiver 2019
- Groupe     : 040
- Enseignant : François-Xavier Guillemette
- Auteurs    : Frédéric Toussaint-Dupont (TOUF13068106)
- Auteurs    : Maude Singcaster (SINM03549508)
- Auteurs    : Alexandre Croisetiere (CROA11029807)

## 1. Outils

Nous choisissons de comparer les outils Maven et Gradle.

## 2. Description de chaque outil 

### Maven

Maven est un outil de gestion de build développé par Apache et utilisé principalement pour les projets en langage Java. Il fut conçu avec comme premier objectif de permettre aux développeurs de comprendre plus rapidement l’état d’un processus de développement en entier.

Cet outil vise à remplir cette mission notamment en misant sur la facilité du processus de build et sur l’uniformité du système (par l’utilisation du project object model), puis en fournissant de l’information sur la qualité d’un projet et des lignes directrices sur les pratiques de développement, ainsi qu’en permettant la migration vers de nouvelles fonctionnalités de manière transparente. Toutefois, les développeurs de Maven reconnaissent que malgré la flexibilité de l’outil, celui-ci ne pourra pas s’adapter à toute situation ou tout projet sans compromettre l’intégrité de ses objectifs de départ ; une structure de build inhabituelle pourrait obliger l’utilisateur à mettre de côté certaines de ses fonctionnalités [1].

### Gradle

Gradle est un outil d’automatisation de build qui utilise un DSL (domain-specific language) basé sur le langage Groovy ou encore Kotlin. Il comprend les mêmes fonctionnalités que ses prédécesseurs, Ant et Maven, en plus d’être conçu pour supporter des builds de grande envergure. Cet outil mise principalement sur la flexibilité et la performance dans son processus d’automatisation.

Parmi les avantages cités dans son guide de l’utilisateur [^2], on compte le fait que Gradle soit hautement personnalisable, même dans ses ramifications les plus fondamentales. On y vante également sa rapidité, alors que les tâches sont accomplies plus vites en effectuant celles-ci en parallèle, en utilisant les sorties obtenues lors d’exécutions précédentes, puis en traitant seulement les entrées qui ont changé. Étant un outil puissant, il s’agit également de l’outil de build officiel pour Android ; Gradle inclut d’ailleurs du soutien pour son utilisation avec différents langages (Java, C++, Javascript).

## 3. Critères

### Gestion des dépendances

La gestion des dépendances est une technique pour déclarer, résoudre et utiliser des dépendances requises par un projet de façon automatique [^3]. Nous avons choisi ce critère car la majorité des projets, de petite, moyenne ou grande envergure requièrent des dépendances open source. De plus, les plugins sont au cœur de Maven et un élément important de Gradle.

Premièrement ces deux outils de build ont certains points en commun au niveau de la gestion des dépendances. Tous deux peuvent gérer des dépendances directe, par exemple déclarées dans le fichier pom de Maven sous <dependencies>, des dépendances transitives, c’est-à-dire des dépendances de dépendances directes d’un projet incluses automatiquement et finalement des dépendances déclarées de façon dynamique, c’est à dire incluses seulement si on veut compiler un certain type de build. Ce dernier type de dépendance peut par exemple être ajouté sous Maven avec l’utilisation de profils ( élément <profile>) et avec l’utilisation de déclarations conditionnelles sous Gradle [^4]. Ensuite, tant Maven que Gradle ont un outil pour copier les dépendances d’un dépôt distant vers une location (répertoire) donné. Sous Maven on peut utiliser un plugin pour cette tâche soit le Apache Maven Dependency Plugin. Sous Gradle, une fonctionnalité similaire peut être ajouté avec une task simple [^5].

Pour ce qui est des dépôts distants de dépendances et plugins, Maven a le Maven Central et Gradle a le Jcenter. Un avantage de ce dernier à ce niveau est qu’il est possible d’utiliser des dépôt Maven comme le Maven Central dans un projet Gradle [^6]. Maven comme Gradle a la possibilité d’utiliser une cache pour les dépendances et Gradle permet l’inclusion d’un checksum de cache SHA-1 et a aussi l’inclusion de metadata de dépôt, ce qui permet de conserver plusieurs version d’un même artefact et permet à deux projets utilisant la même cache de ne pas s’écraser [^7]. Pour le remplacement de dépendances, Maven permet d’écraser une dépendance avec une semblable mais seulement par version. Gradle tant qu’à lui permet des règles de substitutions, qui offrent une plus grande flexibilité de remplacement, notamment en remplaçant une dépendance de projet avec une dépendance externe et vice-versa. Cette fonctionnalité permet notamment à Gradle de fair un build de plusieurs code sources pour créer des builds composites [^8].

Bien que Gradle offre plus de possibilités pour la gestion des dépendances et une plus grande flexibilité à ce niveau, il semble que cet avantage n’en soit qu’un que pour des projet de moyenne et grande envergure ou avec des besoin de build assez complexes. Certains témoignages soulignent que la gestion simple et efficace des dépendances avec Maven lui confère un avantage vis-à-vis Gradle pour un projet d’envergure et complexité standard [^9].

### Complexité de l’outil

En termes d’évaluation de la complexité, quelques critères peuvent être regroupés sous cette plus grande catégorie, telles que la nécessité d’écriture du build, la courbe d’apprentissage et la clarté du script. Il est essentiel de tenir compte du niveau de complexité de l’outil utilisé lorsqu’on en choisit un, selon le projet, sa taille envisagée, ainsi que le niveau de connaissance de l’outil chez ses utilisateurs.

Du côté de Gradle, tout est possible à partir du script de build. Combiné au langage de programmation Groovy, qui permet l’utilisation de conditions, boucles, sous-routines et librairies Java, on laisse une grande liberté aux développeurs, mais cette souplesse a un prix. De par sa complexité plus importante (liée à sa flexibilité), Gradle demande une connaissance particulière de ses rouages alors que la courbe d’apprentissage est particulièrement à pic. Certaines parties du DSL de Groovy peuvent être moins claires, comme savoir quelles notations ou quels symboles peuvent être utilisés [^9]. Ce langage est également plus complexe que XML et nécessitera d’investir plus de temps d’apprentissage que pour un projet utilisant Maven.

La courbe d’apprentissage de Maven est plus douce ; quelques heures de lecture en parallèle avec l’écriture d’un script seront suffisantes à acquérir l’expérience nécessaire pour travailler avec cet outil [^10]. Il est possible d’écrire un fichier POM soi-même à partir de rien, mais cette étape peut être facilitée par l’utilisation d’un IDE. Lorsqu’on choisit Maven pour des petits projets, celui-ci répond généralement bien aux besoins des programmeurs, mais peut rapidement paraître encombré alors qu’on rajoute de plus en plus de spécifications et plugins dans le fichier POM, le rendant illisible [^11]. Il sera préférable de migrer un projet vers Gradle dans cette situation, dans la mesure où cet outil est bien connu par quelques membres de l’équipe.

Ainsi, le choix d’outil de build dépend certainement du niveau de complexité recherché selon le projet à accomplir. On préférera utiliser Maven pour des plus petits projets, tandis que Gradle sera préférable si le projet prend de l’envergure [^12]. Dans le cadre de notre projet de session, en tenant compte de cet enjeu seul, Maven représente un compromis juste, considérant le temps total à investir dans le projet et le fait qu’il s’agit de notre premier projet incluant un outil de build dans un contexte académique.

### Flexibilité de l’outil

La flexibilité d’un outil de build peut être décrite comme son habileté d’être modifiés en fonction du projet en question, sans avoir de restrictions. Ce critère est important car plusieurs projets ont des besoins spécifiques qui peuvent être non réalisable avec un outil qui ne possède pas les bonnes options et qui ne permet pas de modifications. 

L’outil de gestion de build Maven utilise un lifecycle pour la construction de builds. Le lifecycle est composé des plusieurs phases prédéfinies qui exécutent une série de goals. Par défaut, ces phases du cycle sont les suivantes : validate, compile, test, package, verify, install, deploy. Les étapes sont clairements définies, ce qui facilite la compréhension des builds. Par contre, le modèle du processus est standardisé et peut rendre difficile voir impossible certaine modifications [^12]. Pour modifier des aspects du lifecycle, il faut mettre en place des plugins et les détails de sa configuration[^14]. La diversité des plugins est limité, donc certains projets avec des besoins spécifiques préférons éviter Maven. Il est nécessaire de bien comprendre Maven pour faire des modifications, car c’est un framework. C’est pourquoi certains programmeurs décrivent l’outil comme la convention avant la configuration [^14]. En résumé, Maven est peut flexible, mais la rigidité du lifecycle permet aux programmeurs de comprendre des builds avec facilité. 

De son côté, Gradle permet de suivre une convention comme pour Maven, en plus de permettre d'altérer complètement des tâches [^13]. Cet outil est une combination de la flexibilité de Ant et le lifecycle de Maven. Effectivement, les builds sont customisable puisqu’il est possible de créer ses propres tasks et de les utiliser comme on le désire [^9]. Pour ce faire, le langage de programmation Groovy offre plusieurs fonctionnalité utile pour scripter des builds [^9]. D’un autre côté, l’apprentissage de Gradle est compliqué car il est difficile de comprendre certains plugins et la distribution des tâches [^9]. De plus, il faut apprendre Groovy, un langage qui est difficile à assimiler. C’est pourquoi certains programmeurs décrivent l’outil comme la convention et la configuration [^13]. En résumé, Gradle est un outil flexible qui est difficile à apprendre. 

En conclusion, Maven et Gradle se ressemble car tout deux utilise un lifecycle. Par contre, Gradle est plus flexible quand à l’utilisation de ce cycle mais il est très compliqué au début. Maven est un outil très rigide qui permet peut de modification mais qui est qui est relativement simple. Donc, un programmeur devra choisir son outil de construction de build en fonction du temps qu’il a et des caractériques de ses builds.

## Sources

[1]: https://maven.apache.org/what-is-maven.html 
[^2]: https://docs.gradle.org/current/userguide/userguide.html
[^3]: https://docs.gradle.org/current/userguide/introduction_dependency_management.html
[^4]: https://stackoverflow.com/questions/10209686/maven-dynamic-specification-of-dependencies
[^5]: https://www.baeldung.com/ant-maven-gradle
[^6]: https://www.softwareyoga.com/10-reasons-why-we-chose-maven-over-gradle/
[^7]: https://stackify.com/gradle-vs-maven/
[^8]: https://gradle.org/maven-vs-gradle/
[^9]: https://phauer.com/2018/moving-back-from-gradle-to-maven/ 
[^10]: https://zeroturnaround.com/rebellabs/java-build-tools-part-2-a-decision-makers-comparison-of-maven-gradle-and-ant-ivy/2/
[^11]: https://dzone.com/articles/gradle-vs-maven 
[^12]: https://stackify.com/gradle-vs-maven/
[^13]: https://www.bizety.com/2018/11/08/gradle-vs-maven-vs-ant/
[^14]: https://medium.com/@Colin_But/ant-vs-maven-vs-gradle-801fde21af80




