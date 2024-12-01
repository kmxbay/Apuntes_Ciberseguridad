### Métricas de Explotabilidad

Al evaluar las métricas de Base, se debe suponer que el atacante ha avanzado conocimiento del sistema de destino, incluida la configuración general y el valor predeterminado mecanismos de defensa (por ejemplo, firewalls incorporados, límites de tarifas, vigilancia de tráfico).

### Vector de Ataque (AV)

Contexto por el cual la explotación de la vulnerabilidad es posible.

Será más grande en cuanto más remoto sea (lógica y físicamente) puede estar en orden un atacante explotar el sistema vulnerable.

Suponemos que el número de atacantes desde una red es mayor que el número de atacantes que podrían requerir acceso físico a un dispositivo, y por lo tanto garantiza una mayor severidad.

Al decidir entre Network y Adjacent, revisamos si un ataque se puede lanzar a través de una red de área amplia o desde fuera del lógicamente adyacente dominio de red administrativa.

| Network (N)  | El sistema está conectado a la red, cualquier persona desde Internet puede intentar atacarlo.<br><br>Vulnerabilidad "explotable de forma remota"<br><br>El atacante puede explotarlo sin necesidad de estar cerca, incluso atravesando varios enrutadores.<br><br>Por ejemplo enviando un paquete TCP modificado a través de Internet para interrumpir el servicio (CVE-2004-0230). |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Adjacent (A) | El sistema vulnerable está conectado a una red, pero el ataque solo puede ocurrir dentro de una red cercana o compartida, como Bluetooth, Wi-Fi o una subred local.<br><br>Por ejemplo un ataque ARP o de descubrimiento vecino que cause una denegación de servicio en la red local (CVE-2013-6014).                                                                               |
| Local (L)    | El sistema vulnerable no está relacionado con la red, y los atacantes pueden aprovechar la vulnerabilidad al acceder localmente (teclado, consola o terminal SSH).<br><br>También a través de ingeniería social, para realizar la explotación.                                                                                                                                      |
| Physical (P) | El ataque requiere que el atacante tenga acceso físico al sistema vulnerable.<br><br>Por ejemplo un ataque de arranque en frío, donde el atacante obtiene las claves de cifrado del disco por acceso físico.                                                                                                                                                                        |

### Complejidad de Ataque (AC)

Acciones que el atacante toma para sortear medidas de seguridad del sistema (medidas de seguridad diseñadas para dificultar el ataque).

Un sistema con más barreras de seguridad (como tener que personalizar el exploit) es más complejo de explotar que uno sin estas medidas.

Esta métrica se enfoca en las protecciones del sistema no en el tiempo o número de intentos que el atacante necesita para tener éxito.

La evasión de mecanismos de autenticación o el conocimiento detallado del sistema es fuera del alcance de la Complejidad de Ataque se evalúa por separado, en términos de privilegios requeridos, y no se considera aquí.

| Bajo (L) | El atacante no necesita tomar ninguna acción medible para explotar la vulnerabilidad.<br><br>Se puede esperar un éxito repetible contra el sistema vulnerable.                                                                                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alto (H) | El éxito del ataque depende de eludir las medidas de seguridad que impiden la explotación.<br><br>Además, el atacante puede necesitar información específica del objetivo (como claves criptográficas). Secretos que no se obtienen  solo con reconocimiento, implicando pasos adicionales o romper medidas de seguridad adicionales. |

### Requisitos de Ataque (AT)

Esta métrica se refiere a las condiciones previas del sistema vulnerable que permiten el ataque.

A diferencia de las medidas de seguridad, estas condiciones no están diseñadas para mitigar ataques, sino que surgen de cómo se implementa y ejecuta el sistema.

Si el atacante no supera estas condiciones, el ataque puede tener éxito solo de manera ocasional o no tener éxito en absoluto.

| Ninguno (N)  | El ataque exitoso no depende de condiciones de implementación y ejecución del sistema vulnerable.<br><br>Se espera explotar la vulnerabilidad en todas o la mayoría de las instancias de esta. |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Presente (P) | El éxito del ataque depende de condiciones específicas del sistema vulnerable. (Condición de carrera, Condiciones de ejecución, Inyección de red)                                              |

### Privilegios Requeridos (PR)

Esta métrica se refiere al nivel de privilegios que un atacante debe poseer anterior a explotar con éxito la vulnerabilidad.

Por ejemplo, el privilegio que otorgan las cuentas de prueba gratuitas está fuera del alcance de esta métrica.

| Ninguno (N) | El atacante no está autenticado antes del ataque , es decir, no requiere ningún acceso a la configuración o los archivos del sistema vulnerable para llevar a cabo un ataque. |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bajo (L)    | El atacante ocupa privilegios con capacidades básicas que tengan configuraciones y recursos de un solo usuario de bajo privilegio (acceso a recursos no sensibles).           |
| Alto (H)    | El atacante requiere privilegios que proporcionen un control significativo a la configuración y los archivos de los sistemas vulnerables.                                     |

### Interacción del Usuario (UI)

Esta métrica captura el requisito para un usuario humano, que no sea el atacante participar en el compromiso del sistema.

Esta métrica determina si la vulnerabilidad puede ser explotada únicamente a voluntad del atacante, o si un usuario separado debe participa de alguna manera.

La puntuación resultante es mayor cuando no hay usuario se requiere interacción.

| Ninguno (N) | El sistema vulnerable puede ser explotado sin la interacción de ningún usuario humano, aparte del atacante                                                                                                                                                                 |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bajo (L)    | La explotación exitosa requiere una interacción limitada del usuario objetivo con el sistema vulnerable. Estas interacciones se considerarían involuntarias y no requieren que el usuario subvierta activamente las protecciones integradas en el sistema vulnerable       |
| Alto (H)    | La explotación requiere que un usuario objetivo realice interacciones específicas y conscientes con el sistema vulnerable o las interacciones de los usuarios subvertirían activamente los mecanismos de protección que conducirían a la explotación de la vulnerabilidad. |

## Métricas de Impacto

Al evaluar el impacto de una vulnerabilidad, se debe usar el impacto final, no el cambio intermedio. Por ejemplo, si un atacante comienza con acceso limitado a la confidencialidad y luego obtiene acceso completo, el impacto final debe ser el de "Confidencialidad Alta".

Al asignar valores de impacto, los evaluadores deben considerar tanto los efectos en el sistema vulnerable como en los sistemas relacionados.

Un "sistema de interés" se define como un conjunto de componentes que operan juntos para cumplir una función con políticas de seguridad comunes. Cuando un sistema depende de otro, ambos se consideran parte del sistema vulnerable. Por ejemplo, una base de datos que solo sirve a un altavoz inteligente se considera parte de ese sistema.

Si una vulnerabilidad no afecta a otros sistemas, el impacto externo se considera "Ninguno". Además, los impactos fuera del sistema vulnerable, como los efectos en los humanos, deben reflejarse en las métricas del impacto del sistema posterior.

### Confidencialidad (VC)

La confidencialidad se refiere a limitar el acceso a la información y la divulgación a usuarios autorizados.

Esta métrica mide el impacto en la confidencialidad de la información gestionado por el sistema debido a una vulnerabilidad explotada con éxito.

La puntuación resultante es mayor cuando la pérdida para el sistema es más alta.

| Alto (H)    | Hay una pérdida total de confidencialidad, toda la información dentro del Sistema Vulnerable se divulgue al atacante.<br><br>O se obtiene acceso solo a cierta información restringida con un impacto directo y grave.                                                     |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bajo (L)    | La explotación requiere una interacción limitada del usuario objetivo con el sistema vulnerable. Estas interacciones se \|considerarían involuntarias y no requieren que el usuario subvierta activamente las protecciones integradas en el sistema vulnerable             |
| Ninguno (N) | La explotación requiere que un usuario objetivo realice interacciones específicas y conscientes con el sistema vulnerable o las interacciones de los usuarios subvertirían activamente los mecanismos de protección que conducirían a la explotación de la vulnerabilidad. |

## Encuesta CVSS 4.0

![[Pasted image 20241130235858.png]]

![[Pasted image 20241130235940.png]]

![[Pasted image 20241201000004.png]]

![[Pasted image 20241201000014.png]]

![[Pasted image 20241201000021.png]]

![[Pasted image 20241201000032.png]]

![[Pasted image 20241201000043.png]]

![[Pasted image 20241201000051.png]]

