# Immich-Pilot

Interface graphique pour **immich-go**, conçue pour Windows, avec un terminal intégré affichant toutes les commandes réelles exécutées.

## Concept

Comme **WinCVS** affichait en temps réel les commandes CVS exécutées en arrière-plan, Immich-Pilot affiche toutes les commandes `immich-go` exécutées :

- API calls HTTP
- Opérations sur les médias (upload, suppression, lecture)
- Requêtes à l'API Immich
- Migrations, transformations

## Structure

```
immich-go-pilot/
├── immich-pilot/      # Interface graphique Windows
│   ├── cmd/           # Points d'entrée
│   ├── internal/      # Logique interne
│   └── pkg/           # Bibliothèques partagées
└── docs/              # Documentation
    └── PROJECT.md     # Ce fichier
```

## Fonctionnalités prévues

### Terminal intégré (style WinCVS)
- Affichage temps réel de chaque commande exécutée
- Copier-coller des commandes pour débogage
- Historique des commandes
- Filtres par type (API, fichiers, erreurs)
- Coloration syntaxique des commandes

### Interface principale
- Navigation dans la bibliothèque Immich
- Upload de médias avec suivi de progression
- Gestion des albums
- Gestion des utilisateurs et permissions
- Recherche et filtrage

### Couche immich-go
- Wrapper Go pour l'API Immich
- Authentification et gestion des tokens
- Gestion des erreurs reproductible
- Logging détaillé

## Objectif

Rendre l'écosystème Immich accessible aux utilisateurs Windows qui n'ont pas la mainmise en ligne de commande, tout en gardant une transparence totale sur ce qui est exécuté — d'où l'idée du terminal visible comme WinCVS le faisait pour CVS.
