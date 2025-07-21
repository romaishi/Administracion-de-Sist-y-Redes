# TP5: Clínica Multi-Sucursal - Diseño y Configuración de Redes

Este repositorio contiene el diseño, la configuración y la verificación del funcionamiento de una red de múltiples sucursales para una clínica, utilizando Cisco Packet Tracer. Este proyecto es una continuación del TP4, con la adición de una tercera sucursal y la reestructuración de los servicios existentes.

## 🎯 Objetivo del Proyecto

El objetivo principal de este trabajo práctico es integrar conceptos avanzados de redes para diseñar una infraestructura robusta y funcional que soporte la operación de una clínica con múltiples sucursales. Esto incluye:

* Segmentación de redes mediante subredes (VLSM y convencionales)
* Asignación de IPs estáticas y dinámicas
* Implementación y testeo de servicios de red reales (DNS, FTP, SMTP, WEB, DHCP)
* Configuración de infraestructura física y lógica en Packet Tracer (edificios, racks, cableado ordenado)
* Enrutamiento estático y dinámico (RIPv2)
* Conexiones inter-sucursales y distribución de roles según ubicación

## 🏢 Organización Física y Lógica en Packet Tracer

Además del diseño lógico de la red, se deberá replicar su representación física utilizando las herramientas de Packet Tracer, para simular un entorno profesional de redes empresariales.

### 🏬 Distribución por Edificio y Piso

La clínica se expandió a tres edificios (Sucursal 1, Sucursal 2 y Sucursal 3), cada uno con dos pisos funcionales, que contienen las distintas redes conectadas a sus respectivos switches.

| Sucursal   | Piso        | Switch        | Nombre sugerido    |
| :--------- | :---------- | :------------ | :----------------- |
| Sucursal 1 | Planta Baja | SW_Principal  | Sw_Princ_Suc1      |
| Sucursal 1 | Planta Baja | SW1           | Sw_Pb_Suc1         |
| Sucursal 1 | Primer Piso | SW2           | Sw_1ro_Suc1        |
| Sucursal 2 | Planta Baja | SW_Principal  | Sw_Princ_Suc2      |
| Sucursal 2 | Planta Baja | SW3           | Sw_Pb_Suc2         |
| Sucursal 2 | Primer Piso | SW4           | Sw_1ro_Suc2        |
| Sucursal 3 | Planta Baja | SW_Principal  | Sw_Princ_Suc3      |
| Sucursal 3 | Planta Baja | SW5           | Sw_Pb_Suc3         |
| Sucursal 3 | Primer Piso | SW6           | Sw_1ro_Suc3        |

### 🧱 Capa Física – Requisitos

* **Edificios y pisos**:
    * Cada switch debe estar ubicado en el piso correspondiente del edificio asignado.
    * Utilizar los elementos de Packet Tracer para representar pisos y edificios (pueden usar etiquetas, textos o agrupaciones visuales).
* **Racks**:
    * Todos los dispositivos de red (Switches, Access Points, Servidores) deben estar montados en racks bien organizados.
    * Usar racks separados para los Access Points, si es necesario, para mejorar la cobertura inalámbrica.
    * Opcional: pueden agregar UPS o equipos decorativos si lo consideran relevante.
* **Cableado**:
    * Utilizar diferentes colores de cables por red o subred para facilitar la lectura.
    * Los cables deben estar ordenados, sin cruces innecesarios, y bien distribuidos dentro del rack.

### 🧠 Capa Lógica – Organización

* **Clusters**:
    * En la vista lógica, agrupar mediante Clusters:
    * Cada Sucursal completa (SW1+SW2 o SW3+SW4 con sus PCs).
    * Cada Switch con sus PCs en un subcluster dentro de su sucursal.
    * Asignar colores distintos a cada cluster para facilitar la comprensión visual.
* **Nombre de dispositivos**: Todos los dispositivos deben estar correctamente nombrados.

## 🔧 Topología General de Toda la Red

La red consta de:
* 3 switches principales (SW_Princ_Suc1, SW_Princ_Suc2 y SW_Princ_Suc3).
* 6 switches seccionales (SW1, SW2, SW3, SW4, SW5, SW6).
* 3 Routers (cada uno conectado a un Switch Principal de cada sucursal).

Cada Switch Principal se conectará solo a un Switch seccional de cada sucursal (usar las interfaces FastEthernet empezando de la 0/1).
Cada switch seccional gestiona 2 redes cableadas distintas:
* Las primeras 10 interfaces (FastEthernet 0/1 a 0/10) para la Red A.
* Las siguientes 10 interfaces (FastEthernet 0/11 a 0/20) para la Red B.
* Si es necesario, achicar la cantidad de interfaces para colocar las 5 redes pedidas por sucursal (wifi’s).
Los puertos GigabitEthernet se utilizarán para conectar:
* Routers
* SW1 con SW2
* SW3 con SW4
* SW5 con SW6
* SW1 con SW_Princ
* SW3 con SW_Princ
* SW5 con SW_Princ
En lo posible usar los GigabitEthernet restantes para conectar servidores, en caso de no poder, usar los últimos puertos FastEthernet 0/24 a 0/20 o como se haya dividido.
Cada switch seccional gestiona 2 redes inalámbricas en común para la sucursal:
* Cada AP se conecta a una de las bocas disponibles de la red correspondiente.
* 1 subRed inalámbrica compartida por todas las redes cableadas de SW1- SW2, otra para el SW3-SW4 y otra para el SW5-SW6.
* Deberá tener su propia subred.
* Conectar dos Access Point por switch (12 AP en total), uno por red cableada, pero todos configurados para la misma red Wifi por sucursal.

## 🖥️ Redes de Sucursales

### Redes de SW5 y SW6 (Clase B - IP Dinámica DHCP)

* **Estructura**:
    * Un Router principal para la sucursal (conectado al Switch principal).
    * 1 switch Principal conectado en cascada a 1 de los switches seccionales.
    * El Switch principal debe separar interfaces para conexión de servidores.
    * Cada Switch seccional dividirá en partes necesarias sus interfaces de red para tener 2 subRedes cableadas + la una wifi (AP).
    * 2 switches seccionales (conectados entre sí en cascada), con:
        * 2 PCs cableadas por subRedes.
        * 1 Access Point por subRedes (AP) (de una sucursal mismo SSID).
        * 1 notebook por subRedes.
* **Total de equipos por sucursal**:
    * 1 Router
    * 3 switches
    * 4 Access Point
    * 8 PC cableadas
    * 4 notebook
* **Direccionamiento**:
    * Cada alumno deberá ver qué red de clase B le tocó para trabajar.
    * Reservar la 1° IP de host disponible de cada subRed como Puerta de Enlace.
    * Asignar direcciones IP dinámicas DHCP.
    * La asignación de DHCP la deberá realizar el Router de la sucursal 3.
    * SubNetear en 5 subRedes del mismo tamaño: Wifi, servidores, médicos, rrhh, directivos.
    * Establecer el orden de IP para la subred de los servidores (IP estáticas):
        * 1° para el servidor DNS
        * 2° para el servidor FTP
    * Configurar máscara, puerta de enlace y DNS.
* **Red WiFi compartida**:
    * Una subred (wifi) inalámbrica compartida para toda la sucursal.
    * Configurar los Access Points para usar la misma SSID y Password.
    * La cobertura de red debe ser solo la mitad del piso por AP.
    * Deben tener usuario FTP y SMTP configurado igual que las PCs cableadas.

### Redes de SW1 y SW2 (Clase A - IP Estática)

* **Estructura**:
    * Un Router principal para la sucursal (conectado al Switch principal).
    * 1 switch Principal conectado en cascada a 1 de los switches seccionales.
    * El Switch principal debe separar interfaces para conexión de servidores.
    * Cada Switch seccional dividirá en partes necesarias sus interfaces de red para tener 2 subRedes cableadas + la una wifi (AP).
    * 2 switches seccionales (conectados entre sí en cascada), con:
        * 2 PCs cableadas por subRedes.
        * 1 Access Point por subRedes (AP) (de una sucursal mismo SSID).
        * 1 notebook por subRedes.
* **Total de equipos por sucursal**:
    * 1 Router
    * 3 switch
    * 4 Access Point
    * 8 PC cableadas
    * 4 notebook
* **Direccionamiento**:
    * Cada alumno deberá ver qué red de clase A le tocó para trabajar.
    * Reservar la 1° IP de host disponible de cada subRed como Puerta de Enlace.
    * Asignar direcciones IP estáticas.
    * SubNetear en 5 redes por VLSM (wifi, servidores, médicos, rrhh, directivos)
    * Hosts necesarios:
        * Wifi → 300
        * servidores → 5
        * médicos → 100
        * rrhh → 20
        * directivos → 10
    * +2 redes de enlace.
    * Establecer el orden de IP para la subred de los servidores (IP estáticas):
        * 1° para el servidor SMTP
        * 2° para el servidor FTP
    * Configurar máscara, puerta de enlace y DNS.
    * El servidor DNS no estará en esta parte de la red, pero deberá estar configurado como si existiera, apuntando al servidor DNS de la red correspondiente.
* **Red WiFi compartida**:
    * Una subred (wifi) inalámbrica compartida para toda la sucursal.
    * Configurar los Access Points para usar la misma SSID y Password.
    * La cobertura de red debe ser solo la mitad del piso por AP.
    * Deben tener usuario FTP y SMTP configurado igual que las PCs cableadas.

### Redes de SW3 y SW4 (Clase C con DHCP)

* **Estructura**:
    * Un Router principal para la sucursal (conectado al Switch principal).
    * 1 switch Principal conectado en cascada a 1 de los switches seccionales.
    * El Switch principal debe separar interfaces para conexión de servidores.
    * Los servidores se configuran de forma estática siempre.
    * Cada Switch seccional dividirá en partes necesarias sus interfaces de red para tener 2 subRedes cableadas + la una wifi (AP).
    * 2 switches seccionales (conectados entre sí en cascada), con:
        * 2 PCs cableadas por subRedes.
        * 1 Access Point por subRedes (AP) (de una sucursal mismo SSID).
        * 1 notebook por subRedes.
* **Total de equipos por sucursal**:
    * 1 Router
    * 3 switch
    * 4 Access Point
    * 8 PC cableadas
    * 4 notebook
* **Red WiFi compartida**:
    * Una subred (wifi) inalámbrica compartida para toda la sucursal.
    * Configurar los Access Points para usar la misma SSID y Password.
    * La cobertura de red debe ser solo la mitad del piso por AP.
    * Deben tener usuario FTP y SMTP configurado igual que las PCs cableadas.
* **Direccionamiento IP (Clase C con DHCP)**:
    * Cada alumno deberá ver qué red de clase C le tocó para trabajar.
    * Reservar la 1° IP de host disponible de cada subRed como Puerta de Enlace.
    * Subnetear 5 subRedes con la misma cantidad de host para: Wifi, Servidores, Médicos, RRHH, Directivos.
    * Armar los 5 pool de DHCP en el servidor.
    * Direccionamiento entregado automáticamente por servidor DHCP a todas las PC.
    * Establecer el orden de IP para la subred de los servidores (IP estáticas):
        * 1° para el servidor DHCP
        * 2° para el servidor Web Institucional
        * 3° para el servidor Web RRHH
        * 4° para el servidor Web Directivos
        * 5° para el servidor Web Médicos
    * Configurar máscara, puerta de enlace y DNS.
    * El servidor DNS no estará en esta parte de la red, pero deberá estar configurado como si existiera, apuntando al servidor DNS de la red correspondiente.
* **Servidor DHCP (Centralizado)**:
    * Un único servidor DHCP para todas las redes de esta sucursal.
    * 5 scopes (uno por subRed) que deben incluir:
        * Rango válido de IPs para las PCs (con reserva de primeras IP no disponibles).
        * Gateway
        * Máscara
        * Apuntar al servidor DNS (aunque este en otra red de otra sucursal).
        * Pool con cantidad de host correspondientes establecidas.

## 🌐 Servidores

### 🌍 Servidor DNS (Interno)

* Debe poder resolver nombres de todos los servicios internos de todas las sucursales.
* Configurar zonas directas para los siguientes nombres:
    * `web-clinica.org`
    * `medicos.clinica.org`
    * `directivos.clinica.org`
    * `rrhh.clinica.org`
* IPs internas de servidores FTP/SMTP/DHCP (`ftp.clinica.org`, etc…).
* IPs interna del servidor DNS (`dns.clinica.org`).
* IPs de las Puertas de Enlace de cada Sucursal (`Sucursal1.clinica.org`, etc..).
* IPs de enlace entre sucursales:
    * `R1-R2.clinica.org`
    * `R2-R1.clinica.org`
    * `R1-R3.clinica.org`
    * `R3-R1.clinica.org`
    * `R2-R3.clinica.org`
    * `R3-R2.clinica.org`

### 📁 Servidor FTP

* El servidor FTP debe permitir subir y descargar archivos por parte de las PCs conectadas.
* Debe contener al menos una carpeta compartida con archivos de prueba.
* Cada usuario debe tener una cuenta con:
    * Nombre de usuario
    * Contraseña
    * Permisos de lectura y escritura

| Rol       | Permisos         | Descripción                                                                 |
| :-------- | :--------------- | :-------------------------------------------------------------------------- |
| Médicos   | Lectura / Escritura | Acceso a carpetas de médicos con datos de pacientes, etc.        |
| RRHH      | Lectura / Escritura | Acceso a carpetas de personal, altas/bajas, contratos, etc. |
| Directivo | Lectura / Escritura | Acceso a informes generales, estratégicos, y documentos de gestión. |

### 📨 Servidor SMTP

* Este servidor se encargará del envío de correos internos entre las PCs de las 3 sucursales.
* Debe configurarse para permitir envío entre usuarios configurados en las PCs.
* Todas las PC de todas las sucursales deben quedar configuradas para envió/recepción de email.
* El dominio es `@clinica.org`.
* Cada usuario creado debe tener:
    * Nombre de usuario
    * Contraseña
    * Buzón de correo asociado

| Dispositivo    | Usuario SMTP | Email                |
| :------------- | :----------- | :------------------- |
| PC1            | rrhh1        | rrhh1@clinica.org    |
| PC2            | rrhh2        | rrhh2@clinica.org    |
| PC3            | medico1      | medico1@clinica.org  |
| PC4            | medico2      | medico2@clinica.org  |
| PC5            | dir1         | dir1@clinica.org     |
| PC6            | dir2         | dir2@clinica.org     |
| PC7            | enfer1       | enfer1@clinica.org   |
| PC8            | enfer2       | enfer2@clinica.org   |
| Laptop1 (WiFi) | wifi1        | wifi1@clinica.org    |
| Laptop2 (WiFi) | wifi2        | wifi2@clinica.org    |

### 🌐 Servidores Web – Características por función

Cada servidor HTTP debe estar instalado en una máquina distinta.

| Servidor Web        | Nombre DNS        | Funcionalidad                                     |
| :------------------ | :---------------- | :------------------------------------------------ |
| Página Institución  | `web-clinica.org` | Página institucional de acceso libre (público) |
| Panel de Médicos    | `medicos.clinica.org` | Login con autenticación, vista médica (consultas, pacientes) |
| Panel Directivo     | `directivos.clinica.org` | Login con autenticación, vista de reportes y gestión de gastos |
| Panel RRHH          | `Rrhh.clinica.org` | Login con autenticación, vista de gestión de personal |

#### 🧑‍💻 Desarrollo de Sitios Web (HTML + CSS) – Servidores Web

Se solicita que para cada servidor web implementado, los estudiantes diseñen e integren un pequeño sitio web funcional, utilizando únicamente HTML y CSS (compatible con el servidor HTTP de Packet Tracer).
* **Requisitos generales**:
    * Los archivos deben estar ubicados en el directorio del servidor web correspondiente dentro de Packet Tracer.
    * Deben tener al menos:
        * Un archivo `index.html`
        * Un archivo `style.css`
    * Todo el contenido debe estar bien vinculado (rutas relativas).
    * No se requiere JS ni formularios funcionales (pero sí simulación visual de login/paneles).
    * Se pueden usar imágenes livianas (formato `.jpg`, `.png`, `.gif`), siempre embebidas correctamente.

* **Estructura de los sitios web requeridos**:

| Servidor Web        | Nombre DNS          | Contenido mínimo requerido                                                                                                                                                                                                     |
| :------------------ | :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Página institucional | `web-clinica.org`   | Página de inicio con información general de la clínica, presentación de servicios, imágenes, misión y datos de contacto.                                                                                                 |
| Panel Médicos       | `medicos.clinica.org` | Login visual + redirección a un panel donde se muestren pacientes en tabla (nombre, DNI, diagnóstico). Identificación clara del sector ("Panel Médico").                                                                                             |
| Panel RRHH          | `rrhh.clinica.org` | Login visual + redirección a un panel con tabla completa del personal (nombre, puesto, sector, legajo). Título claro "Panel de Recursos Humanos".                                                                                                 |
| Panel Directivos    | `directivos.clinica.org` | Login visual + redirección a un panel con sección de finanzas (puede incluir tablas con gastos por sucursal, gráfico simulado, resumen financiero).                                                            |

#### 🔒 Login unificado (simulado)

* Todos los sitios que requieren autenticación (RRHH, Médicos, Directivos) deben compartir una misma pantalla de login estática (mismo diseño).
* Al hacer clic en “Iniciar sesión”, el botón debe redirigir visualmente al panel correspondiente (`panel.html` u otro nombre interno).
* El login no tiene que funcionar realmente, pero debe estar bien estructurado.

## 🌍 Enrutamiento Propuesto

* **Sucursal 3**: Red de enlace con Sucursal 1 (usando IP de enlace VLSM de la red de la Sucursal 1 para las conexiones con el Router de la sucursal 1) y con Sucursal 2 (usando IP de enlace estática clase A pública para la conexión con el Router de la sucursal 2).
* **Sucursal 1**: Red de enlace con Sucursal 2 y 3 (usando IP de enlace VLSM de la red de la Sucursal 1 para las conexiones con ambos Routers de las otras sucursales).
* **Sucursal 2**: Red de enlace con Sucursal 1 (usando IP de enlace VLSM estática de la red de la Sucursal 1 para las conexiones con el Router de la sucursal 1) y con Sucursal 3 (usando IP de enlace estática clase A pública para la conexión con el Router de la sucursal 3).

El enrutamiento está configurado con la opción más eficiente dependiendo de las configuraciones de las redes a conectar (red origen $\leftrightarrow$ red destino).

## 📁 Entrega

* Nombre del archivo: `TP5_Redes_Clinica_[Apellido].pkt`
* Entregar en repositorio INDIVIDUAL de GITHUB de la materia, en una nueva BRANCH llamada `TP5`.
* Entregar el Link/URL de la Branch en la tarea del ClassRoom.
* Incluir un breve documento PDF con:
    * Esquema de subredes utilizadas
    * Rango de IPs por red
    * IPs asignadas a servidores
    * Usuarios y contraseñas creados para SMTP/FTP
    * Tabla de direccionamientos DNS
    * Tabla de enrutamiento (IPs, máscara, tipo (estático/rip), dispositivo de origen/destino)
    * Listado utilizado de comandos para configuración de Routers
    * Screenshots de pruebas de conectividad y accesibilidad a servicios:
        * Usando la herramienta de PING gráfica [p]
        * PING por consola yendo a la PC → Desktop → Command Prompt → `ping [IP o DNS]`
        * Saltos de paquetes usando el comando Command Prompt → `tracert [IP o DNS]`
        * Prueba de envío de correos (SMTP)
        * Prueba de acceso a FTP
        * Prueba de navegación web
