# Playbooks en Ansible

Los Playbooks en Ansible permiten definir configuraciones y tareas en servidores de manera estructurada utilizando YAML. Son la forma más poderosa de automatización en Ansible.

## Estructura Básica de un Playbook

Un playbook está compuesto por una lista de `plays`, cada uno de los cuales define:
- **Hosts**: Los servidores donde se ejecutará el playbook.
- **Tareas (tasks)**: Acciones que se realizarán en los servidores.
- **Roles y Variables (opcional)**: Para organizar mejor la configuración.

Ejemplo básico:
```yaml
- name: Configurar servidores web
  hosts: servidores_web
  become: yes  # Usar sudo
  tasks:
    - name: Instalar Nginx
      apt:
        name: nginx
        state: present
    
    - name: Iniciar Nginx
      service:
        name: nginx
        state: started
```

## Ejecutar un Playbook

Para ejecutar un playbook, usa:
```bash
ansible-playbook playbook.yml
```
Si se necesita sudo:
```bash
ansible-playbook playbook.yml --ask-become-pass
```

## Uso de Variables

Las variables permiten hacer los playbooks más dinámicos. Se pueden definir en el propio playbook:
```yaml
- name: Configurar servidores
  hosts: servidores_web
  vars:
    paquete: nginx
  tasks:
    - name: Instalar {{ paquete }}
      apt:
        name: "{{ paquete }}"
        state: present
```

También pueden definirse en archivos separados:
```yaml
vars_files:
  - variables.yml
```

## Uso de Handlers

Los handlers son tareas que solo se ejecutan si han sido notificadas por otra tarea:
```yaml
- name: Configurar servidor
  hosts: servidores_web
  tasks:
    - name: Instalar Nginx
      apt:
        name: nginx
        state: present
      notify: Reiniciar Nginx
  
  handlers:
    - name: Reiniciar Nginx
      service:
        name: nginx
        state: restarted
```

## Uso de Loops

Los loops permiten ejecutar una tarea varias veces con diferentes valores:
```yaml
- name: Crear usuarios
  user:
    name: "{{ item }}"
    state: present
  loop:
    - usuario1
    - usuario2
    - usuario3
```

## Uso de Condiciones

Se pueden usar condiciones para ejecutar tareas solo en ciertos casos:
```yaml
- name: Instalar Apache solo en Debian
  apt:
    name: apache2
    state: present
  when: ansible_os_family == "Debian"
```

## Playbooks con Roles

Para organizar mejor los playbooks, se recomienda el uso de roles:
```yaml
- name: Aplicar configuración
  hosts: servidores_web
  roles:
    - rol_webserver
```

Los roles permiten estructurar tareas, variables y archivos en un formato reutilizable.

## Conclusión

Los playbooks son la base de la automatización en Ansible. Al combinarlos con variables, handlers, loops y roles, se pueden crear configuraciones flexibles y escalables.
