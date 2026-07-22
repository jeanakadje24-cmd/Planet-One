# Planet One MVP

MVP local pour la vente de forfaits en Côte d’Ivoire.

## Démarrage

1. Installez Node.js 20 ou plus récent.
2. Copiez `.env.example` vers vos variables d’environnement, puis définissez les secrets avant le lancement :

   `KONEKT_JWT_SECRET=un-secret-long KONEKT_WEBHOOK_SECRET=un-autre-secret node server.js`

3. Ouvrez `http://localhost:8080` pour l’application client et `http://localhost:8080/admin.html` pour l’administration.

## Android

L’interface est adaptée aux petits écrans et peut être installée comme application depuis Chrome Android lorsque le projet est publié avec HTTPS. Ouvrez l’adresse du site, puis utilisez le menu Chrome `Installer l'application` ou `Ajouter à l'écran d'accueil`.

Le compte administrateur initial est créé à partir de `ADMIN_EMAIL` et `ADMIN_PASSWORD` (variables obligatoires en production). Sans ces variables, le mode démonstration utilise `admin@konekt.local` / `ChangeMe!2026`.

## Intégrations réelles à terminer

- Remplacer `createPaymentIntent()` par l’API du partenaire de paiement agréé.
- Faire pointer le partenaire vers `POST /api/webhooks/payment`. La signature HMAC est vérifiée avant toute modification de transaction.
- Remplacer `deliverTopup()` par l’API officielle/agrégateur de recharges.
- Utiliser PostgreSQL, un gestionnaire de secrets, HTTPS et un fournisseur SMS/push pour la production.

Ne jamais stocker de PIN Mobile Money, de code OTP ni de fonds clients.

## Publication publique

Le projet contient `render.yaml` pour Render. Le choix retenu est une instance `Starter` avec un disque persistant de 1 Go, car les données de demandes doivent survivre aux redémarrages. Dans Render, créez un nouveau Blueprint depuis le dépôt GitHub, renseignez `ADMIN_EMAIL` et `ADMIN_PASSWORD`, puis déployez. Render attribuera une adresse HTTPS publique `onrender.com`.
