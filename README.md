Claro, aquí tenés el README actualizado:

---

# 🧠 Trabajo Práctico – Programación sobre Redes

## 👤 Datos del Alumno

* **Nombre y Apellido:** Roman Abalos Ishida
* **Correo Electrónico:** [romanabalosishidaet32@gmail.com](mailto:romanabalosishidaet32@gmail.com)
* **Curso y División:** 6.1C

## 👨‍🏫 Docente

* **Nombre y Apellido:** Gonzalo Nicolás Consorti

## 🧾 Materia

**Programación sobre Redes**
Esta materia tiene como objetivo enseñar los fundamentos del trabajo en redes de computadoras, abarcando conceptos de direccionamiento, servicios, protocolos, segmentación lógica y control de acceso, utilizando herramientas como Cisco Packet Tracer.

---

## 🌐 Trabajo Práctico – ACL Estándar (Packet Tracer)

Este trabajo se divide en dos ejercicios principales: uno con una red sin VLANs, y otro con segmentación lógica mediante VLANs y subinterfaces. En ambos se implementan listas de control de acceso (ACLs) estándar para controlar el tráfico según el origen IP.

---

### 🔸 Ejercicio 1: ACL Estándar sin VLAN / sin SVI

#### 🔧 Topología:

* 2 Routers conectados mediante un enlace serial `/30` (red clase A: `10.0.0.0/30`)
* R1: red clase C `192.168.1.0/24`
* R2: red clase B `172.16.0.0/24`
* Cada router se conecta a un switch principal, que a su vez conecta con un switch seccional y una PC.
* En la red de R2 se encuentran un servidor Web (`172.16.0.10`) y un servidor DNS (`172.16.0.11`).

#### 📋 Objetivos:

* Configurar DHCP en R1 y R2 para asignar IPs en sus respectivas redes.
* Aplicar una ACL estándar en R2 que bloquee el acceso de **PC1** (`192.168.1.10`) al servidor Web, permitiendo el resto del tráfico.

#### ✅ ACL de ejemplo:

```bash
access-list 1 deny 192.168.1.10 0.0.0.0
access-list 1 permit any
```

---

### 🔸 Ejercicio 2: ACL Estándar con VLAN y SVI

#### 🔧 Topología:

* Misma estructura general del ejercicio anterior.
* Cada switch seccional está dividido en 2 VLANs:

  * R1: VLAN10 (`192.168.10.0/24`) y VLAN20 (`192.168.20.0/24`)
  * R2: VLAN30 (`172.16.30.0/24`) y VLAN40 (`172.16.40.0/24`)
* Cada VLAN tiene una subinterfaz configurada en los routers con `dot1q`.
* El enlace serial entre routers ahora es `10.0.0.4/30`.

#### 📋 Objetivos:

* Crear 2 VLANs por router (4 en total).
* Conectar 2 PCs por switch seccional (una por VLAN).
* Configurar subinterfaces en los routers para cada VLAN.
* Ubicar los siguientes servicios:

  * VLAN40: Servidor Web y Servidor DNS (sin PCs)
  * VLAN20: Servidor FTP y una PC
  * VLAN10 y VLAN30: 2 PCs cada una
* Aplicar una ACL estándar que:

  * Permita que **solo VLAN10** acceda al servidor Web y al DNS.
  * **Bloquee a VLAN10** el acceso al servidor FTP.

#### 🧠 Direccionamiento IP:

* **R1:**

  * VLAN10: `192.168.10.0/24`
  * VLAN20: `192.168.20.0/24`
* **R2:**

  * VLAN30: `172.16.30.0/24`
  * VLAN40: `172.16.40.0/24`
* **Enlace serial:** `10.0.0.4/30`

#### ✅ ACL de ejemplo:

```bash
access-list 10 permit 192.168.10.0 0.0.0.255
access-list 10 deny 192.168.10.0 0.0.0.255 eq ftp
access-list 10 deny any eq ftp
access-list 10 permit any
```

---
