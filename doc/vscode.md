# Configuración de Ansible en Visual Studio Code

Visual Studio Code (VS Code) es un editor ligero y potente que se puede utilizar para desarrollar y gestionar proyectos de Ansible con características como resaltado de sintaxis, autocompletado y ejecución de comandos.

## Instalación de VS Code
Si aún no tienes Visual Studio Code instalado, puedes descargarlo desde:
[https://code.visualstudio.com/](https://code.visualstudio.com/)

## Extensiones Recomendadas
Para mejorar la experiencia al trabajar con Ansible, se recomienda instalar las siguientes extensiones en VS Code:

### 1. **Ansible**
- Nombre: `redhat.ansible`
- Proporciona soporte para la sintaxis YAML de Ansible, autocompletado y validación.

### 2. **YAML**
- Nombre: `redhat.vscode-yaml`
- Mejora el soporte para archivos YAML, incluyendo validación y formato automático.

### 3. **Python** (Opcional, pero recomendado)
- Nombre: `ms-python.python`
- Si usas Ansible con Python, esta extensión proporciona resaltado de sintaxis y herramientas adicionales.

## Configuración de Extensiones

Después de instalar las extensiones, configura el soporte de YAML y Ansible agregando las siguientes opciones en `settings.json` de VS Code:

```json
{
  "ansible.validation.enabled": true,
  "yaml.schemas": {
    "https://json.schemastore.org/ansible-playbook": "/*.yml"
  }
}
```

Esto activará la validación automática para archivos `.yml` utilizados en Ansible.

## Integración con Ansible y Terminal

### Configuración de la Terminal para Ansible
Puedes configurar VS Code para ejecutar comandos de Ansible directamente desde su terminal integrada. Para ello:

1. Abre la terminal en VS Code (`Ctrl + Ñ` en Windows/Linux, `Cmd + Ñ` en macOS).
2. Navega al directorio de tu proyecto de Ansible.
3. Ejecuta comandos como:
   ```bash
   ansible-playbook playbook.yml
   ```

### Ejecutar Ansible con un Atajo de Teclado
Puedes configurar una tarea en VS Code para ejecutar Ansible con un atajo de teclado:

1. Abre `tasks.json` dentro de `.vscode/`.
2. Agrega lo siguiente:
   ```json
   {
     "version": "2.0.0",
     "tasks": [
       {
         "label": "Ejecutar Ansible Playbook",
         "type": "shell",
         "command": "ansible-playbook playbook.yml",
         "problemMatcher": []
       }
     ]
   }
   ```
3. Ahora puedes ejecutar `Ctrl + Shift + B` para correr el Playbook directamente.
