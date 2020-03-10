##########################
### Instalar Oracle 12 ###
##########################

docker pull truevoly/oracle-12c
mkdir ~/oracle_data
docker run -d -p 8080:8080 -p 1521:1521 -v ~/oracle_data/:/u01/app/oracle truevoly/oracle-12c

# Prepare Oracle enviroment. TEST.
# Correr scripts.


#####################################
### Buildear la imagen Docker/EAR ###
#####################################
# Ir a la carpeta /witbor-docker
# Previo debemos colocar en la carpeta ear la ùltima version del ear, que será el que se deploye en el conenedor.
  
# Armar la imagen para despeglar en contenedor
docker build .

# Buscar la imagen generada
docker images

# Levantar un contenedor desde la imagen anteriormente creada.
# ORACLE_CONNECTION="jdbc:oracle:thin:@//192.168.31.107:1521/xe" Pasamos como parametro los datos de la conexion a la base de datos. Puede ser local remota o estar en otro docker.
# ORACLE_USER="tyc" Pasamos como parámetro el usuario de la base Oracle. 
# ORACLE_PASWORD="tyc" Pasamos como parámetro el usuario de la base Oracle. 
# 8081:8080 Ruteamos el puerto 8081 del host al 8080 del wildfly en docker. Por este puerto es donde accederemos a la app. (http://localhost:8081/tyc/ecomm/om/) 
# 9990:9990 Ruteamos el puerto 9990 del host al 9990 del wildfly en docker. Este puerto es utilizado para adminsitrar wildfly en caso de ser necesario. (http://localhost:9990 login con user:admin pass:adm1n) 
# 8443:8443 Ruteamos el puerto 8443 del host al 8443 del wildfly en docker. Puerto para acceso https.
# 7777:7777 Ruteamos el puerto 7777 del host al 7777 del wildfly en docker. Puerto debug de la aplicaciòn.

docker run -d -e ORACLE_CONNECTION="jdbc:oracle:thin:@//192.168.31.107:1521/xe" -e ORACLE_USER="tyc" -e ORACLE_PASWORD="tyc" -p 8081:8080 -p 9990:9990 -p 8443:8443 -p 7777:7777 imageid












@OneToMany(fetch = FetchType.EAGER, mappedBy = "order", cascade = CascadeType.ALL)
private List<OrderItem> orderItems = new ArrayList<>();

 @OneToMany(fetch = FetchType.EAGER, mappedBy = "orderItem", cascade = CascadeType.ALL)
private List<OrderItemAddon> orderItemAddons = new ArrayList<>();