# Analyse des retards de livraison – DataCo Supply Chain (R)

Projet d'analyse de données réalisé en **R de base** (sans package) et rédigé avec **Quarto**, sur les commandes de l'entreprise fictive DataCo.

**Question centrale :** d'où viennent les retards de livraison ?

---

## Données

- **Source :** jeu de données *DataCo Smart Supply Chain for Big Data Analysis* (Kaggle). Il n'est pas inclus dans ce dépôt à cause de sa taille (≈ 90 Mo) : [lien vers la page Kaggle]
- **180 519 lignes et 53 colonnes.** Une ligne correspond à un article commandé, pas à une commande entière.
- Fichier lu avec `fileEncoding = "latin1"`.

## Questions et résultats

### Q1 – Les retards dépendent-ils du mode de livraison ?
- **54,8 %** des commandes sont livrées en retard.
- C'est le facteur principal. Standard Class respecte en moyenne son délai (4 jours prévus, 4 réels). First Class et Second Class livrent en près de **deux fois** le délai promis (1 → 2 jours, 2 → 3,99 jours).

### Q2 – Que devient le taux de retard sans les commandes annulées ?
- Une commande annulée n'est pas un retard. En les retirant, le nombre de retards reste le même mais le nombre de livraisons diminue : le taux de retard passe à **57,3 %**.

### Q3 – Le taux de retard dépend-il du mode de livraison ?
- Oui, très fortement : **First Class 100 %**, Second Class 79,8 %, Same Day 47,9 %, Standard Class 39,8 %.
- Toutes les commandes First Class livrées arrivent en retard : le délai promis (1 jour) n'est jamais tenu.

### Zoom Same Day
- Le taux de retard varie peu selon la **région** (45,4 % à 50,4 %), le **mois** (43,6 % à 52,1 %) et le **segment de clientèle** (44,4 % à 48,7 %).
- Selon le **type de produit**, les grands rayons sont tous autour de 47-48 %. Book Shop (76 %) et Pet Shop (60 %) sont plus élevés, mais sur trop peu de commandes (42 et 38) pour conclure.
- Aucun de ces facteurs n'explique les retards Same Day.
### Les retards coûtent-ils de l'argent ?
- Le bénéfice moyen par commande est presque identique quel que soit le statut de livraison (20,70 € à 22,71 €).
- Ce bénéfice est enregistré **à la vente** : même les commandes annulées en affichent un. Ces données ne mesurent donc pas le coût réel des retards.

### Durée des retards par marché
- Parmi les commandes en retard, le retard moyen est le même dans tous les marchés (**1,60 à 1,62 jour**). La géographie n'explique pas la durée des retards.

---

## Conclusion

Sur les commandes livrées, **57,3 %** arrivent en retard. Le mode de livraison est le principal facteur : **toutes** les commandes First Class sont en retard, et Second Class livre en près de deux fois le délai promis, alors que Standard Class respecte en moyenne son délai. Pour Same Day, ni la région, ni le mois, ni le type de produit, ni le segment de clientèle n'expliquent les retards. La durée moyenne d'un retard est aussi la même dans tous les marchés (1,60 à 1,62 jour).

Le bénéfice par commande étant enregistré à la vente, ces données ne mesurent pas le coût réel des retards. Une prochaine analyse pourrait vérifier si les clients livrés en retard à leur première commande recommandent moins souvent.

## Limites

- Jeu de données **en partie simulé** : les retards y sont répartis de façon très uniforme.
- Une ligne correspond à un article et non à une commande. Les taux sont donc calculés par article.
- Le coût réel des retards (perte de clients) n'est pas mesurable directement. **Piste :** vérifier si les clients livrés en retard à leur première commande recommandent moins souvent.

## Méthode et utilisation de l'IA

Fonctions R utilisées : `subset()`, `table()`, `prop.table()`, `tapply()`, `aggregate()`, `sort()`, `barplot()`.

J'ai utilisé **Claude** comme tuteur : il me donnait l'objectif et des indices, j'écrivais le code, puis il corrigeait mes erreurs. Les choix d'analyse et les conclusions sont les miens.

**Vérifications :** dimensions du tableau à chaque étape, cohérence entre le nombre de commandes en retard et le taux global (98 977 / 180 519 = 54,8 %), écart minimal de 1 jour pour toutes les commandes en retard.

## Fichiers

- `analyse_retards_dataco.qmd` : le document Quarto (code R et texte)
- `analyse_retards_dataco.html` : le rapport généré, autonome

## Reproduire l'analyse

1. Télécharger le CSV depuis Kaggle et le placer dans `data/DataCoSupplyChainDataset.csv`.
2. Ouvrir `analyse_retards_dataco.qmd` dans RStudio (R 4.5.2) et cliquer sur **Render**. Aucun package n'est nécessaire.
