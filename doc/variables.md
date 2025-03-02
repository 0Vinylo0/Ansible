# Variables en Ansible

Las variables en Ansible permiten hacer los Playbooks más dinámicos y reutilizables, facilitando la administración de configuraciones en diferentes entornos.

## Definición de Variables

### Variables en el Playbook
Las variables pueden definirse directamente dentro del Playbook:
```yaml
- name: Configurar servidor web
  hosts: servidores_web
  vars:
    paquete: nginx
  tasks:
    - name: Instalar {{ paquete }}
      apt:
        name: "{{ paquete }}"
        state: present
```

### Variables en Archivos Externos
Se pueden almacenar variables en archivos YAML para mayor organización:
```yaml
# variables.yml
paquete: nginx
```

Se incluyen en el Playbook con:
```yaml
vars_files:
  - variables.yml
```

## Uso de `host_vars` y `group_vars`

Las variables pueden asignarse a hosts o grupos específicos creando directorios `host_vars/` y `group_vars/` dentro del inventario.

Ejemplo:
```
inventario/
  host_vars/
    servidor1.yml
  group_vars/
    servidores_web.yml
```

`host_vars/servidor1.yml`:
```yaml
paquete: apache2
```

`group_vars/servidores_web.yml`:
```yaml
paquete: nginx
```

## Variables en la Línea de Comandos

Se pueden definir variables en la ejecución de `ansible-playbook`:
```bash
ansible-playbook playbook.yml -e "paquete=apache2"
```

## Factores de Ansible (`ansible_facts`)

Ansible puede recopilar información del sistema automáticamente:
```yaml
- name: Mostrar información del sistema
  hosts: all
  tasks:
    - name: Ver nombre del sistema operativo
      debug:
        msg: "El sistema operativo es {{ ansible_distribution }}"
```

Algunos `ansible_facts` comunes:
- `ansible_os_family` → Familia del SO (Debian, RedHat, etc.)
- `ansible_hostname` → Nombre del host
- `ansible_default_ipv4.address` → Dirección IP del servidor

## Uso de `set_fact`

Se pueden definir variables dinámicamente en tiempo de ejecución:
```yaml
- name: Definir variable dinámica
  hosts: all
  tasks:
    - name: Guardar fecha actual en una variable
      set_fact:
        fecha: "{{ ansible_date_time.date }}"
    - name: Mostrar la fecha guardada
      debug:
        msg: "La fecha es {{ fecha }}"
```

## Conclusión

Las variables en Ansible permiten flexibilizar los Playbooks, hacer configuraciones reutilizables y gestionar múltiples entornos de manera eficiente. El uso adecuado de `vars`, `vars_files`, `host_vars`, `group_vars`, `ansible_facts` y `set_fact` facilita la automatización avanzada.
