---
author: msmimart
ms.service: active-directory-b2c
ms.subservice: B2C
ms.topic: include
ms.date: 07/05/2021
ms.author: mimart
# Used by Azure AD B2C app integration articles under "App integration".
---
After authenticating, the user interacts with the app, which invokes a protected web API. The web API uses [bearer token](https://datatracker.ietf.org/doc/html/rfc6750) authentication. The bearer token is the access token that the app obtained from Azure AD B2C. The app passes the token in the authorization header of the HTTPS request. 
    
```http
Authorization: Bearer <token>
```

If the access token scope doesn't match the web API scopes, the authentication library obtains a new access token with the correct scopes.
