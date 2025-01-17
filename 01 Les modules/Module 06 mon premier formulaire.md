# Module 6 mon premie formulaire

```
symfony console make:form 
```

Le controller :
```php
#[Route('films/ajouter', name: 'app_film_ajouter')]
    public function ajouter(Request $request,EntityManagerInterface $em): Response
    {
       $film = new Film(); 
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
       return $this->render('film/ajouter.html.twig', [
        'titre' =>'Ajouter film',
        'formFilm' => $formFilm,
    ]);
    }
```

Le twig :
```html
{{ form_start(formFilm)}}
    {{ form_widget(formFilm)}}
    <button type="submit">Ajouter</button>
{{ form_end(formFilm)}}

```