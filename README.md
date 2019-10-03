# Cifrado_transparente_ORACLE
El cifrado de datos transparente (TDE) te permite cifrar datos confidenciales que almacena en tablas y espacios de tablas.
Después de que los datos se cifran, estos datos se descifran de forma transparente para los usuarios o aplicaciones autorizados cuando acceden a estos datos. TDE ayuda a proteger los datos almacenados en los medios (también llamados datos en reposo) en caso de que se roben los medios de almacenamiento o el archivo de datos.

Oracle Database utiliza mecanismos de autenticación, autorización y auditoría para proteger los datos en la base de datos, pero no en los archivos de datos del sistema operativo donde se almacenan los datos. Para proteger estos archivos de datos, Oracle Database proporciona cifrado de datos transparente (TDE). TDE cifra los datos confidenciales almacenados en archivos de datos. Para evitar el descifrado no autorizado, TDE almacena las claves de cifrado en un módulo de seguridad externo a la base de datos, denominado almacén de claves.

## Tipos de cifrado 
El cifrado de datos transparente de Oracle admite dos modos de cifrado: el cifrado de espacios de tabla de TDE y el cifrado de columnas de TDE. El cifrado de espacios de tabla de TDE se utiliza para cifrar tablas de aplicaciones completas. El cifrado de columnas de TDE se utiliza para cifrar elementos de datos individuales que contienen información confidencial. También es posible aplicar una solución de cifrado híbrida que utilice tanto el cifrado de espacios de tabla como el cifrado de columnas de TDE.

# Keystore (Software)
#### Configuración para sistema operativo Windows 10
Debes definir una ubicación para ello en el archivo sqlnet.ora. Hay un almacén de claves por base de datos, y la base de datos localiza este almacén de claves comprobando la ubicación del almacén de claves que define en el archivo sqlnet.ora.
### Paso1: Crea un directorio para el almacen de claves(keystore) en alguna parte de tu elección dentro del directorio de oracle y copia la ruta a ese directorio ya que esa ruta la ocuparas en el paso 2 .

### Paso 2: Establece la ubicación del almacén de claves de software en el archivo sqlnet.ora
para configurar un almacén de claves de software, debes modificar el archivo sqlnet.ora. que se encuentra por default en el directório ORACLE_HOMEdb\network\admin,para poder encontrar la ruta del directório ORACLE_HOMEdb ejecuta los siguientes comandos en la terminal:
#### Nota:Asegurate de que este directorio existe de antemano. Preferentemente, este directorio debe estar vacío.

```
sqlplus / as sysdba  
```

```
var OHM varchar2(100); 
```

```
EXEC dbms_system.get_env('ORACLE_HOME', :OHM) ; 
```

```
PRINT OHM
```

Una vez localizado tu direcotrio ORACLE_HOMEdb tienes dos opciones: 

1.-copia la ruta y pegala en la barra de navegación del explorador de archivos agregandole la ruta de \network\admin. 

2.-copia la ruta y pegala en la terminal añadiendo los subdirectorios \network\admin y usa el comando 
```
notepad sqlnet.ora
```
Para crear un almacén de claves de software en un sistema de archivos , usa el siguiente formato cuando edites el archivo sqlnet.ora .
En el formato siguiente en la parte de DIRECTORY = sustituye path_to_keystore con tu ruta a tu directorio que creaste en el paso1.

```
ENCRYPTION_WALLET_LOCATION=
 (SOURCE=
  (METHOD=FILE)
   (METHOD_DATA=
    (DIRECTORY=path_to_keystore)))
```
### Paso 3: Después de haber especificado una ubicación de directorio para el almacén de claves de software,puedes crear el almacén de claves.

-Almacenes de claves de software basados en contraseña

-Almacenes de claves de software de inicio de sesión automático

-Almacenes de claves de software de inicio de sesión automático local

Inicia sesión en la instancia de la base de datos como SYSKM 

```
sqlplus sys/password as sysdba
```
puedes verificar tu usuario con el siguiente comando
```
show user
```
Usa el siguiente comando para crear tu keystore :D
remplaza 'path/keystore' con tu ruta del directorio donde deseas crear tu key store
Asegurate de guardar bien tu contraseña ya que la utilizaremos posteriormente.
```
SQL> ADMINISTER KEY MANAGEMENT CREATE KEYSTORE 'C:path/Keystore' IDENTIFIED BY "password";
```
Debes de tener como respuesta un mensaje de ...
```
almacen de claves modificado
```
Despúes de que corras el comando anterior se habra creado un archivo llamado. 

```
ewallet
```

OPCIONALMENTE puedes crear un Auto-login para evitar el acceso manual cada que quieras hacer algún cambio

```
ADMINISTER KEY MANAGEMENT CREATE LOCAL AUTO_LOGIN KEYSTORE FROM KEYSTORE 'keystore_location' IDENTIFIED BY password;
```

### Paso 4:Abre la keystore
```
ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN IDENTIFIED BY "password";
```

