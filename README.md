# Cifrado_transparente_ORACLE

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
