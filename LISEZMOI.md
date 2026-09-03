# Deep Intron Atlas — accès protégé

*État au 3 septembre 2026.*

L'atlas est chiffré (AES-256-GCM, clé dérivée par PBKDF2-SHA256, 600 000 itérations).
Le déchiffrement a lieu dans le navigateur ; le mot de passe n'est envoyé nulle part.

Le fichier chiffré étant public, un mot de passe faible reste attaquable hors ligne.
Ce n'est pas une authentification serveur : c'est une barrière contre la consultation
opportuniste et l'indexation, sur des données de recherche non publiées.

L'historique git a été réécrit **deux fois**. Le 01/09, parce qu'il contenait l'atlas en
clair dans 26 commits, ce qui annulait la protection. Le 03/09, parce que le chiffrement
tire un sel aléatoire à chaque exécution : `atlas.enc` différait donc octet pour octet
même quand l'atlas était identique, le garde-fou « rien à pousser » ne s'était jamais
déclenché, et le dépôt avait atteint **906 Mo pour quatre fichiers**. La publication
hache désormais l'atlas **en clair**, qui est déterministe, avant de chiffrer.

## Ce que l'atlas dit, et ce qu'il ne dit pas

**Le score du variant discrimine.** AUC appariée 0,943 sur la cohorte patients ; et sur un
jeu indépendant de **52 variants dont la conséquence sur l'ARN est prouvée sur cDNA de
patient** (Koczkowska 2023), 44 sur 52 passent le seuil publié.

**Aucun avantage mesurable d'AlphaGenome sur SpliceAI n'a pu être mis en évidence.** Sur
ces mêmes 52 variants, avec 1 000 témoins appariés des deux côtés : **28 égalités sur 52**,
test des signes p = 0,31, et une équivalence établie à ±0,05 (TOST p = 0,001). Ce n'est
plus une absence de puissance, c'est un test. Sur la désignation des bornes, McNemar
p = 0,50 — les deux modèles se valent aussi sur la position.

**Le résultat positif est ailleurs.** AlphaGenome désigne la borne publiée du pseudoexon
dans **49 cas sur 50**, contre 54 sur 150 témoins appariés du même intron (Fisher
p = 1,5 × 10⁻¹⁶). Nommer la bonne borne n'est donc pas spécifique — un tiers des témoins
bénins la nomment aussi — mais la nommer **fort** l'est.

**L'appartenance à un hotspot n'apporte rien**, et le panneau le dit désormais : sous
relocalisation au hasard, la carte NF1 contient 141 hotspots contre 141 attendus, et la
carte ANK1 en contient 32 **de moins** que le hasard.

**Hors épissage, il n'y a pas de terrain.** Ce qui était présenté comme « 4 variants
promoteurs pathogènes » n'en compte que **deux** : les deux autres sont des délétions de
24 558 et 5 626 pb, scorées à tort comme des substitutions ponctuelles à leur point de
cassure. Sur les 2 SNV réels, à une seule position, aucun test ne passe, et plus aucun
p brut ne descend sous 0,05.

**Aucun seuil n'est transférable d'un gène à l'autre.** Le FPR réel de `q ≥ 0,999` varie
d'un facteur **6,8** entre LDLR et NF1. Les classes affichées ne sont calibrées que sur NF1.

## Usage

Recherche uniquement. Aucun résultat n'est validé pour un usage diagnostique, et les
seuils ne doivent pas être reportés dans un compte rendu de patient.

Les chiffres, leurs intervalles et les 33 pièges rencontrés sont dans `docs/` et
`CLAUDE.md` du dépôt de travail, non publié ici.
