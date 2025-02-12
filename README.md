# Workshop - Databasemigraties met Laravel
**Volg de onderstaande stappen om de applicatie klaar te zetten voor het eerste gebruik!**

- `;extension: zip` uncommenten in `php.ini` zodat het installatieproces versnelt wordt en geen problemen gooit
- Het `.env` moet bestaan omdat de waarden hieruit uitgelezen worden door de applicatie.
- Het `database/database.sqlite` bestand moet bestaan om een connectie te kunnen maken met de database.

1. Installeer afhankelijkheden (dependencies): `composer install`
2. Setup toepassen: `php artisan migrate`
3. Applicatie starten: `php artisan serve`

Volg de bovenstaande stappen om de applicatie klaar te zetten voor het eerste gebruik!
---
---
---
---
---

## Algemene informatie
- Error log bestanden staan in `logs/laravel.log`
- Je krijgt een Server Error 500 wanneer je geen `.env` bestand hebt.
- sqlite databaseviewer in VSCode moet ververst worden na het uitvoeren van een migratie om de wijzigingen te laten zien.

Nadat je geen bekende foutmeldingen meer krijgt kan je `php artisan migrate` uitvoeren om de eerste tabelopstelling te genereren.

## Foutmeldingen en oplossingen
-  MissingAppKeyException: (komt omdat APP_KEY in .env niet is gezet.)
    `php artisan key:generate` kan uitgevoerd worden om de APP_KEY value in de .env automatisch te vullen met een gegenereerde sleutel

- QueryException -> [XXXXXX.sqlite] does not exit.
    Bestand aanmaken: database/database.sqlite

- QueryException -> could not find driver (Connection: sqlite, SQL: PRAGMA foreign_keys = ON;)
    `php.ini` aanpassen: Volgende drivers uncommenten:
        - extension=pdo_sqlite
        - extension=sqlite3

## Handige commando's
- `php.ini`-locatie vinden:
    `php --ini`

# Migraties
## Algemene migratie informatie
Tabel hernoemen: (`hasTable` zou nodig kunnen zijn voor het geval dat de tabel mogelijk niet bestaat wanneer de `down()` functie aangeroepen wordt)
```php
if (Schema::hasTable('visitors')) {
    Schema::rename('visitors', 'users');
}
```

## Het aanmaken van een migratie
`php artisan make:migration <action_<tablename>_table` maakt een scaffolding bestand aan.
Bevat de `up()` en `down()` functies. Hierin kunnen acties worden toegevoegd die uitgevoerd dienen te worden wanneer de migratie wordt uitgevoerd.

## Alle migraties opnieuw uitvoeren
`php artisan migrate:refresh`

## Alle onuitgevoerde migraties uitvoeren
`php artisan migrate`

## Migratiestatus inzien
`php artisan migrate:status`

## Alle migraties terugrollen
`php artisan migrate:rollback`

## Een specifiek aantal migraties terugrollen (ongedaan maken)
`php artisan migrate:rollback --step=2`

## Migraties 'pretenden' en SQL query ervan inzien (deze migraties worden opgevangen en worden niet daadwerkelijk toegepast op de database)
`php artisan migrate --pretend`

## Informatieve bronnen
- https://laravel.com/docs/11.x/migrations
- https://en.wikipedia.org/wiki/Schema_migration
