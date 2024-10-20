# Aplikacja Fitness

## Przegląd

Ten projekt to aplikacja fitness zaprojektowana w celu pomocy użytkownikom w obliczaniu spożycia kalorii, generowaniu planów dietetycznych oraz śledzeniu postępów. Aplikacja składa się z trzech głównych komponentów:

- **API**: Backend oparty na Django, który obsługuje przetwarzanie danych, interakcje z bazą danych oraz stanowi główną logikę aplikacji.
- **UI**: Frontend oparty na React, który zapewnia interfejs użytkownika do interakcji z aplikacją.
- **Baza Danych**: Baza danych PostgreSQL, która przechowuje dane użytkowników, plany dietetyczne oraz inne niezbędne informacje.

## Architektura

Aplikacja używa Docker Compose do orkiestracji trzech usług:

1. **Baza Danych PostgreSQL (`db`)**
   - Obraz: `postgres:latest`
   - Zmienne środowiskowe:
     - `POSTGRES_DB`: Nazwa bazy danych (domyślnie: `fit-db`)
     - `POSTGRES_USER`: Użytkownik bazy danych (domyślnie: `db-user`)
     - `POSTGRES_PASSWORD`: Hasło do bazy danych (domyślnie: `password`)

2. **API (`api`)**
   - Obraz: `x03xd/fit-app-api:latest`
   - Zależności: `db`
   - Zmienne środowiskowe:
     - `DATABASE_NAME`: Nazwa bazy danych
     - `DATABASE_USER`: Użytkownik bazy danych
     - `DATABASE_PASSWORD`: Hasło do bazy danych
     - `DATABASE_HOST`: Host bazy danych (domyślnie: `db`)
     - `DATABASE_PORT`: Port bazy danych (domyślnie: `5432`)
     - `SENTRY_DSN`: Sentry Data Source Name do śledzenia błędów
     - `UI_URL`: URL dla komponentu UI
   - Porty: Eksponowane na porcie `8000`

3. **UI (`ui`)**
   - Obraz: `x03xd/fit-app-ui:latest`
   - Zmienne środowiskowe:
     - `SENTRY_DSN`: Sentry Data Source Name do śledzenia błędów
     - `REACT_APP_API_URL`: URL API dla frontend
   - Porty: Eksponowane na porcie `3000`

### Instalacja
   - git clone https://github.com/x03xd/fit-app.git
   - docker-compose up
