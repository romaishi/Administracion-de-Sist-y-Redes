# 🧠 Trabajo Práctico – Programación sobre Redes

## 👤 Datos del Alumno

- **Nombre y Apellido:** Roman Abalos Ishida  
- **Correo Electrónico:** romanabalosishidaet32@gmail.com  
- **Curso y División:** 6.1C  

## 👨‍🏫 Docente

- **Nombre y Apellido:** Gonzalo Nicolás Consorti  

## 🧾 Materia

**Programación sobre Redes**  
Esta materia tiene como objetivo enseñar los fundamentos del trabajo en redes de computadoras, abarcando conceptos de direccionamiento, servicios, protocolos, segmentación lógica y control de acceso, utilizando herramientas como Cisco Packet Tracer.

---

## 🌐 Trabajo Práctico – ACL Estándar (Packet Tracer)

Este trabajo se divide en dos ejercicios principales: uno sin VLAN y otro con segmentación mediante VLAN y subinterfaces. En ambos casos se implementan listas de control de acceso (ACLs) estándar para filtrar tráfico según origen IP.

---

### 🔸 Ejercicio 1: ACL Estándar sin VLAN / sin SVI

#### 🔧 Topología:
- 2 Routers conectados por enlace serial `/30` (red clase A - `10.0.0.0/30`)
- R1: Red clase C `192.168.1.0/24`
- R2: Red clase B `172.16.0.0/24`
- Cada router está conectado a un switch principal, que a su vez se conecta a un switch seccional con una PC.
- Servidor Web (`172.16.0.10`) y DNS (`172.16.0.11`) detrás de R2.

#### 📋 Objetivos:
- Configurar DHCP en R1 y R2 para sus respectivas redes.
- Aplicar una ACL estándar en R2 que bloquee el acceso de **PC1** (IP: `192.168.1.10`) al servidor Web, pero permita todo lo demás.

#### ✅ ACL configurada:
```bash
access-list 1 deny 192.168.1.10 0.0.0.0
access-list 1
