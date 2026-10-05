# Aura — la météo qui se voit

Application météo en temps réel construite sur les API gratuites d'[Open-Meteo](https://open-meteo.com/). Un seul fichier `index.html`, sans framework ni dépendance, sans clé d'API.

## L'idée

La plupart des applications météo empilent des cartes de chiffres. Aura part d'un autre principe : **le ciel est la donnée**.

- **Un ciel vivant, piloté par l'API.** Le fond animé (canvas 2D) traduit les mesures : densité des nuages selon la couverture nuageuse, pluie inclinée selon la vitesse et la direction du vent, neige, brouillard, éclairs en cas d'orage, soleil placé entre son lever et son coucher réels, lune dessinée dans sa phase réelle.
- **Un curseur temporel.** On fait glisser le doigt sur la courbe des 48 prochaines heures et toute l'interface voyage dans le temps : ciel, température, instruments. Les valeurs prévues passent en italique, les valeurs actuelles restent en romain.
- **La couleur, c'est la température.** L'unique couleur d'accent de l'interface est calculée à partir de la température affichée.

## Fonctionnalités

- **Vos meilleurs créneaux** : pour six activités (course, vélo, terrasse, linge, photo à l'heure dorée, observation des étoiles), un score horaire transparent identifie le meilleur créneau des 48 h et nomme son point faible. Un clic montre le ciel à ce moment-là.
- **Résumé en langage naturel** : « Pluie probable vers 17 h (70 %). Demain sera nettement plus frais. »
- **Les 7 prochains jours** : barres de températures à l'échelle de la semaine, détails dépliables.
- **Instruments** : vent (boussole et échelle de Beaufort), UV, humidité et point de rosée, pression et tendance sur 3 h, visibilité, phase de la lune, course du soleil, qualité de l'air européenne.
- **Mémoire du climat** : 30 ans d'archives ERA5 situent la journée par rapport à la normale (centile, nuage de points, bandes climatiques annuelles, tendance par décennie).
- **Pratique** : recherche de ville au clavier (touche `/`), géolocalisation, lieux enregistrés avec leur température, °C/°F, URL partageable, rafraîchissement automatique toutes les 15 minutes.

## API utilisées

| Service | Point d'accès | Usage |
| --- | --- | --- |
| Prévisions | `api.open-meteo.com/v1/forecast` | conditions actuelles, horaire, quotidien sur 8 jours |
| Géocodage | `geocoding-api.open-meteo.com/v1/search` | recherche de ville |
| Qualité de l'air | `air-quality-api.open-meteo.com/v1/air-quality` | indice européen, PM2,5, PM10, ozone, NO₂ |
| Archives | `archive-api.open-meteo.com/v1/archive` | maximales quotidiennes sur 30 ans |

Les archives sont mises en cache dans le navigateur (une requête par lieu et par jour).

## Choix techniques

- JavaScript natif, CSS et SVG écrits à la main, aucun outil de build.
- Le ciel est un moteur de particules en canvas : chaque paramètre est interpolé vers sa cible, ce qui produit les transitions fluides quand on change d'heure ou de lieu.
- Phase et position de la lune calculées localement (période synodique), sans API supplémentaire.
- Si l'API est injoignable, un **mode démonstration** clairement signalé génère des données réalistes au même format.

## Accessibilité

Navigation complète au clavier (la frise est un `slider` ARIA piloté aux flèches), recherche en `combobox` ARIA, annonces vocales au changement de lieu, focus visible, respect de `prefers-reduced-motion` (ciel figé, pas d'éclairs), mise en page responsive jusqu'à 320 px.

## Lancer le projet

Ouvrez `index.html` dans un navigateur. Pour le mettre en ligne, déposez le fichier sur GitHub Pages, Netlify ou Vercel.

Avant publication, remplacez `Votre nom` dans le pied de page (lien `#author`) par votre nom et un lien vers votre portfolio.

## Crédits

Données météo, qualité de l'air et archives : [Open-Meteo.com](https://open-meteo.com/), licence [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). L'attribution est requise et figure dans le pied de page de l'application.
