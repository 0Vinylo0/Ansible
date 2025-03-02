# Gestión de Servicios en Ansible

Ansible permite gestionar servicios en servidores remotos de manera sencilla utilizando el módulo `service` o `systemd`. Esto permite iniciar, detener, reiniciar y habilitar servicios para que se ejecuten automáticamente al inicio del sistema.

## Control de Servicios con `service`
El módulo `service` funciona con sistemas basados en SysVinit y systemd. Ejemplo de uso:

```yaml
- name: Administrar servicios con service
  hosts: servidores
  become: yes
  tasks:
    - name: Iniciar servicio Nginx
      service:
        name: nginx
        state: started

    - name: Detener servicio Apache
      service:
        name: apache2
        state: stopped

    - name: Reiniciar servicio MySQL
      service:
        name: mysql
        state: restarted
```

## Control de Servicios con `systemd`
Si los servidores usan systemd, se recomienda el módulo `systemd`:

```yaml
- name: Administrar servicios con systemd
  hosts: servidores
  become: yes
  tasks:
    - name: Habilitar Nginx al inicio
      systemd:
        name: nginx
        enabled: yes

    - name: Deshabilitar Apache al inicio
      systemd:
        name: apache2
        enabled: no
```

## Verificar el Estado de un Servicio
Para comprobar si un servicio está activo:

```yaml
- name: Verificar si Nginx está activo
  command: systemctl is-active nginx
  register: nginx_status
  changed_when: false

- name: Mostrar estado de Nginx
  debug:
    msg: "El estado de Nginx es {{ nginx_status.stdout }}"
```

## Uso de Handlers para Reiniciar Servicios
Los handlers permiten reiniciar servicios solo cuando hay cambios:

```yaml
- name: Configurar servidor web
  hosts: servidores
  become: yes
  tasks:
    - name: Modificar configuración de Nginx
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Reiniciar Nginx

  handlers:
    - name: Reiniciar Nginx
      service:
        name: nginx
        state: restarted
```

## Conclusión
Ansible facilita la administración de servicios en servidores remotos. Usando `service` o `systemd`, se pueden iniciar, detener y habilitar servicios, asegurando un control eficiente en entornos automatizados.
