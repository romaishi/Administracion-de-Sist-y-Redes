# 🧠 Trabajo Práctico – Programación sobre Redes

## 👤 Datos del Alumno

- **Nombre y Apellido:** Roman Abalos Ishida  
- **Correo Electrónico:** romanabalosishidaet32@gmail.com  
- **Curso y División:** 6.1C  

## 👨‍🏫 Docente

- **Nombre y Apellido:** Gonzalo Nicolás Consorti  

## 🧾 Materia

**Programación sobre Redes**  
Esta materia tiene como objetivo enseñar los fundamentos de la programación aplicada al trabajo en redes de computadoras, combinando conceptos de entrada/salida, estructuras de datos y lógica de resolución de problemas.

---

## 📁 Estructura del Proyecto

Contiene todas las clases Java desarrolladas para los ejercicios propuestos en la guía.  
Cada clase resuelve uno de los enunciados de la consigna utilizando exclusivamente los métodos permitidos según se indica:

- **Entrada:** métodos de la clase `System` o de la clase `Reader`.
- **Salida:** `PrintStream`.

---

## 📌 Consigna

Desarrollar una serie de ejercicios en Java utilizando exclusivamente:

- Entrada: `System` o `Reader`.
- Salida: `PrintStream`.

---

### ✅ Ejercicios con `System` + `PrintStream`

- Calcular sueldo bruto: valor de hora × cantidad de horas trabajadas.
- Calcular el tercer ángulo de un triángulo dados dos.
- Calcular el perímetro de un cuadrado dada su superficie.
- Convertir temperatura de Fahrenheit a Centígrados.
- Convertir segundos a días, horas, minutos y segundos.
- Calcular planes de pago con distintos porcentajes y cuotas:
  - Plan 1: 10% descuento al contado.
  - Plan 2: 50% al contado, 2 cuotas, +10% al total.
  - Plan 3: 25% al contado, 5 cuotas, +15% al total.
  - Plan 4: 8 cuotas con distribución desigual, +25% al total.
- Mostrar mes aproximado de nacimiento a partir del signo zodiacal.

---

### ✅ Ejercicios con `Reader` + `PrintStream`

- Mostrar tres apellidos ordenados alfabéticamente.
- Indicar el menor entre cuatro números reales.
- Determinar si un número es par o impar.
- Verificar si el mayor entre dos números es divisible por el menor.
- Determinar el signo del zodíaco según la fecha de nacimiento.
- Comparar apellidos de dos personas según su longitud.
- Mostrar la tabla de multiplicar de un número N.
- Indicar si un número natural es primo o no.

---

## 🌐 Parte de Redes – Cisco Packet Tracer

### 🔸 Ejercicio 1: ACL Estándar sin VLAN / sin SVI

#### 🔧 Topología:
- 2 Routers conectados por enlace serial `/30`.
  - R1 (Red clase C - `192.168.1.0/24`)
  - R2 (Red clase B - `172.16.0.0/24`)
- Cada router conectado a un switch, con un switch seccional y una PC.
- Servidor Web (`172.16.0.10`) y DNS (`172.16.0.11`) detrás de R2.

#### 📋 Objetivos:
- Configurar DHCP en R1 y R2 para sus respectivas redes.
- Aplicar una ACL estándar en R2 que bloquee el acceso de PC1 (IP: `192.168.1.10`) al servidor Web, pero permita el resto del tráfico.

#### ✅ ACL configurada:
```bash
access-list 1 deny 192.168.1.10 0.0.0.0
access-list 1 permit any
interface GigabitEthernet0/0
ip access-group 1 out
