# Obligatorio Taller de Servidores Linux

Este repositorio contiene la implementación del obligatorio del **Taller de servidores Linux** de la universidad ORT que tiene como objetivo aplicar los conocimientos básicos de Ansible sobre dos distribuciones Linux: Centos Stream 9 y Ubuntu 24.04.


## Estructura del proyecto

```plaintext
obligatorioTallerLinux/
├── collections/
│   └── requirements.yml
├── inventories/
│   ├── group_vars/
│   │   └── linux.yml
│   └── servers.ini
├── results/
├── templates/
│   ├── index.j2
│   └── virtualhost.j2
├── playbooks/
│   ├── webserver.yml
│   ├── hardening.yml
│   └── updates.yml
├── LICENSE
├── README.md
└── ansible_report.md
```

## Configuración

1.  Clonar el repositorio:
   ```bash
   git clone https://github.com/jennilopez/obligatorioTallerLinux.git
   ```
2.  Configurar el inventario en inventories/inventory.ini
3.  Probar conexión con Ansible:
   ```bash
   ansible all -i inventories/servers.ini -m ping
   ```

## Requisitos previos

Las colecciones necesarias están definidas en collections/requirements.yml. Instalación:
   ```bash
   ansible-galaxy collection install -r collections/requirements.yml
   ```

## Documentación

La documentación completa sobre la ejecución de los comandos ad-hoc y playbooks, junto con capturas de pantalla y análisis, se encuentra en [`documento.md`](documento.md).

Este archivo contiene:
- Salidas de los comandos ejecutados.
- Capturas de pantalla guardadas en `results/`.
- Explicación de cada playbook y su impacto en los servidores.
- Respuestas a las preguntas teóricas sobre Ansible.
