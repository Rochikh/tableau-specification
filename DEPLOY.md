# Déploiement sur quizz.rochane.fr

Objectif : publier ce site statique sur https://quizz.rochane.fr, sur ce serveur, sans toucher aux autres applications.

1. Vérifie que l'IP publique de ce serveur est 168.231.81.126 et que `dig +short quizz.rochane.fr` renvoie cette IP. Si ce n'est pas le cas, arrête-toi et dis-le.
2. Repère où vivent les autres applications et clone https://github.com/Rochikh/tableau-specification dans un dossier voisin, selon la même convention.
3. Inspecte la configuration Traefik en place à partir d'une application déjà en production : réseau Docker, entrypoints, certresolver, redirection HTTP vers HTTPS. Reprends exactement ces conventions.
4. Crée un docker-compose.yml dans le dossier cloné : conteneur nginx:alpine, labels Traefik pour Host(`quizz.rochane.fr`) en HTTPS avec le certresolver existant. Monte en lecture seule uniquement `index.html` et `demo.gif` dans /usr/share/nginx/html. Aucun port publié sur l'hôte.
5. Lance le conteneur. Vérifie que `curl -sI https://quizz.rochane.fr` renvoie 200 avec un certificat valide, que la page contient « Tableau de spécification » et que https://quizz.rochane.fr/demo.gif répond 200.
6. Vérifie qu'aucun autre conteneur n'a été modifié ni redémarré.
7. Termine par un résumé : dossier, nom du conteneur, commande de mise à jour (git pull).

Ne modifie ni la configuration globale de Traefik ni les autres conteneurs. En cas de doute, arrête-toi et demande.
