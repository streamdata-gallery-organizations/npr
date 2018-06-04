---
name: NPR
x-slug: npr
description: NPR delivers breaking national and world news. Also top stories from
  business, politics, health, science, technology, music, arts and culture. Subscribe
  to podcasts and RSS feeds.
image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
x-kinRank: "9"
x-alexaRank: "641"
tags: NPR
created: "2018-06-03"
modified: "2018-06-03"
url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/apis.md
specificationVersion: "0.14"
apis:
- name: NPR Show a web-based login/signup form to a user
  x-api-slug: npr
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
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////authorization/v2/authorize
  tags: News,Authorization, Authorize
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2authorize-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2authorize-get-openapi.md
- name: NPR Initiate an OAuth2 login flow for limited input devices
  x-api-slug: npr
  description: |-
    This flow should only be used by clients who cannot show a native webview or do not have advanced input controls. It is an alternative to `GET /authorization/v2/authorize`.

    Third-party clients will need to use one or the other of these two endpoints, but they will generally not use both.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////authorization/v2/device
  tags: News,Authorization, Device
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2device-post-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2device-post-openapi.md
- name: NPR Create a new OAuth2 access token
  x-api-slug: npr
  description: |-
    Please be aware that the required parameters are contingent on the `grant_type` that you select.

    For the `authorization_code` grant type, you are **required** to pass in the `code` and `redirect_uri` parameters. `service`, `username` and `password` parameters will be ignored.

    For the `client_credentials` grant type, you do not need to pass in any additional parameters beyond the basic requirements. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.

    For the `device_code` grant type, you are **required** to pass in the `code` parameter. `redirect_uri`, `service`, `username` and `password` parameters will be ignored.

    For the `password` grant type, you are **required** to pass in the `username` and `password` parameters. If you are logging in via a social service, you should also pass in the `service` parameter. (In this case, the access token you receive from the social service will serve as both your username and password.) The `code` and `redirect_uri` parameters are ignored.
    Third-party developers do not have access to this grant type.

    For the `refresh_token` grant type, you are **required** to pass in the `refresh_token` parameter. The `scope` parameter can optionally be used to request a different set of scopes than were used in the original request, but it **cannot** contain any scopes that were not previously requested. If not specified, then `scope` will be set to whichever scopes were used for the original access token request. If trading in an old non-expiring access token for a refresh-enabled token, set the value of `refresh_token` to the access token value and `token_type_hint` must be set to `access_token`. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.

    The `temporary_user` and `anonymous_user` grant types are custom grant types created by NPR to suit our needs for functionality such as our &quot;try-before-you-buy&quot; experience. If you are a third-party developer, you will not have access to these grant types unless we have explicitly given you permission within our system.
    For these grant types, you do not need to pass in any additional parameters beyond the basic requirements. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.

    If you are unsure of which grant type to select, assume that `authorization_code` is the one you want.

    Note that at this time, refresh tokens are an opt-in feature; however, in the future, they will gradually transition to being opt-out, and ultimately required for all clients. Our general guidance at this time is that if this endpoint starts returning refresh tokens for you, you are responsible for implementing the code to handle them appropriately in accordance with the OAuth 2.0 spec. For more information about our gradual rollout of this feature, please contact the NPR One API team.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////authorization/v2/token
  tags: News,Authorization, Token
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2token-post-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2token-post-openapi.md
- name: NPR Revoke an existing OAuth2 access token
  x-api-slug: npr
  description: |-
    Our implementation follows the proposed IETF specification [RFC-7009](https://tools.ietf.org/html/rfc7009).

    If your client application offers the ability to for a logged-in user to log out, and you have access to a long-lived
    `client_credentials` token (i.e. you have generated one that you are storing securely for the lifetime of the entire app
    install), we suggest (but do not require) that you call this endpoint and revoke the access token belonging to the
    logged-in user as part of your logout process. If you do not already have a long-lived `client_credentials` token,
    please don't generate one just for the purposes of calling this endpoint.

    If you are building a prototype application, we also recommend that you use this endpoint to clean up access tokens
    that you generate during the testing of your app and do not intend to reuse.

    Note that revoking an access token will automatically revoke any refresh tokens associated with it, and vice-versa.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////authorization/v2/token/revoke
  tags: News,Authorization, Token, Revoke
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2tokenrevoke-post-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/authorizationv2tokenrevoke-post-openapi.md
- name: NPR Update the following status of the logged-in user for a particular aggregation
  x-api-slug: npr
  description: After a successful call, this returns a User document with an updated
    list of affiliations.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////identity/v2/following
  tags: News,Entity, Following
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/identityv2following-post-openapi.md
- name: NPR Update the logged-in user's favorite station(s)
  x-api-slug: npr
  description: Right now, only the primary station can be changed. Previously selected
    stations will not be deleted, but the new station will be moved to first in the
    array.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////identity/v2/stations
  tags: News,Entity, Stations
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/identityv2stations-put-openapi.md
- name: NPR Get the latest state information about the logged-in user
  x-api-slug: npr
  description: After a successful login, the client should send a `GET` call approximately
    once an hour to refresh the user data.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////identity/v2/user
  tags: News,Entity, User
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/identityv2user-get-openapi.md
- name: NPR Copy listening data from a temporary user account to the logged-in user's
    account
  x-api-slug: npr
  description: |-
    This can and should only be used by clients who have access to the `temporary_user` grant type.
        Third-party developers do not have access to this grant type by default, and will not need this endpoint.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////identity/v2/user/inherit
  tags: News,Entity, User, Inherit
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/identityv2userinherit-post-openapi.md
- name: NPR Get a set of recommendations for an aggregation
  x-api-slug: npr
  description: This endpoint provides a list of recent audio items associated with
    the aggregation along with metadata about the aggregation.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/aggregation/{aggId}/recommendations
  tags: News,Listening, Aggregation, Agg, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2aggregationaggidrecommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2aggregationaggidrecommendations-get-openapi.md
- name: NPR Get the list of available channels
  x-api-slug: npr
  description: These channels allow the user to specify a focus for the content returned
    in the recommendations endpoint.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/channels
  tags: News,Listening, Channels
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2channels-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2channels-get-openapi.md
- name: NPR Get recent ratings the logged-in user has submitted
  x-api-slug: npr
  description: This endpoint provides the list of recently-rated audio recommendations
    that the logged-in user has consumed. Some rated recommendations are filtered,
    such as sponsorship and donation.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/history
  tags: News,Listening, History
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2history-get-openapi.md
- name: NPR Get a list of recommendations from a category of content from an organization
  x-api-slug: npr
  description: This endpoint provides a list of recommendations from a category of
    content from  an organization.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/organizations/{orgId}/categories/{category}/recommendations
  tags: News,Listening, Organizations, Org, Categories, Category, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2organizationsorgidcategoriescategoryrecommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2organizationsorgidcategoriescategoryrecommendations-get-openapi.md
- name: NPR Get a variety of details about an organization including various lists
    of recent audio items
  x-api-slug: npr
  description: This endpoint provides a variety of details about an organization including
    various lists of recent audio items.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/organizations/{orgId}/recommendations
  tags: News,Listening, Organizations, Org, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2organizationsorgidrecommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2organizationsorgidrecommendations-get-openapi.md
- name: NPR Retrieve the most recent promo audio heard by the logged-in user
  x-api-slug: npr
  description: Gets the most recently played promo for which the user has neither
    tapped through the promo or listened to the target story.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/promo/recommendations
  tags: News,Listening, Promo, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2promorecommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2promorecommendations-get-openapi.md
- name: NPR Collect new ratings for media previously recommended to the logged-in
    user
  x-api-slug: npr
  description: |-
    This endpoint is the main mechanism for providing feedback from the user to NPR about the recommendations that are obtained from `GET /listening/v2/recommendations`.

    A fully-populated link to this endpoint is returned with each individual recommendation and is located in the AudioItemDocument under the `links['recommendations']` object. The query parameters in this link should not be modified.
    Be sure to copy and send back the entire ratings object (RatingData), as new fields may be added to it in the future.

    This endpoint can return a blank JSON.doc or AudioItemDocument depending on the `recommend=true|false` parameter. The `recommend=true` flag allows this endpoint to both receive ratings and send back recommendations in the same call.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/ratings
  tags: News,Listening, Ratings
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2ratings-post-openapi.md
- name: NPR Get a list of media for the logged-in user from NPR's recommendation engine
  x-api-slug: npr
  description: |-
    This endpoint returns a list of audio recommendations. It is designed to be used for an initial list of recommendations, and then `GET /listening/v2/ratings?recommend=true` should be used for subsequent requests for recommendations.

    A fully-populated link to the ratings endpoint is returned with each individual recommendation and is located in the AudioItemDocument under the `links['recommendations']` object. The query parameters in this link should not be modified.
    Be sure to copy and send back the entire ratings object (RatingData), as new fields may be added to it in the future.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/recommendations
  tags: News,Listening, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2recommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2recommendations-get-openapi.md
- name: NPR Get a list of recent audio and aggregation items associated with search
    terms
  x-api-slug: npr
  description: In the schema shown below, SearchItemDocument is not an actual type
    of returned object; the object returned by a search will be either an AggregationAudioItemListDocument
    or an AudioItemDocument.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////listening/v2/search/recommendations
  tags: News,Listening, Search, Recommendations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2searchrecommendations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/listeningv2searchrecommendations-get-openapi.md
- name: NPR Send a donation email to the logged-in user (only on request)
  x-api-slug: npr
  description: This will send a station-specific donation email to the logged-in user.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////localactivation/v2/donate_email
  tags: News,Localactivation, Donate, Email
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/localactivationv2donate-email-get-openapi.md
- name: NPR Request DAAST sponsorship units
  x-api-slug: npr
  description: |-
    **Not** for use by NPR One clients (for whom sponsorship is already integrated into the Listening Service), this endpoint is designed to be used by our other client applications to request sponsorship on behalf of a user. Sponsorship units are returned in the form of DAAST XML. It is worth noting that this endpoint attempts to always return XML, even in the case of exceptions.

    The default behavior of this endpoint is asynchronous; on an initial request, a call to our external sponsorship provider is placed on a queue, which is typically processed within 3 minutes. Once the sponsorship call is received and processed, the returned sponsorship units are placed in a cache on our server for the current user. Subsequent calls to this endpoint will return DAAST sponsorship units from this cache until tracking information is submitted, which removes the ad from the cache and will automatically request additional ads asynchronously if there are fewer than a certain number remaining in the cache.

    For development purposes, it's worth noting that there is currently no way to clear a user's cache without submitting some form of tracking.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////sponsorship/v2/ads
  tags: News,Sponsorship, Advertising
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/sponsorshipv2ads-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/sponsorshipv2ads-get-openapi.md
- name: NPR Record tracking data for DAAST sponsorship units
  x-api-slug: npr
  description: |-
    **Not** for use by NPR One clients (for whom sponsorship is already integrated into the Listening Service), this endpoint is designed to be used by our other client applications to submit tracking information for sponsorship units obtained from the `GET /sponsorship/v2/ads` endpoint.

    The tracking information should be submitted in the body of the request in the form of a JSON object following the Collection.Doc+JSON specification.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////sponsorship/v2/ads
  tags: News,Sponsorship, Advertising
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/sponsorshipv2ads-post-openapi.md
- name: NPR List stations close to you or filter by search criteria
  x-api-slug: npr
  description: |-
    This endpoint has two main use cases:

    - If no query parameters passed in, it returns a list of stations that are geographically closest to the calling client (based on GeoIP information)
    - If one or more query parameters are passed in, it performs a search of NPR stations that match those search criteria (not taking into account the client's physical location)

    Clients wanting to implement a 'Change Station' UI should use this endpoint to power their search. In most cases, you'll want to build a search interface that uses one of the 3 provided schemas: `lat` and `lon` (using e.g. the HTML5 Geolocation API), `city` and `state`, _or_ the generic `q` query which can accept a station name, call letters, network name, or zip code. Technically speaking, `q` can also take in either a city name or a state name, but using the `city` and `state` parameters together will yield more accurate geographic search results than `q={cityName}`.

    The `lat` and `lon` query parameters should always be passed in together (otherwise the API will return a 400 error), and if included in the query, they will take precedence over any other search criteria; that is, `lat` and `lon` will do a purely geographic search and not take into account `q`, `city` or `state`.

    Similarly, `city` and/or `state` will take precedence over (and ignore) `q`.

    If clients want to be able to offer multiple types of searches (e.g. 'Search for a station name, city or zipcode') using a *single* search input form, `q` should be used. But again, be aware that using `city` and `state` together will yield more accurate search results than `q={cityName}`.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////stationfinder/v3/stations
  tags: News,Stationfinder, Stations
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/stationfinderv3stations-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/stationfinderv3stations-get-openapi.md
- name: NPR Retrieve metadata for the station with the given numeric ID
  x-api-slug: npr
  description: |-
    This endpoint retrieves information about a given station, based on its numeric ID, which is consistent across all of NPR's APIs.

    A typical use case for this data is for clients who want to create a dropdown menu, modal/pop-up or dedicated page displaying more information about the station the client is localized to, including, for example, links to the station's homepage and donation (pledge) page.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org////stationfinder/v3/stations/{stationId}
  tags: News,Stationfinder, Stations, Station
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/stationfinderv3stationsstationid-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/stationfinderv3stationsstationid-get-openapi.md
- name: NPR
  x-api-slug: npr
  description: NPR delivers breaking national and world news. Also top stories from
    business, politics, health, science, technology, music, arts and culture. Subscribe
    to podcasts and RSS feeds.
  image: http://kinlane-productions.s3.amazonaws.com/screen-capture-api/141-npr.jpg
  humanURL: http://npr.org
  baseURL: https://api.npr.org//
  tags: NPR
  properties:
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-organizations/npr/master/_listings/npr/openapi.md
x-common:
- type: x-base
  url: http://api.npr.org/
- type: x-codecademy
  url: http://www.codecademy.com/tracks/npr
- type: x-crunchbase
  url: https://crunchbase.com/organization/npr
- type: x-crunchbase
  url: http://www.crunchbase.com/company/npr
- type: x-developer
  url: http://dev.npr.org/
- type: x-documentation
  url: http://dev.npr.org/#accessing-the-api
- type: x-email
  url: permissions@npr.org
- type: x-email
  url: ogcstaff@npr.org
- type: x-email
  url: employment@npr.org
- type: x-email
  url: careers@npr.org
- type: x-email
  url: kroc@npr.org
- type: x-email
  url: mediarelations@npr.org
- type: x-email
  url: sponsorship@npr.org
- type: x-email
  url: ashamblin@npr.org
- type: x-email
  url: giving@npr.org
- type: x-email
  url: giftplanning@npr.org
- type: x-getting-started
  url: http://dev.npr.org/#quick-start
- type: x-github
  url: https://github.com/npr
- type: x-selfservice-registration
  url: http://www.npr.org/templates/reg/
- type: x-terms-of-service
  url: http://www.npr.org/about-npr/179876898/terms-of-use
- type: x-twitter
  url: https://twitter.com/NPR
- type: x-twitter
  url: https://twitter.com/NPRTechTeam
- type: x-website
  url: http://npr.org
- type: x-website
  url: http://www.npr.org
include: []
maintainers:
- FN: Kin Lane
  x-twitter: apievangelist
  email: info@apievangelist.com
---