# PROJET FINAL DEVOPS. 
 ### Stagiaire

Prénom : Junior

Nom : Mbogning

17ème Bootcamp DevOps  d'Eazytraining

LinkedIn : https://www.linkedin.com/in/juniormbogning/

Site Internet : https://mbogning.com/


## **1) Introduction**

La société **IC GROUP** dans laquelle vous travaillez en tant qu’ingénieur Devops souhaite mettre sur pied un site web vitrine devant permettre d’accéder à ses 02 applications phares qui sont :  

1) Odoo et 
1) pgAdmin 

**Odoo**, un ERP multi usage qui permet de gérer les ventes, les achats, la comptabilité, l’inventaire, le personnel …  

Odoo est distribué en version communautaire et Enterprise. ICGROUP souhaite avoir la main sur le code et apporter ses propres modifications et customisations ainsi elle a opté pour l’édition communautaire.  Plusieurs versions de Odoo sont disponibles et celle retenue est la 13.0 car elle intègre un système de LMS (Learning Management System) qui sera utilisé pour publier les formations en internes et ainsi diffuser plus facilement l’information.  

### **2) Conteneurisation de l’application web.** 

## **a. Commencez par créer un fichier nommé Dockerfile sans extension.**

```bash
   # Utilisation de l'image de base Python 3.11 Alpine pour sa légèreté
   FROM python:3.11-alpine
   
   # Définition du répertoire de travail dans le conteneur
   WORKDIR /opt
   
   # Installation de Flask
   RUN pip install flask
   
   # Exposition du port 8080, utilisé par défaut par l'application
   EXPOSE 8080
   
   # Création de variables d'environnement pour configuration externe
   ENV ODOO_URL=https://www.odoo.com
   ENV PGADMIN_URL=https://www.pgadmin.org
   
   # Définition du point d'entrée, lance l'application
   ENTRYPOINT ["python", "app.py"]
```
Ce Dockerfile définit une image de base légère (Alpine), installe les dépendances nécessaires, expose le port de l'application, définit des variables d'environnement pour une configuration flexible et configure le conteneur pour lancer votre application au démarrage.

## **b. Création d'une image Docker nommée `ic-webapp` avec le tag 1.0.**
Exécutez la commande suivante dans le terminal, à l'emplacement du Dockerfile, pour construire l'image Docker de l'application :
```bash
   # Utilisation de l'image de base Python 3.11 Alpine pour sa légèreté
   docker build -f Dockerfile -t mbogning/ic-group:v1.0 .
```
![](images/build-image.png)

## **c. Lancement d'un container test**
Après avoir construit l'image, lancez un conteneur de test en utilisant :
```bash
   # Utilisation de l'image de base Python 3.11 Alpine pour sa légèreté
   docker run -d --name test-ic-webapp -p 7000:8080 mbogning/ic-webapp:v1.0
```
![](images/run-container.png)

## **d. Vérification de l'adresse IP de l'hote**
```bash
    ip -a
```
![](images/verify-ip-adress.png)

## **e. Page d'accueil IC-WEBAPP**

![](images/ic-webapp-homepage.png)

## **3) Déploiement des applications dans un cluster Kubernetes.** 
## **a. Module ic-webapp.**
## **i. Mise en place du Namespace.**

