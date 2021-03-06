# API_TCC_Django

Construção de uma API em Django usando Python.


## Como rodar o projeto?

* Clone esse repositório.

* Crie um virtualenv com Python 3.

* Ative o virtualenv.

* Instale as dependências.

* Rode as migrações.

## Git Clone

Link: **ErnestoMoraes/API_TCC_Django.git**

 ## Criar Venv

> cd API_TCC_Django

> python3 -m venv .venv

  ## Ativar Venv

>Linux

`source .venv/bin/activate`.

>Windows

`./.venv/Scripts/activate`.

 ## Instalar extenções


pip install -U pip - Update em PIP

pip install django dj-database-url python-decouple django-extensions

pip freeze - Lista com os Downloads

pip freeze > requirements.txt

### instalando coisas do Requeriments.txt
pip install -r requirements.txt :

### deletar biblioteca
deletar: sqlparse==0.4.2 -> Ele já baixa automaticamente!


 ## Criar env_gen.py
python contrib/env_gen.py:

Buscar repositorio: https://github.com/rg3915/django-simples/blob/master/contrib/env_gen.py

  
## Criar pasta contrib e env_gen.py

python -m django startproject myproject .

  

cd myproject

python3 ..\manage.py startapp core

cd ..

python manege.py migrate

##  Settings

Entrar em API_TCC_Django\myproject\settings.py:

- import os

- from pathlib import Path

- from decouple import config , Csv

- from dj_database_url import parse as dburl

 ### Substituição

SECRET_KEY = config('SECRET_KEY')

DEBUG = config('DEBUG', default=False, cast=bool)

ALLOWED_HOSTS = config('ALLOWED_HOSTS', default=[], cast=Csv())

  

INSTALLED_APPS = [

... Adicionar ao final

#Apps de terceiros

'django_extensions',

#Minhas Apps

'myproject.core',

]

  

Deletar e Substituir:

DATABASES = {

'default': {

'ENGINE': 'django.db.backends.sqlite3',

'NAME': BASE_DIR / 'db.sqlite3',

}

}

  

por

  

default_dburl = 'sqlite:///' + os.path.join(BASE_DIR, 'db.sqlite3')

DATABASES = {

'default': config('DATABASE_URL', default=default_dburl, cast=dburl),

}

  

LANGUAGE_CODE = 'pt-br'

TIME_ZONE = 'America/Sao_Paulo'

  

Adicionar:

STATIC_URL = 'static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

  


- mkdir -p .\myproject\core\static\css

- criar arquivo .\myproject\core\static\css\main.css

- mkdir -p .\myproject\core\templates\includes

- criar arquivo .\myproject\core\templates\includes\nav.html

- criar arquivos .\myproject\core\templates\{base, index}.html

 - criar arquivo .\myproject\core\templates\base.html:
-- link do repositorio:
	> https://github.com/rg3915/django-simples/blob/master/myproject/core/templates/base.html

  

- Adicionar ao .\myproject\core\templates\index.html:
-- link do repositorio:
	> https://github.com/rg3915/django-simples/blob/master/myproject/core/templates/index.html

  

- Adicionar ao .\myproject\core\templates\includes\nav.html:
-- link do repositorio:
	> https://github.com/rg3915/django-simples/blob/master/myproject/core/templates/includes/nav.html

  

## Para fazer funcionar:

- cd myproject\urls.py

Adicionar:

- from myproject.core.views import index

  

urlpatterns = [

path('', index, name='index'),

path('admin/', admin.site.urls),

]

  

- cd myproject\core\views.py

- from django.shortcuts import render

- from django.contrib.auth.models import User

  
  

def index(request):

users = User.objects.all()

context = {'object_list': users}

template_name = 'index.html'

return render(request, template_name, context)

  

## Testar