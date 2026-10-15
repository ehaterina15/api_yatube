# Yatube API

**A REST API for Yatube, a social network for personal blogs.** Authenticated users read and publish posts, browse community groups and comment on posts. Only the author of a post or comment can change or delete it.

![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-3.2-092E20?logo=django&logoColor=white)
![DRF](https://img.shields.io/badge/Django_REST_Framework-3.12-A30000?logo=django&logoColor=white)
![pytest](https://img.shields.io/badge/tests-pytest-0A9EDC?logo=pytest&logoColor=white)

## Features

- Full CRUD for posts, with optional image upload
- Read-only access to groups
- Nested comments resource: `/posts/{post_id}/comments/`
- Token authentication (`TokenAuthentication`)
- Custom `IsAuthorOrReadOnly` permission: anyone signed in can read, only the author can edit or delete
- The author is set automatically from the request, so it can't be spoofed
- Covered by pytest tests and a Postman collection

## Endpoints

All endpoints require the header `Authorization: Token <your_token>`.

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/v1/api-token-auth/` | Get a token (`username`, `password`) |
| `GET`, `POST` | `/api/v1/posts/` | List posts / create a post |
| `GET`, `PUT`, `PATCH`, `DELETE` | `/api/v1/posts/{id}/` | Retrieve / update / delete a post |
| `GET` | `/api/v1/groups/` | List groups |
| `GET` | `/api/v1/groups/{id}/` | Retrieve a group |
| `GET`, `POST` | `/api/v1/posts/{post_id}/comments/` | List / add comments on a post |
| `GET`, `PUT`, `PATCH`, `DELETE` | `/api/v1/posts/{post_id}/comments/{id}/` | Retrieve / update / delete a comment |

### Example

```bash
curl -X POST http://127.0.0.1:8000/api/v1/api-token-auth/ \
     -d "username=alice&password=secret"
# {"token": "9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"}

curl -X POST http://127.0.0.1:8000/api/v1/posts/ \
     -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b" \
     -d "text=Hello, Yatube!"
```

## Getting started

```bash
git clone https://github.com/ehaterina15/api_yatube.git
cd api_yatube
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

cd yatube_api
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Run the tests from the repository root:

```bash
pytest
```

A Postman collection for manual testing is in [`postman_collection/`](postman_collection/).

## Context

Built during the Python backend course at [Yandex Practicum](https://practicum.yandex.com/). The data models were provided; I implemented the API layer: serializers, viewsets, routing and permissions.

## Author

**Ekaterina Mashentseva** · [GitHub](https://github.com/ehaterina15)
