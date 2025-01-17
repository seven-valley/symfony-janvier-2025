# Supprimer un élément
Le controller
```php
 #[Route('films/enlever/{id}', name: 'app_film_enlever')]
    public function enlever(Film $film,EntityManagerInterface $em): Response
    {
        $em->remove($film);
        $em->flush();
        return $this->redirectToRoute("app_film");
       
    }
```