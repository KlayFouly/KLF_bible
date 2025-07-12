## Installation de Prometheus et Grafana sur Debian 12

Voici la procédure détaillée pour installer Prometheus et Grafana sur Debian 12, en utilisant les dépôts officiels et les bonnes pratiques.

----------

## **1. Installation de Prometheus**

**a. Installer Prometheus et Node Exporter**
```bash
sudo apt update 
sudo apt install prometheus prometheus-node-exporter
```

>Cela installe le serveur Prometheus et l’exporter qui collecte les métriques système[7](https://reintech.io/blog/installing-configuring-prometheus-monitoring-debian-12)[8](https://www.howtoforge.com/how-to-install-prometheus-and-node-exporter-on-debian-12/)[6](https://docs.nehemiebarkia.fr/books/installations/page/installer-un-serveur-prometheus-et-grafana).

**b. Configurer Prometheus**

-   Le fichier de configuration principal est :  `/etc/prometheus/prometheus.yml`
    
-   Exemple de configuration pour monitorer la machine locale :
    
```text
global: 
	scrape_interval: 15s 
	scrape_configs:
		- job_name: 'node' static_configs:
		- targets: ['localhost:9100'] 
``` 
-   Modifiez si besoin, puis redémarrez Prometheus :
```bash
sudo systemctl restart prometheus
```

**c. Vérifier le service**
```bash
sudo systemctl status prometheus
```
>L’interface web Prometheus est accessible sur :  
>`http://<IP_serveur>:9090`
    

## **2. Installation de Grafana**

**a. Ajouter le dépôt officiel Grafana**
```bash
sudo apt-get install -y apt-transport-https \
						software-properties-common \
						wget \
						gnupg 
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -echo "deb https://packages.grafana.com/oss/deb stable main" | sudo  tee /etc/apt/sources.list.d/grafana.list 
sudo apt update
```

**b. Installer Grafana**
```bash
sudo apt install grafana
```

**c. Démarrer et activer Grafana**
```bash
sudo systemctl start grafana-server 
sudo systemctl enable grafana-server
```
>L’interface web Grafana est accessible sur :  `http://<IP_serveur>:3000`
>  
>Identifiants par défaut :  **admin / admin**  (à changer lors de la première connexion)[6](https://docs.nehemiebarkia.fr/books/installations/page/installer-un-serveur-prometheus-et-grafana) [3](https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/).


## **3. Connecter Prometheus à Grafana**

1.  Connectez-vous à Grafana via le navigateur.
    
2.  Allez dans  **Configuration > Data Sources**.
    
3.  Cliquez sur  **Add data source**  et choisissez  **Prometheus**.
    
4.  Renseignez l’URL :  `http://localhost:9090`  (ou l’IP/port de Prometheus si différent).
    
5.  Cliquez sur  **Save & Test**  pour valider la connexion.
    

----------

## **4. Importer un dashboard**

-   Dans Grafana, cliquez sur le « **+** » >  **Import**  et saisissez l’ID d’un dashboard public (*par exemple, 1860 pour un dashboard système Linux*) ou importez un fichier ***JSON***.
    
-   Sélectionnez **Prometheus** comme source de données.


## **Résumé des commandes principales**
```bash
# Installer Prometheus et Node Exporter 
sudo apt update 
sudo apt install prometheus \
			prometheus-node-exporter   
# Ajouter le dépôt Grafana et installer Grafana 
sudo apt-get install -y apt-transport-https \
						software-properties-common \
						wget \
						gnupg
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add - echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list 
sudo apt update 
sudo apt install grafana   
# Démarrer et activer les services 
sudo systemctl start prometheus 
sudo systemctl enable prometheus 
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```
**Vous avez maintenant une stack de supervision complète, prête à collecter et visualiser les métriques de votre homelab ou de vos serveurs !**

------------
*Written by [KlayFouly](https://github.com/KlayFouly) with [Perplexity](https://www.perplexity.ai/) using [StackEdit](https://stackedit.io/) for [La Capsule](https://lacapsule.org/).*
