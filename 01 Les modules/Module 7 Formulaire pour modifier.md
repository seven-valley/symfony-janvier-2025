# Formulaire Modifier

le controller  
On vient récupérer le film en injection de dépendance
```php
#[Route('films/modfier/{id}', name: 'app_film_modifier')]
    public function modifier(Film $film,Request $request,EntityManagerInterface $em): Response
    {
       //$film = new Film(); 
       // relier $film <=> $formFilm
       $formFilm = $this->createForm(FilmType::class, $film);
       // hydrater le formulaire avec $request
       // $request <=> $formFilm <=> $film
       $formFilm->handleRequest($request);
       //dd($film);
       //if($formFilm->isSubmitted() && $formFilm->isValid()){
       if($formFilm->isSubmitted() ){
        $em->persist($film); // je viens persister qd c 1 nouvel objet
        $em->flush(); // save
 
        return $this->redirectToRoute("app_film");
       }

      
       //return $this->redirectToRoute("app_film");
       return $this->render('film/modifier.html.twig', [
        'titre' =>'Modifier film',
        'formFilm' => $formFilm,
    ]);
    }

```

on ajoute le lien sur la home
```html
<a href="{{path('app_film_modifier',{'id':f.id})}}">Modifier</a>
```