# Immich-Pilot

Interface graphique pour **immich-go**, conçue pour Windows, avec un terminal intégré affichant toutes les commandes réelles exécutées.

## Concept

Immich-Pilot est un **wrapper graphique** au-dessus de `immich-go`. Il expose un terminal intégré qui exécute réellement les commandes `immich-go`, mais dans un langage compréhensible pour le grand public — pas de syntaxe technique brute, des formulations naturelles.

Quand l'utilisateur clique "Uploader mes photos de vacances", le terminal montre la commande `immich-go` équivalente, mais il a été formulée à partir d'un choix simple et clair.

Le terminal affiche en temps réel :
- API calls HTTP
- Opérations sur les médias (upload, suppression, lecture)
- Requêtes à l'API Immich
- Migrations, transformations

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

### Terminal intégré

- Affichage temps réel des commandes `immich-go` exécutées
- Formulation en langage naturel à la place de la syntaxe technique
- Copier-coller des commandes pour débogage
- Historique des commandes
- Filtres par type (API, fichiers, erreurs)
- Coloration syntaxique

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

### Gestion des instances

Immich-Pilot supporte **plusieurs instances Immich**. Au premier lancement, une fonction propose de lister et configurer les instances disponibles :

1. **Ajout d'une instance** — l'utilisateur donne un **nom** (ex: "Bureau", "Cloud") et l'**URL** de l'instance (`http://192.168.1.50:2283`)
2. **Récupération des API Keys** — l'outil contacte l'instance pour lister les utilisateurs existants, puis récupère les API Keys associées
3. **Sauvegarde** — chaque instance est stockée dans `.config/immich-pilot.yaml` avec son nom, URL et clés API
4. **Switch rapide** — l'interface permet de basculer d'une instance à l'autre depuis un sélecteur

Exemple de config résultante :

```yaml
instances:
  - name: "Bureau"
    url: "http://192.168.1.50:2283"
    api_key: "abc123..."
  - name: "Cloud"
    url: "https://immich.monsite.fr"
    api_key: "xyz789..."
```

### Objectif

Rendre l'écosystème Immich accessible aux utilisateurs Windows en leur offrant une interface claire, un terminal transparent qui montre ce qui est exécuté, et des commandes exprimées dans un langage compréhensible — pas besoin de connaître `immich-go` ou sa syntaxe.
