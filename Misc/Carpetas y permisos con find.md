Encontrar todas las carpetas que son **escribibles** para el usuario actual con el comando `find` junto con opciones para buscar directorios y comprobar sus permisos.

### 1. **Comando `find` básico para buscar directorios**:

El comando `find` te permite buscar archivos y directorios con criterios específicos. En este caso, queremos buscar directorios y verificar si son escribibles por el usuario actual.

Para buscar todos los directorios del sistema, puedes usar el siguiente comando:

```bash
find / -type d
```

Este comando buscará todos los directorios en el sistema, comenzando desde la raíz (`/`).

### 2. **Filtrar los directorios escribibles por el usuario actual:

Para encontrar solo aquellos directorios que son escribibles para el usuario actual, necesitas comprobar los permisos de los directorios. Una manera de hacerlo es utilizar `find` en combinación con `-perm` para filtrar por permisos de escritura.

Buscando todos los directorios en los que el usuario actual tenga permiso de escritura (independientemente de si es el propietario, el grupo o "otros"):

```bash
find / -type d -perm /u=w,g=w,o=w 2>/dev/null
```

**Explicación**:
- `/` : Inicia la búsqueda desde la raíz del sistema.
- `-type d` : Limita la búsqueda a directorios.
- `-perm /u=w,g=w,o=w` : Busca directorios donde los permisos de escritura estén habilitados para el propietario (`u=w`), el grupo (`g=w`) o "otros" (`o=w`).
- `2>/dev/null` : Redirige los errores (como los permisos denegados al acceder a ciertos directorios) al "null" para evitar mensajes de error innecesarios.

Este comando buscará **todos los directorios** con permisos de escritura para el usuario, el grupo o para otros usuarios.

**B.** Para limitar la búsqueda solo a los directorios donde el usuario `alexi` tenga permisos de escritura específicos, puedes usar el siguiente enfoque:

```bash
find / -type d -exec ls -ld {} \; 2>/dev/null | grep "w.*alexi"
```

**Explicación**:
- `find / -type d -exec ls -ld {} \;` : Esto ejecutará el comando `ls -ld` en cada directorio encontrado, lo cual muestra los detalles de permisos de los directorios.
- `grep "w.*pylon"` : Filtra las líneas que contienen la letra `w` (escritura) y la palabra "pylon", que indica que este directorio es escribible para el usuario `pylon`.

### 3. **Opciones adicionales**:

- Si deseas buscar solo los directorios donde el usuario `alexi` sea el **propietario** y tenga permisos de escritura, puedes usar:

```bash
find / -type d -user alexi -perm /u=w 2>/dev/null
```

Este comando limita la búsqueda a los directorios donde `pylon` sea el propietario y tenga permisos de escritura.

### Resumen de los pasos:

1. **Buscar directorios escribibles en general**:

   ```bash
   find / -type d -perm /u=w,g=w,o=w 2>/dev/null
   ```

2. **Buscar directorios escribibles donde el usuario actual sea el propietario**:

   ```bash
   find / -type d -user pylon -perm /u=w 2>/dev/null
   ```

3. **Buscar directorios escribibles para `alexi` con permisos generales** (usuario, grupo, o "otros"):

   ```bash
   find / -type d -exec ls -ld {} \; 2>/dev/null | grep "w.*alexi"
   ```
   