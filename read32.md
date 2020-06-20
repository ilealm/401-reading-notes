[ HOME ](README.md)
# Permissions & Postgresql

- Together with authentication and throttling, permissions determine whether a request should be granted or denied access.
- Permission checks are always run at the very start of the view, before any other code is allowed to proceed. 
- Permission checks will typically use the authentication information in the request.user and request.auth properties to determine if the incoming request should be permitted.
- Style of permission would be to allow access to any authenticated user, and deny access to any unauthenticated user. This corresponds to the IsAuthenticated class in REST framework.
- Allow full access to authenticated users, but allow read-only access to unauthenticated users. This corresponds to the IsAuthenticatedOrReadOnly class in REST framework.
- Permissions in REST framework are always defined as a list of permission classes.
- Before running the main body of the view each permission in the list is checked. - If any permission check fails an exceptions.PermissionDenied or exceptions.NotAuthenticated exception will be raised, and the main body of the view will not run.

### API Reference
- **AllowAny:** permission class will allow unrestricted access, regardless of if the request was authenticated or unauthenticated.
- **IsAuthenticated:** permission class will deny permission to any unauthenticated user, and allow permission otherwise.
- **IsAdminUser:** permission class will deny permission to any user, unless user.is_staff is True in which case permission will be allowed.
- **IsAuthenticatedOrReadOnly** will allow authenticated users to perform any request. Requests for unauthorised users will only be permitted if the request method is one of the "safe" methods; GET, HEAD or OPTIONS.

### Django Model Permissions
- This permission class ties into Django's standard django.contrib.auth model permissions. 
- This permission must only be applied to views that have a .queryset property set.
- Authorization will only be granted if the user is authenticated and has the relevant model permissions assigned.

**POST** requests require the user to have the add permission on the model.

**PUT and PATCH** requests require the user to have the change permission on the model.

**DELETE** requests require the user to have the delete permission on the model.

# Source

[Source](https://www.django-rest-framework.org/api-guide/permissions/#allowany)