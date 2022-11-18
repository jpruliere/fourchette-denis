# Le jeu de la fourchette

Le jeu de la fourchette est un petit jeu à deux très célèbre dans lequel un premier joueur pense à un nombre entre 1 et 100, et l'autre tente de le deviner. Le premier joueur ne peut que répondre que le nombre proposé est plus grand, plus petit ou égal au nombre choisi. La partie se termine quand le nombre est trouvé.

## Version serveur Express

### v1

Tu vas reproduire ce jeu, de sorte que :
- Le serveur représente le joueur qui choisit un nombre (`Math.random()` et `Math.floor()` vont t'aider). Ce nombre sera choisi au lancement du programme.
- Le client représente l'autre joueur, qui propose des nombres à l'aide d'une route dynamique `/propose/:nombre`. Cette route s'assure que le nombre en est un, et qu'il est bien compris dans la fourchette [1, 100], elle retourne une erreur 400 sinon.

### v2

Une fois que la partie est terminée, il faut relancer le serveur pour rejouer, c'est un peu pénible. Ajoute une route `/recommencer` qui choisit un nouveau nombre.

### v2.1

Transforme la route en `/recommencer/avecLesBornes/:min/et/:max` qui permet de choisir d'autres bornes que 1 et 100. La route ne retournera une erreur que si l'écart entre les deux est inférieur à 10 (la partie ne serait vraiment pas longue, sinon). Si `min` est supérieur à `max`, les deux bornes sont simplement inversées et la partie se lance.

### ettehcruof

Ce projet au nom curieux est tout simplement celui de la fourchette inversée, c'est-à-dire où les rôles sont échangés :
- Le client appelle une route `/commencons` (normalement il y a une cédille, mais on ne met pas d'accents dans les URL) une fois qu'il a choisi son nombre entre 1 et 100
- Le serveur répond avec une proposition (choisis la au hasard)
- Le client peut alors appelle `/plusPetit`, `/plusGrand` ou `/bravo` pour indiquer sa réponse au serveur, qui donne alors une nouvelle proposition tenant compte de cette réponse

Je te laisse réfléchir à comment faire pour que le serveur tienne compte de la réponse du client.

Quand le client appelle `/bravo`, c'est que le serveur a gagné, il peut donc répondre avec un petit message où il se vante de ses prouesses.

### v1.1

Fais en sorte que le serveur compte ses tentatives et adapte le message de victoire :
- S'il trouve en moins de 5 essais, il est très vantard
- S'il trouve entre 5 et 9 essais, il trouve quand même que sa performance n'est pas si mal
- Au delà de 10 essais, il dit simplement qu'il fera mieux la prochaine fois.

### v1.2

Optimise la proposition du serveur pour gagner en un minimum de coups (une petite recherche sur le terme `dichotomie` peut t'aider si tu ne vois pas comment faire).

### v2

À tout moment, le client doit pouvoir appeler `/recommencons` pour indiquer au serveur qu'il souhaite démarrer une nouvelle partie.

### v2.1

Permet au client de personnaliser les bornes grâce à la route `/recommencons/avecLesBornes/:min/et/:max`.