# Otros Módulos en Ansible

Además de los módulos más comunes (`ping`, `service`, `package`, `copy`, `command`, etc.), Ansible cuenta con una gran variedad de módulos que facilitan la administración de servidores, configuración de redes, gestión de bases de datos y mucho más.

## 1. Módulos para Gestión de Archivos
Estos módulos permiten manipular archivos y directorios en servidores remotos.

### Crear un directorio
```yaml
- name: Crear un directorio
  file:
    path: /opt/mi_directorio
    state: directory
    mode: '0755'
```

### Borrar un archivo
```yaml
- name: Eliminar un archivo
  file:
    path: /tmp/archivo.txt
    state: absent
```

## 2. Módulos para Gestión de Usuarios y Grupos

### Crear un usuario
```yaml
- name: Crear un usuario
  user:
    name: juan
    state: present
    shell: /bin/bash
```

### Agregar un usuario a un grupo
```yaml
- name: Agregar usuario a un grupo
  user:
    name: juan
    groups: sudo
    append: yes
```

## 3. Módulos para Administración de Bases de Datos
Ansible permite gestionar bases de datos como MySQL y PostgreSQL.

### Crear una base de datos en MySQL
```yaml
- name: Crear una base de datos en MySQL
  mysql_db:
    name: mi_base_de_datos
    state: present
    login_user: root
    login_password: contraseña
```

### Crear un usuario en PostgreSQL
```yaml
- name: Crear un usuario en PostgreSQL
  postgresql_user:
    db: mi_base
    name: usuario
    password: contraseña_segura
    state: present
```

## 4. Módulos para Administración de Redes
Estos módulos permiten configurar interfaces de red, firewalls y dispositivos de red.

### Configurar una interfaz de red en Linux
```yaml
- name: Configurar una interfaz de red
  nmcli:
    conn_name: eth0
    ifname: eth0
    type: ethernet
    ip4: 192.168.1.100/24
    gw4: 192.168.1.1
    state: present
```

### Configurar reglas de firewall con UFW
```yaml
- name: Permitir tráfico en el puerto 80
  ufw:
    rule: allow
    port: 80
    proto: tcp
```

## 5. Módulos para Administración de Servicios en la Nube
Ansible permite administrar recursos en AWS, Azure y GCP.

### Crear una instancia en AWS EC2
```yaml
- name: Crear una instancia en AWS
  ec2_instance:
    name: mi_servidor
    key_name: mi_clave
    instance_type: t2.micro
    image_id: ami-12345678
    region: us-east-1
    count: 1
    state: running
```

## 6. Módulos para Manejo de Tareas en Paralelo

### Esperar a que un puerto esté abierto
```yaml
- name: Esperar a que el puerto 22 esté abierto
  wait_for:
    port: 22
    timeout: 30
```

### Ejecutar tareas en segundo plano
```yaml
- name: Ejecutar una tarea en segundo plano
  command: "long_running_script.sh"
  async: 300
  poll: 0
```

## Conclusión
Ansible cuenta con una gran cantidad de módulos que permiten automatizar diversas tareas. Conocer y utilizar estos módulos puede simplificar y optimizar la administración de servidores, bases de datos, redes y servicios en la nube.
