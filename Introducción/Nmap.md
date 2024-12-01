Nmap escanea 1,000 puertos por defecto. Estos puertos son los más comunes y están definidos en el archivo "nmap-services" que viene incluido con Nmap.

Sin embargo, es importante destacar que Nmap puede ser configurado para escanear cualquier rango de puertos, incluyendo todos los 65,535 puertos posibles en un sistema TCP/IP.

Algunos ejemplos de cómo cambiar el rango de puertos escaneados en Nmap son:

- `-p 1-100`: Escanea los puertos del 1 al 100.
- `-p 100-200`: Escanea los puertos del 100 al 200.
- `-p-`: Escanea todos los puertos posibles (0-65535).
- `-p T:1-100,U:1-100`: Escanea los puertos TCP del 1 al 100 y los puertos UDP del 1 al 100.

El comando en Nmap para realizar un escaneo que identifique todos los puertos y servicios de un activo es:

`nmap -p- -sV <dirección_IP>`

Donde:

- `-p-` indica que se deben escanear todos los puertos posibles (0-65535).
- `-sV` activa la detección de versiones de servicios, lo que permite identificar los servicios y sus versiones que están ejecutándose en cada puerto.
- `<dirección_IP>` es la dirección IP del activo que se desea escanear.
- `-sS` realiza un escaneo de puertos SYN (half-open), que es rápido y evita establecer una conexión completa.

Este comando realizará un escaneo exhaustivo de todos los puertos y tratará de identificar los servicios y sus versiones que están ejecutándose en cada puerto abierto.

También se puede agregar la opción -T4 para acelerar el escaneo, o -v para obtener más información detallada.

Ejemplo: `nmap -p- -sV -T4 -v <dirección_IP>`
