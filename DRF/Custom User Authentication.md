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