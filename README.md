Projet Django avec tailwind intégrée.

# Commande à exécuter pour avoir un projet Django avec tailwind :

## Création du projet & environnement & activation & installation de django dans l'environnement :
```
django-admin startproject django_tailwind_integrate
python -m venv .env
source .env/bin/activate
pip install Django
```

#Installation de tailwind dans le projet :
[Documetation](https://django-tailwind.readthedocs.io/en/latest/installation.html)

## Commandes : installation & raffraichissement de page automatique

```
python -m pip install django-tailwind
python -m pip install 'django-tailwind[reload]'
```

**Dans le projet django, ajouter dans settings.py (INSTALLED_APPS):**

```
INSTALLED_APPS = [
  #other Django apps
  'tailwind',
] 
```

**Création d'application**

```
python manage.py tailwind init
```

**Ajoutez votre application nouvellement créée à INSTALLED_APPS dans settings.py**

```
INSTALLED_APPS = [
  #other Django apps
  'tailwind',
  'theme'
] 
TAILWIND_APP_NAME = 'theme'
```

**Installez les dépendances CSS Tailwind en exécutant la commande suivante :**

```
python manage.py tailwind install
```

**Ajoutons et configurons également , qui s’occupe des actualisations automatiques des pages et des css dans le fichier mode de développement. Ajoutez-le à INSTALLED_APPS dans settings.py:**

```
INSTALLED_APPS = [
  # other Django apps
  'tailwind',
  'theme',
  'django_browser_reload'
]
```

**Ajoutez dans middleware :**

{{ 
MIDDLEWARE = [
  # ...
  "django_browser_reload.middleware.BrowserReloadMiddleware",
  # ...
]
}}

## Inclure django_browser_reload URL dans votre root url.py:

```
from django.urls import include, path
urlpatterns = [
    ...,
    path("__reload__/", include("django_browser_reload.urls")),
]
```

**Enfin, vous devriez être capable d’utiliser les classes CSS Tailwind en HTML. Démarrez le serveur de développement en exécutant la commande suivante dans votre terminal :**

```
python manage.py tailwind start
```

**Enfin la touche final : dans settings.py, ajouter ceci**

```
STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```