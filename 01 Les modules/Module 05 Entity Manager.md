# Entity Manager

```php
#[Route('/nouveau-film', name: 'app_film_new')]
    public function nouveauFilm(EntityManagerInterface $em): Response
    {
       $film = new Film(); 
       $film->setTitre("Star Wars 2");   
       $film->setAnnee(1980);
       $film->setIsValid(true);
       $em->persist($film); // je viens persister qd c 1 nouvel objet
       $em->flush(); // save

        //dd($films);
         return $this->redirectToRoute("app_films");
    }
}
```