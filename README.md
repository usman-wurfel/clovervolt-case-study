# CloverVolt

CloverVolt is an EV charging product for drivers in Pakistan and for the people who run the chargers.

A driver opens the phone app, finds a station, starts a charge, watches the session, and pays. An operator opens the web console and runs the network: stations, prices, live chargers, bookings, wallets, partners, and on-location services.

This repository is the case study. It does not contain the application source.

The phone screens are from the CloverVolt design file. The console screens are from the operations console. Names, email addresses, and phone numbers in those console tables are placeholders.

## Customer app

The home screen is the front door. The driver sees a wallet balance, the nearest station, and the services on the network.

<p>
  <img src="screens/home.png" alt="CloverVolt home" width="260" />
  <img src="screens/login.png" alt="Email and password login" width="220" />
  <img src="screens/otp.png" alt="Mobile one-time code" width="220" />
</p>

### Account

Sign-in matches how people in this market actually log in.

- Email and password
- Mobile number and a one-time code
- Google
- Apple
- Create account
- A second step for a one-time code when the account asks for it

The driver also has a profile, saved vehicles, and a support entry from the home screen.

### Home

Home shows the wallet, promotional banners, and tiles for EV charging, car wash, oil change, tyres, and LPG. Some tiles in this frame are marked Coming Soon. The nearest station shows the name and the distance. Bottom navigation is Home, Bookings, Wallet, and Profile.

### Stations and booking

The driver can look at stations on a map, filter by connector and power, and open a station. A booking is a date and a time on a specific connector. The booking has an 8-digit code the driver can use at the charger.

### Starting a charge

The driver does not connect the phone to the charger. Start goes to the server, and the server talks to the charger.

A charge can be started with:

- the 6-digit charger ID
- the 8-digit booking ID
- the QR code on the charger

If the charger is offline, the start is refused. The app does not pretend a session is running.

### Live session

While the car is charging, the phone keeps one connection open to the API. Energy, power, elapsed time, and the running cost arrive on that connection when the charger reports a new meter reading. The app does not call the API every few seconds to ask for the same numbers.

The running bill uses the same figures the final bill uses: energy cost, time cost, session fee, idle fee, discount, and total. Stopping the session closes it and opens the bill. The driver can download a PDF invoice.

### Money

The driver can pay from the wallet, JazzCash, Easypaisa, or a card. Coupons reduce the session total. A finished session stays in bookings with its receipt.

### Vehicles

The driver saves the cars they charge. The catalog behind that is brands, models, battery types, and connector types, so a station can be matched to the car.

### On-location services

These are jobs that come to the driver, not a charger session.

- Oil change: brand, grade, a health check, a price, a pin, and a time slot
- Tyre fitting: brand, size, wheel balancing, a pin, and a slot
- Rescue and emergency: fuel dispatch, jump-start, an emergency tyre, or a tow

The driver pays these from the wallet. The operator sees the order, assigns the work, and moves the status.

### Car wash and LPG

Both are part of the product design.

Car wash covers packages at the station, a time slot, and pick-up and drop-off: the car is collected, washed, and returned. LPG covers cylinder pickup at an outlet and home delivery inside a coverage area, with a slot and a status the driver can follow.

In the operations console those two modules are still marked as a later milestone. Oil, tyres, and rescue are already in the console.

## Operations console

The same network is run from a web console. A partner who signs in sees their own stations and their own settlements. They do not see another company's numbers.

<img src="screens/admin/login.png" alt="Operations console sign in" width="100%" />

### Dashboard

The first screen is the network for today: revenue, sessions, chargers in service, stations online, the last 30 days of charging, revenue by company-operated and partner stations, and a network count.

<img src="screens/admin/dashboard.png" alt="Dashboard" width="100%" />

### Stations, chargers, and amenities

Operators add stations, set hours, attach a partner, and see utilization. Each station opens into its chargers, connector type, power, status, and a QR code that can be downloaded or printed for the unit.

Amenities (coffee, food, mosque, parking, a shop, a washroom) are what the phone shows on the station card.

<img src="screens/admin/stations.png" alt="Charging stations" width="100%" />

<img src="screens/admin/station-detail.png" alt="Station detail and charger QR" width="100%" />

<img src="screens/admin/chargers.png" alt="Chargers" width="100%" />

<img src="screens/admin/amenities.png" alt="Station amenities" width="100%" />

### OCPP

Chargers stay connected to the server with OCPP 1.6J. The status board shows which charge points are online, and it can send a remote start, stop, or reset and read the protocol log. The phone never opens that connection.

<img src="screens/admin/ocpp.png" alt="OCPP status board" width="100%" />

### Tariffs

Price is set per station: a flat rate per kWh, or peak and off-peak. A session can also carry a per-minute charge, a session fee, and an idle fee. The live total on the phone uses this tariff.

<img src="screens/admin/tariffs.png" alt="Tariffs" width="100%" />

### Bookings, cashier, and sessions

Bookings are the reservations across the network, with status from pending through charging, completed, cancelled, and no-show.

The cashier desk is for a walk-in driver who does not have the app. Staff pick the station and charger, take cash or card at the desk, and start the session from the same screen.

Charging sessions are the actual energy events: payment method, kilowatt-hours, cost, and a link into the live view while a car is charging.

<img src="screens/admin/bookings.png" alt="Bookings" width="100%" />

<img src="screens/admin/cashier.png" alt="Cashier desk" width="100%" />

<img src="screens/admin/sessions.png" alt="Charging sessions" width="100%" />

### Wallets, coupons, and reviews

Operators see wallet balances, the transaction history, and can adjust a balance. Coupons are percent or fixed discounts on a charging session. Reviews are moderated per station and can be hidden.

<img src="screens/admin/wallets.png" alt="Wallets" width="100%" />

<img src="screens/admin/coupons.png" alt="Coupons" width="100%" />

<img src="screens/admin/reviews.png" alt="Reviews" width="100%" />

### Reports and financials

Reports cover network performance, revenue, and usage over a chosen range. Financials is the business view of the same activity: today's revenue, wallets, and station sales.

<img src="screens/admin/reports.png" alt="Reports and analytics" width="100%" />

<img src="screens/admin/financials.png" alt="Financials" width="100%" />

### Dealers and partners

A partner company has a commission, linked stations, and a wallet. Settlements turn session revenue into a payable: gross revenue, platform fee, and net. The ledger records payouts and session credits. A partner login is scoped to that company's own rows.

<img src="screens/admin/partners.png" alt="Partners" width="100%" />

<img src="screens/admin/settlements.png" alt="Settlements" width="100%" />

### Users, roles, and the audit log

Staff, customers, partners, and station managers are separate roles. Permissions decide who can open each screen. The audit log records who changed a station, a user, a charger, or a service order.

<img src="screens/admin/users.png" alt="Users" width="100%" />

<img src="screens/admin/roles.png" alt="Roles and permissions" width="100%" />

<img src="screens/admin/audit.png" alt="Audit log" width="100%" />

### Vehicle catalog

The console holds the reference data the app uses when a driver adds a car: brands, models, battery chemistries, and connector types.

<img src="screens/admin/vehicle-brands.png" alt="Vehicle brands" width="100%" />

<img src="screens/admin/vehicle-models.png" alt="Vehicle models" width="100%" />

<img src="screens/admin/battery-types.png" alt="Battery types" width="100%" />

<img src="screens/admin/connectors.png" alt="Connector types" width="100%" />

### On-location services

Oil, tyres, and rescue each have orders, a catalog, and a coverage area. An order shows the city, the amount, the slot, and the status. Staff can move a job from pending to on the way, in progress, and completed.

<img src="screens/admin/oil-change.png" alt="Oil change" width="100%" />

<img src="screens/admin/tyre.png" alt="Tyre services" width="100%" />

<img src="screens/admin/emergency.png" alt="Rescue and emergency" width="100%" />

### What the app shows

Banners are the cards on the phone home screen. Terms and privacy are edited in the console and served to the app. Settings hold the product name, the support number, email, SMS, payment gateways, currencies, and the booking rules. The payments and SMS screens are not shown here because they contain merchant secrets.

<img src="screens/admin/banners.png" alt="Home banners" width="100%" />

<img src="screens/admin/terms.png" alt="Terms and conditions editor" width="100%" />

<img src="screens/admin/settings.png" alt="General settings" width="100%" />

## How a charge moves

1. The charger stays connected to the server over OCPP.
2. The driver taps start. The server sends a remote start to that charger.
3. The charger accepts, opens a transaction, and begins sending meter readings.
4. Each meter reading is stored, priced from the station tariff, and pushed to that driver's open session.
5. The driver taps stop, or an operator stops it from the console. The server stops the charger, closes the session, and issues the bill.

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

## What these screens are

The three phone images are the home, login, and one-time-code frames from the design file. The console images are the live operations screens: dashboard, stations, a station with its charger QR, chargers, amenities, OCPP, tariffs, bookings, the cashier desk, sessions, wallets, coupons, reviews, reports, financials, partners, settlements, users, roles, the audit log, the vehicle catalog, oil, tyres, rescue, banners, terms, and settings.
