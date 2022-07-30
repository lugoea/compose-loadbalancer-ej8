**1.- Iniciar la ejecución usando el siguiente comando**

PS C:\Users\elugo> docker-compose up --scale web=2

**2.- Validar los IDs de los containers para verificar el balanceo mas adelante**

PS C:\Users\elugo> docker ps
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS          PORTS                            NAMES
5af025f82fb9   nginx:latest                  "/docker-entrypoint.…"   29 seconds ago   Up 28 seconds   80/tcp, 0.0.0.0:8080->8080/tcp   nginx_nginx_1
dcfaee57675e   nicopaez/password-api:2.1.0   "docker-entrypoint.s…"   32 seconds ago   Up 29 seconds   3000/tcp                         nginx_web_2
eafbe7fcf04a   nicopaez/password-api:2.1.0   "docker-entrypoint.s…"   32 seconds ago   Up 29 seconds   3000/tcp                         nginx_web_1

**3.- Detener uno de los contenedores y utilizar el endpoint para ver cual instancia atiende el request**

PS C:\Users\elugo> docker stop eafbe7fcf04a
eafbe7fcf04a

**4.-Utilizar el endpoint para ver cual instancia atiende el request**

http://localhost:8080/health
{"host":"dcfaee57675e","loadavg":[0,0.0146484375,0],"freemem":203378688,"appversion":"2.1.0"}

**5.- Iniciar el contenedor detenido en el paso 3 y detener el otro que estaba aun ejecutandose**

PS C:\Users\elugo> docker start eafbe7fcf04a
eafbe7fcf04a

PS C:\Users\elugo> docker stop dcfaee57675e
dcfaee57675e

**6.- Utilizar el endpoint para ver cual instancia atiende el request**

http://localhost:8080/health
{"host":"eafbe7fcf04a","loadavg":[0.02978515625,0.04296875,0.00927734375],"freemem":192999424,"appversion":"2.1.0"}



