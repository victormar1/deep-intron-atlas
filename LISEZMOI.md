# Deep Intron Atlas — accès protégé

Atlas des variants introniques profonds évalués par AlphaGenome, avec le comparateur
SpliceAI, la cartographie des pseudoexons et le panneau **Régulation** (régions
régulatrices hors transcrit).

## Accès

Le site demande un mot de passe. Le contenu est **réellement chiffré** — ce n'est pas une
vérification JavaScript, qui laisserait tout lisible dans le source :

| | |
|---|---|
| chiffrement | AES-256-GCM |
| dérivation de clé | PBKDF2-SHA256, 600 000 itérations, sel aléatoire de 16 octets |
| fichiers publiés | `index.html` (page de garde) et `atlas.enc` (l'atlas chiffré) |

Le déchiffrement a lieu **dans le navigateur**. Le mot de passe n'est envoyé nulle part et
aucun serveur ne le voit. Web Crypto exige une origine sécurisée : `https://` ou
`localhost`.

## Limite, dite explicitement

`atlas.enc` est un fichier public. Qui le télécharge peut tenter une attaque **hors ligne**
en essayant des mots de passe. Les 600 000 itérations rendent chaque essai coûteux, mais
ce n'est **pas** une authentification serveur : un mot de passe court ou prévisible finira
par tomber. Cette protection arrête la consultation opportuniste et l'indexation par les
moteurs, pas un attaquant déterminé.

L'historique git a été réécrit le 01/09/2026 : il contenait l'atlas en clair dans
26 commits, ce qui annulait la protection. Le dépôt ne porte plus qu'un seul commit.

## Ce que l'atlas contient

Une réserve à lire avant toute interprétation : **aucun avantage mesurable d'AlphaGenome
sur SpliceAI n'a pu être mis en évidence** sur ce jeu, y compris au-delà de 1 000 pb d'un
site d'épissage — là où l'avantage était attendu. Sur les 8 pseudoexons prouvés par ARN,
SpliceAI désigne les deux bornes exactes 5 fois sur 6, AlphaGenome 2 fois sur 6.

Hors épissage, sur les 4 variants promoteurs pathogènes de la cohorte NF1 — le seul terrain
sans concurrent — **aucune séparation exploitable** non plus : 0 test sur 88 ne passe
Benjamini-Hochberg à 5 %, contre un fond de 69 480 variants.

Les chiffres, leurs intervalles et les pièges rencontrés sont dans `docs/` du dépôt de
travail, non publié ici.
