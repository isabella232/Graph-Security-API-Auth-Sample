---
page_type: sample
products:
- ms-graph
languages:
- csharp
description: "Les données de sécurité accessibles via l’API Microsoft Graph Security sont très sensibles et sont donc protégées par les autorisations et les rôles Azure AD."
extensions:
  contentType: samples
  technologies:
  - Mcirosoft Graph
  - Microsoft Graph
  services:
  - Security 
  createdDate: 4/19/2018 10:35:33 AM
---
# Exemple d'application d’Authentification Microsoft Graph C#

## Introduction

Les données de sécurité accessibles via l’API Microsoft Graph Security sont très sensibles et donc protégées par les autorisations (c'est-à-dire les étendues) et les rôles d’Azure AD (AAD). L’API Microsoft Graph Security applique l’authentification et l’autorisation (AuthNZ) pour protéger les données sensibles qu’elle rend accessibles. Ce document est plus amplement documenté dans
[Comprendre l’autorisation lors de l’appel de l’API Microsoft Graph Security](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2) sur la Communauté technique de l’API Microsoft Graph Security 

## Authentification et autorisation dans Microsoft Graph

L’API Microsoft Graph Security prend en charge deux types d’authentification et d’autorisation d’application (alias AuthNZ) :
* **l'autorisation pour application uniquement**, dans laquelle l'utilisateur n'est pas connecté (par exemple, un scénario SIEM ou d’automatisation standard).
Les autorisations/étendues ici accordées à l’application déterminent l’autorisation
* **Autorisation déléguée de l’utilisateur**, dans laquelle un utilisateur qui est membre du locataire AAD est connecté.

Pour appeler l’API Microsoft Graph Security, l’utilisateur doit avoir un rôle d’administrateur limité de Lecteur sécurité (Limited Security Reader) dans Azure Active Directory, les autorisations requises (c'est-à-dire les étendues) doivent être définies dans l'[**Inscription d'application**](https://go.microsoft.com/fwlink/?linkid=2083908), et l’application doit recevoir l'autorisation requise par l’administrateur client Azure Active Directory. Ce processus est également décrit dans l'[Exemple d’API Microsoft Graph Security pour ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample)

Cet exemple d’application d’Authentification Graph fournit une meilleure visibilité sur les deux types d’AuthNZ lors de l’appel de l’API Microsoft Graph Security, en affichant le contenu du jeton d’authentification, ainsi que le contenu et les en-têtes de la réponse.
L’application possède un onglet pour l’authentification déléguée utilisateur et un autre pour l’authentification de l’application uniquement.
Il dispose également d'un onglet d'**Aide** présentant quelques erreurs courantes ainsi que des correctifs.
L’application vous permet également d’entrer la requête REST de votre choix pour pouvoir afficher la réponse. 

## Informations nécessaires pour l’exécution de l’application

Informations nécessaires à l’exécution de l’application d’Authentification Graph :
![Pour les deux types d’authentification] :
* ID d’application – à partir de l’inscription d’application (vous avez seulement besoin d’une authentification déléguée utilisateur).
![Pour l’authentification de l’application uniquement] (en plus de l’ID d’application)
* **Clé d’application** (c'est-à-dire la clé secrète d’application) – également à partir de l’inscription d'applications
* **ID de client** (ID de votre client Azure AD) – c'est une propriété obligatoire de toute entité de l’API Microsoft Graph Security (réponse)

## Prise en main de l’exemple d’application d’Authentification Graph

 1. Téléchargez ou copiez l'exemple d'application d’Authentification Microsoft Graph.

 2. Si vous n’avez pas enregistré d'application, ni défini et accordé et accordé de façon explicite les autorisations nécessaires, suivez les instructions de l’[Exemple d’API Microsoft Graph Security pour ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample). (veillez à enregistrer la Clé d’application (alias clé secrète d’application) lorsque vous inscrivez l’exemple d’application).

 3. N'oubliez pas d'ajouter **Application native** sur la page d’inscription de l’application si vous exécutez l’exemple ASP.NET. Ceci est requis pour l’exemple d’application Microsoft Graph Security Authentication.
 
 ## Configurez et exécutez l’exemple d'application 
 1. Ouvrez le projet Graph\_Security\_API\_Auth\_Sample.
 
 2. Appuyez sur F5 pour créer et exécuter l’exemple. Cela entraîne la restauration des dépendances du package NuGet et l’ouverture de l’application.

   >Si vous constatez des erreurs pendant l’installation des packages, vérifiez que le chemin d’accès local où vous avez sauvegardé la solution n’est pas trop long/profond. Pour résoudre ce problème, vous pouvez déplacer la solution dans un dossier plus près du répertoire racine de votre lecteur.

## Utilisation de l'exemple d'application d’Authentification Microsoft Graph

1. Le lancement de l’exemple d’application permet d'afficher l’interface utilisateur de l’exemple d’application

![Interface utilisateur de l'exemple d'application d’Authentification Microsoft Graph](readme-images/Default_screen.png)

2. Entrez l’ID d’application dans la zone de texte en haut de la page

## Test de l’autorisation déléguée utilisateur

1. Pour exécuter le flux d’authentification déléguée utilisateur, cliquez sur le bouton **Envoyer une demande**. La boîte de dialogue authentification de Microsoft s’ouvre.

2. Connectez-vous à l'aide de votre compte professionnel ou scolaire.

3. L’interface utilisateur de l'exemple d’application affiche le jeton Auth dans le volet gauche, comme vous pouvez le voir ci-dessous 

![Exemple d’authentification Graph – Autorisation déléguée utilisateur](readme-images/User_delegated_auth.png)

* La propriété **scp** (en surbrillance) affiche les étendues ou les autorisations accordées à l’utilisateur
* La propriété **wids** affiche les GUID des groupes d’utilisateurs auxquels l’utilisateur connecté appartient.

4. La réponse à la requête REST qui s’affiche dans la zone de texte URL de Graph (sa valeur par défaut renvoie le haut, c’est-à-dire l’alerte la plus récente). Il s’agit de la réponse JSON complète reçue de l’API Microsoft Graph Security. Cliquez sur l’onglet **En-tête** de la réponse pour afficher les en-têtes HTTP de la réponse.

* Remarque : Vous pouvez modifier la requête REST envoyée à l’API Microsoft Graph Security en modifiant l’URL dans la zone de texte de l'**URL Graph**

## Tester l’autorisation pour l'application uniquement (aucun utilisateur connecté)

1. Pour exécuter le flux d’authentification de l'application uniquement, vous devez :

* Entrez la clé d’application (ou clé secrète d’application) générée lorsque vous avez enregistré votre application.
* Entrez l’ID du client AAD (vous pouvez le récupérer dans la propriété « azureTenantId » dans la réponse du flux d’autorisation déléguée utilisateur ci-dessus).
* Cliquez sur le bouton **Envoyer une demande**. 

2. L’interface utilisateur de l'exemple d’application affiche le jeton Auth application uniquement dans le volet gauche, comme vous pouvez le voir ci-dessous 

![Exemple d'authentification Graph – Autorisation de l'application uniquement](readme-images/App_only_auth.png)

* La propriété **rôles** (en surbrillance) affiche les étendues ou les permissions accordées à l'application
* La réponse JSON à la requête REST est identique à celle de l’exemple antérieur

## Onglet Aide

L’onglet **Aide** contient des erreurs courantes, les raisons pour lesquelles elles se produisent et les façons de les résoudre (correction) 

![Exemple d’Authentification Graph – Onglet Aide](readme-images/Help_tab.png)

## Ressources

Documentation :
* [Comprendre l’autorisation lors de l’appel de l’API Microsoft Graph Security](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2)
* [Référence des autorisations Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)

Autres exemples :
* [Exemple d'API Microsoft Graph Security pour ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample)
