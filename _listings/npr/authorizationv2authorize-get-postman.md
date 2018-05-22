{
  "info": {
    "name": "NPR Show a web-based login/signup form to a user",
    "_postman_id": "16cd2cf3-7b0c-4603-8ab1-be9898aeae4a",
    "description": "If the parameters passed to this endpoint are correct, it will redirect to `npr.org/oauth2/login` for the user to complete the sign-in.\n\nCurrently acceptable values for `scope` are any combination of the following:\n- `identity.readonly` - for read-only access to the Identity Service\n- `identity.write` - for write access to the Identity Service\n- `listening.readonly` - for read-only access to the Listening Service\n- `listening.write` - for write access to the Listening Service\n- `localactivation` - for all access to the Local Activation Service\n\nIt is generally suggested that you assume that you will need all of the current scopes in order to successfully implement an NPR One application.\n\nIf the parameters passed in are NOT correct and the client passed in a valid `redirect_uri` parameter, the request will be redirected to `{{YOUR_REDIRECT_URI}}?error={{ERROR_TYPE}}&message={{ERROR_DESCRIPTION}}`.\nIf the parameters passed are NOT correct and the client did not pass in a valid `redirect_uri` parameter, this endpoint will return the errors encoded as JSON objects (along with the corresponding HTTP status code -- usually 400).\nThe latter is intended for development and debugging purposes -- in a real-world situation, errors returned as JSON objects are irretrievable by the client application, and thus passing in a valid `redirect_uri` is critical even for the purpose of capturing errors.\n\nIf the user successfully logs in and authorizes the application, the request will be redirected to `{{YOUR_REDIRECT_URI}}?code={{AUTHORIZATION_CODE}}&state={{CSRF_TOKEN}}`\n\nIf the user DENIES the application, they will be redirected to `{{YOUR_REDIRECT_URI}}?error=denied&message=The%20user%20has%20denied%20the%20login%20and%20access%20request&state={{CSRF_TOKEN}}`.\nThis means that if your application flow requires a user to log in in order to proceed, it is up to you to give them the proper messaging explaining that the sign-in must be authorized in order to continue.\n\nFinally, please do not confuse an authorization code with an access token. Once your app has completed this flow, you will still need to call `POST /authorization/v2/token` in order to swap the code for a valid access token.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "authorization",
      "item": [
        {
          "id": "1829b84d-076b-4240-8b28-9ab5740135af",
          "name": "getAuthorizationPage",
          "request": {
            "url": "http://api.npr.org/authorization/v2/authorize?client_id=%7B%7D&redirect_uri=%7B%7D&response_type=%7B%7D&scope=%7B%7D&state=%7B%7D",
            "method": "GET",
            "body": {
              "mode": "raw"
            },
            "description": "If the parameters passed to this endpoint are correct, it will redirect to `npr"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "cc546821-7ad5-4ea1-9504-85e172d8ce9e"
            }
          ]
        }
      ]
    }
  ]
}