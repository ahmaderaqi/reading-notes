# Q1:
The primary purpose of JSON Web Tokens (JWTs) is to securely transmit information between two parties in a compact and self-contained manner. JWTs are commonly used for authentication and authorization in web applications. They are often used as a way to represent claims between the client (typically a user) and the server.

JWTs are structured as a JSON object and consist of three parts separated by periods ('.'). These three parts are:

1. Header: Contains metadata about the type of token and the hashing algorithm used to sign the token. For example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

The above header specifies that the HMAC SHA-256 algorithm (HS256) is used for signing the token, and the type of the token is JWT.

2. Payload (or Claims): Contains the actual information (claims) that are being transmitted. Claims can include information like user ID, expiration time, user roles, or any other data relevant to the application.

```json
{
  "sub": "user123",
  "name": "John Doe",
  "exp": 1676473600
}
```

The above payload contains a subject claim (`sub`) with the value "user123", a name claim (`name`) with the value "John Doe", and an expiration time (`exp`) with the Unix timestamp 1676473600.

3. Signature: To create the signature, the header and payload are concatenated, and a secret key is used to create a hash of the resulting string. This signature ensures that the token is not tampered with and can be verified by the server.

To summarize the process:

1. The header and payload are encoded using Base64Url encoding to create the first two parts of the JWT.
2. A secret key, known only to the server, is used to create the signature of the encoded header and payload.
3. The signature is appended to the encoded header and payload to form the complete JWT.

The server can then verify the authenticity of the token by performing the following steps:

1. Recreate the signature using the received header and payload, along with the server's secret key.
2. Compare the recreated signature with the signature in the received JWT.
3. If they match, the token is considered valid and can be trusted. Otherwise, the token may have been tampered with and should be rejected.

# Q2:
JWT Authentication can be integrated with Django REST Framework (DRF) to secure API endpoints by using the `djangorestframework-simplejwt` library. This library provides easy-to-use tools for implementing JWT-based authentication in Django projects. To set up JWT Authentication in Django REST Framework, the key components involved are:

1. Install the required package:
First, you need to install the `djangorestframework-simplejwt` package. You can do this using pip:

```bash
pip install djangorestframework-simplejwt
```

2. Configure Authentication Classes:
In your Django settings.py file, you need to configure the authentication classes to include JWTAuthentication.

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```

3. Obtain JWT Tokens:
To obtain a JWT token, users typically need to provide their credentials (username and password) through a login API. DRF provides built-in views to handle this authentication process.

```python
from rest_framework_simplejwt.views import TokenObtainPairView, TokenRefreshView

urlpatterns = [
    # Obtain JWT token
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),

    # Refresh JWT token
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]
```

4. Secure API Endpoints:
To secure your API endpoints, you can use the `@authentication_classes` and `@permission_classes` decorators provided by DRF.

```python
from rest_framework.decorators import api_view, authentication_classes, permission_classes
from rest_framework.permissions import IsAuthenticated

@api_view(['GET'])
@authentication_classes([JWTAuthentication])
@permission_classes([IsAuthenticated])
def secure_endpoint(request):
    # Your view logic here
```

In the above example, the `secure_endpoint` view is protected by both JWTAuthentication and IsAuthenticated permission classes. This means that the user needs to provide a valid JWT token in the Authorization header to access this endpoint, and the token must be associated with a valid and authenticated user.

5. Customization (Optional):
You can further customize JWT settings by adding the `SIMPLE_JWT` dictionary in your settings.py file. This allows you to modify things like token expiration time, token user claims, and more.

```python
SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
    'SLIDING_TOKEN_REFRESH_LIFETIME': timedelta(days=1),
    'SLIDING_TOKEN_REFRESH_LIFETIME_GRACE_PERIOD': timedelta(days=2),
    'SLIDING_TOKEN_REFRESH_TIMEOUT': timedelta(days=30),
    'ALGORITHM': 'HS256',
    'SIGNING_KEY': SECRET_KEY,
    'AUTH_HEADER_TYPES': ('Bearer',),
}
```

# Q3:
Django's built-in development server (`runserver`) is not suitable for production environments due to several reasons:

1. **Performance**: The `runserver` is designed for development and debugging purposes, not for handling the high traffic and load that production environments typically face. It is single-threaded and not optimized for handling concurrent requests efficiently.

2. **Security**: The `runserver` is not hardened against various security threats that production servers need to mitigate, such as Denial-of-Service (DoS) attacks, brute-force attempts, and other vulnerabilities.

3. **No Static File Serving**: In production, web applications often serve static files (CSS, JavaScript, images) using dedicated web servers or content delivery networks (CDNs) for better performance and caching. The `runserver` doesn't handle this efficiently.

4. **No HTTPS**: HTTPS is essential for securing data transmission in production environments. The `runserver` doesn't provide built-in HTTPS support, whereas production servers typically require SSL/TLS certificates.

5. **No Process Manager**: In production, you need a process manager to ensure your Django application runs continuously, manages restarts, and scales based on demand. The `runserver` doesn't offer such functionality.

For deploying a Django application in a production environment, consider using one of the following server options:

1. **Gunicorn (Green Unicorn)**: Gunicorn is a popular WSGI HTTP server that is often used in conjunction with Nginx or Apache. It provides multiple worker processes to handle concurrent requests and can be easily integrated with Django using the WSGI interface.

2. **uWSGI**: uWSGI is another WSGI HTTP server that is commonly used to deploy Django applications. Like Gunicorn, it supports multiple worker processes and offers various configuration options for performance tuning.

3. **Nginx with uWSGI or Gunicorn**: Nginx can be used as a reverse proxy to forward requests to uWSGI or Gunicorn. Nginx serves static files efficiently and can also handle SSL termination, load balancing, and caching.

4. **Apache with mod_wsgi**: Apache can be used with mod_wsgi, which allows Django applications to be served via Apache. It supports multiple processes or threads and is known for its robustness.

5. **Docker Containers**: You can containerize your Django application using Docker and deploy it using container orchestration tools like Kubernetes or Docker Compose. This allows for easier scaling and management of your application.

6. **Platform-as-a-Service (PaaS) Solutions**: Cloud-based PaaS solutions like Heroku, AWS Elastic Beanstalk, or Google App Engine provide simplified deployment options for Django applications, handling server setup and scaling for you.

