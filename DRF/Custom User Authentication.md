first must have completed the setup [[setup]]
#flashcards #review #Authentication #drf  #django #restapi #backend 
## Steps

---
### 1.Create a model Based on the existing model
Import the abstractuser class
```
from django.contrib.auth.models import AbstractUser

```
Make a CustomUser model my Importing the abstractuser
	
```
class CustomUser(AbstractUser):

name = models.CharField(max_length=255, null=True , default='Annonymous')

cemail = models.EmailField(unique=True, max_length=255, null=True)

username = None # Disable username field
USERNAME_FIELD = 'email' # Use email as the unique identifier
REQUIRED_FIELDS = [] # No required fields other than email
phone = models.CharField(max_length=15, null=True, blank=True)
gender = models.CharField(
max_length=10,

)

session_token = models.CharField(max_length=10 , default=0)

created_at = models.DateTimeField(auto_now_add=True)

updated_at = models.DateTimeField(auto_now=True)
```
Add this is settings.py
```
AUTH_USER_MODEL = "users.CustomUser"
```
## 2. Serialize the Model
```
##import this 
from django.contrib.auth.hashers import make_password
from rest_framework.decorators import authentication_classes, permission_classes
```
create User Serializer
```
from rest_framework import serializers
from django.contrib.auth.hashers import make_password
from rest_framework.decorators import authentication_classes, permission_classes
from .models import CustomeUser

class UserSerializer(serializers.HyperlinkedModelSerializer):

def create(self, validated_data):

password = validated_data.pop('password', None)

instance =self.Meta.model(**validated_data)

if password is not None:

instance.set_password(password)

instance.save()

return instance

  

def update(self, instance, validated_data):

for attr , value in validated_data.items():

if attr == 'password':

instance.set_password(value)

else:

setattr(instance , attr , value)

instance.save()

return instance

class Meta:

model = CustomeUser

extra_kwargs = {

'password': {'write_only': True}

}

fields = ('name' , 'email', 'phone' , 'gender' , 'is_active', 'is_staff', 'is_superuser' , 'password', 'session_token', 'created_at', 'updated_at')
```

🔐 `create(self, validated_data)`

Handles **custom creation logic**, especially to hash the password.
```
password = validated_data.pop('password', None)
instance = self.Meta.model(**validated_data)
if password is not None:
    instance.set_password(password)
instance.save()
return instance

```

- Extracts and **removes** `password` from validated data.
- Creates a user instance without the password.
- Uses `set_password()` to **hash** the password before saving.
- Saves and returns the instance.

🔄 `update(self, instance, validated_data)`

Handles updating the user, including password hashing:
```
for attr, value in validated_data.items():
    if attr == 'password':
        instance.set_password(value)
    else:
        setattr(instance, attr, value)
instance.save()
return instance

```

- Iterates over all fields being updated.
- If the field is `password`, it’s hashed.
- Other fields are updated normally.

🛠️ `Meta` class

```
class Meta:
    model = CustomeUser
    extra_kwargs = {
        'password': {'write_only': True}
    }
    fields = ('name', 'email', 'phone', 'gender', 'is_active', 'is_staff', 'is_superuser', 'password', 'session_token', 'created_at', 'updated_at')


```

- Specifies the model this serializer is for (`CustomeUser`).
- `fields`: All the fields you want included in the API input/output.
- `extra_kwargs`: Makes `password` write-only (not readable through the API).

🧠 Tips
- Always use `set_password()` to hash passwords.
- Never expose password fields in serialized output.
- Use `extra_kwargs` to set sensitive fields to `write_only`.
## 3. Generating a token

```
def generate_session_token(length=10):

return ''.join(random.SystemRandom().choice([chr(i) for i in range (97,123)]+[str(i) for i in range (10)]) for _ in range (length))

```

## 4. Custom User Login
https://regex101.com/ for a email strings validations 
make following imports in users/views.py
```
from rest_framework import viewsets

from rest_framework.permissions import IsAuthenticated , AllowAny

from .serializers import UserSerializer, UserCreateSerializer

from .models import CustomUser

from django.http import JsonResponse

from django.views.decorators.csrf import csrf_exempt

from django.contrib.auth import login, get_user_model

import re
```

🔐 Django Signin View — Explained in Detail

📍 Code Snippet

```
@csrf_exempt

def signin(request):

	if not request.method == 'POST':

		return JsonResponse({'error': 'Send a post request with valid parameters'})

	username = request.POST['email']

	password = request.POST['password']

  

	if not re.match(r"^[\w\.-]+@[\w\.-]+\.\w+$", username):

		return JsonResponse({'error': 'Invalid email format'})

	if len(password) < 8:

		return JsonResponse({'error': 'Password must be at least 8 characters long'})

	UserModel = get_user_model()

	try:

	user = UserModel.objects.get(email = username)

	if user.check_password(password):

		usr_dict = UserModel.objects.filter(email=username).values().first()

		usr_dict.pop('password')

  

		if user.session_token != "0":

			user.session_token = "0"

			user.save()

			return JsonResponse({'error': 'User already logged in'})

		token = generate_session_token()

		user.session_token = token

		user.save()

		login(request, user)

		return JsonResponse({'token': token, 'user': usr_dict})

	else:

		return JsonResponse({'error': 'Invalid Password '})

	except UserModel.DoesNotExist:

		return JsonResponse({'error': 'User does not exist'})
```

🧩 Explanation (with Highlights)

🚫 CSRF Exempt

```
@csrf_exempt

```

- Disables CSRF protection for this view.
- Useful for APIs where tokens aren't submitted (like mobile apps or Postman).

📮 Check Request Method

```
if not request.method == 'POST':
    return JsonResponse({'error': 'Send a post request with valid parameters'})

```

- Only allows POST requests.
- Returns an error for GET or other HTTP methods.

📥 Retrieve Inputs

```
username = request.POST['email']
password = request.POST['password']

```

- Grabs `email` and `password` from POST data.
- `email` is stored in `username` variable.

✅ Validate Email Format
```
if not re.match(r"^[\w\.-]+@[\w\.-]+\.\w+$", username):

```

👤 Get User Model

```
UserModel = get_user_model()

```

- Loads custom user model if defined in `settings.AUTH_USER_MODEL`.
- Safer than importing `User` directly.

🔎 Query User By Email

```
user = UserModel.objects.get(email=username)

```

- Tries to find a user with the given email.
- Wrapped in `try/except` in case user doesn't exist.

📤 Prepare User Data (Without Password)

```
usr_dict = UserModel.objects.filter(email=username).values().first()
usr_dict.pop('password')
```

- Grabs user info as dictionary.
- Removes password field before sending to client.

🔄 Check Session Token (Already Logged In)

```
if user.session_token != "0":
    user.session_token = "0"
    user.save()
    return JsonResponse({'error': 'User already logged in'})

```

- If token is already set, another session is active.
- Resets it to "0" and blocks login.

🪙 Generate Token & Log In

```
token = generate_session_token()
user.session_token = token
user.save()
login(request, user)

```

- Creates a new session token.
- Saves it to DB.
- Logs user in via Django's built-in login system.

📦 Return Token + User Info

```
return JsonResponse({'token': token, 'user': usr_dict})

```

- Responds with token and sanitized user info (without password).

⚠️ Error Handling

```
except UserModel.DoesNotExist:
    return JsonResponse({'error': 'User does not exist'})

```

- Handles case where email is not found.

❗ Using `request.POST[...]` directly can raise `KeyError`. Safer alternative:

```
username = request.POST.get('email', '')

```

