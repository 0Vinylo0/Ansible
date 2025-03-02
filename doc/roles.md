# Roles en Ansible

Los roles en Ansible permiten estructurar y reutilizar configuraciones de manera modular. Son una forma organizada de agrupar tareas, archivos, plantillas y variables.

## Creación de un Rol

Para crear un rol, usa el comando:
```bash
ansible-galaxy init mi_rol
```
Esto generará la siguiente estructura:
```
mi_rol/
├── defaults/      # Variables por defecto
│   └── main.yml
├── files/         # Archivos estáticos
├── handlers/      # Tareas que se ejecutan cuando son notificadas
│   └── main.yml
├── meta/          # Metadatos del rol
│   └── main.yml
├── tasks/         # Lista de tareas principales
│   └── main.yml
├── templates/     # Plantillas Jinja2
├── tests/         # Pruebas para el rol
└── vars/          # Variables específicas del rol
    └── main.yml
```

## Uso de un Rol en un Playbook

Una vez creado el rol, se puede usar dentro de un playbook:
```yaml
- name: Configurar servidores web
  hosts: servidores_web
  roles:
    - mi_rol
```

## Configuración de Tareas en un Rol

El archivo `tasks/main.yml` define las tareas que ejecutará el rol.
```yaml
- name: Instalar Nginx
  apt:
    name: nginx
    state: present
  notify: Reiniciar Nginx
```

## Uso de Variables en Roles

Las variables pueden definirse en `defaults/main.yml` para valores predeterminados o en `vars/main.yml` para valores específicos del rol.
```yaml
# defaults/main.yml
paquete: nginx
```

Y se usan en `tasks/main.yml` así:
```yaml
- name: Instalar {{ paquete }}
  apt:
    name: "{{ paquete }}"
    state: present
```

## Uso de Handlers en Roles

Los handlers se definen en `handlers/main.yml` y se ejecutan cuando son notificados.
```yaml
- name: Reiniciar Nginx
  service:
    name: nginx
    state: restarted
```

## Uso de Plantillas en Roles

Las plantillas Jinja2 permiten generar archivos dinámicos. Se almacenan en `templates/` y se usan en las tareas:
```yaml
- name: Copiar configuración de Nginx
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: Reiniciar Nginx
```

Ejemplo de plantilla `nginx.conf.j2`:
```jinja
server {
    listen 80;
    server_name {{ ansible_hostname }};
}
```

## Conclusión

Los roles permiten estructurar configuraciones de Ansible de manera modular y reutilizable. Usando roles, se pueden organizar tareas, variables, archivos y plantillas de forma eficiente, facilitando la gestión y escalabilidad de las automatizaciones.
