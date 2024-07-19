# Dokumentacja Schematów Bazy Danych

## Przegląd Tabel

1. **users**: przechowuje informacje o użytkownikach.
2. **clients**: przechowuje dane specyficzne dla klientów powiązane z użytkownikami.
3. **readings**: przechowuje różne odczyty sensorów powiązane z klientami.
4. **watering_times**: przechowuje zaplanowane czasy podlewania dla klientów.
5. **settings**: przechowuje ustawienia specyficzne dla klientów.

## Szczegółowa Dokumentacja Tabel

### 1. users

**opis**: przechowuje informacje o zarejestrowanych użytkownikach.

| nazwa kolumny | typ danych | ograniczenia | opis |
| ------------- | ---------- | ------------ | ---- |
| id            | integer    | klucz główny, auto increment | unikalny identyfikator użytkownika |
| username      | varchar(150) | unikalny, nie null | nazwa użytkownika |
| password      | varchar(128) | nie null | hasło w postaci zaszyfrowanej |
| email         | varchar(254) | unikalny | email użytkownika |
| is_staff      | boolean    | nie null, domyślnie false | wskazuje, czy użytkownik jest pracownikiem |
| is_superuser  | boolean    | nie null, domyślnie false | wskazuje, czy użytkownik jest superużytkownikiem |
| date_joined   | datetime   | nie null | data i czas dołączenia użytkownika |
| last_login    | datetime   |           | data i czas ostatniego logowania |

### 2. clients

**opis**: przechowuje informacje specyficzne dla urządzeń klienta, powiązane z użytkownikami.

| nazwa kolumny | typ danych | ograniczenia | opis |
| ------------- | ---------- | ------------ | ---- |
| id            | integer    | klucz główny, auto increment | unikalny identyfikator klienta |
| user_id       | integer    | klucz obcy (users.id) | użytkownik powiązany z klientem |
| client_id     | integer    | unikalny, nie null | unikalny identyfikator urządzenia klienta |
| created_at    | datetime   | nie null, domyślnie current_timestamp | znacznik czasowy rejestracji klienta |

### 3. readings

**opis**: przechowuje różne odczyty sensorów powiązane z urządzeniami klienta.

| nazwa kolumny | typ danych | ograniczenia | opis |
| ------------- | ---------- | ------------ | ---- |
| id            | integer    | klucz główny, auto increment | unikalny identyfikator odczytu |
| client_id     | integer    | klucz obcy (clients.id) | klient powiązany z odczytem |
| temperature   | float      | nie null | odczyt temperatury |
| soil_humidity | float      | nie null | odczyt wilgotności gleby |
| insolation    | float      | nie null | odczyt nasłonecznienia |
| reading_time  | datetime   | nie null | czas odczytu |

### 4. watering_times

**opis**: przechowuje zaplanowane czasy podlewania dla urządzeń klienta.

| nazwa kolumny | typ danych | ograniczenia | opis |
| ------------- | ---------- | ------------ | ---- |
| id            | integer    | klucz główny, auto increment | unikalny identyfikator czasu podlewania |
| client_id     | integer    | klucz obcy (clients.id) | klient powiązany z czasem podlewania |
| watering_time | time       | nie null | zaplanowany czas podlewania |

### 5. settings

**opis**: przechowuje ustawienia specyficzne dla klientów.

| nazwa kolumny           | typ danych | ograniczenia | opis |
| ----------------------- | ---------- | ------------ | ---- |
| id                      | integer    | klucz główny, auto increment | unikalny identyfikator ustawienia |
| client_id               | integer    | klucz obcy (clients.id) | klient powiązany z ustawieniem |
| sleep_time              | integer    | nie null | czas uśpienia ustawienia |
| soil_humidity_threshold | float      | nie null | próg wilgotności gleby |

## Diagram Mermaid

Oto diagram Mermaid przedstawiający schemat bazy danych:

```mermaid
erDiagram
    USERS {
        integer id PK "unikalny identyfikator użytkownika"
        varchar username "nazwa użytkownika"
        varchar password "hasło w postaci zaszyfrowanej"
        varchar email "email użytkownika"
        boolean is_staff "wskazuje, czy użytkownik jest pracownikiem"
        boolean is_superuser "wskazuje, czy użytkownik jest superużytkownikiem"
        datetime date_joined "data i czas dołączenia użytkownika"
        datetime last_login "data i czas ostatniego logowania"
    }
    CLIENTS {
        integer id PK "unikalny identyfikator klienta"
        integer user_id FK "użytkownik powiązany z klientem"
        integer client_id "unikalny identyfikator urządzenia klienta"
        datetime created_at "znacznik czasowy rejestracji klienta"
    }
    READINGS {
        integer id PK "unikalny identyfikator odczytu"
        integer client_id FK "klient powiązany z odczytem"
        float temperature "odczyt temperatury"
        float soil_humidity "odczyt wilgotności gleby"
        float insolation "odczyt nasłonecznienia"
        datetime reading_time "czas odczytu"
    }
    WATERING_TIMES {
        integer id PK "unikalny identyfikator czasu podlewania"
        integer client_id FK "klient powiązany z czasem podlewania"
        time watering_time "zaplanowany czas podlewania"
    }
    SETTINGS {
        integer id PK "unikalny identyfikator ustawienia"
        integer client_id FK "klient powiązany z ustawieniem"
        integer sleep_time "czas uśpienia ustawienia"
        float soil_humidity_threshold "próg wilgotności gleby"
    }

    USERS ||--o{ CLIENTS : "posiada"
    CLIENTS ||--o{ READINGS : "ma wiele"
    CLIENTS ||--o{ WATERING_TIMES : "ma wiele"
    CLIENTS ||--o{ SETTINGS : "ma jedno"

erDiagram
    users {
        integer id
        varchar username
        varchar password
        varchar email
        varchar first_name
        varchar last_name
        boolean is_active
        boolean is_staff
        boolean is_superuser
        datetime date_joined
        datetime last_login
    }

    clients {
        integer id
        integer user_id
        integer client_id
        datetime created_at
    }

    readings {
        integer id
        integer client_id
        float temperature
        float soil_humidity
        float insolation
        datetime reading_time
    }

    watering_times {
        integer id
        integer client_id
        time watering_time
    }

    settings {
        integer id
        integer client_id
        integer sleep_time
        float soil_humidity_threshold
    }

    users ||--o{ clients : "has"
    clients ||--o{ readings : "records"
    clients ||--o{ watering_times : "has"
    clients ||--o{ settings : "has"
