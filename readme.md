1. ¿Por qué el frontend no necesita conectarse a PostgreSQL?
- No necesita conectarse a PostgreSQL, porque el frontend solo sirve la interfaz y envía las peticiones a la API, es el backend quien accede a los datos.

2. ¿Por qué el backend pertenece a dos redes?
- Porque es el puente entre ambas capas por seguridad.

3. ¿Qué servicio necesita publicar un puerto en el anfitrión?
- El frontend que es la interfaz que ve el usuario desde el navegador.

4. ¿Por qué publicar PostgreSQL hacia fuera no es la solución adecuada para un fallo de comunicación interno?
- Porque no arregla la causa, ya que la comunicacion utiliza la red de docker y es un riesgo exponer la base de datos fuera del entorno.

5. ¿Qué ventaja ofrece Docker Compose respecto a ejecutar los tres contenedores manualmente?
- Con ese comando levantamos todo el entorno de golpe, es mas cómodo, ya que reproduce el archivo compose.yaml para crear el mismo.

6. ¿Por qué hemos dividido la arquitectura en dos redes?
- Porque no queremos que el frontend se comunique o acceda a los datos por seguridad, se hara a través del backend.

7. ¿Por qué el backend utiliza `db` como dirección de PostgreSQL?
- Porque cada contenedor tiene su propio localhost, el nombre del servicio db no cambia, además la ip cambia al recrear el contenedor y el nombre no.

8. ¿Qué diferencia existe entre detener un proyecto y eliminar sus volúmenes?
- docker compose down elimina contenedores y redes, pero conserva el volumen y los datos. docker compose down -v elimina también el volumen, y con él todos los datos. Detener (stop) solo para los contenedores sin borrar nada.

9. ¿Qué consecuencias tendría para la empresa perder el volumen de PostgreSQL?
- Se perderían los datos, a menos que tengamos una copia de seguridad.

## Nota sobre la plataforma

Las imágenes `cloud-incidencias-backend:1.0` y `cloud-incidencias-frontend:1.0` solo están publicadas para `linux/arm64`. Por eso el `compose.yaml` incluye `platform: linux/arm64` en ambos servicios, y en equipos amd64 (como el mío) se ejecutan con emulación.