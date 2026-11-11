# Rail Express

Simulateur de conduite ferroviaire 3D : composez votre train, choisissez un itinéraire entre de vraies gares françaises et conduisez avec signalisation BAL/TVM, KVB, VACMA et procédures de mise en service.

**▶ Démo en ligne : [https://yoannservices.github.io/rail-express/](https://yoannservices.github.io/rail-express/)**

## Fonctionnalités

- Assistant : engin moteur, composition, itinéraire (départ / arrivée)
- Ligne générée entre de vraies gares françaises
- Signalisation BAL / TVM, contrôle de vitesse KVB, VACMA, procédures de mise en service
- Pupitre de conduite, documents de bord (bulletin de composition, saisie KVB)
- Progression enregistrée (`localStorage`)

## Lancer en local

Aucune installation : ouvrez `index.html` dans un navigateur, ou servez le dossier :

```bash
python -m http.server 8000
```

puis allez sur http://localhost:8000 (dans le dossier `web/` de Mes Projets : http://localhost:8000/loisirs/rail-express/).

## Structure

- `index.html`, `style.css`
- `js/main.js` : boucle principale
- `js/setup.js` : assistant de préparation
- `js/data.js` : gares, engins, wagons
- `js/track.js` : génération de la ligne
- `js/sim.js` : simulation
- `js/cab.js` : pupitre, HUD, modales
- `js/world.js`, `js/models.js` : décor et modèles 3D
- `js/audio.js` : sons
- `ROBLOX.md` : notes sur le portage Roblox (« Voie Libre »)

## Technologies

HTML, CSS et JavaScript ; rendu 3D avec [Three.js](https://threejs.org/) r186 (chargé depuis un CDN par `assets/three-compat.js`). Sans étape de build.

---

Fait partie de [Mes Projets](https://yoannservices.github.io/) · [Portfolio](https://yoannservices.github.io/portfolio/) · par [@yoannservices](https://github.com/yoannservices)

## Fiche technique

Résumé de ce que fait le code, tenu à jour à chaque modification : le lire suffit pour vérifier une information sans relire tout le jeu.

- **Code** : `js/models.js` (matériel roulant), `js/track.js`, `js/main.js` (vues, boucle), `js/audio.js`.
- **Vrais modèles** (tous de Nikcore, CC-BY) : `fitGLB(longueur du véhicule du jeu, 0)` (longueur sur Z comme les véhicules du jeu ; l'ancien `π/2` les mettait en travers de la voie), puis `capH` : si l'étirement à la longueur du jeu les rend trop hauts, hauteur ramenée au gabarit (`REAL_H` : Corail 4,05 m, citerne 4,3 m, loco 4,3 m).
  - voitures Corail et couchettes : `passenger-wagon.glb` (20,5 m d'origine, étirée à 26,4 m) ;
  - wagons-citernes : `tank-wagon-8axle.glb` ;
  - locomotives diesel (BB 67400, BB 75000, CC 72000) : `loco-sd40.glb` (`realLoco`). Les maillages procéduraux de la loco sont masqués un par un, feux gardés (`userData.lw` / `lr`) : masquer le groupe ne marche pas, `world.js` remet sa visibilité à chaque image ;
  - le reste est procédural.
- **Vues (C ou bouton « Vue (C) »)** : `M.toggleView` bascule cabine / extérieure (glisser pour tourner, molette pour zoomer).
- **Sauvegarde** : composition du train `train:setup`.

## Crédits des modèles 3D

Véhicules réels sous licence CC-BY (Sketchfab) : auteurs et licences dans `assets/models/CREDITS.md`.
