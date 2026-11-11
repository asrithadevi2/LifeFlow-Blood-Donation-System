# Deployment

LifeFlow is a **Spring Boot application that serves its own frontend**. Deploy it to a Java-capable host (such as Render, Railway, or a VPS). **Do not deploy the static HTML to Vercel alone**: its `/api` calls require the Java server.

## Build

```bash
mvn clean package
java -jar target/lifeflow-1.0.0.jar
```

The application listens on `PORT` if supplied by your host, otherwise 8080.

## Docker option

```bash
docker build -t lifeflow .
docker run -p 8080:8080 -v lifeflow-data:/app/data lifeflow
```

A persistent mounted volume is required to preserve the demo H2 database. Do not run the seeded admin account on a public production site. The demo lacks essential production security controls. For a real service, migrate to PostgreSQL, implement CSRF protection and login throttling, restrict administrator provisioning, protect personal information, and get appropriate compliance and clinical review.

For your **Java external project**, local deployment at `http://localhost:8080` is the recommended safe demonstration mode.
