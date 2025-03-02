# Configuración de Ansible

El fichero de configuración de Ansible (`ansible.cfg`) permite personalizar el comportamiento de Ansible, definiendo opciones como la ubicación del inventario, los métodos de conexión y la gestión de privilegios.

## Ubicación del Archivo `ansible.cfg`

Ansible busca su configuración en los siguientes lugares en este orden:
1. **Variable de entorno** `ANSIBLE_CONFIG`.
2. **En el directorio actual** (`./ansible.cfg`).
3. **En el directorio del usuario** (`~/.ansible.cfg`).
4. **En la configuración global** (`/etc/ansible/ansible.cfg`).

Se recomienda colocar el archivo `ansible.cfg` en la raíz de tu proyecto para una configuración específica.

## Estructura Básica de `ansible.cfg`

```ini
[defaults]
inventory = ./inventario.ini  # Define el inventario
remote_user = ubuntu           # Usuario por defecto para SSH
ask_pass = false               # No pedir contraseña al conectar
private_key_file = ~/.ssh/id_rsa  # Archivo de clave privada
host_key_checking = false      # No verificar claves SSH

[privilege_escalation]
become = True                  # Habilitar sudo
become_method = sudo           # Método de escalado de privilegios
become_ask_pass = False        # No preguntar contraseña sudo

[ssh_connection]
timeout = 30                   # Tiempo de espera para conexiones SSH
pipelining = True              # Mejora el rendimiento reduciendo conexiones SSH
```

## Explicación de las Opciones
- **`inventory`**: Especifica el archivo de inventario a utilizar.
- **`remote_user`**: Define el usuario por defecto con el que se conectará a los nodos.
- **`ask_pass`**: Si está en `false`, no pedirá contraseña, útil para claves SSH.
- **`private_key_file`**: Especifica la clave privada para autenticación SSH.
- **`host_key_checking`**: Si está en `false`, evita advertencias de claves SSH.
- **`become`**: Habilita el uso de `sudo` para ejecutar comandos con privilegios.
- **`become_method`**: Define el método de escalado de privilegios (`sudo`, `su`, etc.).
- **`become_ask_pass`**: Si `false`, no pedirá contraseña al usar `sudo`.
- **`timeout`**: Tiempo máximo en segundos antes de que una conexión SSH falle.
- **`pipelining`**: Mejora el rendimiento al reducir conexiones SSH innecesarias.

## Aplicar la Configuración
Para asegurarte de que Ansible está usando el archivo `ansible.cfg` correcto, puedes ejecutar:
```bash
ansible --version
```
Esto mostrará la ubicación del archivo de configuración en uso.

## Conclusión
El fichero `ansible.cfg` permite personalizar la ejecución de Ansible según las necesidades del proyecto. Una configuración bien optimizada puede mejorar la seguridad y el rendimiento de la automatización.
