---
layout: post
tags: llm mcp légifrance
---

# llm : que faire quand tes enfants vivent le mythe de Prométhée ?

On a déjà tant écrit sur les llm : pourquoi écrire un blog-post supplémentaire sur ce sujet ?

Je vis de l'informatique depuis plus de 20 ans, impossible de passer à côté de saut technologique. Pour commencer, mon goût pour la technique me pousse à jouer sur ce nouveau ballon qui arrive dans mon terrain de jeu professionnel. Et puis, l'adoption fulgurante de ChatGPT, Copilot, Mistral et consor par tous les publics ne peuvent laisser indifférent. Enfin, pour tenter de guider mes 2 ado dans l'usage de cet outil qui va certainement façonner leur manière de penser (comme le web et les moteurs de recherche ont certainement façonner la mienne il  ya 20 ans). 

Pour toutes ces raisons : impossible de ne rien faire.

Mais comment ignorer les inquiétudes au sujet la direction que nous prenons tambour battant avec les llm  ? Certains en parlent comme la pire découverte humaine depuis la bombe atomique. Le célèbre [Yuval Noah Harari évoque un techno-autoritarisme](https://www.wired.com/story/questions-answered-by-yuval-noah-harari-for-wired-ai-artificial-intelligence-singularity/)). Il est certain que le monstre GodziLLM sort à peine du bac à sable, et que le pire est devant nous. Que le robot vocal de mon garagiste, avec son parlé parfaitement "naturel", soit insupportable : ce n'est pas grave. Mais quelles firmes prendra le pouvoir de la défense, de la culture, de l'éducation quand les llm seront partout dans ces domaines d'activité, et que les états (et donc les citoyens) auront perdu le contrôle ce qui s'y passe ? Comment les jeunes génération peuvent-elles séparer le bon grain de l'ivraie quand il est impossible de dissocier sur leurs écran et dans leurs écouteurs le contenu "synthétisé" par une IA (probablement massivement et à moindre coût) d'un contenu humainement consolidé (certainement plus rare et plus coûteux).

A n'en pas douter, les llm font partie de ces technologie qui ravivent le mythe de Prométhée : une fois de plus, l'Homme a volé le feu à Héphaïstos (l'énergie des datacenters) et la connaissance à Athéna (le calcul matriciel à grande échelle et les GPU qui le permettent) : la punition des Dieux va être terrible.

Donc pour se préparer à la tempête : apprenons à jouer avec le feu !


# Le terrain de jeu : un seveur mcp pour légifrance

## Pourquoi un serveur mcp ?

Pour un humble développeur, la création d'un llm est sans doute une tâche ardue.

Par contre, le concept de mcp (le nouveau buzz word ?) est outil qui constitue un terrain de jeu plus abordable. 

En 2 mots : un serveur mcp permet d'interfacer un llm à un logiciel tiers, pas forcément exposé sur le web. [La spécification](https://modelcontextprotocol.io/introduction) a été introduite fin 2024 par la société Antropic. De nombreux acteurs s'en sont emparés, et on trouve de nombreuses implémentations, notamment dans l'univers Java avec notammment spring, quarkus, et l'incontournable langchain4j.

Il y a plein de raisons de s'intéresser au concept de mcp :
- Le serveur mcp constitue une interface avec un service qui peut être un service propriétaire. C'est donc une brique qui permet à un llm de manipuler des données qui ne sont pas exposées sur internet (qui n'ont donc pas été l'objet de l'entraînement d'un llm). Techniquement, on peut facilement envisager avec un serveur mcp de faire interagir un llm avec des données d'un SI d'entreprise. Cela soulève évidemment plein de questions sur la sécurité des données traitées par le llm.
- C'est indépendant du llm auquel on est connecté : là aussi, ça favorise l'indépendance vis-à-vis d'un llm particulier. Donc en théorie, pas besoin de se marrier pour la vie avec Gemini, ChatGPT ou Mistral.
- Comme c'est indépendant du llm, si on a l'infrastucture adéquate, cela permet même de s'interfacer avec un modèle qui tourne dans son propre SI si on a de forte de contrainte de sécurité
- C'est une spécifcation avec différentes implémentations : cela favorise le choix des langages, des outils, des frameworks, des plateformes utilisés. 


# Pourquoi légifrance ?

[Légifrance est un service proposé par le gouvernement français pour exposer publiquement les données juridiques officielles du droit français.](https://www.data.gouv.fr/dataservices/legifrance/)

On y trouve notamment :
- tous les textes de loi, les ordonnances, les décrets, et les arrêtés en vigueur.
- leur historique dans le temps
- les textes de jurisprudence

Les données sont exposées par une API REST.

Tout ce qu'il faut pour brancher créer un serveur mcp.

Et comme c'est important de travailler avec un contexte métier qui a du sens, autant travailler avec légifrance [qu'avec les personnages de Star Wars](https://swapi.py4e.com/documentation).


# Remettons à César...

D'autres ont eu l'idée de faire un serveur mcp avec les données de légifrance.
En particulier [le cabinet d'avocats Raphaël D'Assignies](https://lab.dassignies.law/) a publié :
- [une API de recherche des données légales ou réglementaires basées sur légifrance](https://lab.dassignies.law/api/docs), dont [le code est opensource, disponible sur github](https://github.com/pylegifrance/pylegifrance)
- [un serveur mcp connectées aux données de légifrance via son API de recherche des données légifrance](https://ubos.tech/mcp/mcp-server-legifrance/), dont [le code est aussi sur github](https://github.com/pylegifrance/mcp-server-legifrance) (en python)
- [un chatbot **PEDAGOGIQUE** nommé "bodacc"](https://lab.dassignies.law/#bodacc)

Merci à eux, je me réfère quelques fois à leur code, notamment pour comprendre le fonctionnement de l'API officielle de légifrance (dont la doc est parfois obscure).