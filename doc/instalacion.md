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
