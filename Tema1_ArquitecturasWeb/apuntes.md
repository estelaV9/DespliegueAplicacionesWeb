# Tema 1: Arquitecturas Web

> [!NOTE]
> [Test](https://github.com/estelaV9/DespliegueAplicacionesWeb/blob/master/Tema1_ArquitecturasWeb/test_inicial.md) inicial del tema


## 1. Internet 
**Internet** es una red global de redes que conecta a miles de millones de nodos en todo el mundo. Se compone de:
- Un conjunto de nodos (equipos) conectados en forma de malla parcial
- Un conjunto de protocolos para comunicar dichos nodos, donde cada protocolo permite ofrecer un servicio o parte de él
- Diseño inicial cliente/servidor, donde los equipos intermedios conectan con los equipos finales

### 1.1 Protocolo TCP/IP 
**TCP/IP** es el conjunto de protocolos de red que funciona como base de Internet, permitiendo la comunicación entre dispositivos. Cada host se identifica mediante una **dirección IP**, y para conectar con las aplicaciones dentro de ese host se utilizan los **puertos** (por ejemplo, FTP: 20/21, SSH: 22, HTTP: 80, HTTPS: 443).
 
El modelo TCP/IP divide los datos en paquetes según cuatro capas. Los datos atraviesan estas capas en un sentido al enviarse y en sentido contrario al recomponerse en el destino (**encapsulación de datos**):
| Capa | Protocolos |
|---|---|
| **Aplicación** | HTTP, HTTPS, TLS, FTP, DNS, SSH... |
| **Transporte** | TCP y UDP |
| **Red** | IP |
 
> La información transmitida por una red puede estudiarse con un analizador de paquetes (p. ej. Wireshark)
 
### 1.2 Protocolos de la capa de aplicación
| Protocolo | Función |
|---|---|
| **FTP** | Transferencia de archivos de manera interactiva entre sistemas |
| **DNS** | Resuelve nombres de Internet en direcciones IP |
| **Telnet** | Acceso remoto a servidores y dispositivos de red (sin cifrar) |
| **SSH** | Conexión remota por terminal (cifrada) |
| **HTTP** | Transfiere los archivos que forman las páginas web |
| **SMTP/POP/IMAP** | Correo electrónico: SMTP para enviar, POP e IMAP para recibir |
| **DHCP** | Asigna direcciones IP a los dispositivos de red de forma dinámica y temporal |
| **SMB** | Protocolo cliente-servidor de solicitud-respuesta para compartir archivos |
 
Para que la comunicación sea exitosa, el protocolo de capa de aplicación implementado en el host de origen debe coincidir con el del host de destino, ya que establecen las reglas para intercambiar datos entre aplicaciones y servicios.
 
### 1.3 URL (Localizador Uniforme de Recursos)
Una **URL** es la secuencia estándar de caracteres que identifica y permite localizar y recuperar un recurso en Internet — es la "dirección" que escribimos en el navegador. Cada recurso (imagen, vídeo, texto, página) tiene su propia URL, incluso los que forman parte de una misma página
 
**Partes de una URL:**
| Parte | Descripción |
|---|---|
| **Protocolo de red** | http, https, mailto, ftp: indica el tipo de conexión y el lenguaje que se usará |
| **Subdominio** | Por ejemplo, www (ya no es obligatorio y puede omitirse) |
| **Top Level Domain (TLD)** | Extensión final del dominio: .com, .es, .org, .net, .info, etc |
| **Subdirectorio/subcarpeta** | Carpeta dentro de un dominio usada para agrupar contenido por categorías (p. ej. /blog/) |
| **Nombre del archivo, página o slug** | Identifica el contenido concreto de esa página |
 
**URL y SEO:** según un estudio de Backlinko sobre más de 200 factores de posicionamiento en Google, los relacionados con la URL ocupan puestos relativamente bajos en importancia: longitud (#51), ruta (#52), palabras clave (#55) y cadena (#56)
 
<br>
 
## 2. Protocolo HTTP
### 2.1 Características
- Permite el servicio WWW
- Desarrollado por el W3C y la Internet Engineering Task Force
- El servidor HTTP atiende peticiones en el puerto 80 (HTTPS, su versión segura, en el 443)
- La versión más usada es HTTP/1.1 (RFC 2616); existe también HTTP/2, aún poco extendida
- Es un **protocolo sin estado**: no guarda información sobre conexiones anteriores (para ello se usan cookies y variables de sesión)

### 2.2 Transacción HTTP
| Ejemplo de una petición | Ejemplo de una respuesta |
|---|---|
| `GET /index.html HTTP/1.1`<br>`Host: www.example.com` | `HTTP/1.1 200 OK`<br>`Date: Mon, 23 May 2005 22:38:34 GMT`<br>`Content-Type: text/html; charset=UTF-8`<br>`Content-Length: 138`<br>`Server: Apache/1.3.3.7 (Unix)`<br>`Connection: close` |
 
### 2.3 Métodos HTTP
| Método | Función |
|---|---|
| **GET** | Solicita un recurso (p. ej. un HTML) al servidor; solo debe obtener datos, sin modificarlos |
| **POST** | Envía al servidor paquetes de datos grandes o privados (formularios, imágenes); a diferencia de GET, los datos no viajan visibles en la URL |
| **PUT** | Actualiza información existente (equivalente a un UPDATE); es **idempotente**: ejecutarlo varias veces produce el mismo resultado |
| **DELETE** | Elimina un recurso específico (equivalente a un DELETE de base de datos); también es idempotente |
| **Otros** | HEAD, OPTIONS, CONNECT, PATCH, TRACE |
 
### 2.4 Códigos de respuesta HTTP
| Rango | Significado |
|---|---|
| **1xx** | Mensajes informativos |
| **2xx** | Operación exitosa |
| **3xx** | Redirección |
| **4xx** | Errores del cliente |
| **5xx** | Errores del servidor |
 
### 2.5 Cabeceras HTTP
Fragmentos de información (metadatos) que se envían en cada petición/respuesta: tipo de agente de usuario, autenticación de seguridad, caché, etc.
 
**En la petición (Request):**
| Cabecera | Ejemplo | Descripción |
|---|---|---|
| Accept | `text/html` | Tipos de contenido admitidos como respuesta |
| Accept-Charset | `utf-8` | Juegos de caracteres admitidos |
| Accept-Encoding | `gzip, deflate` | Codificaciones (compresión) admitidas |
| Accept-Language | `en-US` | Idiomas admitidos como respuesta |
| Host | `en.wikipedia.org:8080` | Dominio del servidor (y puerto si no es el 80) |
| User-Agent | `Mozilla/5.0...` | Identifica al agente de usuario (navegador) |
 
**En la respuesta (Response):**
| Cabecera | Ejemplo | Descripción |
|---|---|---|
| Content-Encoding | `gzip` | Codificación de los datos enviados |
| Content-Language | `es` | Idioma del contenido |
| Content-Type | `text/html; charset=utf-8` | Tipo MIME del contenido |
| Server | `Apache/2.4.1 (Unix)` | Servidor web utilizado |
| Status | `200 OK` | Código de estado |
 
### 2.6 Tipos MIME
Los **tipos MIME** (Multipurpose Internet Mail Extension) son la manera estándar de indicar qué tipo de datos contiene un archivo transmitido por la red
| Tipo MIME | Contenido |
|---|---|
| text/plain | Texto plano |
| text/html | Texto en formato HTML |
| text/css | Hoja de estilo CSS |
| application/javascript | Código JavaScript |
| application/json | Datos en formato JSON |
| image/jpeg, image/png, image/svg+xml | Imágenes |
| audio/ac3, audio/ogg | Audio |
| video/H264 | Vídeo |
 
> El JSON se transmite como datos pero se clasifica dentro de `application`
 
<br>
 
## 3. W3C: estandarización
El **W3C (World Wide Web Consortium)** es el organismo, fundado en 1994, encargado de desarrollar estándares web internacionales (HTML, CSS y más), llamados **"Recomendaciones del W3C"**. Su misión es guiar la web hacia su máximo potencial promoviendo su evolución e interoperabilidad

Aunque no tiene el mismo peso legal que organismos como ISO, sus recomendaciones son estándares de facto, con la misma consideración práctica que un estándar oficial, pese a estar compuesto principalmente por empresas con intereses en el sector (Microsoft, Google, Apple, Opera, Mozilla)
 
<br>
 
## 4. Aplicaciones web
### 4.1 Aplicaciones de escritorio vs. web
| | Escritorio | Web |
|---|---|---|
| **Ejecución** | Requiere instalación en un SO específico | Se accede mediante navegador, sin instalación |
| **Rendimiento** | Depende del hardware local; mayor potencia | Menor potencia; no aprovecha el hardware local |
| **Actualización** | Difícil, costosa e incompatible entre versiones | Centralizada en el servidor; siempre última versión |
| **Datos** | Locales | Centralizados en el servidor |
| **Movilidad** | Limitada al equipo instalado | Accesible desde cualquier ubicación y SO con navegador |
| **Coste** | Elevado | Menor |
| **Requisito clave** | — | Necesita conectividad rápida y constante |
 
### 4.2 Arquitectura cliente-servidor y capas
Las aplicaciones web se basan en la arquitectura **cliente-servidor**: el cliente accede mediante el navegador, y el servidor procesa las peticiones ejecutando la lógica de negocio y el acceso a datos
 
**Capas de la arquitectura:**
| Capa | Función |
|---|---|
| **Presentación** | Navegabilidad, validación de datos de entrada, formateo de salida; es la que ve el usuario |
| **Negocio** | Recibe las peticiones, envía las respuestas y verifica que se cumplen las reglas establecidas |
| **Acceso a datos** (opcional) | Almacena, estructura y recupera los datos solicitados por la capa de negocio |
 
**Modelo de 2 capas:** no usa base de datos (cliente ↔ servidor)

**Modelo de 3 capas:** usa base de datos, repartiendo funciones para mayor seguridad, flexibilidad y escalabilidad:
- **Cliente**: realiza la petición de recursos mediante la interfaz de usuario
- **Servidor de aplicaciones**: recibe las peticiones y usa otro servidor para resolverlas
- **Servidor de datos**: proporciona los datos al servidor de aplicaciones desde una base de datos

<br>
 
## 5. Navegadores
Un **navegador (browser)** es la aplicación que permite acceder a páginas web y navegar por Internet
| Navegador | Desarrollador | Lanzamiento | Notas |
|---|---|---|---|
| **Google Chrome** | Google | 2008 | Código abierto, gratuito, multiplataforma; el más popular actualmente |
| **Mozilla Firefox** | Corporación/Fundación Mozilla | 2004 | Gratuito y de código abierto |
| **Apple Safari** | Apple | 2003 | Código cerrado; funciona en OS X, iOS y Windows |
| **Microsoft Edge** | Microsoft | — | Integrado en Windows |
| **Opera** | Opera Software | — | Compatible con Windows y Mac OS X |
 
<br>
 
## 6. Servidores web
Un **servidor web** es una aplicación de servidor que responde a las peticiones de acceso a un recurso web (p. ej. una página HTML), utilizando el protocolo HTTP
 
### 6.1 Funcionamiento básico
1. El navegador consulta al **servidor DNS**, que responde con la IP del servidor web donde está alojado el contenido
2. Se envía una solicitud de contenido mediante HTTP (puerto 80) o HTTPS (puerto 443)
3. El servidor web recibe la solicitud, busca y procesa el contenido (ejecutando código si es dinámico)
4. Envía el contenido solicitado (típicamente HTML) al cliente

### 6.2 Servidores web más populares 
| Servidor | Características |
|---|---|
| **Apache** | Código abierto, multiplataforma, muy robusto; líder histórico hasta ser superado por Nginx en 2021; limitaciones de velocidad en ciertos entornos |
| **Nginx** | Software libre, multiplataforma; excelente con gran número de peticiones simultáneas y bajo consumo de recursos |
| **IIS** | Servidor propietario de Microsoft, orientado a Windows y aplicaciones .NET/ASP |
| **LiteSpeed** | Sustituto de Apache, alto rendimiento en entornos de tráfico elevado, compatible con configuraciones de Apache |
| **Tomcat** | Servidor orientado a desarrollo Java; contenedor de servlets |
 
### 6.3 Apache en detalle
Nació a mediados de los 90 gracias a la Apache Software Foundation, llegando a alcanzar una cuota del 70% de las webs y siendo el primer servidor en alojar más de 100 millones de sitios
 
**Características:** gratuito y de código abierto, instalación sencilla, altamente extensible mediante módulos, autenticación/validación integrada, soporte para Perl, PHP y Python
 
**Ventajas:** gran soporte y documentación, multiplataforma, muchos módulos disponibles, sencillez de instalación, seguridad integrada (SSL/TLS, autenticación)
 
**Desventaja:** rendimiento inferior frente a alternativas más veloces con los mismos recursos
 
<br>
 
## 7. Lenguajes de programación en la web
### 7.1 Frontend vs. backend
| | Frontend (cliente) | Backend (servidor) |
|---|---|---|
| **Dónde se ejecuta** | En la máquina del cliente | En el servidor, antes de enviar la página al usuario |
| **Qué gestiona** | Lo que ve el usuario: tipografía, colores, adaptación a pantallas (RWD), interacción con ratón/teclado, efectos visuales | Acceso a base de datos, conexión en red, lógica de negocio |
| **Tecnologías** | HTML/XHTML (contenido), CSS (estética), JavaScript/jQuery (interacción) | PHP, Java, Perl, Python, .NET |
 
### 7.2 PHP
Lenguaje de scripting del lado del servidor, de código abierto, interpretado (se ejecuta sobre la marcha sin necesidad de compilación previa)
 
**Ventajas:** libre y abierto, curva de aprendizaje baja, configuración rápida, fácil integración con bases de datos (Oracle, MySQL, SQL Server), gran comunidad, multiplataforma, ideal para contenido dinámico. Usado por sitios como Facebook, Yahoo, Flickr o Wikipedia
 
**Desventajas:** el código fuente es difícil de ocultar de forma eficiente, requiere buena configuración para evitar brechas de seguridad, solo se ejecuta en un servidor web
 
> El navegador del cliente solo recibe HTML; el código PHP se ejecuta y se "oculta" en el servidor
 
### 7.3 Java (comparativa con PHP)
Lenguaje de propósito general orientado a objetos, muy usado por grandes empresas y en aplicaciones científicas. Requiere la **JVM (Java Virtual Machine)** para interpretar el código
 
A diferencia de PHP (interpretado), Java es **compilado**: código fuente → compilador → JVM → compilador → ejecución (frente al flujo más directo de PHP: código → intérprete → ejecución). Por ello, Java puede requerir más tiempo y coste de desarrollo
 
### 7.4 MySQL
Sistema gestor de bases de datos relacionales más popular de Internet, de código abierto, desarrollado inicialmente por Sun Microsystems y adquirido después por Oracle (licencia dual: GPL/código abierto y comercial). Esta dualidad dio origen a **MariaDB**, un gestor compatible creado por los desarrolladores originales de MySQL
 
**Características:** multiplataforma, arquitectura cliente/servidor, ligero, fácil de usar y mantener, robusto y seguro, forma parte de la arquitectura LAMP
 
**phpMyAdmin:** aplicación web basada en PHP que permite administrar bases de datos MySQL con una interfaz gráfica sencilla (crear/modificar/eliminar bases de datos y tablas)
 
<br>
 
## 8. Plataformas web: LAMP y WISA
| Plataforma | Componentes | Licencia |
|---|---|---|
| **LAMP** | **L**inux (SO) + **A**pache (servidor web) + **M**ySQL/MariaDB (BBDD) + **P**HP (lenguaje, a veces Perl o Python) | Libre |
| **WISA** | **W**indows (SO) + **I**nternet Information Services (servidor web) + **S**QL Server (BBDD) + **A**SP/ASP.NET (lenguaje) | Propietaria |
 
<br>
 
## 9. Despliegue en Internet
### 9.1 Escalabilidad
Capacidad de un sistema web de adaptar su rendimiento cuando aumenta el número de usuarios, sin que el aumento de recursos suponga modificar su comportamiento o capacidades
- **Escalabilidad vertical**: servidores más potentes
- **Escalabilidad horizontal**: más servidores
### 9.2 Tipos de servidores (evolución)
 
**Sin virtualización (hosting tradicional):**
- Servidor dedicado
- Servidor compartido
**Con virtualización:**
- Servidor virtual (VPS)
- Nube (Cloud)

### 9.3 Servicios en la nube
| Tipo | Significado |
|---|---|
| **IaaS** | Infraestructura como Servicio |
| **PaaS** | Plataforma como Servicio |
| **SaaS** | Software como Servicio |
 

<br>

---
>_Estela de Vega Martín | IES Ribera de Castilla 26/27._
