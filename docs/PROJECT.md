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

## Configuration

Avant de fonctionner, Immich-Pilot doit localiser **immich-go**. Le processus est :

1. **Recherche locale** — l'outil scanne les chemins courants (`$GOPATH/bin`, `%LOCALAPPDATA%\Programs`, PATH) pour trouver `immich-go.exe`
2. **Mémorisation** — le chemin trouvé est sauvegardé dans un fichier de config local `.config/immich-pilot.yaml`
3. **Installation automatique** — si immich-go n'est pas trouvé, le tool le télécharge depuis son dépôt GitHub (release la plus récente pour Windows amd64) dans un dossier local `vendor/immich-go/`

Cela garantit une expérience "prête à l'emploi" sans dépendre d'une installation manuelle.

## Objectif

Rendre l'écosystème Immich accessible aux utilisateurs Windows qui n'ont pas la mainmise en ligne de commande, tout en gardant une transparence totale sur ce qui est exécuté — d'où l'idée du terminal visible comme WinCVS le faisait pour CVS.
