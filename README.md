
---

# Docker Phase 2 Project

Ce projet utilise Docker Compose pour orchestrer plusieurs conteneurs Docker, facilitant la gestion des services et le déploiement local. Le fichier `compose.yaml` gère la configuration des conteneurs et les connexions réseau entre eux.

## Prérequis

Avant de commencer, assurez-vous d’avoir installé :

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

## Structure du Projet

Le projet est organisé de la manière suivante :

```plaintext
.
├── compose.yaml            # Fichier de configuration Docker Compose
├── Dockerfile              # Dockerfile pour construire une image de base (si applicable)
├── README.md               # Documentation du projet
└── autres fichiers...      # Autres fichiers de configuration, scripts, etc.
```

## Configuration du Projet

### `compose.yaml`

Le fichier `compose.yaml` définit la configuration des services Docker. Voici un aperçu des principaux éléments :

- **Services** : Ce projet semble définir plusieurs services (comme `alpine`, `ubuntu`, etc.), chacun configuré avec une image spécifique et des options de démarrage.
- **Networks** : Un réseau personnalisé (`mon_reseau` dans l’exemple) est configuré pour permettre aux conteneurs de communiquer entre eux.
- **Volumes** : Permet de persister certaines données dans des volumes Docker, accessibles par les conteneurs.

### Exemple de Configuration dans `compose.yaml`

Le fichier `compose.yaml` pourrait ressembler à ceci :

```yaml
version: '3'
services:
  alpine:
    image: alpine
    container_name: test_alpine
    command: ["sh", "-c", "while true; do echo 'Alpine running'; sleep 3600; done"]
    networks:
      - mon_reseau

  ubuntu:
    image: ubuntu
    container_name: romuald_test
    command: ["bash", "-c", "while true; do echo 'Ubuntu running'; sleep 3600; done"]
    networks:
      - mon_reseau

networks:
  mon_reseau:
    driver: bridge
```

## Lancer le Projet

Pour démarrer les services définis dans `compose.yaml`, utilisez la commande suivante dans le répertoire racine du projet (là où se trouve `compose.yaml`) :

```bash
docker-compose up -d
```

L’option `-d` exécute les conteneurs en arrière-plan.

### Vérifier les Conteneurs en Cours d’Exécution

Pour lister les conteneurs qui tournent, utilisez :

```bash
docker ps
```

### Consulter les Logs d’un Conteneur

Pour afficher les logs d’un conteneur (par exemple, `romuald_test`), exécutez :

```bash
docker logs romuald_test
```

## Arrêter les Services

Pour arrêter les conteneurs en cours d'exécution, utilisez :

```bash
docker-compose down
```

Cette commande arrête et supprime également les conteneurs, réseaux et volumes créés par `docker-compose up`.

## Dépannage

### Erreurs Courantes

1. **Port déjà utilisé** : Si un service utilise un port déjà occupé, modifiez le mappage du port dans `compose.yaml`.
2. **Problème de réseau** : Assurez-vous que les conteneurs sont bien connectés au réseau défini dans `compose.yaml`.

## Ressources Supplémentaires

- [Documentation Docker Compose](https://docs.docker.com/compose/)
- [Documentation Docker](https://docs.docker.com/)

---

