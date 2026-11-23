# CloverVolt

CloverVolt is an EV charging product for drivers in Pakistan and for the people who run the chargers.

A driver opens the phone app, finds a station, books a connector, starts a charge, and pays. An operator opens the web console and runs the network: stations, prices, live chargers, bookings, wallets, and partners.

This repository is the case study. It does not contain the application source.

Names, emails, and phone numbers on these screens are sample values from the design, not live customer records.

## Customer app — charging flow

Only the screens that sit on the main path are shown here.

<p>
  <img src="screens/app/flow.png" alt="CloverVolt charging flow" width="900" />
</p>

### Auth and home

<p>
  <img src="screens/app/onboarding.png" alt="Onboarding" width="170" />
  <img src="screens/app/login.png" alt="Login" width="170" />
  <img src="screens/app/otp.png" alt="OTP" width="170" />
  <img src="screens/app/home.png" alt="Home" width="170" />
</p>

### Find, book, charge, pay

<p>
  <img src="screens/app/stations-map.png" alt="Stations on the map" width="170" />
  <img src="screens/app/select-charger.png" alt="Select a charger" width="170" />
  <img src="screens/app/slot.png" alt="Pick a slot" width="170" />
  <img src="screens/app/booking-confirmed.png" alt="Booking confirmed" width="170" />
  <img src="screens/app/start-charging.png" alt="Start charging" width="170" />
  <img src="screens/app/charging-complete.png" alt="Charging complete" width="170" />
  <img src="screens/app/invoice.png" alt="Invoice" width="170" />
</p>

### Vehicles and payments

<p>
  <img src="screens/app/vehicles.png" alt="Saved vehicles" width="170" />
  <img src="screens/app/payment-methods.png" alt="Payment methods" width="170" />
</p>

## Operations console

Same network, run from the web console. A partner login only sees that partner’s stations and settlements.

<img src="screens/admin/login.png" alt="Console sign in" width="100%" />

<img src="screens/admin/dashboard.png" alt="Dashboard" width="100%" />

<img src="screens/admin/stations.png" alt="Stations" width="100%" />

<img src="screens/admin/station-detail.png" alt="Station detail and charger QR" width="100%" />

<img src="screens/admin/chargers.png" alt="Chargers" width="100%" />

<img src="screens/admin/ocpp.png" alt="OCPP status" width="100%" />

<img src="screens/admin/tariffs.png" alt="Tariffs" width="100%" />

<img src="screens/admin/bookings.png" alt="Bookings" width="100%" />

<img src="screens/admin/sessions.png" alt="Sessions" width="100%" />

<img src="screens/admin/wallets.png" alt="Wallets" width="100%" />

<img src="screens/admin/partners.png" alt="Partners" width="100%" />

## How a charge moves

1. The charger stays connected to the server over OCPP.
2. The driver taps start. The server sends a remote start to that charger.
3. The charger accepts, opens a transaction, and begins sending meter readings.
4. Each meter reading is stored, priced from the station tariff, and pushed to that driver’s open session.
5. Stop closes the session and issues the bill.

## Stack

| Layer | Choice |
| --- | --- |
| Customer app | React Native |
| Operations console | React |
| API | Node.js |
| Data | PostgreSQL |
| Chargers | OCPP 1.6J |
| Live session | One WebSocket from the phone to the API |
| Auth | JWT, with Google and Apple sign-in |
| Money | Wallet, JazzCash, Easypaisa, and card |
