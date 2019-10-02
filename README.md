# Cifrado_transparente_ORACLE
El cifrado de datos transparente (TDE) te permite cifrar datos confidenciales que almacena en tablas y espacios de tablas.

Después de que los datos se cifran, estos datos se descifran de forma transparente para los usuarios o aplicaciones autorizados cuando acceden a estos datos. TDE ayuda a proteger los datos almacenados en los medios (también llamados datos en reposo) en caso de que se roben los medios de almacenamiento o el archivo de datos.

Oracle Database utiliza mecanismos de autenticación, autorización y auditoría para proteger los datos en la base de datos, pero no en los archivos de datos del sistema operativo donde se almacenan los datos. Para proteger estos archivos de datos, Oracle Database proporciona cifrado de datos transparente (TDE). TDE cifra los datos confidenciales almacenados en archivos de datos. Para evitar el descifrado no autorizado, TDE almacena las claves de cifrado en un módulo de seguridad externo a la base de datos, denominado almacén de claves.

## Tipos de cifrado 
El cifrado de datos transparente de Oracle admite dos modos de cifrado: el cifrado de espacios de tabla de TDE y el cifrado de columnas de TDE. El cifrado de espacios de tabla de TDE se utiliza para cifrar tablas de aplicaciones completas. El cifrado de columnas de TDE se utiliza para cifrar elementos de datos individuales que contienen información confidencial. También es posible aplicar una solución de cifrado híbrida que utilice tanto el cifrado de espacios de tabla como el cifrado de columnas de TDE.

# Keystore Externa (Hardware)
#### Configuración para sistema operativo Windows 10
### Paso 1: Establece el tipo de almacén de claves de hardware en el archivo sqlnet.ora

Nota:para configurar un almacén de claves de hardware, debes modificar el archivo sqlnet.ora. que se encuentra por default en el directório ORACLE_HOMEdb,para poder encontrar la ruta del directório ejecuta los siguientes comandos en la terminal:

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
Una vez localizado tu direcotrio ORACLE_HOMEdb
utiliza la siguiente configuración en el archivo sqlnet.ora para definir el tipo de almacén de claves de hardware, que es HSM(Hardware Security Model).

```
ENCRYPTION_WALLET_LOCATION=
 (SOURCE=
  (METHOD=HSM))
```


