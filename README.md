# blog_react_django

## Дружим Django и React
### Установим Django и React
```bash
# Создаем папку для проектов

mkdir Projects
cd Projects

# Устонавливаем виртуал окруженеи
python3 -m venv venvdir

# Вход в виртуал среду
source venvdir/bin/activate

# Установка django
pip install django

# Создаем проект
django-admin startproject blog

# Создаем приложение внутри созданного проекта в данном случаи blog
cd blog
django-admin startapp blogapp

# Устонавливаем React выполнить команду в внутри созданного проекта blog
npx create-react-app blog-ui
cd blog-ui
npm run build
cd ../
```
### Устонавливаем связь
файл ___blog/setting.py___
```python
INSTALLED_APP = [
  'blogapp'
]

TEMPLATES = [
    {
        'DIRS': [BASE_DIR / 'blog-ui/build'],
    }
]  

STATIC_ROOT = BASE_DIR / 'static'

STATICFILES_DIRS = (
    (BASE_DIR / 'blog-ui/build/static'),
)
```
файл ___blog/urls.py___
```python
# подключаем виды из приложения

from blogapp.views from index

urlpatterns = [
  path('', index)
]

```
файл ___blogapp/views.py__
```python
def index(request):
  return render(request, 'index.html', {})
```
```bash
# Копируем css js html в папку static
python manage.py collectstatic

# Запускаем сервер
python manage.py runserver
```
