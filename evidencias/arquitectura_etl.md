# Arquitectura

### Contenedores activos
```
NAMES\         IMAGE\                PORTS\                                                                                      STATUS
odoo.18\       odoo:18.0\            0.0.0.0:8001->8069/tcp, [::]:8001->8069/tcp, 0.0.0.0:8002->8072/tcp, [::]:8002->8072/tcp\   
Up 31 minutes
postgres.db\   postgres:16-alpine\   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp\
Up 31 minutes
```
### Network

```
NETWORK ID     NAME                     DRIVER    SCOPE
5a9c92bc9280   uf1886-e2-noel_default   bridge    local
```
### Volume

```
DRIVER    VOLUME NAME
local     uf1886-e2-noel_odoo-db-data
local     uf1886-e2-noel_odoo-web-data

```
### Recursos del host

```
Name                      : 11th Gen Intel(R) Core(TM) i5-1135G7 @ 2.40GHz
NumberOfCores             : 4
NumberOfLogicalProcessors : 8
MaxClockSpeed             : 2419
AddressWidth              : 64

TotalRAM(GB) FreeRAM(GB)
------------ -----------
       15,74        6,16

```

### Arquitectura lógica

```
docker port odoo.18
```
```
8069/tcp -> 0.0.0.0:8001
8069/tcp -> [::]:8001
8072/tcp -> 0.0.0.0:8002
8072/tcp -> [::]:8002
```
```
docker port postgres.db
```
```
5432/tcp -> 0.0.0.0:5432
5432/tcp -> [::]:5432
```

### Confirmar Apache Hop está en el host
```
hop-conf.bat -v
```
```
===[Environment Settings - hop-conf.bat]===================================

Java identified as java

HOP_OPTIONS=-Xmx2048m -DHOP_AUDIT_FOLDER=.\audit -DHOP_PLATFORM_OS=Windows -DHOP_PLATFORM_RUNTIME=Conf -DHOP_AUTO_CREATE_CONFIG=Y --add-opens java.xml/jdk.xml.internal=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.lang.invoke=ALL-UNNAMED --add-opens java.base/java.lang.reflect=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.util.concurrent=ALL-UNNAMED --add-opens java.base/java.util.concurrent.atomic=ALL-UNNAMED --add-opens java.base/sun.nio.ch=ALL-UNNAMED --add-opens java.base/sun.nio.cs=ALL-UNNAMED --add-opens java.base/sun.security.action=ALL-UNNAMED --add-opens java.base/sun.util.calendar=ALL-UNNAMED --add-opens java.security.jgss/sun.security.krb5=ALL-UNNAMED --add-exports java.base/sun.nio.ch=ALL-UNNAMED

Command to start Hop will be:
java -classpath lib\core\*;lib\beam\*;lib\swt\win64\* -Djava.library.path=lib\core;lib\beam -Xmx2048m -DHOP_AUDIT_FOLDER=.\audit -DHOP_PLATFORM_OS=Windows -DHOP_PLATFORM_RUNTIME=Conf -DHOP_AUTO_CREATE_CONFIG=Y --add-opens java.xml/jdk.xml.internal=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.lang.invoke=ALL-UNNAMED --add-opens java.base/java.lang.reflect=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.util.concurrent=ALL-UNNAMED --add-opens java.base/java.util.concurrent.atomic=ALL-UNNAMED --add-opens java.base/sun.nio.ch=ALL-UNNAMED --add-opens java.base/sun.nio.cs=ALL-UNNAMED --add-opens java.base/sun.security.action=ALL-UNNAMED --add-opens java.base/sun.util.calendar=ALL-UNNAMED --add-opens java.security.jgss/sun.security.krb5=ALL-UNNAMED --add-exports java.base/sun.nio.ch=ALL-UNNAMED org.apache.hop.config.HopConfig -v

===[Starting HopConfig]=========================================================
2.16.0
```






