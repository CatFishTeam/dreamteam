# Compte-rendu DevOps

  

Groupe : Anthony LESAGE, Maël MAYON, Guillaume PHAM NGOC, Robin REGIS

  
  

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

<img width="1007" alt="devops1" src="https://user-images.githubusercontent.com/10799586/57179289-6f129680-6e7c-11e9-8b7e-5e3387b79569.png">
