# 📦 OpenMediaVault (OMV) en Raspberry Pi — Instalación y Configuración

Guía práctica para instalar y configurar **OpenMediaVault 7 (OMV7)** en **Raspberry Pi** y montar un **NAS casero/lab** estable, con buenas prácticas y resolución de problemas comunes.

> **Compatibilidad**: OMV 7 se basa en **Debian 12 (Bookworm)**. En Raspberry Pi se recomienda usar **Raspberry Pi OS Lite (64-bit)** (sin entorno gráfico).

---

## 🗂️ Tabla de contenidos

- [Requisitos](#requisitos)
- [Instalación rápida (TL;DR)](#instalación-rápida-tldr)
- [Paso a paso](#paso-a-paso)
  - [1) Preparar la microSD](#1-preparar-la-microsd)
  - [2) Primer arranque e IP](#2-primer-arranque-e-ip)
  - [3) Acceso por SSH](#3-acceso-por-ssh)
  - [4) Actualizar el sistema](#4-actualizar-el-sistema)
  - [5) Instalar OMV 7](#5-instalar-omv-7)
  - [6) Entrar a la interfaz web](#6-entrar-a-la-interfaz-web)
  - [7) Checklist de posinstalación](#7-checklist-de-posinstalación)
- [Configurar almacenamiento y comparticiones](#configurar-almacenamiento-y-comparticiones)
- [OMV-Extras y Docker/Compose](#omv-extras-y-dockercompose)
- [Mantenimiento y actualizaciones](#mantenimiento-y-actualizaciones)
- [Resolución de problemas (FAQ)](#resolución-de-problemas-faq)
- [Notas importantes](#notas-importantes)
- [Licencia](#licencia)

---

## ✅ Requisitos

- **Raspberry Pi 3B+ / 4 / 5 (recomendado 4 o 5)**  
- **microSD 16 GB+ (Clase 10)** o SSD USB para el **SO**  
- **Fuente de alimentación** oficial o equivalente  
- **Red por cable** (recomendado por estabilidad)  
- **PC** con lector de microSD  
- **Imagen**: Raspberry Pi OS **Lite 64-bit** (Bookworm) **sin escritorio**

> **No se recomienda** instalar OMV sobre imágenes con **entorno gráfico** (desktop). OMV gestiona red y servicios; los escritorios suelen interferir.

---

## ⚡ Instalación rápida (TL;DR)

1) Flashea **Raspberry Pi OS Lite (64-bit)** en la microSD.  
2) Arranca la Pi, obtén su **IP** o usa **hostname.local**.  
3) Conéctate por SSH y actualiza:

```bash
sudo apt update && sudo apt upgrade -y
```

4) Instala OMV + OMV-Extras:

```bash
sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

5) Abre en tu navegador: `http://IP_DE_TU_PI`  o `http://HOSTNAME.local` 
   - Usuario: **admin**  
   - Contraseña: **openmediavault**  

6) Cambia la contraseña de **admin**, configura zona horaria/idioma, crea discos/volúmenes y comparte por **SMB/NFS**.

---

## 🧭 Paso a paso

### 1) Preparar la microSD

- Descarga **Raspberry Pi Imager** y flashea **Raspberry Pi OS Lite (64-bit)**.  
- (Opcional) En *cog/engranaje* de Imager, **activa SSH**, define **usuario/clave** y **Wi‑Fi** si lo usarás.  
- Expulsa la microSD de forma segura.

### 2) Primer arranque e IP

- Inserta la microSD en la Pi, conecta red y corriente.  
- Encuentra la IP (router/DHCP o desde otro equipo con `arp -a` o `nmap`).

### 3) Acceso por SSH

```bash
ssh <usuario>@<IP_DE_TU_PI>
# ej.
ssh pi@192.168.1.50
```

### 4) Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```

> Tip: Asegúrate de estar en **Debian 12/Bookworm** (Raspberry Pi OS actual).

### 5) Instalar OMV 7

**Método recomendado (script oficial OMV-Extras):**

```bash
sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

- Este script **instala OMV, OMV-Extras y Flashmemory** automáticamente.  
- Si **no** quieres que toque tu configuración de red, puedes descargar y ejecutar con `-n`:

```bash
wget https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install
chmod +x install
sudo ./install -n
```

### 6) Entrar a la interfaz web

- Abre: `http://<IP_DE_TU_PI>`  
- Credenciales por defecto:
  - **Usuario**: `admin`
  - **Contraseña**: `openmediavault`

### 7) Checklist de posinstalación

- 🔐 **Cambia** la contraseña de `admin`  
- 🌍 **Zona horaria/idioma**  
- 🧱 **Red**: usar **DHCP** inicialmente; si necesitas **IP estática**, configúrala desde OMV  
- 💾 **Montar discos**  
- 👤 **Usuarios/Grupos**  
- 🗂️ **Carpetas compartidas**  
- 🖥️ **Servicios**  
- 🔄 **Actualizaciones**

---

## 💽 Configurar almacenamiento y comparticiones

1) **Sistemas de archivos**  
   - Conecta discos (USB/SATA).  
   - Verifica en **Almacenamiento → Discos**.  
   - Crea y monta en **Sistemas de archivos**.

2) **Carpetas compartidas**  
   - Crear carpeta y asignar permisos.

3) **SMB/NFS**  
   - Activar en servicios y compartir carpetas.

---

## 🧩 OMV-Extras y Docker/Compose

Ya incluido con el script, permite gestionar Docker y Compose desde OMV.

---

## 🔧 Mantenimiento y actualizaciones

```bash
sudo omv-upgrade
```

---

## 🆘 Resolución de problemas (FAQ)

- **Usuario/contraseña no funciona**: usar `omv-firstaid`
- **Problemas de red**: configurar desde la interfaz de OMV
- **Rendimiento bajo**: usar conexión por cable y discos rápidos

---

## 📎 Comandos útiles

```bash
sudo apt update && sudo apt upgrade -y
sudo omv-firstaid
```

---

