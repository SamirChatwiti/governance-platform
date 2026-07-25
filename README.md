# Governance Platform — Institutional Operations for Judicial Officers

Institutional governance platform designed to support the structured management of judicial officers, courts, professional records and operational workflows across multiple regions.

Built with Laravel, Filament, role-based access control and Arabic RTL support, the platform centralizes member administration, judicial acts, court assignments, dashboards, reporting and secure API integrations.

The solution also integrates with the NOUR mobile application to support coordinated institutional and field workflows.

**Stack:** Laravel 12 · Filament 3 · MySQL · Sanctum · Arabic RTL UI

## Overview

This platform provides an institutional back-office for managing judicial officers, courts, professional records and structured operational workflows.

It centralizes member administration, court assignments, judicial acts, dashboards, reporting and role-based access within an Arabic RTL environment.

A Sanctum API supports secure integration with the NOUR mobile application, enabling coordinated institutional and field workflows.

The repository presents the platform’s foundational architecture, data model and principal operational modules developed for judicial-sector digital modernization.

## Business Problem

Professional institutions that manage regulated members across multiple regions often rely on fragmented spreadsheets, manual records, paper-based procedures and disconnected communication channels.

This creates operational challenges:

* inconsistent member records;
* limited visibility across regions and courts;
* weak access control between national and regional administrators;
* difficult tracking of procedures, acts and complaints;
* lack of centralized dashboards and institutional KPIs;
* poor integration between back-office governance and field/mobile operations.

Governance Platform addresses this by centralizing institutional records, regional administration, court structures, member profiles, procedures, complaints and mobile access provisioning in one secure Laravel-based back-office.

---

## My Role

I designed and developed Governance Platform as a full institutional back-office system.

My work included:

* designing the Laravel/Filament application architecture;
* implementing the core data model for regions, courts, members, acts and complaints;
* building Filament resources, dashboards and administrative workflows;
* structuring role-based access control for national and regional administration;
* preparing Arabic RTL interfaces for institutional users;
* integrating Laravel Sanctum for mobile/API access;
* designing the user provisioning logic connected to NOUR Mobile;
* preparing the platform as the administrative backbone of the broader WITI ecosystem.

---

## Security & Access Model

Governance Platform uses a role-based access model designed for institutional environments.

The platform separates access between:

* **Super Admin** — national-level administration and full platform visibility;
* **Regional Admin** — access limited to assigned regional scope;
* **Huissier / Member User** — controlled access for mobile and field integration.

Security and access decisions include:

* role-based permissions;
* regional data scoping;
* Laravel policies and Filament access controls;
* Sanctum-based API authentication;
* automatic user provisioning for mobile access;
* separation between administrative back-office and field/mobile workflows;
* portfolio-safe public repository with production secrets and private operational data excluded.

---

## Dashboard & Analytics

| KPI Overview | Account Widget |
|---|---|
| ![Dashboard KPIs](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc1.png) | ![Dashboard account](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc2.png) |

| Analytics Charts — Huissiers by Region & Status |
|---|
| ![Charts](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc3.png) |

Dashboard statistics: **73 courts (mahakems)**, **12 regions** — demo instance. Charts rendered via Filament widgets with Recharts.

---

## Judicial Acts (Actes & Procédures)

| New Act Form — Date & Type | Act Type Selection |
|---|---|
| ![Acte form 1](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc4.png) | ![Acte type dropdown](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc5.png) |

| Act Form — Reference Fields |
|---|
| ![Acte form 2](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc6.png) |

Act types: Notification, Status Change, Constat/Saisie. Full lifecycle tracking with timestamps and reference numbers.

---

## Complaints (الشكايات)

| Complaint Form — Rich Text | Complaint Status & Urgency |
|---|---|
| ![Complaint form 1](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc7.png) | ![Complaint form 2](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc8.png) |

Complaint intake with rich text editor, status workflow (pending/in review/resolved), and urgency classification.

---

## Huissier Management

| Huissiers List — Search & Filter | Add Huissier — Personal Info |
|---|---|
| ![Huissiers list](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc9.png) | ![Add huissier 1](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc10.png) |

| Add Huissier — Address Fields |
|---|
| ![Add huissier 2](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc11.png) |

On huissier creation, the `HuissierObserver` auto-provisions a `User` record with Sanctum credentials — same credentials sync to NOUR mobile via Supabase Auth (shared email identity).

---

## Regional Administration

| Add Regional Admin (مسؤول جهوي) |
|---|
| ![Regional admin form](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc12.png) |

RBAC with roles: `super_admin`, `regional_admin`, `huissier`. Regional admins manage their own jurisdiction scope.

---

## Geographic Coverage — Regions & Courts

| 12 Moroccan Regions (الجهات) | Regions — Continued |
|---|---|
| ![Regions 1](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc13.png) | ![Regions 2](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc14.png) |

| 73 Courts (المحاكم) | Courts — Continued |
|---|---|
| ![Mahakems 1](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc15.png) | ![Mahakems 2](https://raw.githubusercontent.com/sanadidari/governance-platform/main/docs/screenshots/sc16.png) |

Full geographic coverage of Morocco's judicial map: all regions and all courts pre-seeded.

---

## Architecture

```
┌─────────────────────────────────────────────┐
│         Governance Platform (Laravel)        │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  │
│  │  Filament│  │ Sanctum  │  │  HuissierO│  │
│  │  Admin   │  │  API     │  │  bserver  │  │
│  └──────────┘  └────┬─────┘  └─────┬─────┘  │
└───────────────────┼────────────────┼────────┘
                    │                │
                    ▼                ▼
          NOUR Mobile App      User provisioning
          (Flutter + QRPRUF)   (shared credentials)
```

- **HuissierObserver** — auto-provisions User on Huissier creation, bridges both apps via shared email identity
- **Sanctum API** — token-based auth for mobile client
- **Filament 3** — full Arabic RTL admin panel (via `APP_LOCALE=ar`)
- **RBAC** — policies enforce scope per role (super_admin / regional_admin / huissier)

---

## Installation

```bash
git clone https://github.com/sanadidari/governance-platform.git
cd governance-platform
composer install
cp .env.example .env
php artisan key:generate
# Configure DB in .env
php artisan migrate --seed
php artisan serve
```

Admin panel at: `http://127.0.0.1:8000/admin/shuffle`

---

## Related Projects

| Project | Description |
|---|---|
| [NOUR Mobile](https://github.com/sanadidari/nour-mobile) | Unified judicial mobile app (Flutter) — this platform + QRPruf |
| [QRPruf](https://github.com/sanadidari/qrpruf) | Zero-trust proof of presence (QR cryptography) |

---

*Built by [Samir Chatwiti](https://sanadidari.com) — Sanadidari SARL · LegalTech · Morocco*
