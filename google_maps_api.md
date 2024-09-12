# Google Maps API

I only found the compute routes to be what we'll be utilizing the most

[Maps API Pricing](https://mapsplatform.google.com/pricing/)
[Compute Routes](https://developers.google.com/maps/documentation/routes/compute_route_directions)

Example Request:
POST `https://routes.googleapis.com/directions/v2:computeRoutes`
```json
{
  "origin": {
    object (`[Waypoint](https://developers.google.com/maps/documentation/routes/reference/rest/v2/Waypoint)`)
  },
  "destination": {
    object (`[Waypoint](https://developers.google.com/maps/documentation/routes/reference/rest/v2/Waypoint)`)
  },
  "intermediates": [
    {
      object (`[Waypoint](https://developers.google.com/maps/documentation/routes/reference/rest/v2/Waypoint)`)
    }
  ],
  "travelMode": enum (`[RouteTravelMode](https://developers.google.com/maps/documentation/routes/reference/rest/v2/RouteTravelMode)`),
  "routingPreference": enum (`[RoutingPreference](https://developers.google.com/maps/documentation/routes/reference/rest/v2/RoutingPreference)`),
  "polylineQuality": enum (`[PolylineQuality](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#PolylineQuality)`),
  "polylineEncoding": enum (`[PolylineEncoding](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#PolylineEncoding)`),
  "departureTime": string,
  "arrivalTime": string,
  "computeAlternativeRoutes": boolean,
  "routeModifiers": {
    object (`[RouteModifiers](https://developers.google.com/maps/documentation/routes/reference/rest/v2/RouteModifiers)`)
  },
  "languageCode": string,
  "regionCode": string,
  "units": enum (`[Units](https://developers.google.com/maps/documentation/routes/reference/rest/v2/Units)`),
  "optimizeWaypointOrder": boolean,
  "requestedReferenceRoutes": [
    enum (`[ReferenceRoute](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#ReferenceRoute)`)
  ],
  "extraComputations": [
    enum (`[ExtraComputation](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#ExtraComputation)`)
  ],
  "trafficModel": enum (`[TrafficModel](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TrafficModel)`),
  "transitPreferences": {
    object (`[TransitPreferences](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TransitPreferences)`)
  }
}
```


## Response Body
```json
{
  "routes": [
    {
      object (`[Route](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#Route)`)
    }
  ],
  "fallbackInfo": {
    object (`[FallbackInfo](https://developers.google.com/maps/documentation/routes/reference/rest/v2/FallbackInfo)`)
  },
  "geocodingResults": {
    object (`[GeocodingResults](https://developers.google.com/maps/documentation/routes/reference/rest/v2/TopLevel/computeRoutes#GeocodingResults)`)
  }
}

```
