---
layout: post
title: Confessions d'un développeur anonyme...
published: true
categories: [devops, retour-experience]
---

**… ou comment j’en suis arrivé à déployer mes applications en production tout seul**

*Avant propos : toute ressemblance avec des personnes ayant existé ou existant serait purement fortuite.*

Je suis un développeur. Un développeur Java. Et je déploie mes applications en production. Tout seul. Depuis 1 mois. Comment j’en suis arrivé là ? Petit retour en arrière :

Depuis tout petit, en tant que développeur Java on m’a tenu éloigné de la ligne de production. Là où ça canarde, avec des gros serveurs, des gros tuyaux et des grosses roquettes… heu, requêtes.
Il paraît que c’était pour mon bien. J’avais rien à faire là, il fallait que je reste jouer dans l’arrière court, avec mon tomcat.

Ca à duré un moment. On travaillait en cachette dans l’arrière court, avec nos jouets à nous, et de temps en temps il y a un intermédiaire qui passait, on lui donnait ce qu’on avait fait, et il repartait. Souvent, il revenait quelques heures ou quelques jours plus tard, assez énervé, en nous rejetant tout à la figure. Et on recommençait, en essayant de deviner à l’aveugle ce qui n’allait pas.

On aurait presque finit par s’habituer à cette façon de travailler. Sauf que ça pouvait pas durer éternellement. Le premier changement est venu avec la mise en place d’une conférence Jabber commune aux 2 équipes. Oui, un “chat” tout bête auquel les développeurs et les administrateurs système sont connectés toute la journée. Le simple fait de pouvoir suivre en temps réel les mises en production de nos applications, et d’aider en cas de problème, à commencé à faire évoluer notre façon de travailler ensemble. 1 point pour la communication.

Le deuxième changement est venu avec l’accès aux logs. Pareil, ça a l’air bête à dire, mais un développeur qui ne voit pas ses logs, ça donne des logs qui ne servent à rien : soit trop verbeux, soit pas assez détaillés en cas de problème, mais généralement les 2 à la fois ! D’autre part, il faut bien avouer que la majorité des admins système ne sont pas expert en analyse de stacktrace java, et qu’on se retrouve souvent à leur en demander toujours un peu plus : “tu peux me copier-coller la fin de la stack stp”.
Bref, à force d’insister, nous avons eu accès aux logs de production. Via un outil commun avec l’équipe système. Le premier outil lié à la production qu’on partage avec l’équipe système. 1 point pour le partage d’outils.

A partir de là, on s’est senti de plus en plus concernés par ce qu’il se passait en production. On pouvait suivre les mises en production. Voir les erreurs directement, par exemple en cas de mauvaise configuration dans le JNDI. Proposer une solution rapidement. L’idée d’automatiser le déploiement est donc arrivée progressivement.
Comme souvent, la première tentative à été un échec. Mais pas un échec total. En effet, nous avons commencé par un script ant, ce qui nous semblait une bonne solution. Assez “neutre” pour être utilisée par des développeurs et des admins système, dans notre environnement de dev, et dans l’environnement de production. Et bien non, l’équipe système à développée son propre script shell.
Nous avons donc passé plusieurs mois ainsi, dans une pseudo-automatisation, avec des scripts (et méthodes) différentes dans des environnements différents.

Un peu plus tard, nous avons cru voir notre salut dans un outil commercial. La solution était attirante, et l’idée d’utiliser la même méthode pour déployer sur les différents environnements nous plaisait. Surtout qu’on imaginait déjà au bout du tunnel le fait de pouvoir faire nous même les mises en production. 2ème échec : problème de budget. Et oui, “pourquoi dépenser de l’argent pour quelque chose qui marche déjà ?”

Je ne vais pas vous faire le coup du guerrier qui se relève plus fort après avoir été blessé. Si ? Bon ok : nous avons donc commencé à travaillé ensemble sur la mise en place d’outils et de processus pour l’automatisation de la mise en production de nos applications. Bref, nous avons regardé tout ce qui tournait autour de devops, en se disant : “ok on est prêt, on peut y aller”.
Je garde les détails pour un prochain billet, sinon on est encore là demain matin ! Sachez juste que notre objectif était le mythique “1-click deploy” : une interface web simple, qui permet de déployer en production en 1 seul click.
Il est donc temps de passer aux choses sérieuses : la première fois.

La première fois. On était seuls. En tête à tête. Par où commencer ? En théorie je sais très bien comment faire, mais là c’est la pratique. Je repère le “spot”, ok c’est là qu’il faut aller. L’adrénaline monte. Un coup d’oeil à droite, un autre à gauche, histoire de vérifier que personne ne surveille. On sait jamais, un type qui se pointerai à la dernière minute, et me dirait "Non mais monsieur, c’est interdit ce que vous allez faire là ![](".
Reprenons. Je commence à transpirer. Je me déboutonne. Allez, j'y vais ) La machine est lancée, j’ai l’impression que rien ne pourra l’arrêter. En tout cas je n’ai pas la volonté de le faire. Le temps ralenti, les secondes durent des heures. Est-ce que tout se passe bien ? Un dernier soubresaut, et c’est fini. Déjà ? Est-ce que ce n’est pas trop court ? Est-ce que tout s’est bien déroulé comme prévu ?
Et oui, notre application s’est bien déployée ! Et je peux même me permettre de recommencer. De cliquer comme un forcené sur ce bouton. D’appeler les autres pour leur montrer. Hé les gars, je l’ai fait !

Un mois plus tard. Qu’est ce qui a changé ? Et bien finalement, pas tant de choses que ça. Et pourtant si.
Est-ce qu’on fait 50 déploiements par jour ? Non. 10 peut-être ? Non. Plusieurs par jour alors ? Non. Bon au moins un par jour ? Et bien… même pas forcément.
Ce qui change surtout, c’est la possibilité de déployer quand on veut. On ne dépend pas de la présence et de la disponibilité de quelqu’un d’autre. Le système est fiable, et la confiance s’est installée.
Alors pourquoi ne pas déployer plusieurs fois par jour ? Tout simplement car ça demande un changement d’organisation et de méthode de développement, donc du temps. On ne passe pas d’un déploiement toutes les 2 semaines à plusieurs déploiements par jour en claquant des doigts. Mais on y travaille.

L’autre gros changement, le plus important pour moi : le changement de philosophie. Officiellement, les développeurs ne font pas d’astreinte. Néanmoins en cas de problème, on a maintenant la capacité d’intervenir : on connait l’infrastructure, on a accès aux machines, à la configuration, aux logs, et bien sur au code source des applications. On sait ce qui a été modifié récemment, ce qu’on peut désactiver pour remettre le service en ligne. Et on le fait. En tout cas je l’ai fait.
Et intervenir comme ça un soir tard, ça fait réfléchir quand à la façon de développer. On est responsable du fonctionnement de notre application, on est investi dans son bon fonctionnement en production.

L’automatisation du déploiement, le partage d’outils, la communication, la confiance, c’est bien. Mais ce n’est qu’une partie des concepts devops. Il nous reste encore beaucoup de travail : améliorer les tests automatisés en amont des déploiements, le monitoring et les alertes, continuer à faire évoluer notre façon de développer, etc.
Et au final, le grand gagnant ce n’est pas tant les développeurs ou les admins système, mais le client. Que ce soit le client interne qui fait ses demandes d’évolution, ou le client externe qui utilise l’application.

Voilà. Je suis un développeur. Un développeur Java. Et je déploie mes applications en production. Tout seul. Depuis 1 mois.

*PS: inspiré d’une histoire réelle, même si tout à été volontairement exagéré dans ce texte. Mais sachez tout de même qu’aucun développeur ou administrateur système n’a été maltraité durant l’écriture de ce texte ;-)*
