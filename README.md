# TP journalisation

## Installer Docker

```bash
sudo apt install docker wget
```

## Conteneur docker rsyslog pour jouer le rôle du serveur central

## Créer la configuration rsyslog de réception des messages

Ecouter sur le port 514
```bash
# Provides UDP syslog reception
$ModLoad imudp
$UDPServerRun 514

# Provides TCP syslog reception
$ModLoad imtcp
$InputTCPServerRun 514
```

Editer le fichier rsyslog.conf 
Créer les images docker pour simuler les VMs de relai et d’entrepôt
Compiler les image docker
Vérifier la création de l’image
docker images
