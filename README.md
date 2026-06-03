# Django REST Framework Patterns Sandbox

A learning repo that walks through the main view styles supported by Django
REST Framework on top of a handful of small domain apps. The goal is to have
side-by-side examples of the same idea (CRUD) implemented with different
DRF building blocks so I can refer back to them.

## What's demonstrated

| Pattern                                | Where it lives                        |
| -------------------------------------- | ------------------------------------- |
| Function-based views (`@api_view`)     | `api/views.py` — student endpoints    |
| `APIView` class                        | `api/views.py` — blog & comments      |
| Generic concrete views                 | `api/views.py` (commented examples)   |
| Mixins on `GenericAPIView`             | `api/views.py` (commented examples)   |
| `ModelViewSet` + `DefaultRouter`       | `api/views.py` — employees            |
| Custom permission classes              | `api/views.py`                        |
| Filtering with `django-filter`         | `employees/filters.py`                |
| OpenAPI schema (`drf-spectacular`)     | `django_rest_main/urls.py`            |
| JWT auth (`simplejwt`)                 | `django_rest_main/urls.py`            |

## Apps

- `students` — small `Student` model with function-based views.
- `employees` — `Employee` model used by the `ModelViewSet`, plus a
  `django-filter`-style `EmployeeFilter` class.
- `blogs` — `Blog` model and serializer used by the `APIView`-style views in
  `api/`.
- `api` — the central "view styles tour" — all four view patterns
  registered in `api/urls.py` against the models from the other apps.

## Endpoints

| URL                                  | Style                                  |
| ------------------------------------ | -------------------------------------- |
| `/students/...`                      | function-based views (`students.urls`) |
| `/api/v1/students/`                  | function-based views (`api.views`)     |
| `/api/v1/employees/`                 | `ModelViewSet` + router                |
| `/api/v1/blogs/`                     | `APIView` (list)                       |
| `/api/v1/blogs/<id>`                 | `APIView` (detail)                     |
| `/api/v1/comments/`                  | `APIView` (list)                       |
| `/api/v1/comments/<id>`              | `APIView` (detail)                     |
| `/api/token/` + `/api/token/refresh/`| JWT pair / refresh                     |
| `/api/schema/swagger-ui/`            | Swagger UI                             |
| `/api/schema/redoc/`                 | ReDoc                                  |

## Tech stack

- Python 3.10+
- Django 4.2
- Django REST Framework 3.15
- `djangorestframework-simplejwt`
- `django-filter`
- `drf-spectacular` (OpenAPI 3)
- SQLite (default)

## Setup

```bash
python -m venv env
.\env\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # set SECRET_KEY, DEBUG, ALLOWED_HOSTS
python manage.py migrate
python manage.py runserver
```

Swagger UI: <http://127.0.0.1:8000/api/schema/swagger-ui/>

## Project structure

```text
drf-repo/
├── django_rest_main/      # Django project (settings, urls)
├── api/                   # The "view styles tour"
├── students/              # Function-based views example
├── employees/             # ModelViewSet + filters
├── blogs/                 # APIView example
└── manage.py
```

## Note

This is intentionally a sandbox — `api/views.py` keeps commented-out
alternatives next to the active code so the older patterns stay visible
side-by-side. Treat the file as a notebook, not as production code.
