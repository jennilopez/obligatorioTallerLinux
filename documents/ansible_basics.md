# Respuestas a preguntas teóricas sobre Ansible

## ¿Qué es Ansible y por qué es "sin agente" (agentless)?
Ansible es una herramienta de automatización de código abierto para gestión de servidores. Se destaca por ser "agentless", lo que significa que no requiere instalar software adicional en los servidores gestionados, en lugar de utilizar agentes que consumen recursos y requieren mantenimiento, Ansible se conecta a los servidores mediante SSH (para Linux) o WinRM (para Windows) y ejecuta las tareas de manera remota.

Fuente: [`Introducción a Ansible`](https://docs.ansible.com/ansible/latest/getting_started/introduction.html)

## Explica la diferencia entre un comando ad-hoc y un playbook
Los comandos ad-hoc en Ansible permiten ejecutar una sola tarea puntual sin necesidad de definir un archivo estructurado. Son ideales para tareas que rara vez se repiten, como verificar el estado de un servicio.

Por otro lado, un playbook es un conjunto de tareas organizadas en un archivo YAML, permitiendo definir configuraciones estructuradas y gestionarlas de manera automatizada.

Fuente: [`Introducción a los comandos ad hoc`](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html), 
[`Playbooks Ansible`](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html)

## ¿Qué es la idempotencia y por qué es importante en Ansible?
La idempotencia en Ansible significa que una misma tarea puede ejecutarse múltiples veces sin cambiar el estado final del sistema si este ya está correctamente configurado.

Esto sucede porque las tareas en un playbook definen el estado deseado de un sistema, entonces antes de aplicar cambios, Ansible evalúa si el sistema ya se encuentra en el estado definido.

Esto permite aplicar configuraciones sin preocuparse de generar cambios innecesarios. Si un recurso ya está en el estado deseado, Ansible no realiza ninguna modificación, lo que evita configuraciones repetitivas y reduce el riesgo de errores.

Fuente: [`Estado deseado e idempotencia`](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html#desired-state-and-idempotency)


## ¿Cómo funcionan los handlers y cuándo deberías usarlos?
Los handlers en Ansible son tareas especiales que solo se ejecutan si una tarea cambia el estado del sistema. Se usan principalmente para acciones que deben ocurrir después de una modificación, como reiniciar un servicio cuando su archivo de configuración ha cambiado.

Un handler no se ejecuta automáticamente en cada ejecución del playbook, sino que debe ser notificado por una tarea. Si varias tareas notifican el mismo handler, este solo se ejecutará una vez al final del playbook, optimizando la ejecución.

Fuente: [`Handlers: operaciones de ejecución en caso de cambio`](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html)

## ¿Cómo verificas errores de sintaxis en un playbook de Ansible?

Para verificar errores en un playbook antes de ejecutarlo, se pueden utilizar varias herramientas:

**Modo `--syntax-check` en Ansible**

   ```bash
   ansible-playbook playbook.yml --syntax-check
   ```

Este comando revisa la sintaxis YAML del playbook sin ejecutarlo. Detecta errores estructurales, como indentación incorrecta o palabras clave mal escritas.

**Uso de `ansible-lint`**

   ```bash
   ansible-lint playbook.yml
   ```

ansible-lint no solo verifica la sintaxis, sino que también analiza buenas prácticas en la escritura de playbooks, identificando errores comunes y sugiriendo mejoras.

**Check Mode (`--check`)**

   ```bash
   ansible-playbook playbook.yml --check
   ```

El modo check permite ejecutar el playbook en modo simulación, mostrando los cambios que se aplicarían sin modificar realmente el sistema. No todos los módulos de Ansible soportan esta opción, por lo que es importante verificar la compatibilidad con las tareas utilizadas.

Fuente: [`Verificación de playbooks`](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html#verifying-playbooks), 
[`Ejecución de playbooks en modo de verificación`](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html#running-playbooks-in-check-mode)