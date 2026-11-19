# COnfiguracion Basica

# Guía Rápida de SSH (Secure Shell)

**SSH** (*Secure Shell*) es un protocolo de red que permite acceder y administrar servidores remotos de forma segura mediante una conexión cifrada. Por defecto, opera a través del **puerto TCP 22**.

---

## 1. Conexión Básica

Para conectarte a un servidor remoto, utiliza la siguiente sintaxis en tu terminal:

```bash
ssh usuario@direccion_ip_o_dominio
```

* **Especificar un puerto diferente:** Si el servidor no usa el puerto 22, añade la bandera `-p`.
  ```bash
  ssh -p 2222 usuario@192.168.1.100
  ```
* **Cerrar la sesión:** Escribe `exit` o presiona `Ctrl + D`.

---

## 2. Autenticación con Claves SSH

Usar un par de claves (pública y privada) es mucho más seguro que usar contraseñas.

### Generar un par de claves
Ejecuta el siguiente comando en tu equipo local (se recomienda el algoritmo moderno **Ed25519**):

```bash
ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"
```

### Copiar la clave pública al servidor
Para autorizar tu equipo en el servidor remoto sin tener que copiar el archivo manualmente:

```bash
ssh-copy-id usuario@direccion_ip
```

---

## 3. Transferencia de Archivos

Puedes mover archivos de forma cifrada usando **SCP** (*Secure Copy Protocol*):

| Acción | Comando |
| :--- | :--- |
| **Subir** archivo al servidor | `scp archivo.txt usuario@ip:/ruta/destino/` |
| **Descargar** archivo del servidor | `scp usuario@ip:/ruta/archivo.txt ./ruta_local/` |
| **Copiar carpeta** completa | `scp -r carpeta/ usuario@ip:/ruta/destino/` |

---

## 4. Archivo de Configuración (`~/.ssh/config`)

Para evitar escribir direcciones IP, usuarios y puertos largos cada vez, puedes crear atajos en el archivo `~/.ssh/config`:

```text
Host mi-servidor
    HostName 192.168.1.100
    User admin
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
```

Con esta configuración, solo tendrás que ejecutar:

```bash
ssh mi-servidor
```

---

## 5. Buenas Prácticas de Seguridad

* **Deshabilitar el acceso como `root`:** Edita `/etc/ssh/sshd_config` en el servidor y cambia `PermitRootLogin no`.
* **Desactivar contraseñas:** Una vez configuradas las claves SSH, establece `PasswordAuthentication no` para evitar ataques de fuerza bruta.
* **Cambiar el puerto por defecto:** Modifica la línea `Port 22` por un número distinto para reducir el ruido de bots automatizados.


---
*Publicado desde la web de CASADOMOTICA (2º ASIR).*