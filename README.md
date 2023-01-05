# projet-vue-sfc
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
##Présentation du projet

###Introduction
Ce projet est une application web de présentation de séries TV réalisé en VueJS. Il comporte deux vues:
- La vue de la liste des séries les plus populaires (HomeView)
- La vue de détail d'une série (component DetailView)

###Fonctionnalités de la vue 'HomeView'
- Affichage d'une liste de séries télévisées les plus populaires grâce à l'utilisation de l'API d'[Episodate](https://www.episodate.com/api).
- Affichage des informations de chaque série dans des cartes (component ShowCard) avec l'image, le titre et une description.
- Mise en place d'une barre de recherche (component Navbar) permettant de filtrer les séries en fonction du nom.
- Chargement des séries par lots (pagination) lorsque l'utilisateur scrolle en bas de la page.

###Affichage des informations détaillées d'une série sélectionnée à partir de l'API d'Episodate.
- Affichage de l'image de la série, du titre, d'une description, de la note et de la date de début et de fin de diffusion.
- Affichage du statut de diffusion de la série (en cours ou terminée).
- Mise en place d'un bouton permettant de consulter la page de la série sur Episodate.
