### 1. **Utilizando `socat` 
`Socat` es una herramienta similar a `netcat` y suele estar instalada en muchos sistemas. Puedes probar con `socat` de la siguiente manera:

#### En el servidor (172.17.0.1):
```bash
socat TCP-LISTEN:1234,fork FILE:secretitotraviesito.zip
```

#### En el cliente (172.17.0.3):
```bash
socat FILE:secretitotraviesito.zip TCP:172.17.0.1:1234
```

**Explicación:**
- El comando en el servidor escucha en el puerto `1234` y recibe los datos, redirigiéndolos al archivo `secretitotraviesito.zip`.
- El comando en el cliente transfiere el archivo `secretitotraviesito.zip` al servidor a través del puerto `1234`.

### 2. **Utilizando `bash` (por ejemplo, con redirección de sockets)**
Si no tienes herramientas adicionales, puedes usar bash y algunas redirecciones. Aquí hay un enfoque más rudimentario usando `bash` y `exec`:

#### En el servidor (172.17.0.1):
```bash
nc -lvp 1234 > secretitotraviesito.zip
```

#### En el cliente (172.17.0.3):
```bash
exec 3<>/dev/tcp/172.17.0.1/1234
cat secretitotraviesito.zip >&3
```

**Explicación:**
- En el cliente, la redirección `exec 3<>/dev/tcp/172.17.0.1/1234` establece una conexión TCP hacia el servidor.
- `cat secretitotraviesito.zip >&3` envía el archivo a través de esa conexión.

Este método no requiere instalaciones adicionales, pero depende de que el sistema soporte la funcionalidad de `/dev/tcp` (que está habilitada en la mayoría de distribuciones de Linux).

### 3. **Usando `dd` y `ssh` (si tienes acceso SSH al servidor)**
Si tienes acceso SSH a ambas máquinas, puedes usar `ssh` junto con `dd` para transferir archivos entre ellas.

#### En el cliente (172.17.0.3):
```bash
dd if=secretitotraviesito.zip | ssh usuario@172.17.0.1 'dd of=secretitotraviesito.zip'
```

**Explicación:**
- El comando `dd` lee el archivo `secretitotraviesito.zip` en el cliente y lo envía a través de `ssh` al servidor, donde otro `dd` escribe el archivo en el destino.

### 4. **Usando `tar` y `ssh` (si tienes acceso SSH)**
Otra alternativa es usar `tar` sobre SSH, que puede ser útil para comprimir el archivo y transferirlo en un solo paso:

#### En el cliente (172.17.0.3):
```bash
tar czf - secretitotraviesito.zip | ssh usuario@172.17.0.1 'tar xzf - -C /ruta/de/destino'
```

**Explicación:**
- `tar czf - secretitotraviesito.zip` comprime el archivo en el cliente y lo envía a través de `ssh` al servidor, donde se descomprime y almacena en la ruta de destino.

### 5. **Usando `python` como servidor y cliente**
Si tienes Python instalado en ambas máquinas, puedes usar Python para transferir archivos de manera sencilla. El cliente puede usar el siguiente comando:

#### En el servidor (172.17.0.1):
```bash
python3 -m http.server 1234
```

#### En el cliente (172.17.0.3):
```bash
curl -O http://172.17.0.1:1234/secretitotraviesito.zip
```

**Explicación:**
- En el servidor, `python3 -m http.server 1234` inicia un servidor HTTP en el puerto `1234`.
- En el cliente, `curl -O` descarga el archivo desde el servidor a través de HTTP.

### 6. **Usando `wget` o `curl` para transferencias HTTP**
Si tienes una pequeña infraestructura de servidor web (como `python -m http.server`), puedes usar `wget` o `curl` en el cliente para descargar el archivo.

#### En el servidor (172.17.0.1), puedes usar `python` como servidor HTTP:
```bash
python3 -m http.server 1234
```

#### En el cliente (172.17.0.3):
```bash
curl -O http://172.17.0.1:1234/secretitotraviesito.zip
```

O si prefieres `wget`:
```bash
wget http://172.17.0.1:1234/secretitotraviesito.zip
```

### 7. Estableciendo conexión TCP
Desde el host que comparte el archivo, la redirección  establece una conexión TCP hacia el servidor.
Posteriormente se envía el archivo a través de esa conexión.

#### En el servidor
```bash
nc -lvp PORT > secretitotraviesito.zip
```
#### En el cliente (172.17.0.3):
```bash
exec 3<>/dev/tcp/<IP_destino>/PORT

cat secretitotraviesito.zip >&3
```