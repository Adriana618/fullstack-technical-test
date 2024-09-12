# Albergue Management System

This is a Django-based application for managing an animal shelter with features for administrators, volunteers, and adoptants. The system uses JWT (JSON Web Tokens) stored in HTTP-only cookies for authentication and implements testing with pytest along with linting tools like Black and Pylint. Additionally, `pip-tools` is used for managing dependencies efficiently through `.in` and `.txt` files.

## Features

- **User Roles**: Supports three roles: Administrator, Volunteer, and Adoptant, each with different permissions.
- **JWT Authentication**: Uses JWT for authentication. The access and refresh tokens are stored in HTTP-only cookies to improve security.
- **REST API**: Built using Django Rest Framework (DRF) with pagination and custom serializers.
- **Testing**: Implemented comprehensive tests using `pytest`, `pytest-django`, and `pytest-cov`.
- **Code Linting**: Enforced code style using Black and Pylint.
- **Dependency Management**: Dependencies are managed using `pip-tools` with `.in` files for clean separation of base, dev, and test environments.

## Key Highlights

### JWT Authentication in Cookies

Instead of using localStorage or sessionStorage, JWT tokens are stored in HTTP-only cookies, which increases security. This way, the tokens are not accessible via JavaScript, reducing the risk of XSS (Cross-Site Scripting) attacks. 

To configure the JWT in cookies:
- Access and refresh tokens are set in HTTP-only cookies using Django's `set_cookie`.
- The access token expires after 60 minutes, while the refresh token expires after 1 day.
- In the frontend, we ensure the `withCredentials: true` option is enabled in the Axios requests to send cookies along with requests.

### Testing with Pytest

The project is set up to use `pytest` along with `pytest-django` for testing the Django application. The test files are located in the `tests/` directory. Additionally, we configured code coverage using `pytest-cov`.

To run tests and check for 80% code coverage, use the following command:

```bash
pytest --ds=demo_django.settings --cov=. --cov-fail-under=80
```

### Linting with Black and Pylint

We enforce code formatting and style using Black and Pylint. Black automatically formats the code, while Pylint is used for checking code quality. The `.in` files in the project help manage the linting tools and testing packages efficiently.

To lint the project:

```bash
black .
```

```bash
pylint albergue/
```

### Dependency Management with Pip-Tools

We manage dependencies using `pip-tools`. Instead of directly modifying the `requirements.txt` files, we use `.in` files (`base.in`, `dev.in`, `test.in`) to specify dependencies. Then, we use `pip-compile` to generate the corresponding `.txt` files.

For example, to update the base dependencies:

```bash
pip-compile base.in
```

### Installation Instructions

1. Clone the repository:

```bash
git clone <repository_url>
```

2. Install dependencies using pip-tools:

```bash
pip install -r requirements/base.txt
```
```bash
pip install -r requirements/dev.txt
```

3. Set up Django environment variables using `django-environ` in a `.env` file.

4. Run migrations:

```bash
python manage.py migrate
```

5. Start the development server:

```bash
python manage.py runserver
```

### Running Tests

To run the tests, including coverage checks:

```bash
pytest --ds=demo_django.settings --cov=. --cov-fail-under=80
```

### Linting Code

To check code formatting and linting:
```bash
black .
```
```bash
pylint albergue/
```