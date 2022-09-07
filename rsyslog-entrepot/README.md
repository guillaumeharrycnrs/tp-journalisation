# Conteneur docker rsyslog pour jouer le rôle du serveur Entrepôt

## Créer le répertoire de travail

```bash
mkdir rsyslog-entrepot
cd rsyslog-entrepot
```

## Créer une image docker basée sur la générique

Reprendre le fichier [Dockerfile](Dockerfile)

Le fichier `rsyslog.conf` est compris dans l'image générique générée à l'étape précédente

## Créer la configuration rsyslog de réception des messages

Ecouter sur le port 2514 dans les fichiers [12-listen-local-udp.conf](12-listen-local-udp.conf)

```bash
input(
  type="imudp"
  Port="2514"
)
```

et

[13-listen-local-tcp.conf](13-listen-local-tcp.conf)

```bash
input(
  type="imudp"
  Port="2514"
)
```

Inclure les directives d'arborescence de stockage dans le fichier [90-local-all-log.conf](90-local-all-log.conf)

Pour aller plus loin, jouer avec les directives

```bash
if $hostname == 'anf-securinfo-2022-student-xx' and $programname == 'audispd' then /logs/anf-securinfo-2022-student-xx/inject/anf-securinfo-2022-student-xx-auditd.log
if $hostname == 'anf-securinfo-2022-student-xx' and $programname == 'audispd' then stop
:hostname,isequal,"anf-securinfo-2022-student-xx" /logs/anf-securinfo-2022-student-xx/inject/anf-securinfo-2022-student-xx.log
:hostname,isequal,"anf-securinfo-2022-student-xx" stop
```

## Compiler l'image docker

```bash
sudo su -
cd /home/ubuntu/rsyslog-entrepot
docker build -t rsyslog/entrepot .
# Verify
docker images
```

## Lancer le conteneur Entrepôt en écoute sur le port 2514

```bash
sudo su -
docker run -it -d -v /home/centos/logs:/logs -p2514:2514 rsyslog/entrepot
# Verify
docker ps
```