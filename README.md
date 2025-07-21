# TP6: Diseño y Configuración de Redes con ACLs

Este repositorio contiene el diseño, la configuración y la verificación de una red con dos routers interconectados, switches seccionales con VLANs, y diversos servicios de red. Además, se incluyen 5 ejercicios prácticos enfocados en la implementación y prueba de Listas de Control de Acceso (ACLs) Estándar y Extendidas.

## 🎯 Objetivo del Proyecto

El objetivo principal de este trabajo práctico es aplicar conceptos de enrutamiento, VLANs, servicios de red y, especialmente, la implementación de ACLs para controlar el tráfico y la seguridad en una topología de red simulada en Cisco Packet Tracer.

## 🔧 Topología General de la Red

La red base consta de los siguientes elementos:

* **Routers**: 2 Routers (R1 - Clase C, R2 - Clase B) interconectados.
    * Conexión serial entre R1 y R2 usando un enlace `/29` (clase A, por ejemplo, de la red 10.0.0.0 /8).
* **Switches Principales**: Cada router está conectado a un switch principal.
    * Estos switches se encargan de distribuir DHCP para las siguientes redes:
        * `192.168.0.0/24`
        * `192.168.1.0/24`
        * `172.16.0.0/16`
        * `172.17.0.0/16`
        * `172.18.0.0/16`
* **Enrutamiento**: Configuración de protocolo RIP entre los routers.
* **Switches Seccionales**: Cada switch principal se conecta a un switch seccional.
* **VLANs**: Cada switch seccional soporta múltiples VLANs:
    * `VLAN_10`
    * `VLAN_20`
    * `VLAN_30`
    * `VLAN_40`
    * `VLAN_50` (Esta VLAN_50 se agrega específicamente en el Switch principal del Router 2 y **no lleva PCs**).
* **PCs por VLAN**:
    * `VLAN_10`: 2 PCs
    * `VLAN_20`, `VLAN_30`, `VLAN_40`: 1 PC por cada VLAN.
    * `VLAN_50`: Sin PCs.

## 🌐 Servidores y Servicios

La red incluye varios servidores que proveen servicios esenciales:

* **Servidor HTTP/HTTPS**:
    * Ubicado en la `VLAN_40`.
    * Se mantiene la página por defecto.
* **Servidor DNS**:
    * Ubicado en la `VLAN_50`.
    * Configurado para resolver los servicios existentes en ambas redes.
    * La configuración del DNS debe ser distribuida por DHCP.
* **Servidor FTP**:
    * Ubicado en la `VLAN_20`.
    * Se mantiene la configuración por defecto.
* **Servidor SMTP**:
    * Ubicado en la `VLAN_30`.
    * Se deben crear 4 usuarios de correo.
    * Las configuraciones de correo deben realizarse en cada PC de la red.

## 📁 Ejercicios de ACL

Este proyecto se divide en 5 ejercicios, cada uno enfocado en la aplicación de Listas de Control de Acceso (ACLs) para gestionar el tráfico de red. La topología base se copiará y reutilizará 5 veces para cada ejercicio, entregándose un único archivo `.pkt` con las 5 resoluciones.

### Ejercicio 1: ACL Extendida con VLAN

Aplicar las siguientes ACLs:

* Solo la `VLAN_30` y `VLAN_40` deben tener acceso al servicio FTP.
* Bloquear el acceso de las PCs de la `VLAN_10` a la página web HTTPS.

### Ejercicio 2: ACL Extendida con VLAN

Aplicar las siguientes ACLs:

* Bloquear el acceso al servicio SMTP en la `VLAN_30` desde cualquier otra VLAN.
* Restringir el acceso a HTTPS desde los dispositivos en la `VLAN_10`.

### Ejercicio 3: ACL Estándar con VLAN

Aplicar las siguientes ACLs:

* Bloquear todo el tráfico de la `VLAN_40` hacia la `VLAN_20` y viceversa.
* Bloquear el acceso al servidor HTTP desde la `VLAN_30` hacia la `VLAN_40`.
* Permitir solo FTP y SMTP entre la `VLAN_10` y la `VLAN_20`.

### Ejercicio 4: ACL Extendida con VLAN

Crear una ACL extendida que:

* Permita solamente acceso al servidor DNS en la red `172.16.1.0/16` desde cualquier red.
* Bloquee el acceso a la web HTTP.

### Ejercicio 5: ACL Estándar con VLAN

Aplicar las siguientes ACLs:

* Bloquear el acceso de la `VLAN_10` hacia los servicios FTP, HTTP, HTTPS, DNS y SMTP.
* Permitir que solo una PC de la `VLAN_10` pueda acceder al servicio de HTTPS.

## 📦 Entrega

Se deberá entregar:

* Un único archivo `.pkt` de Cisco Packet Tracer con las 5 topologías resueltas (copias de la topología base con las ACLs aplicadas para cada ejercicio).
* Un documento de texto que contenga únicamente las configuraciones de ACL para cada ejercicio (excluyendo el resto de la configuración de los equipos).
