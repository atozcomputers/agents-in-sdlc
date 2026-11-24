---
title: "Ejercicio 4 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has pedido a Copilot que asumiera tres tareas independientes centradas en mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente en la nube está diseñado para funcionar de forma asincrónica y autónoma, sigue siendo importante poder supervisar estas tareas.

Hay numerosas herramientas disponibles para gestionar las tareas asignadas al agente en la nube, incluida [la página de agentes][agents-page] en GitHub.com. Desde este centro de control puedes ver todas las tareas de agentes con solicitudes de incorporación de cambios abiertas. Puedes consultar las operaciones realizadas e incluso dirigir una sesión en curso para orientar su trabajo.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube;
- dirigirás una sesión en curso para solicitar funcionalidades adicionales.

## Escenario

Después de asignar al agente la creación de un modo de alto contraste, el equipo consideró que sería adecuado añadir también un modo claro. Como ya se estaba actualizando el estilo del sitio y añadiendo la funcionalidad de alternancia, parecía lógico incluir esta funcionalidad. Vas a dirigir el trabajo del agente para asegurarte de que añada tanto el modo claro como el de alto contraste.

## Revisar las tareas del agente en la nube de Copilot

Vamos a consultar el estado actual de todas las tareas asignadas al agente en la nube de Copilot.

1. Navega hasta la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas, tanto en el panel principal como en el panel izquierdo. Deberías ver las tareas que has asignado a Copilot, entre ellas:
    - Actualizar la documentación del código.
    - Generar API para modificar juegos.
    - Añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en ejecución. Revisa las tareas realizadas por Copilot. Pueden incluir:
    - Extraer el código del repositorio.
    - Crear el entorno de Copilot.
    - Configurar servidores MCP.
    - Realizar varios pasos para completar la tarea asignada.

> [!NOTE]
> Los pasos exactos varían según el estado del trabajo de Copilot y el enfoque que haya adoptado.

4. Observa también el panel de solicitudes de incorporación de cambios (PR) que aparece a la derecha. Permite ver la PR y los archivos modificados para realizar una supervisión adicional.

## Dirigir el agente en la nube

Ahora que has visto las tareas activas, vamos a solicitar a Copilot que incluya el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión correspondiente a la incorporación del modo de alto contraste. El título exacto variará según el nombre utilizado por Copilot y el estado actual del trabajo.

    ![Sesión de accesibilidad en mission control](../../../_images/ex6-accessibility-session.png)

2. Observa la sesión durante unos minutos, hasta que indique que ha terminado la configuración y ha comenzado el trabajo. Lo sabrás porque aparecerán mensajes similares a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, añade la siguiente indicación:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de pantalla de la tarea del agente en la nube en la página de agentes con el cuadro de diálogo Steer active session while Copilot is working resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar la indicación.
5. Observa cómo Copilot reconoce la indicación y la incorpora a su flujo.

## Dejar trabajar a Copilot

Igual que antes, Copilot se pondrá a trabajar en la tarea actualizada. Incorporará la nueva solicitud a su flujo después de completar el paso concreto en el que estaba trabajando cuando enviaste el mensaje.

Como antes, esto tardará varios minutos, así que es un buen momento para hacer una pausa y reflexionar sobre todo lo que has aprendido y explorado hasta ahora.

## Resumen y próximos pasos

Esta lección ha explorado la página de agentes de Copilot, tu centro principal para supervisar y orientar las tareas del agente en la nube de GitHub Copilot. Desde este mission control puedes seguir todas las tareas activas y completadas, revisar el trabajo realizado e incluso redirigir tareas en curso para ajustar su alcance o aportar indicaciones adicionales.

Has explorado estos conceptos:

- el uso de mission control y la página de agentes para supervisar las tareas del agente en la nube;
- la redirección de una sesión en curso para solicitar funcionalidades adicionales.

Mientras Copilot termina el trabajo sobre las funciones de accesibilidad, ahora podemos [iterar sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
