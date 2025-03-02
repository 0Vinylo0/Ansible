# Instalación de Ansible

Ansible es una herramienta de automatización que permite gestionar la configuración y despliegue de servidores sin necesidad de instalar agentes en los nodos remotos. A continuación, se presentan los pasos para instalar Ansible en diferentes sistemas operativos.

## Instalación en Linux

### Ubuntu/Debian
```bash
sudo apt update && sudo apt install -y ansible
```

### CentOS/RHEL
```bash
sudo dnf install -y ansible
```

## Instalación en macOS

Si utilizas Homebrew, puedes instalar Ansible con:
```bash
brew install ansible
```

## Instalación en Windows

En Windows, se recomienda utilizar el Subsistema de Windows para Linux (WSL) o una máquina virtual. Sin embargo, también puedes instalar Ansible mediante `pip` en un entorno Python:
```bash
pip install ansible
```

## Verificación de la Instalación

Para comprobar que Ansible se ha instalado correctamente, ejecuta:
```bash
ansible --version
```

Si el comando muestra la versión de Ansible instalada, significa que la instalación ha sido exitosa.

## Configuración de SSH para Ansible

Ansible se conecta a los servidores mediante SSH, por lo que es necesario configurar claves SSH para una conexión sin contraseña.

### Generar una clave SSH
Si aún no tienes una clave SSH generada, puedes crearla con:
```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@example.com"
```
Presiona `Enter` para aceptar la ubicación por defecto y establece (o no) una contraseña para mayor seguridad.

### Copiar la clave al servidor
Para permitir la conexión sin contraseña, copia la clave pública al servidor remoto:
```bash
ssh-copy-id usuario@servidor_remoto
```
Si el comando `ssh-copy-id` no está disponible, puedes copiar la clave manualmente ejecutando:
```bash
cat ~/.ssh/id_rsa.pub
```
Y luego agregando el contenido al archivo `~/.ssh/authorized_keys` del usuario en el servidor remoto.

### Probar la conexión SSH
Una vez configurado SSH, prueba la conexión con:
```bash
ssh usuario@servidor_remoto
```
Si puedes acceder sin introducir una contraseña, significa que la configuración SSH está lista para usar con Ansible.
