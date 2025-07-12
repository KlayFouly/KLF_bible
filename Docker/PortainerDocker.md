## Installer une interface web pour Docker : Portainer

Portainer est la solution la plus populaire pour gérer Docker via une interface web simple et puissante. Voici la procédure recommandée pour l’installer sur Debian (ou toute machine disposant de Docker) :


## **1. Créer un volume Docker pour Portainer**
```bash
docker volume create portainer_data 
```
>Ce volume servira à stocker les données de Portainer (configuration, utilisateurs, etc.) [1](https://www.ionos.fr/digitalguide/serveur/configuration/installer-portainer-sous-docker/) [3](https://aymeric-cucherousset.fr/installer-portainer-io-sur-docker/) [4](https://docs.portainer.io/start/install-ce/server/docker/linux).



## **2. Lancer le conteneur Portainer**
```bash
docker run -d \
	-p 9443:9443 \
	-p 9000:9000 \
	--name=portainer \
	--restart=always \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v portainer_data:/data \
	portainer/portainer-ce:latest
```
>-   Le port 9443 correspond à l’interface web sécurisée (HTTPS).
>    
>-   Le port 9000 permet d’accéder à l’interface en HTTP si besoin.
>  
>-   Le montage du socket Docker permet à Portainer de piloter vos conteneurs locaux [3](https://aymeric-cucherousset.fr/installer-portainer-io-sur-docker/) [4](https://docs.portainer.io/start/install-ce/server/docker/linux) [6](https://zatoufly.fr/installer-docker-et-portainer-sur-linux/).
    

## **3. Accéder à l’interface web**

-   Ouvrez votre navigateur et rendez-vous sur :
    
    >-   [https://votre-ip:9443](https://votre-ip:9443/)  (HTTPS, recommandé)
    >    
    >-   [http://votre-ip:9000](http://votre-ip:9000/)  (HTTP, moins sécurisé)        
  
-   Lors de la première connexion, créez un compte administrateur [1](https://www.ionos.fr/digitalguide/serveur/configuration/installer-portainer-sous-docker/) [3](https://aymeric-cucherousset.fr/installer-portainer-io-sur-docker/) [6](https://zatoufly.fr/installer-docker-et-portainer-sur-linux/).

*Written by [KlayFouly](https://github.com/KlayFouly) with [Perplexity](https://www.perplexity.ai/) using [StackEdit](https://stackedit.io/) for [La Capsule](https://lacapsule.org/).*
