---
swagger: "2.0"
x-collection-name: NPR
x-complete: 0
info:
  title: NPR Show a web-based login/signup form to a user
  description: |-
    If the parameters passed to this endpoint are correct, it will redirect to `npr.org/oauth2/login` for the user to complete the sign-in.

    Currently acceptable values for `scope` are any combination of the following:
    - `identity.readonly` - for read-only access to the Identity Service
    - `identity.write` - for write access to the Identity Service
    - `listening.readonly` - for read-only access to the Listening Service
    - `listening.write` - for write access to the Listening Service
    - `localactivation` - for all access to the Local Activation Service

    It is generally suggested that you assume that you will need all of the current scopes in order to successfully implement an NPR One application.

    If the parameters passed in are NOT correct and the client passed in a valid `redirect_uri` parameter, the request will be redirected to `{{YOUR_REDIRECT_URI}}?error={{ERROR_TYPE}}&message={{ERROR_DESCRIPTION}}`.
    If the parameters passed are NOT correct and the client did not pass in a valid `redirect_uri` parameter, this endpoint will return the errors encoded as JSON objects (along with the corresponding HTTP status code -- usually 400).
    The latter is intended for development and debugging purposes -- in a real-world situation, errors returned as JSON objects are irretrievable by the client application, and thus passing in a valid `redirect_uri` is critical even for the purpose of capturing errors.

    If the user successfully logs in and authorizes the application, the request will be redirected to `{{YOUR_REDIRECT_URI}}?code={{AUTHORIZATION_CODE}}&state={{CSRF_TOKEN}}`

    If the user DENIES the application, they will be redirected to `{{YOUR_REDIRECT_URI}}?error=denied&message=The%20user%20has%20denied%20the%20login%20and%20access%20request&state={{CSRF_TOKEN}}`.
    This means that if your application flow requires a user to log in in order to proceed, it is up to you to give them the proper messaging explaining that the sign-in must be authorized in order to continue.

    Finally, please do not confuse an authorization code with an access token. Once your app has completed this flow, you will still need to call `POST /authorization/v2/token` in order to swap the code for a valid access token.
  termsOfService: http://dev.npr.org/develop/terms-of-use
  contact:
    name: NPR One Enterprise Team
    url: http://dev.npr.org
    email: NPROneEnterprise@npr.org
  version: 1.0.0
host: api.npr.org
basePath: /
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /authorization/v2/authorize:
    get:
      summary: Show a web-based login/signup form to a user
      description: |-
        If the parameters passed to this endpoint are correct, it will redirect to `npr.org/oauth2/login` for the user to complete the sign-in.

        Currently acceptable values for `scope` are any combination of the following:
        - `identity.readonly` - for read-only access to the Identity Service
        - `identity.write` - for write access to the Identity Service
        - `listening.readonly` - for read-only access to the Listening Service
        - `listening.write` - for write access to the Listening Service
        - `localactivation` - for all access to the Local Activation Service

        It is generally suggested that you assume that you will need all of the current scopes in order to successfully implement an NPR One application.

        If the parameters passed in are NOT correct and the client passed in a valid `redirect_uri` parameter, the request will be redirected to `{{YOUR_REDIRECT_URI}}?error={{ERROR_TYPE}}&message={{ERROR_DESCRIPTION}}`.
        If the parameters passed are NOT correct and the client did not pass in a valid `redirect_uri` parameter, this endpoint will return the errors encoded as JSON objects (along with the corresponding HTTP status code -- usually 400).
        The latter is intended for development and debugging purposes -- in a real-world situation, errors returned as JSON objects are irretrievable by the client application, and thus passing in a valid `redirect_uri` is critical even for the purpose of capturing errors.

        If the user successfully logs in and authorizes the application, the request will be redirected to `{{YOUR_REDIRECT_URI}}?code={{AUTHORIZATION_CODE}}&state={{CSRF_TOKEN}}`

        If the user DENIES the application, they will be redirected to `{{YOUR_REDIRECT_URI}}?error=denied&message=The%20user%20has%20denied%20the%20login%20and%20access%20request&state={{CSRF_TOKEN}}`.
        This means that if your application flow requires a user to log in in order to proceed, it is up to you to give them the proper messaging explaining that the sign-in must be authorized in order to continue.

        Finally, please do not confuse an authorization code with an access token. Once your app has completed this flow, you will still need to call `POST /authorization/v2/token` in order to swap the code for a valid access token.
      operationId: getAuthorizationPage
      x-api-path-slug: authorizationv2authorize-get
      parameters:
      - in: query
        name: client_id
        description: The clients ID
      - in: query
        name: redirect_uri
        description: The clients URL to redirect to if the authentication is approved
      - in: query
        name: response_type
        description: The type of response; currently, only `code` is supported
      - in: query
        name: scope
        description: A space-separated list of scope(s) requested by the application
      - in: query
        name: state
        description: A CSRF token generated by the client, to be roundtripped through
          the request for added security
      responses:
        200:
          description: OK
      tags:
      - News
      - Authorization
      - Authorize
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---