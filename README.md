# Iniciar Demo

## Usando Docker

---

1. Lanzaremos `docker-compose up -d`, para lanzar los servicios, a nivel de demo (donde se encuentra **docker-compose.yml**)
2. Accedemos al contenedor **container_app**, `docker exec -ti container_app`, para instalar las dependencias de la demo.
3. Descargamos las dependencias de la demo, `composer install`.
4. Ahora podrás acceder a tu [http://localhost/](http://localhost/), para ver el proyecto iniciado.

## Sin Docker

---

1. A nivel de demo (dónde se encuentra **composer.json**) ejecutaremos el comando, `composer install`.
2. Deberemos ejecutar `symfony server:start` para levantar nuestro servidor local [http://127.0.0.1:8000/](http://127.0.0.1:8000/).
3. Ahora podrás acceder a tu [http://127.0.0.1:8000/](http://127.0.0.1:8000/), para ver el proyecto iniciado.

## Componentes y Bundles Usados

---

* Profile Pack, `composer require symfony/profiler-pack`.
* Var Dumper, `composer require symfony/var-dumper`.
* MakerBundle, `composer require symfony/maker-bundle`.
* Doctrine Annotations, `composer require doctrine/annotations`.
* Twig Bundle, `composer require symfony/twig-bundle`.
* Symfony Assets, `composer require symfony/asset`.

> **Nota importante**: Las tecnologías webs avanzan a una gran velocidad sufriendo cambios a diario, por lo que puede ocurrir que al instalar un componente en tu proyecto, este esté depracado o simplemente haya cambiado de nombre, te animo a que en caso de error en la instalación de cualquier componente/bundle googlees el resultado obtenido.
> Al igual que avanza rápido, y ocurren cambios a diario, siempre hay alguien que ya ha encontrado la solución a tu problema. Aún así, siempre ante cualquier duda escribe al equipo, gustosamente te ayudará.