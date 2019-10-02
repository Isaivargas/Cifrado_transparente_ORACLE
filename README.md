# Cifrado_transparente_ORACLE

El cifrado de datos transparente de Oracle admite dos modos de cifrado: el cifrado de espacios de tabla de TDE y el cifrado de columnas de TDE. El cifrado de espacios de tabla de TDE se utiliza para cifrar tablas de aplicaciones completas. El cifrado de columnas de TDE se utiliza para cifrar elementos de datos individuales que contienen información confidencial. También es posible aplicar una solución de cifrado híbrida que utilice tanto el cifrado de espacios de tabla como el cifrado de columnas de TDE.

# Keystore Externa (Hardware)
Paso 1: establece el tipo de almacén de claves de hardware en el archivo sqlnet.ora
Nota:para configurar un almacén de claves de hardware, debes modificar el archivo sqlnet.ora.



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
