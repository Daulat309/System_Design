# Design a Ride-Sharing Service (Uber, Ola)

- It is an online platform, where user will be able to request and book rides.

## 1. Functional Requirements:

- Riders should be able to get a fare estimation based on start location and destination.
- Riders should be able to request for a ride based on the estimated fare
- Riders should be able to request different categories of rides
- Drivers should be able to accept/decline a request and navigate to pickup/drop-off.
- Upon request, riders should be matched with a driver who is nearby and available
- Get realtime tracking of the driver & user
- Driver & Riders should be able to rate their ride post-trip
- Riders should be able to make the payment

## 2. Non Functional Requirements:

- Scale: millions of users and drivers
- CAP Theorem: Availability > consistency (user)
  consistency >> availability(driver) - strong consistency in ride matching to prevent any driver from being assigned multiple rides simultaneously
- Latency: <1 min driver should get assigned to a particular ride request

## 3. Core Entity

- Rider
- Driver
- Location
- Fare
- Ride/Trip

## 4. API Designing

User:

1. GET: /v1/api/fare?pickupLat=...&pickupLng=...&dropLat=...&dropLng=... -> List<Fare> with Request ID //different types of vehicle
2. POST: /v1/api/rides/request {body: requestId} (Request all nearby drivers) : Return rideId with driver details (if driver accepts th
3. GET: /v1/api/rides/history
4. POST: /v1/api/rides/{rideId}/cancel
5. POST: /v1/api/rides/{rideId}/ratings

Driver:

1. WS: /v1/drivers/location {body:Lat, Long} - Update driver geoLocation
2. POST: /v1/api/ride/rides {body: requestId, accept/deny} - driver will accept/deny: return as rideId
3. POST: /v1/api/ride/{ride_id}/start
4. POST: /v1/api/ride/{ride_id}/end
