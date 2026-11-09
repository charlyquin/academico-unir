# Laboratorio académico

Sitio estático para `academico.entornolab.cloud`. El índice vive en `site/index.html`.
Cada materia tiene una carpeta con su propio `index.html`. Sustituye
`site/gobierno-dato/index.html` por la página de la Actividad 2 y conserva
sus recursos junto a ella. Para recursos de una materia usa rutas relativas.

## Despliegue en la VPS

El DNS debe apuntar a la VPS de Hostinger. Nginx usa la red predeterminada de
Compose. El Traefik existente, que corre en modo `host`, descubre el servicio
mediante sus etiquetas de Docker y usa el resolver `letsencrypt`.

Clona el repositorio completo en la VPS, entra en su carpeta y ejecuta:

```sh
docker compose config --quiet
docker compose up -d
docker compose ps
curl --fail --show-error --silent --output /dev/null https://academico.entornolab.cloud/gobierno-dato/activity2/
```

El volumen `./site` se monta en modo de solo lectura. Se necesita el repositorio
completo en la VPS porque el YAML por sí solo no incluye los archivos del sitio.
Traefik recibe el tráfico HTTPS y Nginx sirve el índice y las carpetas.
