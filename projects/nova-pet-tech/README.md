# NOVA – Site e-commerce (traceurs GPS & santé pour chiens et chats)

Site vitrine / boutique en une seule page, construit à partir de la maquette NOVA
(« Aventurez sans limites. ») et modernisé : tracker en 3D interactif, animations au
défilement, panier, guide d'utilisation, FAQ.

## Ouvrir le site

Ouvrez simplement `index.html` dans un navigateur, ou servez le dossier :

```bash
python3 -m http.server 8080
# puis http://localhost:8080
```

Aucune étape de build : Tailwind, GSAP et Three.js sont chargés depuis des CDN.

## Ce que contient la page

| Section | Contenu |
| --- | --- |
| Hero | Titre de la maquette, CTA, preuves (livraison, 30 jours, 10 000 animaux), **tracker 3D** (glisser pour tourner) avec 4 couleurs : Noir, Crème, Olive, Terracotta |
| Fonctionnalités | Les 7 points de la maquette (GPS, zones, alertes, activité, partage, 7 jours, IP67) |
| Produit + Application | Visuel produit annoté (27 g, 7 jours, IP67, discret), maquette téléphone animée (trajet GPS, zone de sécurité), badges App Store / Google Play |
| Santé & bien-être | Anneau d'objectif animé, barres d'activité, distance / temps actif / sommeil |
| Bénéfices | Exploration, prévention des fugues, suivi santé |
| Guide | 3 étapes (fixer, scanner, partir), guide de compatibilité chien/chat, conseils d'utilisation |
| Offre | Tracker 59,90 € (choix de couleur, ajout au panier), abonnements Basic 5,99 € / Premium 8,99 € avec bascule mensuel / annuel (-20 %), accessoire collier |
| Avis | Citation, 4,8/5, chiffres clés animés, 3 témoignages |
| FAQ | 6 questions (abonnement, chats, autonomie, étranger, essai 30 jours, données) |
| Panier | Tiroir latéral, quantités, barre « livraison offerte dès 59 € », total, sauvegarde locale |

## À personnaliser

- **Photos** : la maquette utilise des photos (chien en montagne, randonneuse). Elles ne sont pas
  incluses ; remplacez les fonds dégradés des cartes « Plus qu'un GPS » et du hero par vos visuels
  (`background-image` sur les blocs concernés).
- **Prix, specs, chiffres** : tout est dans le HTML (recherchez `59,90`, `5,99`, `8,99`, `27 g`, `IP67`).
- **Témoignages** : les trois avis sont des exemples rédigés pour la maquette, à remplacer par de vrais avis.
- **Paiement** : le bouton « Passer la commande » ouvre une fenêtre de démonstration. Branchez
  Stripe Checkout, Shopify Buy Button, PayPal, etc. dans la fonction liée à `#checkout`.
- **Liens app stores** : remplacez les `href="#"` des badges par vos vraies URLs.

## Mettre en ligne

Le site est 100 % statique : un seul fichier `index.html`.

- **Firebase Hosting (Google)** : `npm i -g firebase-tools`, `firebase init hosting`, dossier public =
  ce dossier, puis `firebase deploy`.
- **Google Cloud Storage** : créez un bucket, activez l'hébergement statique, envoyez `index.html`.
- **Netlify / Vercel / GitHub Pages** : glissez-déposez le dossier ou pointez sur `projects/nova-pet-tech`.
- **Google Sites** n'accepte pas de JavaScript personnalisé : hébergez le fichier ailleurs puis
  intégrez-le dans Google Sites via « Intégrer » > URL.

## Technique

- Tailwind CSS (CDN) + styles personnalisés, polices Manrope / Inter / Caveat (Google Fonts)
- GSAP 3 + ScrollTrigger + MotionPath pour les animations (respect de `prefers-reduced-motion`)
- Three.js 0.170 (import map) : tracker modélisé en code (boîte arrondie, plaque, LED, texture « NOVA »,
  sangle nylon), OrbitControls, environnement PBR, ombres ; repli automatique sur une illustration CSS
  si WebGL n'est pas disponible
- Panier en `localStorage`, accessible au clavier (focus visible, aria-labels, Échap pour fermer)
