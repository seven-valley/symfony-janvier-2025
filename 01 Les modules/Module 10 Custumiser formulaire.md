# Customizer formulaire

Formulaire
```php
public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('prenom')
            ->add('nom',null,['mapped'=> false])
            ->add('isValid', CheckboxType::class ,[
                'label'    => 'Majeur?',
                'required' => false,
                'mapped'=> false
                ])
        ;
    }
```


le controller

```php
    if ($form->isSubmitted() && $form->isValid()) {
    // recupérer le nom en mapped= false
    $nom = $form->get('nom')->getData();
    $personne->setNom(strtoupper($nom));
    $test = $form->get('isValid')->getData();
    dd($test);
    if ($test) {
        $entityManager->persist($personne);
        $entityManager->flush();    
    }
    //..
```