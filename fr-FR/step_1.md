### Choisir ou créer un Animator
Le pack de ressources de démarrage Unity comprend des animations qui peuvent être utilisées avec les modèles. Il comprend également quelques Animators, notamment « IdleWalk » ainsi que d'autres dans le dossier « Animation/More/Animators », incluant des Animators pour les modèles de voiture.

![Modèle de voiture animateur et vue Game montrant une voiture rouge se déplaçant avec une animation.](images/car-anim.gif)

Pour créer ta propre animation, sélectionne le dossier « Animation » dans la fenêtre Project et fais un clic droit puis crée un nouveau Animation Controller.

Clique sur le GameObject qui utilisera l'Animator et accède à la fenêtre Inspector. Fais glisser l'Animator Controller sur la propriété « Controller » du composant « Animator » :

![Le composant Animator avec « FollowMove » dans la propriété Controller.](images/animator-follow.png)

Double-clique sur l'Animator pour l'ouvrir dans la fenêtre Animation. Fais glisser les animations que tu veux utiliser. Clique avec le bouton droit sur les animations pour ajouter des transitions pour tous les changements d'animation que ton personnage peut effectuer.

![La fenêtre de l'animateur avec la nouvelle boîte grise « Dog_Run » et les flèches allant entre les boîtes de ralenti et de course dans les deux directions.](images/idle-run-animator.png)

Va dans l'onglet « Parameters ».  Les paramètres bool te permettent de passer d'une animation à l'autre en leur attribuant la valeur « true » ou « false » dans ton code. Les exemples de paramètres incluent « forward », « crashed », « isRunning ». Pour ajouter un paramètre, clique sur la flèche déroulante à côté du « + ». Choisis « bool » et ajoute un nouveau paramètre.

![La fenêtre Animator avec l'onglet Parameters sélectionné en haut à gauche. Le bouton « + » est étendu avec l'option « bool » sélectionnée.](images/animator-parameters.png)

![La fenêtre Animator avec l'onglet Parameters est sélectionnée et un nouveau paramètre appelé « isRunning » apparaît dans la liste.](images/isRunning-param.png)

Sélectionne la transition dans l'Inspector et ajoute une « Condition », et règle-la sur le paramètre `isRunning` que tu as créé sur `true` ou `false`. Dans l'exemple ci-dessous, la transition de `sit` -> `walk` est déclenchée lorsque `isRunning` est `true`.

![transition dans l'Inspector montrant que la condition isRunning définie sur true](images/transition.png)

**Astuce :** désélectionne « Exit Time » sur les transitions pour que l'animation change immédiatement sans se terminer.

### Ajouter du code à ton GameObject pour contrôler l'animation

Ajoute du code à un script sur ton GameObject pour définir le(s) paramètre(s) permettant de modifier l'animation :

--- code ---
---
language: csharp filename: follower.cs line_numbers: false line_number_start:
line_highlights:
---

    Animator anim;
    
    // Start is called before the first frame update
    void Start()
    {
        anim = gameObject.GetComponent<Animator>();
        anim.SetBool("isRunning", false); // idle
    }
    
    void Update()
    {
        if (Input.GetAxis("Vertical") > 0) // forwards
        {
            anim.SetBool("isRunning", true);
        }
        else // idle
        {
            anim.SetBool("isRunning", false);
        }
    
        // Add movement code here
    }

--- /code ---

![Animator de modèle de voiture et vue Game montrant un chien se déplaçant avec une animation.](images/dog-anim-test.gif)
