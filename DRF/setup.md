#django #restapi #cors #backend #drf #react
# 🛠️ Django REST Framework: CORS Headers Setup

## 🧩 Overview

When building a Django REST API that interacts with a frontend (like React), you'll likely encounter **CORS (Cross-Origin Resource Sharing)** issues. This note covers setting up CORS properly using the `django-cors-headers` package.

---

## 📦 Step-by-Step Setup

### 1. Install Required Packages

```
pip install djangorestframework
pip install django-cors-headers   
```

### 2.  Add to `INSTALLED_APPS` in `settings.py
```
INSTALLED_APPS = [
    ...
    'rest_framework',
    'rest_framework.authtoken',
    'corsheaders',
]
```

### 3. Add Middleware in `settings.py`

```
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',  # This too, preferably
    ...
]
```

### 4. Configure Allowed Origins
To allow specific domains 
```
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "http://127.0.0.1:3000",
]
```
Or to allow **all origins** (not recommended in production):
```
	CORS_ALLOW_ALL_ORIGINS = True

```

### 5.Check if the backend is running
```
python manage.py runserver

```
Continue to [[Custom User Authentication]] 