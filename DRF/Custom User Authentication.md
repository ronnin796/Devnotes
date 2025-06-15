first must have completed the setup [[setup]]
#flashcards #review
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