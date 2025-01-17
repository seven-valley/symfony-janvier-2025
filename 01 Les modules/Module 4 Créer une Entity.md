# Créer une Entity et Afficher les données

## :one: Créer une Entity
```
symfony console make:Entity Film
```
- Le nom du champ
- le type [string] par default
- la contrainte de nullite

## :two: Créer la table SQL
Demander à Doctrine de créer la table SQL
```
symfony console d:s:u -f
```
OU
```
symfony console doctrine:shema:update -f
```
## :three: Ajouter des données de test
Je viens rajouter des données de test

## Récupération des donnée avec FilmRepository
Nous allons utiliser l'injection de dépendance  
Dans les parenthèse de la méthode
```php
#[Route('/films', name: 'app_films')]
    public function films(FilmRepository $repo): Response
    {
```
Pensez à l'import
```php
use App\Repository\FilmRepository;
```
Installez le pluggin :  
https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client
  
Je récupère tous les films et je les envoient a Twig
```php
#[Route('/films', name: 'app_films')]
    public function films(FilmRepository $repo): Response
    {
       //$films = $repo->findBy([],['titre'=>'ASC']);
        $films= $repo->findAll();
        //dd($films);
        return $this->render('test/films.html.twig', [
            'titre' => 'Films',
            'films' => $films
        ]);
    }
```
