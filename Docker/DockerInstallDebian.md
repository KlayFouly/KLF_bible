## Procédure d’installation de Docker sur Debian (Debian 11/12)

Voici les étapes recommandées pour installer Docker Engine sur Debian, en suivant les bonnes pratiques et la documentation officielle[1](https://docs.docker.com/engine/install/debian/)[2](https://www.ionos.fr/digitalguide/serveur/configuration/installer-docker-sur-debian-12/)[4](https://oleks.ca/2025/05/27/installation-de-docker-sur-debian/)[5](https://www.it-connect.fr/installation-pas-a-pas-de-docker-sur-debian-11/)[6](https://aymeric-cucherousset.fr/installer-docker-debian-11/).


## **1. Mettre à jour le système et installer les dépendances**
```bash
sudo apt update 
sudo apt install -y apt-transport-https \
		ca-certificates \ 
		curl \
		gnupg \ 
		lsb-release
```

## **2. Ajouter la clé GPG officielle de Docker**
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## **3. Ajouter le dépôt Docker à vos sources APT**
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## **4. Mettre à jour l’index des paquets**
```bash
sudo apt update 
```

## **5. Installer Docker Engine, le CLI et containerd**
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

## **6. (Optionnel) Ajouter votre utilisateur au groupe docker**

Pour exécuter Docker sans sudo :
```bash
sudo  usermod -aG docker  $USER 
```
>Déconnectez-vous puis reconnectez-vous pour que ce changement prenne effet. 

## **7. Vérifier le bon fonctionnement de Docker**
```bash
docker run hello-world 
```
>Cette commande doit afficher un message de bienvenue confirmant que Docker fonctionne correctement.

## **Résumé des commandes**
```bash
sudo apt update 
sudo apt install -y apt-transport-https \
		ca-certificates \
		curl \
		gnupg \
		lsb-release
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable"  |  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
sudo apt update 
sudo apt install -y docker-ce docker-ce-cli containerd.io 
sudo usermod -aG docker $USER 
docker run hello-world
```
------------
*Written by [KlayFouly](https://github.com/KlayFouly) with [Perplexity](https://www.perplexity.ai/) using [StackEdit](https://stackedit.io/) for [La Capsule](https://lacapsule.org/).*
