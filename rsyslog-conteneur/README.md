# Conteneur docker rsyslog de base

## Créer le répertoire de travail

```bash
mkdir rsyslog-conteneur
cd rsyslog-conteneur
```

## Créer une image docker générique avec les répertoires utiles

Reprendre le fichier [Dockerfile](Dockerfile)

- `/etc/rsyslog.d/` - Contient tous les fichiers de configuration. Les fichiers doivent avoir l'extension `*.conf` pour être pris en compte.
- `/srv/rsyslog/` - Répertoire de travail du processus rsyslogd.
- `/logs/` - Répertoire de stockage des logs

`rsyslog` tournera sous un utilisateur non privilégié (UID/GID 1000).

## Créer la configuration rsyslog de base

Le fichier [rsyslog.conf](rsyslog.conf) sera commun à tous les conteneurs.
Les spécificités seront ajoutées dans le répertoire `/etc/rsyslog.d/`.

Le fichier [10-local-file-logging.conf](10-local-file-logging.conf)` permet de définir la gestion des fichiers de logs locaux au conteneur.

## Créer une image docker qui servira de base

```bash
sudo su -
docker build -t rsyslog-conteneur .
# Verify
docker images
```

L'image ne sera pas lancée en tant que conteneur, mais sert de modèle aux différents conteneurs.