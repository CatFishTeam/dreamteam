# Compte-rendu DevOps

  

<b>Groupe : Anthony LESAGE, Maël MAYON, Guillaume PHAM NGOC, Robin REGIS  
Classe : 5 IW1</b>


  
  

Pour le projet Devops nous avons décidé de mettre en place ces outils sur la base existante de notre Projet Annuel.

  

Notre Projet Annuel consiste en une application séparée en 2 parties principales, la partie web pour le front et la partie serveur pour le back. Le front-end étant du React associé à ApolloClient, et le back-end, basé sur Express et associé à du GraphQL et ApolloServer. Le tout est versionné sur Gitlab.

  

De ce fait nous nous sommes naturellement dirigé vers Gitlab CI pour automatiser les tests et le déploiement.

  

Le code source de notre projet utilise TypeScript, notre étape de build est donc indispensable afin de faire la compilation vers du Javascript natif.  
  

Le projet est dockerisé pour notre développement local, et nous souhaitions faire tourner l’application en production également grâce à Docker.

  

Notre process de mise en production se déroule en 4 étapes :

-   push
    
-   Build (Pour compiler le code TypeScript en Javascript et build les images Docker de Web et Server)
    
-   Test (Test pour la partie web avec Jest)
    
-   Deploy (Pull des dernières images docker et run des containers sur le serveur)
    

  

Pour se faire nous avons créé des Dockerfile pour chaque environnement dans le dossier Web et Server, respectivement Dockerfile (local), Dockerfile.staging (preprod), Dockerfike.prod (production).

  

Nous avons défini 3 étapes dans la pipeline grâce au gitlab-ci.yml : Buil, Test et Deploy.

La première va build les images Docker de Web et de Server à partir des Dockerfile.staging puis la push sur le registry Gitlab.

La seconde va lancer les tests sur la partie front.

La dernière va se connecter en SSH à notre serveur de staging basé sur Digital Ocean, stopper les containers Docker en cours, pull les dernières versions des images Docker pour Web et Server et enfin relancer les containers.

### Build

Nous sommes d'abord passé par Jenkins pour l'étape de build :

<img width="1208" alt="devops-jenkins" src="https://user-images.githubusercontent.com/10799586/57179293-96696380-6e7c-11e9-930a-692282afbaa4.png">
<i>Premier test de build sur Jenkins</i>  


Puis nous avons opté pour Gitlab-CI (comme nous utilisons Gitlab pour versionner notre projet), qui nous sert également pour déclencher nos tests et notre déploiement :

<img width="1007" alt="devops1" src="https://user-images.githubusercontent.com/10799586/57179289-6f129680-6e7c-11e9-8b7e-5e3387b79569.png">
<i>Version actuelle de nos jobs avec l'utilisation de Gitlab CI</i>


### Tests

Nous utilisons Jest pour nos tests côté front :  

<img width="918" alt="devops-tests" src="https://user-images.githubusercontent.com/10799586/57179427-2bb92780-6e7e-11e9-99ef-ed6546626418.png">
<i>Exemple de job Gitlab CI exécutant nos tests</i>


  
### Déploiement
Nous avons crée un cluster Kubernetes sur Rancher sur lequel nous deployons le front de l'application en se basant sur le registry interne de Gitlab où nous avons les builds.

<a href="https://ibb.co/x70hSV3"><img src="https://i.ibb.co/rwSkGnv/Screenshot-2019-05-04-at-15-50-02.png" alt="Screenshot-2019-05-04-at-15-50-02" border="0"></a>

### Monitoring
Nous utilisons sonarqube pour le monitoring de notre application.

<img src="https://screenshotscdn.firefoxusercontent.com/images/6917cb1a-d21e-45de-9b3d-49934e68bcba.png">
