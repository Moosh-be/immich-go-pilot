# Immich-Pilot

Interface graphique pour **immich-go** sur Windows — avec terminal visible des commandes réelles.

## Concept

Comme **WinCVS** montrait toutes les commandes CVS exécutées en arrière-plan, Immich-Pilot affiche en temps réel chaque commande `immich-go` qui est exécutée.

## Structure

```
immich-go-pilot/
├── immich-pilot/      # Interface graphique Windows
│   ├── cmd/           # Points d'entrée
│   ├── internal/      # Logique interne
│   └── pkg/           # Bibliothèques partagées
└── docs/              # Documentation
    └── PROJECT.md
```

## Roadmap

- [x] Structure du projet
- [ ] Couche immich-go (API wrapper)
- [ ] Terminal intégré (style WinCVS)
- [ ] Interface principale
- [ ] Upload de médias
- [ ] Gestion des albums
