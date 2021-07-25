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
## Axios и тестовое API
```bash
# Устанавливаем rest_framework
pip install djangorestframework

```
файл ___blog/setting.py__
```python
INSTALLED_APP = [
  'blogapp',
  'rest_framework'
]
```
создаем в нашем приложении папку api
```bash
cd blogapp
mkdir api
cd api
```
>api
>><p align="justify">__init__.py
</p>
>>serializers.py
>>urls.py
>>views.py

#### Установка axios
```bash
cd blog-ui
npm install axios
cd ../
```
```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const App = () => {

	const [post, setPost] = useState([]);
	
	useEffect(() => {
		axios({
			method: "GET",
			url: "http://127.0.0.1:8000/api/test-api/",
		}).then(response() => {
			setPost(response.data)
		})
	}, [])
	
	return (
		<div>
			{ post.title }
		</div>
	)
}
```
