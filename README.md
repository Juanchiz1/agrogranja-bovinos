# AgroGranja Bovinos

Aplicación web para la gestión integral de fincas ganaderas y agrícolas, pensada para pequeños y medianos productores de San Pelayo, Córdoba. Cubre el trabajo diario de la finca (cultivos, animales, gastos, ingresos, tareas y reportes) y tiene un submódulo especializado para ganado bovino.

Proyecto de la materia Desarrollo Web 2, Universidad de Córdoba. Se desarrolló con metodología en cascada y especificación de requisitos según IEEE 830.

## Stack

- PHP 8.2 + Laravel 10
- MySQL 8 (tests con SQLite en memoria)
- Vistas Blade con diseño mobile-first, pensado para conexiones lentas y pantallas pequeñas
- barryvdh/laravel-dompdf (PDF) y PhpSpreadsheet (Excel)
- Cloudinary para las fotos en producción; en local se guardan en disco
- PHPUnit
- Despliegue en Railway con Nixpacks

## Módulos

| Módulo | Qué permite |
|---|---|
| Autenticación | Registro, inicio de sesión y onboarding para elegir las líneas productivas de la finca |
| Cultivos | Lotes, fotos, eventos, fases fenológicas y rendimiento. Los eventos descuentan insumos del inventario y pueden generar gastos |
| Animales | Inventario, pesajes, eventos, propietarios y salidas |
| Bovino | Ordeños, lactancias, servicios, preñez, partos, plan sanitario, pesajes y venta de producción |
| Gastos e ingresos | Proveedores, clientes y gastos recurrentes; los gastos se enlazan con inventario y nómina |
| Inventario | Insumos con movimientos de entrada/salida y alertas de stock bajo |
| Personas | Trabajadores, labores y pagos |
| Tareas | Calendario interactivo con las tareas de cada día |
| Reportes | PDF de cultivos, gastos, cosechas, animales, nómina, inventario, rentabilidad y producción; Excel de cultivos, gastos y cosechas |

## Correr el proyecto en local

Requisitos: PHP 8.2+, Composer y MySQL.

```bash
composer install
cp .env.example .env
php artisan key:generate
```

Crea una base de datos `agrogranja` en MySQL, ajusta las variables `DB_*` del `.env` y luego:

```bash
php artisan migrate
php artisan serve
```

La aplicación queda en http://localhost:8000. Crea una cuenta desde `/register`; el onboarding te pide los datos de la finca y las líneas productivas.

## Tests

```bash
vendor/bin/phpunit
```

Los tests usan SQLite en memoria (configurado en `phpunit.xml`). Hay tests de feature para autenticación, animales, bovinos, cultivos, gastos, ingresos y tareas.

## Despliegue

`nixpacks.toml` instala PHP 8.2 y las dependencias de Composer. Al arrancar, `start.sh` genera el `.env` a partir de las variables de entorno de Railway (base de datos y credenciales de Cloudinary), corre las migraciones y levanta el servidor.

## Proyectos relacionados

- [agrogranja-laravel](https://github.com/Juanchiz1/agrogranja-laravel): versión completa, con líneas avícola, porcícola y piscícola.
- [agrogranja-mobile](https://github.com/Juanchiz1/agrogranja-mobile): app móvil con base de datos local para trabajar sin conexión.

## Autor

**Juan Diego Negrete Portillo**
Estudiante de Ingeniería de Sistemas — Universidad de Córdoba
[Portafolio](https://juanchiz1.github.io/Portafolio-Juan_Diego_Negrete/) · [LinkedIn](https://www.linkedin.com/in/juan-diego-negrete-portillo-352111195/) · [GitHub](https://github.com/Juanchiz1)
