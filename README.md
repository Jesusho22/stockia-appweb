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

## Features (user stories of Chapter III)

| Bounded context | Features |
|---|---|
| IAM | Sign-in with account lock after 5 wrong passwords, password recovery link, profile, password change, team and roles, unlock (US29, US30, US32, US23, US33) |
| Restaurant Registration | Restaurant sign-up (owner = first Administrator, free plan) and restaurant data |
| Stock Management | Supply lots CRUD with exact quantities (32 decimals), shelf life and status (US19, US22) |
| Recipes Management | Recipes linked to the inventory, dish price, sale with stock validation (expired lots are never used), sales history, void (US20, US34, US27, US35) |
| ML & Recommendations | 7-day demand forecast with the ONNX model of the API (Peruvian calendar + Open-Meteo weather) and purchase / menu recommendations (US24, US25) |
| Notifications & Messaging | Automatic and manual alerts, WhatsApp + email delivery for critical alerts, retries, acknowledgement (US26, US28) |
| Subscription & Payments | Plan catalog and simulated Stripe / PayPal checkout (US31) |
| Analytics & Dashboard | KPIs, attention list, recent alerts, projected demand and weekly savings |

## Documentation

- [`webapp/README.md`](./webapp/README.md): architecture by bounded context, routes, how to run and test.
- [`webapp/DEPLOY-VERCEL.md`](./webapp/DEPLOY-VERCEL.md): deploy the web application to Vercel.
- [`mock-api/README.md`](./mock-api/README.md): legacy json-server mock API (no longer used by the web application).

## Stack

- **Web application:** Angular 22 (standalone components, signals), Angular Material (Material Design 3),
  ngx-translate (EN default / ES), decimal.js for exact quantities.
- **RESTful API:** Spring Boot 3.5, Spring Data JPA, Spring Security (JWT), MySQL, ONNX Runtime, OpenAPI —
  [stockia-platform-os](https://github.com/Jesusho22/stockia-platform-os).
- **Quality:** GitHub Actions (production build + Playwright end-to-end test against the API), GitFlow, Conventional
  Commits, Semantic Versioning.
