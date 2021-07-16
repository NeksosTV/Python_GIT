# Content of request
URL <br>
Browser <br>
IP <br>
GET/POST <br>
Files

# Response status code :

- 00 : OK
- 01 : Created
- 04 : No content


- 3xx : Redirection
- 301 : Permanente
- 302 : Found


- 4xx : Erreur utilisateur / client
- 400 : Bad request -> Formulaire invalide
- 401 : Non autorisé -> Vous êtes pas connecté mais la ressource demande que vous soyez authentifié
- 403 : Accès refusé -> Vous êtes connecté mais vous n'avez pas les droits
- 404 : Not found -> Ressource non trouvée
- 405 : Method not allowed -> vous appelez une URL uniquement en GET via le POST
- 409 : Conflict -> Opération que vous voulez effectuée n'est pas possible car elle entre en conflit avec d'autres ressources\
-> Supprimer un élément référencé par d'autres entités\
-> Supprimer un client qui possède des commandes
- 418 : Teapot
  

- 5xx : Erreur serveur
- 500 : Internal server error

En django, les status les plus utilisés dans une application web : 200, 3xx, 401, 403, 404, 500

# IDE 

CTRL + ESPACE -> Bonjour IDE, tu dois travailler pour moi<br/>
Si CTRL + ESPACE ne trouve rien<br/>
CTRL + ESPACE x2 -> IDE, il faut vraiment que tu bosses<br/>

PEP : Convention PYTHON<br/>

Reformat code<br/>
File > Settings > Keymap > Recherche > Reformat > Reformat Code > double click > Add keyboard shortcut

Comment sélectionner plusieurs lignes en même temps :
- Garder ALT enfoncer et cliquer aux différents endroits
- Positionner le curseur sur la première ligne, garder la molette enfoncer en déscendant avec la souris et lacher la molette une fois la sélection terminée
- Utliser les boutons HOME et END pour vous déplacer facilement

# Faire une APP

- Ouvrir le terminal
- Appuie sur le + en haut à gauche de terminal
- Vérifie que tu es à la racine de ton projet
- python manage.py startapp NAME

# Faire une nouveau ENDPOINT

1) Créer une méthode (function) qui va répondre à la requête et qui va renvoyer une réponse (dans le fichier `views.py`)
```python
def index(request):
    return HttpResponse("<h1>Ceci est un titre</h1>")

def index_html(request):
    return render(request, 'examples/example.html', dict())
```
2) Mettre à jour le fichier `urls.py` dans l'app en question. -> Si le fichier n'existe pas, il faut le créer<br />
    C'est l'équivalent de la POSTE -> "Traduire" l'URL client en méthode à appeler<br />
    Path prend 3 paramètres :
        - Le chemin "client"
        - La méthode de callback : views.X
        - Le paramètre nommé `name` qui contient le "nom" de la route

### Toute manipulation dans la même app doit importer ses propres éléments avec `from . import FILE` -> `from . import views` 
### Pq l'écran de DEBUG a disparu


# NEED TO KNOW

- Pour charger les routes d'une app dans le projet, il faut mettre à jour le fichier urls.py du projet avec la valeur suivante :
```python
path('PREFIX/', include('APP.urls')),
```
- Pour charger les modèles (DB) et les templates d'une app, il faut mettre à jour la config du projet en ajoutant une nouvelle clé dans la liste settings.py > INSTALLED_APPS
```python
INSTALLED_APPS = [
    'APP.apps.APPConfig', # Remplacer APP par votre valeur bien sur
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

# Comment utiliser l'outil DB de PyCharm


# ORM
Object<br />
Relation<br />
Mapper<br />

On ne vas pratiquement pas écrire de SQL

Travailler sur des objects qui vont avoir des méthodes de recherche

La base de données va envoyer les données à l'ORM et l'ORM va les transformer en Object


# Modèles

Pour créer une nouvelle table en DB il faut : 
1) Créer une classe dans `models.py` et la faire hériter de `models.Model`
2) Créer les champs nécessaire sans l'id car il est auto-généré
3) Lancer la commande `python manage.py makemigrations APP` -> Générer une migration contenant les changements à apporter à la base de données<br />
   Proposition pour visualiser SQL :
    - dbshell
    - inspectdb
    - showmigrations
    - sqlflush
    
    - dumpdata
    - sqlmigrate
    
    `python manage.py sqlmigrate APP N°_MIGRATION` -> Génère le code SQL qui va être éxécuté
4) `python manage.py migrate` -> update le schéma grace aux migrations


Si je veux mettre à jour un modèle : 
1) Modifier la classe dans `models.py`
2) Générer une nouvelle migration `python manage.py makemigrations`
3) Lancer le migrate : `python manage.py migrate`
