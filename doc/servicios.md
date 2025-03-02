# Gestión de Servicios en Ansible

Ansible permite administrar servicios en servidores remotos mediante el módulo `service`, `systemd` y otros módulos específicos según el sistema operativo.

## Uso del Módulo `service`
El módulo `service` es compatible con la mayoría de sistemas operativos y permite iniciar, detener y reiniciar servicios.

### Iniciar un Servicio
```yaml
- name: Iniciar Nginx
  service:
    name: nginx
    state: started
```

### Detener un Servicio
```yaml
- name: Detener Nginx
  service:
    name: nginx
    state: stopped
```

### Reiniciar un Servicio
```yaml
- name: Reiniciar Nginx
  service:
    name: nginx
    state: restarted
```

### Habilitar un Servicio al Inicio
```yaml
- name: Habilitar Nginx al inicio
  service:
    name: nginx
    enabled: yes
```

## Uso del Módulo `systemd`
En sistemas modernos basados en `systemd`, se recomienda usar el módulo `systemd` para mayor compatibilidad.

### Iniciar un Servicio con `systemd`
```yaml
- name: Iniciar Nginx con systemd
  systemd:
    name: nginx
    state: started
```

### Recargar un Servicio sin Interrupción
```yaml
- name: Recargar Nginx
  systemd:
    name: nginx
    state: reloaded
```

## Comprobación del Estado de un Servicio
Para asegurarse de que un servicio está corriendo, se puede usar la tarea con el módulo `service_facts`:
```yaml
- name: Obtener información de los servicios
  service_facts:

- name: Verificar si Nginx está activo
  debug:
    msg: "Nginx está corriendo"
  when: ansible_facts.services['nginx.service'].state == "running"
```

## Uso de Handlers para Reiniciar Servicios
Los handlers permiten reiniciar un servicio solo si una tarea anterior ha cambiado algo.
```yaml
- name: Instalar Nginx y configurar servicio
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

## Conclusión
La gestión de servicios con Ansible es sencilla y flexible. Se recomienda utilizar `systemd` en sistemas modernos y `service` en entornos heredados. Además, los handlers permiten reiniciar servicios de forma eficiente solo cuando es necesario.
