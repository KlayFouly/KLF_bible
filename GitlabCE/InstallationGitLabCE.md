# Installation de GitLab CE (Community Edition)

## **1. Prérequis**

-   Un serveur sous **Debian** ou **Ubuntu** (physique, virtuel ou VPS)
    
-   Accès **root** ou **sudo**
    
-   Ports ouverts : **80** (HTTP), **443** (HTTPS), **22** (SSH)
    
-   Paquets de base : `curl`, `openssh-server`, `ca-certificates`, `perl`
    

----------

## **2. Mise à jour du système et installation des dépendances**
```bash
sudo apt update -y 
sudo apt install -y curl \
					openssh-server \
					ca-certificates \
					perl
```

## **3. Ajout du dépôt GitLab CE**
```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

## **4. Installation de GitLab CE**

Remplace l’URL par celle que tu veux utiliser (IP locale, nom DNS, etc.) :
```bash
sudo EXTERNAL_URL="http://gitlab.mondomaine.local" apt-get install gitlab-ce
```
## **5. Configuration de GitLab**

-   Modifie le fichier de configuration si besoin :
```bash
sudo nano /etc/gitlab/gitlab.rb
```
-   Change la ligne `external_url` selon ton besoin.
    
-   Applique la configuration :
```bash
sudo gitlab-ctl reconfigure
```

----------

## **6. Premier accès**

-   Accède à l’URL choisie depuis un navigateur.
    
-   Au premier accès, définis le mot de passe du compte administrateur.
    
-   Connecte-toi avec l’utilisateur `root` et le mot de passe choisi.
    

----------

## **Résumé des commandes**
```bash
sudo apt update -y 
sudo apt install -y curl \
					openssh-server \
					ca-certificates \
					perl
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash 
sudo EXTERNAL_URL="http://gitlab.mondomaine.local" apt-get install gitlab-ce 
sudo nano /etc/gitlab/gitlab.rb # (optionnel, pour modifier l’URL) 
sudo gitlab-ctl reconfigure
```

> **Astuce** : Pour une installation locale, utilise une URL du type `http://192.168.x.x` ou `http://gitlab.local`. Pour la production, privilégie **HTTPS** et un **nom de domaine** valide.

----------

**GitLab CE** est maintenant prêt à être utilisé pour héberger tes projets !


------------
*Written by [KlayFouly](https://github.com/KlayFouly) with [Perplexity](https://www.perplexity.ai/) using [StackEdit](https://stackedit.io/) for [La Capsule](https://lacapsule.org/).*
