# StockIA — Web Application Platform

Frontend of the **StockIA** Web Application (DataBit team, Open Source course — UPC). The application is written in
**Angular 22 + Angular Material + ngx-translate**, organized by the eight bounded contexts of the StockIA domain, and
consumes the **StockIA Platform** RESTful API built with Spring Boot:
https://github.com/Jesusho22/stockia-platform-os

```
stockia-appweb/
├── webapp/      # Angular 22 web application (see webapp/README.md)
└── mock-api/    # json-server mock API used before the RESTful API existed (kept for reference)
```

## Quick start

```bash
# 1. API (in the stockia-platform-os repository)
SPRING_PROFILES_ACTIVE=local mvn spring-boot:run      # http://localhost:8181 with demo data

# 2. Web application
cd webapp
npm install
npm start                                            # http://localhost:4200
```

Demo accounts (password `stockia123`): `admin@databitecorp.com` and `empleado@databitecorp.com`.

GitHub Actions builds the application and runs an end-to-end test (Playwright) against the real API.

## Features (user stories of Chapter III of the report)

Story IDs follow the Open Source course report
([stockia-report](https://github.com/upc-pre-202602-1ASI0729-7747-databit/stockia-report), Chapter III).

| Bounded context | Features | Stories |
|---|---|---|
| IAM | Sign-in, session kept on reload, sign-out, profile, team and roles (Administrator / Employee), route guards | US10, US11, RNF08 |
| Restaurant Registration | Restaurant sign-up (the owner is the first Administrator, free plan) and restaurant data | US09 |
| Stock Management | Supply lots CRUD with shelf life and status (Expired, Critical, Low stock) | US12 |
| Recipes Management | Recipes linked to the inventory, sale with automatic deduction (the sold dish is highlighted for 2 s), sales history and void | US13, US14, US15 |
| Analytics & Dashboard | KPIs, critical supplies, recent alerts and the latest forecast | US16 |
| Notifications & Messaging | Automatic and manual alerts, WhatsApp + email delivery for critical alerts, retries, acknowledgement | US17 |
| ML & Recommendations | 7-day demand forecast (ONNX model of the API, Peruvian calendar + Open-Meteo weather) and recommendations | US18 |
| Subscription & Payments | Plan catalog and simulated Stripe / PayPal checkout | US19 |
| Shared | Structure by bounded context, connection to the real API with the JWT in every request, loading / empty / result feedback | TS05, TS10, RNF09 |

Added from the Web Applications course version: account lock after 5 wrong passwords (15 minutes) and unlock by an
Administrator, password recovery with a 6-digit code, exact quantities with up to 32 decimals, freshest usable lot
first (an expired lot is never used in a sale) and the weekly savings card of the dashboard.

Not in this release (simulated or pending in the backlog): CSV sales import (US20), real email delivery with SendGrid
(US21) and real Stripe checkout (US22).

## Documentation

- [`webapp/README.md`](./webapp/README.md): architecture by bounded context, routes, how to run and test.
- [`webapp/DEPLOY-VERCEL.md`](./webapp/DEPLOY-VERCEL.md): deploy the web application to Vercel.
- [`mock-api/README.md`](./mock-api/README.md): legacy json-server mock API (no longer used by the web application).

## Stack

- **Web application:** Angular 22 (standalone components, signals), Angular Material (Material Design 3),
  ngx-translate (English `en-US` by default, Latin American Spanish `es-419`), decimal.js for exact quantities.
- **RESTful API:** Spring Boot 3.5, Spring Data JPA, Spring Security (JWT), MySQL, ONNX Runtime, OpenAPI —
  [stockia-platform-os](https://github.com/Jesusho22/stockia-platform-os).
- **Quality:** GitHub Actions (production build + Playwright end-to-end test against the API), GitFlow, Conventional
  Commits, Semantic Versioning.
