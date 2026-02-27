# ClinicMS-Laravel

Laravel 5.4 based clinic management system.

## Project Status / Compatibility

- Framework: Laravel 5.4
- Database: MySQL / MariaDB
- Recommended PHP: 7.4
- Included local runtime: `.tools/php74/php`

This project is legacy and is **not** directly compatible with PHP 8.x package constraints.

## Requirements

- Windows
- MySQL server (XAMPP, Laragon, or standalone MySQL/MariaDB)
- Composer
- PHP 7.4 (use included local runtime in this repo)

## Setup (Windows)

### 1) Open PowerShell in project root

```powershell
Set-Location "D:\dead\ClinicMS-Laravel"
```

### 2) Use local PHP 7.4 for current terminal session

```powershell
$phpDir = Resolve-Path ".tools\php74\php"
$env:PATH = "$phpDir;$env:PATH"
php -v
```

### 3) Install PHP dependencies

```powershell
composer install
```

### 4) Configure environment

The project already includes `.env`. Confirm DB values are correct:

- DB_CONNECTION=mysql
- DB_HOST=localhost
- DB_PORT=3306
- DB_DATABASE=climslara
- DB_USERNAME=root
- DB_PASSWORD=

### 5) Create and import database

```powershell
# Example using XAMPP mysql client
$mysql = "C:\xampp\mysql\bin\mysql.exe"
& $mysql -u root -e "CREATE DATABASE IF NOT EXISTS climslara CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
Get-Content -Raw ".\DATABASE FILE\climslara.sql" | & $mysql -u root climslara
```

## Run Application

```powershell
php artisan serve --host=127.0.0.1 --port=8000
```

Open:

- http://127.0.0.1:8000

## Default Login

- Username: admin
- Password: RAMSEY

## Update SQL Dump from Current DB

If you changed data/schema in local MySQL and want to replace `DATABASE FILE/climslara.sql`:

```powershell
$mysqldump = "C:\xampp\mysql\bin\mysqldump.exe"
$outFile = "D:\dead\ClinicMS-Laravel\DATABASE FILE\climslara.sql"
& $mysqldump -u root --databases climslara --routines --triggers --events --single-transaction --default-character-set=utf8mb4 | Set-Content -Encoding UTF8 $outFile
```

## Troubleshooting

### `composer install` fails with PHP version errors

Cause: terminal is using PHP 8.x.

Fix:

```powershell
$phpDir = Resolve-Path ".tools\php74\php"
$env:PATH = "$phpDir;$env:PATH"
php -v
composer install
```

### `Unknown database 'climslara'`

Database not created/imported yet. Run the database import step above.

### `php artisan serve` fails

Check:

- PHP 7.4 is active in current terminal (`php -v`)
- `vendor` exists (run `composer install`)
- database credentials in `.env` are correct

## Useful Commands

```powershell
# Laravel version
php artisan --version

# Clear caches
php artisan config:clear
php artisan cache:clear
php artisan route:clear
php artisan view:clear
```