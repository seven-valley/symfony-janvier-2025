# Module 3 Twig
- Envoyer des variables à twig
- Afficher un tableau dans twig
- Afficher un objet dans twig
- Utiliser des assets
- Mettre en place des template avec <code>block</code>

controller :
```php
#[Route('/test', name: 'app_test')]
    public function test(): Response
    {
        $personne = new \StdClass(); // on the fly
        $personne->prenom = "Brad";
        $personne->nom = "PITT";

        $frutis = ["pomme","poire","cerise"];
        $titre_page = 'titre de la page';
        return $this->render('test/test.html.twig', [
            'titre' => $titre_page,
            'tableau'=> $frutis,
            'personne'=> $personne
        ]);
    }
```

twig :
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{{ titre }}</title>
  </head>
  <body>
    <h1>{{ titre }}</h1>
    {# lorem ipsum #}
    {{ dump(tableau) }}
    <table>
      <thead>
        <tr>
          <th>indice</th>
          <th>Fruit</th>
        </tr>
      </thead>
      <tbody>
       {% for indice,fruit in tableau %}
        <tr>
          <td>{{indice}}</td>
          <td>{{fruit}}</td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
    <h2>{{ personne.prenom}} {{ personne.nom}}</h2>
  </body>
</html>
```

asset :
```html
 <link rel="stylesheet" href="{{ asset('./style.css') }}">
```

# les template
modele.html.twig
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{{ asset('./style.css') }}">
    <title>{% block titre %} titre par default {% endblock %} </title>
</head>
<body>
    {% block body%} {% endblock %}
</body>
</html>
```


la page 
```html
{% extends 'modele.html.twig' %}

{% block titre %} {{ titre }} {% endblock %}

{% block body %}
    <h1>{{ titre }}</h1>
    <h2>test avec template</h2>
    {# lorem ipsum #}
    {{ dump(tableau) }}
    <table>
      <thead>
        <tr>
          <th>indice</th>
          <th>Fruit</th>
        </tr>
      </thead>
      <tbody>
       {% for indice,fruit in tableau %}
        <tr>
          <td>{{indice}}</td>
          <td>{{fruit}}</td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
    <h2>{{ personne.prenom}} {{ personne.nom}}</h2>
{% endblock  %}

```

# path pour les liens
```
 <a class="nav-item nav-link" 
  href="{{ path('main_contact')}}" href="/">Contact</a>
```