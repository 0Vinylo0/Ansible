# Comandos Ad-Hoc en Ansible

Los comandos ad-hoc en Ansible permiten ejecutar tareas puntuales en servidores remotos sin necesidad de escribir un playbook. Son útiles para comprobaciones rápidas o cambios temporales.

## Sintaxis Básica

La estructura general de un comando ad-hoc es:
```bash
ansible <grupo_de_hosts> -m <módulo> -a "<argumentos>"
```
Donde:
- `<grupo_de_hosts>`: Define los servidores objetivo (pueden estar en el inventario o usarse directamente con `-i` para indicar un archivo de inventario).
- `-m <módulo>`: Especifica el módulo de Ansible a utilizar.
- `-a "<argumentos>"`: Define los argumentos para el módulo.

## Ejemplos de Comandos Ad-Hoc

### 1. Comprobar Conectividad (Ping)
```bash
ansible all -m ping
```
Este comando verifica la conectividad entre Ansible y los nodos administrados.

### 2. Ejecutar Comandos Remotos
```bash
ansible all -m command -a "uptime"
```
Ejecuta `uptime` en todos los servidores y devuelve su estado.

```bash
ansible all -m shell -a "df -h"
```
Ejecuta `df -h` para ver el espacio en disco de los servidores.

### 3. Gestionar Servicios
```bash
ansible all -m service -a "name=nginx state=started"
```
Inicia el servicio `nginx` en todos los servidores.

```bash
ansible all -m service -a "name=nginx state=restarted"
```
Reinicia el servicio `nginx`.

### 4. Copiar Archivos
```bash
ansible all -m copy -a "src=/local/archivo.txt dest=/remoto/archivo.txt mode=0644"
```
Copia `archivo.txt` desde la máquina local a los servidores remotos.

### 5. Gestionar Usuarios
```bash
ansible all -m user -a "name=usuario state=present"
```
Crea el usuario `usuario` en todos los servidores.

```bash
ansible all -m user -a "name=usuario state=absent"
```
Elimina el usuario `usuario` de todos los servidores.

### 6. Instalar Paquetes
```bash
ansible all -m apt -a "name=htop state=present" -b
```
Instala `htop` en servidores Debian/Ubuntu (requiere sudo, por eso `-b`).

```bash
ansible all -m yum -a "name=htop state=present" -b
```
Instala `htop` en servidores RHEL/CentOS.

### 7. Modificar Permisos
```bash
ansible all -m file -a "path=/ruta/archivo mode=0644"
```
Cambia los permisos del archivo en los servidores remotos.

### 8. Obtener Información del Sistema
```bash
ansible all -m setup
```
Muestra información detallada sobre los servidores remotos (RAM, CPU, interfaces de red, etc.).

