## Procédure d’installation de Jenkins sur Debian (Debian 12/11)

Voici les étapes détaillées et recommandées pour installer Jenkins sur Debian :

----------

## **1. Installer Java (prérequis)**

Jenkins nécessite Java. Installez-le avec :
```bash
sudo apt update 
sudo apt install -y openjdk-11-jdk
```
Vérifiez l’installation :
```bash
java -version
```
>(Jenkins supporte aussi Java 17 ou 21 selon vos besoins [5](https://reintech.io/blog/installing-configuring-jenkins-debian-12).)

## **2. Ajouter la clé GPG officielle de Jenkins**
```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |  sudo apt-key add -
```
ou, pour Debian 12 :
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key |  sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
```

## **3. Ajouter le dépôt Jenkins à vos sources**
```bash
echo "deb https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
```
>ou, pour Debian 12 (avec clé dans /usr/share/keyrings) :
```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo  tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## **4. Mettre à jour les paquets**
```bash
sudo apt update 
```

## **5. Installer Jenkins**
```bash
sudo apt install -y jenkins
```

## **6. Démarrer et activer Jenkins au démarrage**
```bash
sudo systemctl start jenkins 
sudo systemctl enable jenkins
```
Vérifiez que Jenkins fonctionne :
```bash
sudo systemctl status jenkins
```

## **7. Accéder à l’interface web Jenkins**

-   Ouvrez votre navigateur sur :  
    `http://<votre_ip>:8080`
    
-   Récupérez le mot de passe initial :
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
-   Suivez l’assistant de configuration (installation des plugins, création de l’utilisateur admin) [5](https://reintech.io/blog/installing-configuring-jenkins-debian-12) [7](https://vegastack.com/tutorials/how-to-install-jenkins-on-debian-12/).

## **Résumé des commandes principales**
```bash
sudo apt update 
sudo apt install -y openjdk-11-jdk 
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |  sudo apt-key add - 
echo "deb https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list 
sudo apt update 
sudo apt install -y jenkins 
sudo systemctl start jenkins 
sudo systemctl enable jenkins 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
----------

**Votre Jenkins est maintenant prêt à être configuré via l’interface web !**  
>Pensez à sécuriser votre instance (reverse proxy, SSL, firewall) pour une utilisation en production [5](https://reintech.io/blog/installing-configuring-jenkins-debian-12).


------------
*Written by [KlayFouly](https://github.com/KlayFouly) with [Perplexity](https://www.perplexity.ai/) using [StackEdit](https://stackedit.io/) for [La Capsule](https://lacapsule.org/).*
