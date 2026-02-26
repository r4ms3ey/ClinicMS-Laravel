# ClinicMS-Laravel

Laravel 5.4 based clinic management system.

## Requirements

- Windows
- MySQL (XAMPP/Laragon/MySQL Server)
- Composer
- PHP 7.4 (this project includes a local runtime in `.tools/php74/php`)

## Quick Start (Windows)

1. Open PowerShell in the project root.
2. Use local PHP 7.4 for this session:

	```powershell
	$phpDir = Resolve-Path ".tools\php74\php"
	$env:PATH = "$phpDir;$env:PATH"
	php -v
	```

3. Install dependencies:

	```powershell
	composer install
	```

4. Create database and import SQL dump:

	```powershell
	# Example using XAMPP mysql client
	$mysql = "C:\xampp\mysql\bin\mysql.exe"
	& $mysql -u root -e "CREATE DATABASE IF NOT EXISTS climslara CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
	Get-Content -Raw ".\DATABASE FILE\climslara.sql" | & $mysql -u root climslara
	```

5. Ensure `.env` database values are correct:

	- DB_CONNECTION=mysql
	- DB_HOST=localhost
	- DB_PORT=3306
	- DB_DATABASE=climslara
	- DB_USERNAME=root
	- DB_PASSWORD=

6. Start the app:

	```powershell
	php artisan serve --host=127.0.0.1 --port=8000
	```

7. Open in browser:

	- http://127.0.0.1:8000

## Default Login

- Username: admin
- Password: RAMSEY

## Notes

- This codebase is Laravel 5.4 and is not compatible with modern PHP 8.x without package upgrades.
- If `composer install` fails on PHP 8.x, switch to the included PHP 7.4 runtime first.