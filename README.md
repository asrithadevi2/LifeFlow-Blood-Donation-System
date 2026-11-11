# LifeFlow — Java Blood Donation Management (Academic Demo)

**A complete single-deployment Spring Boot + HTML/CSS/JavaScript website.** The Java backend handles authentication, database persistence, blood inventory searches, requests, appointments, camp registrations, and administrator updates. The responsive frontend is served directly by Spring Boot.

> **Important:** All blood banks, stock levels, contacts and camps are **fictional demo data**. This project is **not** affiliated with e-RaktKosh or the Government of India. Do not use it for actual blood availability, emergencies, clinical decisions, or medical bookings.

## Requirements

- Java JDK 17 or newer (tested for source compatibility with Java 17)
- Apache Maven 3.9+
- VS Code with Extension Pack for Java (optional)
- Internet on first run for Maven dependencies

## Start in VS Code (Windows)

1. Extract the ZIP.
2. Open the `LifeFlow-Blood-Donation-System` folder in VS Code.
3. Open **Terminal > New Terminal**.
4. Run:

```powershell
mvn spring-boot:run
```

5. Open **http://localhost:8080** in your browser.
6. To stop, press `Ctrl+C` in the terminal.

No Node.js or npm installation is required. The frontend is included under `src/main/resources/static/`.

## Demo credentials

- **Administrator:** `admin@lifeflow.demo` / `DemoAdmin@123`
- **Donor:** create your own account using the Register form.

The admin account is seeded on the first run. **Never expose these demo credentials on a publicly deployed website.**

## Features to demonstrate

1. Search fictional blood inventory by city, blood group and component.
2. Register a donor, log in and log out (passwords stored as BCrypt hashes).
3. Book and cancel a donation appointment. Five bookings maximum per centre/date/slot in the demo.
4. Create a blood request and view its status.
5. Register for an upcoming fictional camp.
6. Log in as admin to approve/reject requests and edit inventory counts.
7. Search again to show that stock changes persist in the H2 database.

## Project structure

```
LifeFlow-Blood-Donation-System/
├── pom.xml                         # Maven + Spring Boot dependencies
├── src/main/java/com/lifeflow/
│   ├── LifeFlowApplication.java    # Java entry point
│   └── Api.java                    # REST controller, validation, seed data
├── src/main/resources/
│   ├── application.properties      # Server and H2 database settings
│   ├── schema.sql                  # Relational schema
│   └── static/
│       ├── index.html             # Website structure
│       ├── styles.css             # Responsive design
│       └── app.js                 # Frontend interaction and API calls
├── VIVA_GUIDE.md
└── DEPLOYMENT.md
```

## Database

File-backed H2 is created at `./data/lifeflow.mv.db` on first startup. Data remains across restarts when the same working directory is used. The `data/` folder is ignored by Git.

## Known limitations / honest scope

- This is an academic **demo**, not a medically certified platform.
- All seeded centres and stock counts are fictional.
- Login uses server-side HTTP session cookies. Use HTTPS and secure cookie settings in production.
- Administrator access is a single seeded system admin; there is no separate blood-bank-scoped admin role.
- No email/SMS notifications, medical screening, blood reservations, or real integrations.
- The appointment capacity check is not atomic under high concurrency.
- H2 file persistence is suitable for local demos, not ephemeral cloud storage.
- Public deployment requires production hardening: CSRF protection, login rate limits, session security, secret management, proper privacy policy, and production database migration.

## Troubleshooting

- `mvn not recognized`: install Maven and add its `bin` folder to PATH; restart VS Code.
- `java not recognized`: install JDK 17+ and configure JAVA_HOME.
- Port 8080 in use: set `PORT=8081` in your terminal, then run Maven.
- If styles are missing: ensure you visit `http://localhost:8080` (not open index.html directly).
- If database is locked: stop other copies of the app and restart.

## Reference

Functionality inspired by the public e-RaktKosh portal: https://eraktkosh.mohfw.gov.in/ . This is an independent, original student project.
