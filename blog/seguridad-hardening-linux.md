---
title: Hardening de Servidores Linux: Mejores Prácticas
category: Seguridad
readtime: 12 min lectura
date: 2024-04-20
tags: [Linux, Hardening, SSH, Seguridad]
---

## Introducción

Cada día se reportan miles de ataques a servidores Linux. Los attackers buscan sistemas mal configurados, contraseñas débiles y servicios expuestos. En esta guía aprenderás a proteger tus servidores Linux como un profesional.

## ¿Qué es el Hardening?

Hardening es el proceso de asegurar un sistema reduciendo su superficie de ataque. Cada servicio, puerto y configuración que no es estrictamente necesario representa un riesgo potencial.

## Paso a Paso: Hardening de un Servidor Ubuntu

### 1. Actualización Inicial

```bash
# Actualizar todos los paquetes
sudo apt update && sudo apt upgrade -y

# Instalar herramientas de seguridad
sudo apt install -y fail2ban ufw unattended-upgrades
```

### 2. Configuración de SSH

Edita `/etc/ssh/sshd_config`:

```
Port 2222                    # Puerto no estándar
PermitRootLogin no           # No login como root
PasswordAuthentication no    # Solo llaves SSH
X11Forwarding no             # Desactivar si no se necesita
MaxAuthTries 3              # Limitar intentos
ClientAliveInterval 300      # Timeout de sesión
```

```bash
# Reiniciar SSH
sudo systemctl restart sshd
```

### 3. Firewall con UFW

```bash
# Configuración básica
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2222/tcp      # SSH en puerto personalizado
sudo ufw allow 80/tcp        # HTTP
sudo ufw allow 443/tcp       # HTTPS
sudo ufw enable
```

### 4. Protección contra ataques de fuerza bruta

Configurar fail2ban en `/etc/fail2ban/jail.local`:

```ini
[DEFAULT]
bantime = 3600
findtime = 600
maxretry = 3

[sshd]
enabled = true
port = 2222
```

```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### 5. Gestión de Usuarios y Permisos

```bash
# Crear usuario con privilegios sudo
sudo adduser nuevoadmin
sudo usermod -aG sudo nuevoadmin

# Configurar acceso SSH solo para ese usuario
mkdir /home/nuevoadmin/.ssh
chmod 700 /home/nuevoadmin/.ssh
```

### 6. Auditoría de Seguridad con Lynis

```bash
# Instalar y ejecutar Lynis
sudo apt install lynis -y
sudo lynis audit system
```

## Checklist de Hardening

- [ ] Sistema actualizado
- [ ] SSH en puerto no estándar
- [ ] Login root deshabilitado
- [ ] Autenticación por llaves SSH
- [ ] Firewall configurado
- [ ] fail2ban activo
- [ ] Usuarios limitados
- [ ] Auditoría programada

## Conclusión

El hardening no es un evento único sino un proceso continuo. Programa auditorías mensuales y mantén记录 de los cambios realizados.

---

*Más artículos de seguridad en mi blog.*