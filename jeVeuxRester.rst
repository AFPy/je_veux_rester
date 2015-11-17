==============
Je veux rester
==============

:date: 2015-11-03
:author: Pierre Imbaud

*Je Veux Rester* est une initiative de soutien au langage
``RestructuredText``, ou ``ReST``  (en anglais: *I want to rest* (:-)).
https://en.wikipedia.org/wiki/ReStructuredText

``ReST`` est un langage de markup léger, permettant de facilement
agrémenter du texte avec des attributs de mise en page (gras,
italique, titre, lien), sans la lourdeur, considérée (par moi mais pas
que) comme prohibitive, des langages de markup traditionnels que sont
html et xml mais en permettant de garder un texte lisible dans son
code source.

Il s'inscrit dans une lignée de langages de markup légers, née avec
les wiki.

Il est né dans la communauté Python, et continue à y prospérer [1]_ ;
c'est le langage utilisé par Sphinx [2]_ et donc par la documentation
officielle Python. Même ceux qui ne le connaissent pas sont
probablement déjà tombés sur des ``README.rst``, documentant des
paquets Python ou autres.

Comme beaucoup d'outils Python, il a bénéficié d'un design soigné,
aboutissant à un compromis remarquable entre puissance expressive et
simplicité.

Un fichier source ``.rst`` peut être traduit en html, docx, pdf, latex, et
j'en passe.

**Petit mais puissant**, le langage permet de construire des
documentations modernes, puissantes, élégantes. Il suffit de consulter
la documentations officielle Python de [3]_ (générée par Sphinx et
rédigée en ReST) pour s'en convaincre.

Le langage a ses limitations, Latex ou LibreOffice sont préférés par
certains, y compris pour des textes courts. Le fil à couper le beurre
et le tournevis ont eux aussi leurs détracteurs (:-).

Quels objectifs, alors, pour cette initiative de soutien à un bébé
sur le berceau duquel tant de fées se sont déjà penchées ?

Les wiki
========

Il y a de nombreux systèmes de wiki, chacun avec son propre langage,
combinant généralement :

- une certaine pauvreté expressive ;
- le recours à html, pour pallier cette pauvreté.

Le résultat cumule, à mes yeux, les inconvénients des deux approches.

Certains wikis, dont mediawiki (utilisé par wikipedia) permettent
l'utilisation de ``ReST`` ... avec un plugin, mal maintenu : le source
existe, des bugs ou des limitations, pas de mailinglist, pas de bug
tracker, plus de mainteneur depuis des mois. Il faudrait reprendre ou
remplacer ces outils. Les wikis étant généralement en PHP, les outils
sont également en PHP, hors de ma compétence.

Il faudrait par ailleurs :

- identifier les wiki ReST-friendly, ou ReST-compatibles ;
- éventuellement assister les développeurs vers la ReST-compatibilité.


Les éditeurs
============

Il y a un mode emacs, que j'utilise pour saisir ce texte. Il offre un
bon rendu du texte saisi, mais comporte des lourdeurs et des
inélégances pour la saisie ou la modification du texte, entre autres
pour la gestion des listes. Mais peut être suis-je le dernier des
mohicans à utiliser emacs ?

Y a-t-il un mode vim ? eclipse ? quid des ide Python ? (je n'en pratique
aucun).


La traduction
=============

Le traducteur de référence, en particulier entre langages de markup,
est Pandoc. C'est écrit en haskell, ça marche plutôt bien.

Le traducteur est nécessaire, non pas pour traduire vers les cibles
usuelles que sont PDF, LaTeX, HTML, docx, mais vers d'autres langages
de markup, notamment Markdown et MediaWiki et le texte simple.

Pandoc présente deux inconvénients :

- le code n'est pas accessible au Pythonien moyen; du moins pas sans
  un effort notable (:-)  
- l'installation des outils haskell est parfois coûteuse et difficile,
  en particulier sous Gentoo (102 paquets à installer!)

Avoir plusieurs outils qui font le même travail et diffèrent
seulement par le langage d'implémentation, ce n'est pas très
glorieux. Et ça pose, évidemment, des problèmes de maintenabilité.

Aussi une architecture plus sexy serait souhaitable, dans laquelle :

- un langage de description de données est choisi, pour décrire
  syntaxe et sémantique des langages source et cible ; (Yaml ? JSON ?
  Lex/Bison ?)
- chaque langage (source et cible) est décrit dans cette base ;
- les traducteurs sont implémentés en Python, haskell, perl, ou autre,
  en s'appuyant exclusivement sur ces descriptions.

Le projet est utilisable/amendable par les différentes
communautés. C'est plus amusant que de se lancer des anathèmes, et de
boire des bières de marques différentes dans les confs où l'on se
croise. L'introduction d'un nouveau langage cible peut être fait par
un membre de quelque communauté que ce soit **et** bénéficier aux
autres communautés.

L'outil décrit ici n'est peut être pas réaliste ?

:Note: je viens de relire la doc pandoc, l'outil est remarquablement
       bien architecturé, le remplacer sans perdre en qualité semble
       une gageure. différentes solutions de customisation, entre
       autres avec les filtres, méritent sans doute d'être explorées.

Docx
====

Je n'ai pas traduit vers docx depuis longtemps, et mes souvenirs des
problèmes rencontrés sont parcellaires.

Ce qui était clair, c'est que la traduction n'était pas utilisable en
l'état : ça produit du docx difficile à intégrer dans une trame
existante. Et la production de docx depuis du ReST me semble avoir pour
seul intérêt l'intégration dans une trame existante.

Il faut donc un paramétrage, qui peut être fait dans une deuxième
passe, et qui permette de mapper les niveaux de paragraphes ReST sur
ceux de docx.

:Note: Les filtres pandoc peuvent-ils fournir une solution ?


iPython notebooks
=================

Il n'aura pas échappé à ceux qui l'auront remarqué (et vice versa) que
les iPython notebooks permettent de panacher code et texte, **non
pas** en ``ReST``, **mais en** ``Markdown``! Markdown est un assez bon
markup langage, antérieur à ReST, un peu plus répandu... mais moins
complet, moins bien ficelé. Au point que certains utilisent un
markdown "étendu" pour atteindre leurs objectifs. Si mes souvenirs
sont exacts, c'est le cas de doxygen.

Permettre l'utilisation de ReST dans les notebooks serait un progrès
notable. D'ailleurs c'est peut être en cours, d'ailleurs c'est peut
être en place, je regarde toutes les 1/2 heures. (:-)

Chantier
========

Le chantier à entreprendre n'est pas dantesque, mais il est
conséquent. Il est à vocation pratico-pratique, et ne semble pas
impliquer d'algorithmique très décoiffante. Il est cependant un peu
gros pour une seule personne, surtout sans "retour" de la
communauté. Il me semble bien correspondre aux "groupes de travail"
évoqués suite à PyconFR 2015.

Même si vous ne pensez pas participer, votre retour sur la question
m'intéresse :

- utilisez-vous ``ReST`` ? Dans les docstring, sous Sphinx, dans des
  wiki ?
- partagez-vous mon analyse ?
- de meilleurs outils amélioreraient-ils vos cas d'usages ?
- lesquels des outils proposés vous semblent urgents ?

.. [1] les outils de base et la documentation sont disponibles dans
       docutils. http://docutils.sourceforge.net

.. [2] http://sphinx-doc.org

.. [3] https://docs.python.org
