# 📡 Cómo Conectar AppLocker Pro Nexus (Host + Cliente)

> **AppLocker Pro Nexus** funciona en dos partes:
>
> * 🖥️ **AppLocker Host (Servidor)** — se instala en la PC que deseas controlar.
> * 💻 **AppLocker Cliente** — se utiliza para administrar y controlar la PC remota.

---

# 🌐 Métodos de conexión disponibles

AppLocker Pro Nexus puede conectarse de dos formas:

## 🏠 Conexión Local (Misma Red)

Ideal cuando el Host y el Cliente están conectados al mismo router o red local (hogar, oficina, negocio, etc.).

Utiliza la dirección IPv4 local de la PC donde está instalado el Host.

## 🌍 Conexión Remota con Tailscale

Ideal cuando las PCs están en diferentes ubicaciones o redes.

Tailscale crea una red privada segura entre los equipos y proporciona una dirección IP fija que no cambia, permitiendo la conexión desde cualquier lugar sin abrir puertos en el router.

> ⭐ Recomendado para la mayoría de los usuarios.

---

# 🏠 Opción 1 — Conexión Local (Misma Red)

Si ambas PCs están conectadas a la misma red, puedes utilizar AppLocker Pro Nexus sin instalar Tailscale.

## 🔍 Obtener la IP Local del Host

En la PC que deseas controlar:

1. Presiona `Win + R`
2. Escribe `cmd`
3. Presiona Enter
4. Ejecuta:

```cmd
ipconfig
```

Busca una línea similar a esta:

```text
Dirección IPv4 . . . . . . . . . : 192.168.1.100
```

Anota esa dirección IP.

---

## ⚙️ Configurar AppLocker Host

Abre AppLocker Host y ve a:

**⚙ Configuración → 📡 Control Remoto**

Configura:

| Campo           | Valor                                           |
| --------------- | ----------------------------------------------- |
| Interfaz de red | Selecciona la interfaz que contenga tu IP local |
| Puerto          | 9999 (o el que prefieras)                       |
| Token           | Contraseña de acceso                            |

Presiona:

✅ Guardar y activar

---

## 💻 Configurar ALP Cliente

Ingresa:

| Campo  | Valor                           |
| ------ | ------------------------------- |
| IP     | Dirección IPv4 del Host         |
| Puerto | El mismo configurado en el Host |
| Token  | El mismo configurado en el Host |

Ejemplo:

```text
IP:      192.168.1.100
Puerto:  9999
Token:   miClave2025
```

Presiona:

🔌 Probar conexión

---

## ⚠️ Desventaja de la IP Local

La mayoría de routers asignan direcciones automáticamente mediante DHCP.

Esto significa que la IP puede cambiar después de:

* Reiniciar la PC
* Reiniciar el router
* Pasar varios días sin utilizar el equipo

Por ejemplo:

```text
Hoy:      192.168.1.100
Mañana:   192.168.1.105
```

Si la IP cambia, el Cliente dejará de conectarse hasta actualizar la nueva dirección.

---

## 🔒 Solución: Reservar una IP Fija

Muchos routers permiten asignar siempre la misma IP a una PC específica.

Ejemplo:

```text
PC Host → Siempre 192.168.1.100
```

De esta forma la conexión local seguirá funcionando sin necesidad de actualizar la IP.

> 💡 La configuración depende de cada router y normalmente se encuentra en las opciones DHCP Reservation, Static Lease o Reserva DHCP.

---

# 🌍 Opción 2 — Conexión Remota con Tailscale (Recomendada)

## ❓ ¿Por qué usar Tailscale?

Cuando dos PCs están en redes distintas (casa y oficina, por ejemplo), normalmente no pueden comunicarse directamente porque:

* Las IPs locales (`192.168.x.x`) solo funcionan dentro de la misma red.
* Las IPs públicas suelen cambiar periódicamente.
* Abrir puertos en el router puede ser complicado o imposible.

Tailscale resuelve esto creando una red privada virtual segura entre tus dispositivos.

Cada equipo recibe una IP privada permanente que normalmente comienza con:

```text
100.x.x.x
```

Esta IP funciona sin importar dónde se encuentre el equipo.

---

## 🚀 Paso 1 — Instalar Tailscale

En ambas PCs:

1. Descarga Tailscale desde:
   https://tailscale.com/download

2. Instálalo.

3. Inicia sesión con la misma cuenta en ambas PCs.

Puedes utilizar:

* Google
* Microsoft
* GitHub
* Correo electrónico

> ⚠️ Ambas PCs deben estar dentro de la misma cuenta de Tailscale.

---

## ⚙️ Paso 2 — Configurar AppLocker Host

Abre:

**⚙ Configuración → 📡 Control Remoto**

Selecciona la interfaz de Tailscale.

Generalmente aparecerá una IP similar a:

```text
100.84.12.45
```

Configura:

| Campo           | Valor              |
| --------------- | ------------------ |
| Interfaz de red | Tailscale          |
| Puerto          | 9999               |
| Token           | Contraseña secreta |

Presiona:

✅ Guardar y activar

---

## 💡 Importante

El Puerto y el Token configurados en el Host deben coincidir exactamente con los configurados en el Cliente.

Si alguno es diferente, la conexión será rechazada.

---

## 💻 Paso 3 — Configurar ALP Cliente

Ingresa:

| Campo  | Valor                           |
| ------ | ------------------------------- |
| IP     | IP Tailscale del Host           |
| Puerto | El mismo configurado en el Host |
| Token  | El mismo configurado en el Host |

Ejemplo:

```text
IP:      100.84.12.45
Puerto:  9999
Token:   miClave2025
```

Presiona:

🔌 Probar conexión

Si todo está correcto aparecerá:

```text
✅ Conectado (pong | 2026-01-01 12:00:00)
```

---

# ✅ Funciones disponibles una vez conectado

Desde ALP Cliente podrás:

* 🔒 Bloquear y desbloquear aplicaciones remotamente.
* ⏰ Configurar desbloqueos temporales.
* 📅 Crear horarios programados.
* 🌐 Administrar sitios bloqueados con NetBlocker.
* 🖥️ Ver procesos activos.
* ❌ Finalizar procesos remotamente.
* 👁️ Ocultar o mostrar el icono de AppLocker.
* 🔑 Activar licencias remotamente.
* 🔄 Actualizar el Host sin acceso físico.

---

# 🔄 Resumen rápido

## 🏠 Conexión Local

| PC Host                                                                                                                                                                               | PC Cliente                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 1. Obtener IPv4 con `ipconfig`<br>2. Abrir AppLocker Host<br>3. Ir a **Control Remoto**<br>4. Configurar Puerto: `9999`<br>5. Configurar Token: `miClave2025`<br>6. Guardar y activar | 1. Abrir ALP Cliente<br>2. IP: `192.168.1.100`<br>3. Puerto: `9999`<br>4. Token: `miClave2025`<br>5. Probar conexión |

---

## 🌍 Conexión con Tailscale

| PC Host                                                                                                                                                                                                             | PC Cliente                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Instalar Tailscale<br>2. Iniciar sesión<br>3. Abrir AppLocker Host<br>4. Ir a **Control Remoto**<br>5. Seleccionar la interfaz Tailscale<br>6. Puerto: `9999`<br>7. Token: `miClave2025`<br>8. Guardar y activar | 1. Instalar Tailscale<br>2. Iniciar sesión<br>3. Abrir ALP Cliente<br>4. IP: `100.x.x.x`<br>5. Puerto: `9999`<br>6. Token: `miClave2025`<br>7. Probar conexión |

---

# 📊 Comparación de métodos

| Característica                    | IPv4 Local | IPv4 Local + IP Fija | Tailscale |
| --------------------------------- | ---------- | -------------------- | --------- |
| Funciona en la misma red          | ✅          | ✅                    | ✅         |
| Funciona entre redes distintas    | ❌          | ❌                    | ✅         |
| Requiere configuración del router | ❌          | ✅                    | ❌         |
| La IP puede cambiar               | ⚠️ Sí      | ❌ No                 | ❌ No      |
| Fácil de configurar               | ✅          | ⚠️ Intermedio        | ✅         |
| Recomendado para uso local        | ✅          | ⭐⭐⭐                  | ✅         |
| Recomendado para acceso remoto    | ❌          | ❌                    | ⭐⭐⭐       |

---

# ❗ Solución de problemas

| Problema                  | Solución                                                       |
| ------------------------- | -------------------------------------------------------------- |
| ❌ Conexión rechazada      | Verifica que el Host esté activo y el servidor esté habilitado |
| ❌ Timeout                 | Comprueba que ambas PCs tengan conexión de red                 |
| ❌ Token inválido          | Verifica que el Token sea idéntico en ambas aplicaciones       |
| ❌ No aparece IP Tailscale | Inicia sesión correctamente en Tailscale                       |
| ❌ La IP local cambió      | Configura una IP fija en el router                             |
| ❌ Trial expirado          | Activa una licencia desde Configuración → Licencia             |

---

# 🔒 ¿Es seguro?

Sí.

La comunicación está protegida mediante:

* Cifrado de red.
* Autenticación mediante Token.
* Configuración protegida localmente.

Además, cuando se utiliza Tailscale, todo el tráfico se cifra mediante WireGuard, uno de los protocolos VPN más seguros y modernos disponibles actualmente.

---

# ⭐ Recomendación

Si Host y Cliente siempre estarán dentro de la misma red, una IP local puede ser suficiente.

Si deseas evitar problemas por cambios de IP dentro de la red local, configura una IP fija en el router.

Si deseas conectarte desde cualquier lugar o administrar equipos ubicados en distintas redes, se recomienda utilizar Tailscale, ya que funciona tanto local como remotamente sin necesidad de abrir puertos ni realizar configuraciones avanzadas.

---

# ¿Necesitas ayuda?

Si tienes dudas o problemas con la configuración:

* 💬 **Telegram:** [@soporteantimalware](https://t.me/soporteantimalware)
* 📧 **Correo:** [soporteantimalware@gmail.com](mailto:soporteantimalware@gmail.com)

---

*Tutorial oficial para AppLocker Pro Nexus*
