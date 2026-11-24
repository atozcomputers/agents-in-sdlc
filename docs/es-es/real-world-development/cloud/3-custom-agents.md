---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## Qué son los agentes personalizados

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o ámbitos específicos dentro del flujo de trabajo de desarrollo. Al definir agentes mediante archivos Markdown en la carpeta `.github/agents` del repositorio, puedes proporcionar a Copilot instrucciones centradas, mejores prácticas, patrones de programación y conocimientos específicos del dominio que guían su trabajo de forma más eficaz. Los equipos pueden convertir su experiencia en agentes reutilizables: un agente de accesibilidad que exige el cumplimiento de [WCAG][wcag], un agente de seguridad que siga prácticas de programación segura o un agente de pruebas que mantenga patrones de prueba coherentes.

Los agentes personalizados se definen mediante archivos Markdown en la carpeta `.github/agents` del proyecto o de forma global en `~/.copilot/agents`. Cada archivo tiene frontmatter YAML con, como mínimo, los campos `name` y `description`, seguido de una instrucción Markdown que define el comportamiento, la experiencia y las indicaciones del agente.

### Agentes personalizados frente a habilidades de agente

Existe cierta coincidencia conceptual entre los agentes personalizados y las [habilidades de agente][agent-skills-concept]. Ambos se definen principalmente mediante archivos Markdown y indican a una IA cómo realizar operaciones. La forma más clara de distinguirlos es: un **agente personalizado** es el trabajador y las **habilidades** son herramientas.

Los agentes personalizados tienen su propia ventana de contexto y están diseñados para orquestar habilidades (y hasta otros agentes) mientras realizan su trabajo. En este laboratorio, el agente personalizado de accesibilidad revisa y actualiza el sitio conforme a las directrices de accesibilidad; como parte de ese trabajo podría invocar habilidades como una habilidad de flujo de trabajo de solicitudes de incorporación de cambios o una habilidad que ejecuta y gestiona pruebas.

> [!NOTE]
> No existe una única forma «correcta» de crear un agente personalizado. Como ocurre con la IA, prueba e itera para descubrir qué funciona mejor en tus entornos y escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Explorarás lo siguiente con los agentes personalizados:

- cómo se definen los agentes personalizados;
- cómo asignar una tarea a un agente personalizado.

## Escenario

Tailspin Toys se compromete a garantizar que su plataforma de financiación colectiva sea accesible para todas las personas, independientemente de sus capacidades o preferencias visuales. Los comentarios recientes de las personas usuarias han señalado que algunas encuentran difícil leer el tema oscuro actual debido al contraste insuficiente entre el texto y los colores de fondo. Para solucionar este problema de accesibilidad, el equipo de diseño ha solicitado implementar un modo de alto contraste que las personas usuarias puedan activar y desactivar.

Como la accesibilidad es fundamental, quieres asegurarte de que se implemente lo antes posible. Utilizarás un agente personalizado para generar la funcionalidad.

## Revisar el agente personalizado de accesibilidad

Ya se ha creado para ti un agente personalizado de accesibilidad. Vamos a revisar su contenido para comprender cómo orientará a Copilot.

Vuelve a tu codespace y revisa el archivo del agente personalizado de accesibilidad:

1. Abre `.github/agents/accessibility.md`.
2. Observa el frontmatter YAML con los campos `name` y `description`.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

3. Después, examina las secciones siguientes, que destacan:
   - Responsabilidades principales al generar código para un sitio web accesible.
   - Mejores prácticas de accesibilidad.
   - Ejemplos de código en HTML, CSS y JavaScript.
   - Una lista de errores y problemas comunes.

## Crear y asignar una incidencia

Mission control es la ubicación central para trabajar con todos los agentes de tu entorno. Puedes asignar tareas al agente en la nube de Copilot, supervisarlas e incluso redirigirlas y proporcionar orientación adicional. Comencemos asignando una tarea para crear el modo de alto contraste a Copilot.

1. Navega hasta tu repositorio.
2. Selecciona la pestaña Issues.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para crear la nueva incidencia.
5. Establece el **Title** como `Add high contrast mode to website`.
6. Establece el **Description** con:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lateral derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.
9. Selecciona **Accessibility agent** en la lista de agentes personalizados.

    ![Captura de pantalla de la asignación del agente en la nube, con el agente personalizado y Accessibility resaltados](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.
11. Copilot comenzará a trabajar en la tarea en segundo plano.

## Resumen y próximos pasos

Esta lección ha explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes de IA especializados adaptados a tareas y ámbitos concretos. Con los agentes personalizados puedes incorporar la experiencia y los estándares de tu equipo a agentes reutilizables que orientan a Copilot para realizar determinados tipos de trabajo de forma más eficaz.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados;
- cómo asignar una tarea a un agente personalizado.

Con Copilot trabajando en la implementación del modo de alto contraste, podemos ahora [supervisar y dirigir la sesión del agente][next-lesson] desde mission control.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparación para utilizar agentes personalizados en tu organización][org-custom-agents]
- [Preparación para utilizar agentes personalizados en tu empresa][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
