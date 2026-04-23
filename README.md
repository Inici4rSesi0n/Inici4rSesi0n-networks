# 🌐 Inici4rSesiOn-networks

> **Versión 1.0** – Red LAN con SSHv2, Telnet, ping y encapsulamiento HTTP  
> *Repositorio de aprendizaje y práctica de redes con Cisco Packet Tracer*
> 
[![SSHv2](https://img.shields.io/badge/SSH-v2.0-brightgreen)](https://github.com/tuusuario/Inici4rSesiOn-networks)
[![Telnet](https://img.shields.io/badge/Telnet-enabled-blue)]()
[![Packet Tracer](https://img.shields.io/badge/Packet%20Tracer-8.2-orange)]()
[![Licencia MIT](https://img.shields.io/badge/Licencia-MIT-yellow)]()
---

## 📌 Descripción

Este proyecto implementa una **red de área local (LAN)** funcional utilizando **Cisco Packet Tracer**. Se ha configurado un switch de capa 2 con **acceso remoto seguro** (SSH versión 2) y **acceso remoto básico** (Telnet) para administración. La topología incluye cableado estructurado con fibra óptica y cobre, direccionamiento IPv4 estático, pruebas de conectividad y una simulación de **encapsulamiento de una petición HTTP** para comprender el modelo de capas TCP/IP.

**Objetivo:** Demostrar habilidades prácticas en:
- Configuración de switches Cisco.
- Implementación de protocolos de acceso remoto (SSHv2, Telnet).
- Verificación de conectividad (ping, ICMP).
- Análisis de encapsulamiento (HTTP sobre TCP/IP).

---

## 🛠️ Tecnologías y protocolos utilizados

| Capa (TCP/IP) | Protocolos / Tecnologías |
|---------------|--------------------------|
| **Aplicación** | HTTP, SSHv2, Telnet |
| **Transporte** | TCP (puertos 22, 23, 80) |
| **Red** | IPv4, ICMP (ping), ARP |
| **Acceso a red** | Ethernet, Wi‑Fi, Fibra óptica multimodo |

---

## 🖥️ Topología de red
<picture>
<img width="956" height="508" alt="topology" src="https://github.com/user-attachments/assets/b30ad186-4606-4ed1-9b39-f0459d572037" />
</picture>

**Direccionamiento IPv4 (estático):**

| Dispositivo | Dirección IP | Máscara de subred |
|------------|--------------|-------------------|
| PC0         | 192.168.20.10 | 255.255.255.0 |
| Laptop0     | 192.168.20.11 | 255.255.255.0 |
| Server0     | 192.168.20.12 | 255.255.255.0 |
| Laptop1     | 192.168.20.13 | 255.255.255.0 |
| Printer0    | 192.168.20.14 | 255.255.255.0 |
| Switch0 (gestión) | 192.168.20.22 | 255.255.255.0 |

**Dispositivos de red:**
- **Switch0** (2960-24TT): Switch de acceso con SSHv2 y Telnet.
- **Switch1 / Switch2** (Switch-PT-Empty): Switches de distribución.
- **Access Point0**: Conexión inalámbrica para Laptop1.
- **Server0**: Servidor web (HTTP) para pruebas de encapsulamiento.

---

## 🔧 Configuraciones clave

### 🔐 Switch0 – SSH versión 2 y Telnet

```plaintext
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW0

SW0(config)#ip domain-name redes.local
SW0(config)#Username inici4rsesi0n password SW0
SW0(config)#vlan 1
SW0(config-vlan)#exit
SW0(config)#interface vlan 1
SW0(config-if)#ip address 192.168.20.100 255.255.255.0
SW0(config-if)#no shutdown
SW0(config-if)#exit
SW0(config)#crypto key generate rsa general-keys modulus 103

SW0(config-if)#
%LINK-3-UPDOWN: Interface Vlan1, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

SW0(config)#ip ssh version 2
Please create RSA keys (of at least 768 bits size) to enable SSH v2.
SW0(config)#line vty 0 4
SW0(config-line)#password SW0
SW0(config-line)#login
SW0(config-line)#login local
SW0(config-line)#transport input all
SW0(config-line)#exit
SW0(config)#enable secret SW0
SW0(config)#end

%SYS-5-CONFIG_I: Configured from console by console

SW0#copy running-config start
SW0#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
SW0#
