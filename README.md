# simple-saas
- This django project is meant to serve as a boiler plate code for any building any saas tool

- django-rest-framework is used for authentication and creating apis. Please refer to [this](https://github.com/encode/django-rest-framework)
 if not familiar with django-rest-framework since this project heavily relies on it.

- business logic for all APIs is present in serializers.

## APIs inheriting BusinessAPIView
Checks if authtoken present in the header belongs to a valid business and returns the appropriate response if no valid business is found

## APIs inheriting SubscriptionAPIView
Checks if authtoken present in header belongs to a valid business and also an active subscription exists for that business.

## APIs inheriting rest_framework.generics.CreateAPIView
- these are POST apis where `create()` in the serializer will be called after validating post data.
- in serializers where there is an `update()` overridden, refer to the `save()` method to see whether create() is called or `update()` is called

## APIs inheriting rest_framework.generics.RetrieveAPIView
must override the `get_object()` method and whatever is returned by this method is serialized

### APIs

#### Signup
```curl
curl -XPOST 'http://localhost:8000/signup' -d '{"business": {"name": "test inc"}, "email": "test@test.com", "first_name": "sankalp", "last_name": "jonna", "password1": "pleasepass", "password2": "pleasepass"}' -H "Content-type: application/json"
```

#### Login
```curl
curl -XPOST 'http://localhost:8000/login' -d '{"email": "test@test.com", "password": "pleasepass"}' -H "Content-type: application/json"
```

#### Reset password
```curl
curl -XPOST 'http://localhost:8000/passwd/reset' -d '{"email": "test@test.com"}' -H "Content-type: application/json"
```

#### Reset password confirmation
```curl
curl -XPOST 'http://localhost:8000/passwd/reset/cnfrm' -d '{"activation_key": "<activation_key>", "password1": "sankalp", "password2": "sankalp"}' -H "Content-type: application/json"
```

#### Me
```curl
curl -XGET 'http://localhost:8000/me' -H "Authorization: Token <token>"
```

#### Invite
```curl
curl -XPOST 'http://localhost:8000/invite' -H "Authorization: Token 534fe89f5d6b9ff214e8883d7b9664177002056a" -H "Content-Type: application/json" -d '{"email": "test5@test.com"}'
```

#### Prefill Signup form
```curl
curl -XGET 'http://localhost:8000/signup/prefill?key=<activation_key>'
```
