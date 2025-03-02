# Inventario en Ansible

El inventario en Ansible es un archivo que define los hosts y grupos de servidores sobre los que se ejecutarán las tareas. El archivo de inventario predeterminado se encuentra en `/etc/ansible/hosts`, pero también se pueden definir inventarios personalizados.

## Formato del Inventario
Ansible permite definir el inventario en formato INI o YAML.

### Formato INI (Clásico)
```ini
[servidores_web]
192.168.1.10
192.168.1.11

[servidores_db]
db1.example.com

[servidores]
192.168.1.10
192.168.1.11
192.168.1.20
```
- `[servidores_web]`, `[servidores_db]`: Definen grupos de servidores.
- Se pueden utilizar nombres de dominio o direcciones IP.

### Formato YAML (Más moderno)
```yaml
all:
  children:
    servidores_web:
      hosts:
        192.168.1.10:
        192.168.1.11:
    servidores_db:
      hosts:
        db1.example.com:
```

## Uso de Variables en el Inventario
Se pueden definir variables específicas para los hosts o grupos.

### Variables por Host
```ini
[servidores_web]
192.168.1.10 ansible_user=ubuntu ansible_port=22 ansible_python_interpreter=/usr/bin/python3
```

### Variables por Grupo
```ini
[servidores_web:vars]
ansible_user=ubuntu
ansible_port=22
```

### Formato YAML para Variables
```yaml
all:
  children:
    servidores_web:
      hosts:
        192.168.1.10:
      vars:
        ansible_user: ubuntu
        ansible_port: 22
```

## Especificar Inventario en la Línea de Comandos
Para utilizar un inventario personalizado, se puede especificar con `-i`:
```bash
ansible all -m ping -i mi_inventario.ini
```

## Inventario Dinámico
El inventario también puede ser dinámico, obteniendo los hosts de AWS, Kubernetes u otros servicios mediante scripts o plugins.
```bash
ansible-inventory -i script_dinamico.py --list
```

## Verificar el Inventario
Para ver los hosts disponibles en un inventario, usa:
```bash
ansible-inventory --list -i inventario.ini
```

## Conclusión
El inventario es una parte clave en Ansible que permite organizar los servidores de manera flexible. Se puede definir en INI, YAML o de forma dinámica según las necesidades del entorno.
