# Semaille — tableau de bord

Une graineterie imaginaire du Val de Loire, vue depuis l’établi d’Alma un
matin de novembre 2026. L’écran rassemble le registre des lots, la levée de
la saison, les gestes de la semaine, l’agenda et le journal de culture dans
une interface produit dense, calme et vivante.

La direction suit la langue réelle des applications de gestion : rail vert
forêt, canvas sauge clair, cartes blanches, accents lime et orange, Manrope
pour l’interface, un seul mot en Fraunces italique dans le salut. Deux thèmes,
clair et sombre, construits sur les mêmes composants et échangés par une vague
de briques. Le mouvement fait partie de la matière : entrées échelonnées,
pastille de navigation qui glisse, survols qui soulèvent, tracés qui se
dessinent, caméra du clos qui respire. Aucune pastille-badge : filtres, états,
compteurs et repères sont en texte nu, en petites capitales ou soulignés d’un
filet lime.

Démo autonome : un seul fichier HTML, deux fontes locales, Three.js vendorisé,
aucune requête réseau après chargement.

## Ouvrir

Depuis ce dossier :

```bash
python3 -m http.server 5178 --bind 127.0.0.1
```

puis ouvrir <http://127.0.0.1:5178/>. Un serveur local est préférable pour que
les fontes se chargent proprement. `index.html` peut aussi être ouvert
directement dans Chrome, mais certains navigateurs bloquent les fontes en
`file://`.

## Contenu du dossier

- `index.html` — l’écran complet : structure, styles, données, interactions,
  système de mouvement, scène 3D et transition de thème en briques.
- `fonts/` — Manrope variable et Fraunces italique variable, avec leurs
  licences SIL Open Font License.
- `vendor/` — Three.js r184 (module et cœur minifiés) sous licence MIT.
- `captures/` — trente captures de référence : desktop clair et sombre
  (pli et page entière), courbe survolée, clos 3D clair et sombre, infobulle
  du clos, carte du clos mobile, journal, notifications, drawer, dialogue,
  aide, tablette, mobile clair et sombre, journal, calendrier, drawer,
  dialogue et infobulle mobiles, réduction de mouvement, focus, rendu sans
  JavaScript et quatre temps de la transition en briques.

## Structure de l’écran

- **Rail fixe** à gauche (desktop) : marque, tableau de bord, registre,
  calendrier, journal, aide, avatar. Sur mobile, il devient une barre de
  navigation basse.
- **En-tête** : date du jour, semaine, titre, thème, notifications et avatar.
- **Salut** : bandeau forêt en verre liquide — coins squircle, hairline claire,
  texture de bruit, double ombre diffuse — avec le relevé du matin, la phrase
  de saison et le bouton « Nouveau geste ».
- **Indicateurs** : taux de levée avec sparkline, lots en veille, prochaine
  gelée.
- **Levée de la saison** : courbe SVG S40–S45 avec ses hauts et ses bas,
  comparaison 2025, ruban d’amplitude des lots, seuil à 80 %, pastilles pleines
  sur les deux séries (aucun liseré creux), semaine courante à halo plein pulsé,
  légendes désactivables.
- **Le clos en relief** : carte isométrique de dix parcelles témoins, hauteur
  et couleur selon la levée, drapeaux sous le seuil, infobulle de survol,
  glisser pour tourner, oscillation douce, pause et recentrage, parcours au
  clavier.
- **Répartition des lots** : anneau épais de 42 lots, trois classes de levée,
  arcs animés, légende liée au survol, rappel des trois alertes.
- **À l’établi / Mouvements récents** : checklist de la semaine et trois
  derniers mouvements, cliquables vers leur lot.
- **Registre des lots** : dix lots, filtres Tous / Sous 80 % / À semer,
  recherche, onglets Lots et Journal, ouverture d’une fiche latérale.
- **Colonne latérale** : calendrier de novembre 2026, échéances, relevé du
  matin. Elle devient collante sur grand écran et repasse dans le flux en
  dessous de 1121 px.
- **Mobile** : actions rapides, carte de campagne lime « Préparation au
  froid », navigation basse, dialogues en feuille inférieure.

## Ce que l’écran sait faire

- **Registre** : filtres, recherche, compteurs, tri visuel par état. Chaque
  ligne ouvre une fiche avec origine, récolte, stock, note, historique des
  six derniers contrôles et actions « Noter un semis » / « Ajouter une note ».
- **Semis** : semer un lot met à jour sa ligne, le journal, le calendrier, la
  liste des mouvements et une notification, sans recharger la page.
- **Journal** : six entrées de saison, plus les gestes et semis ajoutés. Le
  titre et le sous-titre du registre suivent l’onglet actif.
- **Agenda** : novembre 2026, sélection d’un jour au clic ou au clavier,
  détail des événements, marques de semis, bouton « Aujourd’hui ». Les
  échéances de la colonne latérale sélectionnent leur date.
- **Établi** : quatre gestes de la semaine, progression partagée entre les
  cartes desktop et mobile, état conservé au rechargement.
- **Courbe** : SVG construit à partir des données, tracé au défilement,
  ruban d’amplitude entre le minimum et le maximum des lots, halo sur la
  semaine courante, survol, tactile et clavier, infobulle bornée à l’écran
  avec écart 2025 et amplitude, séries masquables sans jamais tout masquer.
- **Clos 3D** : scène Three.js orthographique, dix parcelles extrudées et
  arrondies, ombres douces, matériaux éclairés par le thème. La caméra oscille
  lentement autour de l’axe idéal ; le glisser tourne librement, le clic ouvre
  la fiche du lot, les flèches de survol suivent les blocs à l’écran. Pause,
  reprise et recentrage sont au clavier et à la souris. Le clavier parcourt
  les dix parcelles (flèches, `Home`, `End`) et `Entrée` ouvre leur fiche ;
  le résumé de survol est annoncé par une zone vivante. Un tap sur mobile
  ouvre directement la fiche. Sans WebGL, un repli SVG statique conserve
  l’information.
- **Mouvement** : entrées échelonnées au chargement, glissement de la pastille
  de navigation, lumière qui suit le pointeur sur le salut et l’indicateur
  principal, carte héros en verre liquide qui s’élève et approfondit son ombre
  au survol, compteurs qui montent, cases qui se dessinent, barres et anneaux
  qui se remplissent, marqueurs de courbe pleins, transition de thème en
  briques. Rien ne dépend du défilement : le contenu hors écran reste lisible
  dans les captures et l’impression.
- **Carnet** : ajout d’une entrée (semis, note, récolte, alerte), compteur de
  caractères, persistance, inscription au calendrier du jour et notification.
- **Notifications** : panneau natif `<details>`, fermeture au clic extérieur
  ou par Échap, chaque ligne mène à sa section.
- **Thèmes** : clair et sombre, mémorisés et appliqués avant le premier
  rendu ; la couleur de la barre du navigateur suit le thème. Le changement
  déploie une mosaïque de briques : une vague part du bouton, les briques
  tombent en cadence depuis le coin, recouvrent tout l’écran, puis le thème
  bascule à l’abri de la couverture et la mosaïque se retire de l’extérieur
  vers le centre. `prefers-reduced-motion` escamote la scène et bascule
  instantanément ; l’API `setTheme` reste immédiate pour l’audit.
- **Dialogues natifs** : fiche de lot, nouveau geste et note d’atelier,
  fermeture par Échap ou clic sur le fond, focus contenu puis rendu au bouton
  d’origine.

## Raccourcis clavier

| Touche | Action |
| --- | --- |
| `T` | Basculer clair / sombre |
| `N` | Nouveau geste au carnet |
| `/` | Aller à la recherche des lots |
| `?` | Ouvrir la note d’atelier |
| `Échap` | Fermer fiche, dialogue, notifications ou note |
| `←` `→` | Changer d’onglet, parcourir les jours, la courbe ou les parcelles du clos |
| `↑` `↓` | Parcourir les semaines du calendrier ou les parcelles du clos |
| `Home` / `End` | Premier / dernier jour, première / dernière semaine, première / dernière parcelle |
| `Entrée` | Ouvrir la fiche du lot sélectionné dans le clos |

Les raccourcis sont ignorés lorsqu’un champ de saisie ou un dialogue a le
focus, sauf `Échap`.

## Données et persistance

Les lots, événements, températures et relevés sont fictifs et embarqués dans le
document. La date de référence est fixée au **8 novembre 2026, semaine 45**,
pour que l’écran reste reproductible.

Tout ce qui est saisi reste dans le navigateur :

| Clé `localStorage` | Contenu |
| --- | --- |
| `semaille.theme` | Thème actif (`clair`, `sombre`) |
| `semaille.tasks.v1` | Gestes cochés |
| `semaille.sown.v1` | Lots semés |
| `semaille.entries.v1` | Entrées ajoutées au carnet |

Les anciennes valeurs de thème (`aube`, `seve`, `sousbois`) sont migrées vers
`clair` ou `sombre` au chargement. Réinitialiser la démonstration :
`localStorage.clear()` puis recharger. Aucun compte, aucun serveur, aucune
donnée envoyée.

## Accessibilité et robustesse

- `lang="fr"`, lien d’évitement, un seul `main`, un seul `h1`, hiérarchie de
  titres cohérente, aucun identifiant dupliqué.
- Onglets avec rôles ARIA et navigation aux flèches ; filtres, thème, légendes
  et jours exprimés par `aria-pressed` ; cases par `role="checkbox"`.
- Dialogues natifs `<dialog>` avec `showModal()`, piège de focus natif et
  restitution du focus à la fermeture.
- Zones vivantes pour le détail du calendrier, la courbe, le survol du clos
  et les notifications. La carte du clos est focusable, se parcourt aux
  flèches et annonce chaque parcelle ; `Entrée` ouvre la fiche.
- Contrastes vérifiés selon WCAG AA sur **282 échantillons** (desktop et
  mobile, clair et sombre, y compris infobulles, drapeaux et anneau) ; aucun
  échantillon sous le seuil. Le dégradé du héros est contrôlé au pixel sous
  chaque texte, minimum **4,9:1**.
- `prefers-reduced-motion` : tracés et révélations affichés immédiatement,
  animations neutralisées, carte du clos immobile, anneau déjà peint,
  transition de thème sans briques.
- Sans JavaScript : les dix lots, les chiffres de la courbe, l’agenda, le
  repli SVG du clos et l’anneau statique restent lisibles ; les commandes
  sans effet sont masquées.
- Aucun débordement horizontal de 390 px à 1440 px.

## Vérification

Audit automatisé avec Chrome headless et Playwright :

- **99/99** tests fonctionnels ;
- **61/61** tests d’états, de mouvement, de 3D, de sémantique et de mobile ;
- **17/17** tests de la transition en briques : montée, couverture opaque,
  bascule sous couverture, retrait, raccourci, API, réduction de mouvement
  et mobile ;
- **282** échantillons de contraste, **0** sous le seuil WCAG AA, plus le
  contrôle au pixel du dégradé du héros ;
- aucun message d’erreur console ou de page, aucune image sans alternative ;
- aucun débordement horizontal sur six largeurs : 390, 480, 768, 1024, 1280
  et 1440 px.

Les trente captures de `captures/` servent de référence visuelle, dont quatre
temps de la transition en briques (`transition-briques-*.png`).

Une petite API de contrôle existe pour l’audit :

```js
window.__semaille.ready();      // true quand l’écran est prêt
window.__semaille.theme();      // thème actif
window.__semaille.setTheme("sombre");
window.__semaille.openLot("SML-012");
window.__semaille.selectTab("journal");
window.__semaille.calendar();   // date sélectionnée
window.__semaille.chartIndex(); // index de semaine survolé
window.__semaille.tasks();      // gestes cochés
window.__semaille.entries();    // nombre d’entrées du carnet
window.__semaille.reduced;      // réduction de mouvement active
window.__semaille.clos();       // { ready, plots, paused, angle } de la carte 3D
window.__semaille.closReset();  // recentre la caméra du clos
window.__semaille.closToggle(); // met en pause ou reprend l’oscillation
window.__semaille.bricks();     // { active, phase } de la transition de thème
```

## Limites assumées

Maquette produit, pas un service de production : données feintes, date figée,
persistance locale uniquement, pas de synchronisation ni de compte. La carte
du clos demande WebGL ; ailleurs, le repli SVG garde les dix relevés et les
commandes utiles. La transition en briques demande un canvas 2D ; en réduction
de mouvement, le thème bascule simplement. Cible testée : Chrome récent sur
desktop, tablette et mobile. Les fontes sont distribuées sous SIL Open Font License et Three.js
sous licence MIT ; les textes, tracés et illustrations sont produits pour
cette démonstration.
