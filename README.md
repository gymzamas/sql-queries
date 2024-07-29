# sql-queries
Introduction
Ce projet contient 23 requêtes SQL conçues pour récupérer des informations spécifiques à partir d'une base de données de films en utilisant phpMyAdmin. Chaque exercice se concentre sur différents aspects de la base de données, tels que la récupération d'informations sur les artistes, les films, les rôles, les notes, et plus encore.
///////////////////////
Exo 1: Nom et année de naissance des artistes nés avant 1950.
sql

SELECT nom, annee_naissance
FROM artistes
WHERE annee_naissance < 1950;
Cette requête récupère le nom et l'année de naissance des artistes nés avant 1950.

Exo 2: Titre de tous les drames.
sql

SELECT titre
FROM films
WHERE genre = 'Drame';
Cette requête récupère les titres de tous les films dramatiques.

Exo 3: Quels rôles a joué Bruce Willis.
sql

SELECT role
FROM roles
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE acteurs.nom = 'Willis' AND acteurs.prenom = 'Bruce';
Cette requête récupère tous les rôles joués par Bruce Willis.

Exo 4: Qui est le réalisateur de Memento.
sql

SELECT realisateurs.nom, realisateurs.prenom
FROM realisateurs
JOIN films ON films.realisateur_id = realisateurs.id
WHERE films.titre = 'Memento';
Cette requête récupère le réalisateur du film Memento.

Exo 5: Quelles sont les notes obtenues par le film Fargo
sql

SELECT notes.note
FROM notes
JOIN films ON notes.film_id = films.id
WHERE films.titre = 'Fargo';
Cette requête récupère les notes attribuées au film Fargo.

Exo 6: Qui a joué le rôle de Chewbacca?
sql

SELECT acteurs.nom, acteurs.prenom
FROM roles
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE roles.role = 'Chewbacca';
Cette requête récupère l'acteur qui a joué le rôle de Chewbacca.

Exo 7: Dans quels films Bruce Willis a-t-il joué le rôle de John McClane?
sql

SELECT films.titre
FROM films
JOIN roles ON films.id = roles.film_id
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE acteurs.nom = 'Willis' AND acteurs.prenom = 'Bruce' AND roles.role = 'John McClane';
Cette requête récupère les films dans lesquels Bruce Willis a joué le rôle de John McClane.

Exo 8: Nom des acteurs de 'Sueurs froides'
sql

SELECT acteurs.nom, acteurs.prenom
FROM acteurs
JOIN roles ON acteurs.id = roles.acteur_id
JOIN films ON roles.film_id = films.id
WHERE films.titre = 'Sueurs froides';
Cette requête récupère les noms des acteurs du film 'Sueurs froides'.

Exo 9: Quelles sont les films notés par l'internaute Prénom0 Nom0
sql

SELECT films.titre
FROM films
JOIN notes ON films.id = notes.film_id
JOIN internautes ON notes.internaute_id = internautes.id
WHERE internautes.nom = 'Nom0' AND internautes.prenom = 'Prenom0';
Cette requête récupère les films notés par l'internaute Prénom0 Nom0.

Exo 10: Films dont le réalisateur est Tim Burton, et l’un des acteurs Johnny Depp.
sql

SELECT films.titre
FROM films
JOIN realisateurs ON films.realisateur_id = realisateurs.id
JOIN roles ON films.id = roles.film_id
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE realisateurs.nom = 'Burton' AND realisateurs.prenom = 'Tim' AND acteurs.nom = 'Depp' AND acteurs.prenom = 'Johnny';
Cette requête récupère les films réalisés par Tim Burton dans lesquels Johnny Depp a joué.

Exo 11: Titre des films dans lesquels a joué Woody Allen. Donner aussi le rôle.
sql

SELECT films.titre, roles.role
FROM films
JOIN roles ON films.id = roles.film_id
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE acteurs.nom = 'Allen' AND acteurs.prenom = 'Woody';
Cette requête récupère les titres des films dans lesquels Woody Allen a joué, ainsi que ses rôles.

Exo 12: Quel metteur en scène a tourné dans ses propres films ? Donner le nom, le rôle et le titre des films.
sql

SELECT realisateurs.nom, realisateurs.prenom, roles.role, films.titre
FROM films
JOIN roles ON films.id = roles.film_id
JOIN realisateurs ON films.realisateur_id = realisateurs.id
WHERE roles.acteur_id = realisateurs.id;
Cette requête récupère les noms, rôles et titres des films des réalisateurs ayant joué dans leurs propres films.

Exo 13: Titre des films de Quentin Tarantino dans lesquels il n’a pas joué.
sql

SELECT films.titre
FROM films
JOIN realisateurs ON films.realisateur_id = realisateurs.id
LEFT JOIN roles ON films.id = roles.film_id AND roles.acteur_id = realisateurs.id
WHERE realisateurs.nom = 'Tarantino' AND realisateurs.prenom = 'Quentin' AND roles.role IS NULL;
Cette requête récupère les titres des films réalisés par Quentin Tarantino dans lesquels il n’a pas joué.

Exo 14: Quel metteur en scène a tourné en tant qu’acteur ? Donner le nom, le rôle et le titre des films dans lesquels cet artiste a joué.
sql

SELECT realisateurs.nom, realisateurs.prenom, roles.role, films.titre
FROM films
JOIN roles ON films.id = roles.film_id
JOIN realisateurs ON roles.acteur_id = realisateurs.id;
Cette requête récupère les noms, rôles et titres des films des réalisateurs ayant joué en tant qu’acteurs.

Exo 15: Donnez les films de Hitchcock sans James Stewart
sql

SELECT films.titre
FROM films
JOIN realisateurs ON films.realisateur_id = realisateurs.id
LEFT JOIN roles ON films.id = roles.film_id
LEFT JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE realisateurs.nom = 'Hitchcock' AND (acteurs.nom != 'Stewart' OR acteurs.prenom != 'James');
Cette requête récupère les titres des films réalisés par Hitchcock sans James Stewart.

Exo 16: Dans quels films le réalisateur a-t-il le même prénom que l’un des interprètes ? (titre, nom du réalisateur, nom de l’interprète). Le réalisateur et l’interprète ne doivent pas être la même personne.
sql

SELECT films.titre, realisateurs.nom AS realisateur_nom, realisateurs.prenom AS realisateur_prenom, acteurs.nom AS acteur_nom, acteurs.prenom AS acteur_prenom
FROM films
JOIN realisateurs ON films.realisateur_id = realisateurs.id
JOIN roles ON films.id = roles.film_id
JOIN acteurs ON roles.acteur_id = acteurs.id
WHERE realisateurs.prenom = acteurs.prenom AND realisateurs.id != acteurs.id;
Cette requête récupère les films où le réalisateur a le même prénom que l’un des acteurs, en excluant les cas où ils sont la même personne.

Exo 17: Les films sans rôle
sql

SELECT films.titre
FROM films
LEFT JOIN roles ON films.id = roles.film_id
WHERE roles.film_id IS NULL;
Cette requête récupère les films sans rôle assigné.

Exo 18: Quelles sont les films non notés par l'internaute Prénom1 Nom1
sql

SELECT films.titre
FROM films
LEFT JOIN notes ON films.id = notes.film_id AND notes.internaute_id = (SELECT id FROM internautes WHERE nom = 'Nom1' AND prenom = 'Prenom1')
WHERE notes.note IS NULL;
Cette requête récupère les films non notés par l'internaute Prénom1 Nom1.

Exo 19: Quels acteurs n’ont jamais réalisé de film ?
sql

SELECT acteurs.nom, acteurs.prenom
FROM acteurs
LEFT JOIN realisateurs ON acteurs.id = realisateurs.id
WHERE realisateurs.id IS NULL;
Cette requête récupère les acteurs n’ayant jamais réalisé de film.

Exo 20: Quelle est la moyenne des notes de Memento
sql

SELECT AVG(notes.note) AS moyenne_note
FROM notes
JOIN films ON notes.film_id = films.id
WHERE films.titre = 'Memento';
Cette requête récupère la moyenne des notes du film Memento.

Exo 21: id, nom et prénom des réalisateurs, et nombre de films qu’ils ont tournés.
sql

SELECT realisateurs.id, realisateurs.nom, realisateurs.prenom, COUNT(films.id) AS nombre_films
FROM realisateurs
JOIN films ON films.realisateur_id = realisateurs.id
GROUP BY realisateurs.id;
Cette requête récupère l'id, le nom et le prénom des réalisateurs, ainsi que le nombre de films qu'ils ont tournés.

Exo 22: Nom et prénom des réalisateurs qui ont tourné au moins deux films.
sql

SELECT realisateurs.nom, realisateurs.prenom
FROM realisateurs
JOIN films ON films.realisateur_id = realisateurs.id
GROUP BY realisateurs.id
HAVING COUNT(films.id) >= 2;
Cette requête récupère les noms et prénoms des réalisateurs ayant tourné au moins deux films.

Exo 23: Quels films ont une moyenne des notes supérieure à 7
sql

SELECT films.titre
FROM films
JOIN notes ON films.id = notes.film_id
GROUP BY films.id
HAVING AVG(notes.note) > 7;
Cette requête récupère les titres des films ayant une moyenne des notes supérieure à 7.

Conclusion
Ce projet démontre comment effectuer diverses requêtes SQL pour récupérer des données spécifiques à partir d'une base de données de films. Chaque requête répond à un besoin unique, mettant en valeur la polyvalence et la puissance de SQL dans la récupération et la manipulation des données.
