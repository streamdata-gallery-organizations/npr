{
  "info": {
    "name": "NPR List stations close to you or filter by search criteria",
    "_postman_id": "5a080da4-10bd-41ab-a4e3-63ca442fef07",
    "description": "This endpoint has two main use cases:\n\n- If no query parameters passed in, it returns a list of stations that are geographically closest to the calling client (based on GeoIP information)\n- If one or more query parameters are passed in, it performs a search of NPR stations that match those search criteria (not taking into account the client's physical location)\n\nClients wanting to implement a 'Change Station' UI should use this endpoint to power their search. In most cases, you'll want to build a search interface that uses one of the 3 provided schemas: `lat` and `lon` (using e.g. the HTML5 Geolocation API), `city` and `state`, _or_ the generic `q` query which can accept a station name, call letters, network name, or zip code. Technically speaking, `q` can also take in either a city name or a state name, but using the `city` and `state` parameters together will yield more accurate geographic search results than `q={cityName}`.\n\nThe `lat` and `lon` query parameters should always be passed in together (otherwise the API will return a 400 error), and if included in the query, they will take precedence over any other search criteria; that is, `lat` and `lon` will do a purely geographic search and not take into account `q`, `city` or `state`.\n\nSimilarly, `city` and/or `state` will take precedence over (and ignore) `q`.\n\nIf clients want to be able to offer multiple types of searches (e.g. 'Search for a station name, city or zipcode') using a *single* search input form, `q` should be used. But again, be aware that using `city` and `state` together will yield more accurate search results than `q={cityName}`.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "stationfinder",
      "item": [
        {
          "id": "69140b7f-2b23-42a4-a071-2ea33af5dcf1",
          "name": "searchStations",
          "request": {
            "url": "http://api.npr.org/stationfinder/v3/stations?city=%7B%7D&lat=%7B%7D&lon=%7B%7D&No Name=%7B%7D&q=%7B%7D&state=%7B%7D",
            "method": "GET",
            "body": {
              "mode": "raw"
            },
            "description": "This endpoint has two main use cases:\n\n- If no query parameters passed in, it returns a list of stations that are geographically closest to the calling client (based on GeoIP information)\n- If one or more query parameters are passed in, it performs a search of NPR stations that match those search criteria (not taking into account the client's physical location)\n\nClients wanting to implement a 'Change Station' UI should use this endpoint to power their search"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "cecb7b60-1361-4df4-b65c-15c49b17817f"
            }
          ]
        }
      ]
    }
  ]
}