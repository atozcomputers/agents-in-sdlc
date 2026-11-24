---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

## Revisar el trabajo

A lo largo de este laboratorio has trabajado con GitHub Copilot en varias tareas centradas en mejorar la experiencia de usuario y añadir funcionalidades. Has pedido a Copilot que añada documentación al código, cree una funcionalidad de juegos relacionados para que el equipo de diseño pueda iterar sobre ella e implemente funciones de accesibilidad, incluidos los modos de alto contraste y claro. Vamos a explorar los cambios de código y, si fuera necesario, proporcionar comentarios a Copilot para mejorar su trabajo.

### Escenario

Como se ha señalado numerosas veces, los fundamentos del diseño de software y de DevOps no cambian al incorporar IA generativa. Siempre queremos revisar el código generado y seguir nuestro proceso habitual de DevOps. Con esto en mente, revisemos las propuestas de GitHub Copilot para crear la documentación, la funcionalidad de juegos relacionados y las funciones de accesibilidad antes de habilitar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

Como el agente en la nube de Copilot realiza sus tareas de forma asincrónica y sin supervisión, se han establecido determinadas restricciones de seguridad para mantener todo protegido. Entre ellas:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utilizará para el código.
- El agente en la nube se ejecuta dentro de GitHub Actions, donde crea un entorno separado y efímero en el que trabajar.
- Cualquier flujo de trabajo de GitHub Actions requiere la aprobación de una persona antes de ejecutarse.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores MCP.

## Revisar la documentación generada

Empecemos explorando la primera solicitud de incorporación de cambios (PR) creada por el agente en la nube de GitHub Copilot: la incorporación de documentación al código. Realizarás esta tarea mediante la interfaz estándar de PR en GitHub.com.

> [!NOTE]
> Al explorar la PR puedes ver una advertencia sobre que GitHub Copilot está bloqueado por un cortafuegos. Esto **es lo esperado**, ya que Copilot tiene acceso limitado a recursos externos de forma predeterminada, incluidas las llamadas a servidores MCP externos. Si quieres, puedes [personalizar o desactivar el cortafuegos del agente en la nube][agent-firewall].

1. Vuelve a tu repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes de incorporación de cambios.
3. Abre la solicitud cuyo título sea similar a **Add missing documentation** o uno más elaborado.

> [!NOTE]
> Si Copilot sigue trabajando en la tarea, la solicitud de incorporación de cambios contendrá el indicador **[WIP]**. En ese caso, espera a que Copilot termine el trabajo. Puede tardar unos minutos, así que puedes tomar un descanso o reflexionar sobre todo lo que has aprendido hasta ahora.

4. Cuando la solicitud esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

    ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Examina el código actualizado, que incluye los nuevos comentarios TSDoc y otra documentación. Los cambios exactos pueden variar.

    Al revisar los cambios, busca comentarios TSDoc, convenciones de TypeScript y encabezados de comentario. Proceden de los archivos de instrucciones personalizados que revisaste al comienzo del Ejercicio 2.

6. Una vez que hayas revisado las actualizaciones y todo tenga el aspecto correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que indica que algunos flujos de trabajo esperan aprobación.
8. Si los flujos de trabajo esperan aprobación, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Deberías ver los flujos de trabajo en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto pasarán para la aplicación Astro. Puede tardar unos minutos.

## Solicitar cambios a GitHub Copilot

Trabajar con Copilot en una solicitud de incorporación de cambios no tiene por qué ser una vía de sentido único. También puedes etiquetar a Copilot en comentarios, como harías con otros miembros del equipo, dentro de la solicitud o en comentarios en línea sobre el código. Copilot verá estos comentarios y iniciará otra sesión para atenderlos. Debido a los resultados no deterministas, no podemos indicar un texto prescriptivo sobre qué pedir. Algunas ideas de cambios que puedes solicitar a Copilot:

- Añadir encabezados de comentario al principio de cada archivo de código con una breve descripción de su función.
- Añadir comentarios TSDoc a los archivos de TypeScript y Astro.
- Crear un README con una descripción de la estructura de la aplicación Astro.

1. Añade un comentario en el que solicites un cambio en la documentación generada y etiqueta a **@copilot**, como harías con cualquier usuario. Utiliza una de las ideas anteriores o cualquier otra sugerencia que quieras ver aplicada al código.
2. Selecciona **View Session** para observar cómo Copilot realiza el trabajo. Verás que Copilot inicia una nueva sesión para efectuar las actualizaciones.
3. Puedes seleccionar **Back to pull request** para volver a la solicitud de incorporación de cambios.

    ![Volver a la solicitud de incorporación de cambios](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot haya completado los cambios, deberías ver una nueva confirmación en la solicitud de incorporación de cambios.
5. Selecciona la pestaña **Files changed** para revisar los cambios.

Puedes seguir iterando hasta quedar satisfecho. Cuando lo estés, convierte la PR de borrador a lista para revisión y combínala en la rama principal.

![Convertir la PR a lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisar la funcionalidad de juegos relacionados

Volvamos a la PR que Copilot creó para resolver nuestra incidencia sobre mostrar juegos relacionados en la página de detalles del juego.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la PR cuyo título sea similar a **Show related games on the game details page** o uno más elaborado.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Una vez que hayas revisado las actualizaciones y todo tenga el aspecto correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Deberías ver un indicador que indica que algunos flujos de trabajo esperan aprobación.
7. Si los flujos de trabajo esperan aprobación, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

8. Deberías ver los flujos de trabajo en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto pasarán para la aplicación Astro. Puede tardar unos minutos.
9. **Opcional:** también puedes cambiar a esta rama en tu Codespace para realizar una prueba manual de la funcionalidad de juegos relacionados. Navega hasta tu Codespace, abre el terminal y ejecuta los siguientes comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

¡Copilot ha creado la funcionalidad de juegos relacionados! Igual que antes, puedes trabajar de forma iterativa con el agente en la nube para solicitar actualizaciones. Por ejemplo, puedes pedir a Copilot que ajuste cuántos juegos relacionados se muestran o que garantice que se añadan encabezados de comentario y comentarios TSDoc (recuerda: esto se asignó **antes** de que actualizases tus instrucciones personalizadas). Como antes, puedes hacer estas solicitudes mediante un nuevo comentario en la pestaña **Conversation**, que Copilot verá e iniciará una nueva sesión.

## Revisar las funciones de accesibilidad

Por último, vamos a revisar las funciones de accesibilidad implementadas mediante el agente personalizado de accesibilidad. Esta PR debería incluir tanto el modo de alto contraste asignado en el Ejercicio 3 como el modo claro solicitado en mission control en el Ejercicio 4.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la PR cuyo título sea similar a **Add high contrast mode to website** o uno más elaborado.

> [!NOTE]
> Si Copilot sigue trabajando en la tarea, la solicitud de incorporación de cambios contendrá el indicador **[WIP]**. En ese caso, espera a que Copilot termine el trabajo. Puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Revisa la implementación, prestando especial atención a:
   - Los componentes de interfaz de alternancia para cambiar entre modos.
   - El uso de almacenamiento local para conservar las preferencias de usuario.
   - Los cambios de CSS o estilo para los modos de alto contraste y claro.
   - Los atributos de accesibilidad (etiquetas ARIA, navegación mediante teclado, etc.).
   - Cualquier código JavaScript/TypeScript que gestione el cambio de modo.

6. Una vez que hayas revisado las actualizaciones y todo tenga el aspecto correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que indica que algunos flujos de trabajo esperan aprobación.
8. Si los flujos de trabajo esperan aprobación, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Deberías ver los flujos de trabajo en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto pasarán para la aplicación Astro. Puede tardar unos minutos.
10. **Opcional:** puedes cambiar a esta rama en tu Codespace para probar manualmente las funciones de accesibilidad. Navega hasta tu Codespace, abre el terminal y ejecuta los siguientes comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Después, inicia la aplicación y prueba los modos de alto contraste y claro en el navegador para asegurarte de que funcionan como se espera y persisten al volver a cargar las páginas.

Observa cómo el agente personalizado de accesibilidad ayudó a orientar a Copilot para implementar estas funciones siguiendo las mejores prácticas de accesibilidad. Si detectas algún problema o posible mejora de accesibilidad, puedes etiquetar a **@copilot** en un comentario para solicitar actualizaciones, igual que hiciste con las PR anteriores.

## Ejercicio opcional — sigue delegando

El agente en la nube funciona mejor cuando puedes entregarle elementos reales del backlog y dedicar tu atención a otras tareas. Para desarrollar este hábito, registra algunas incidencias más en tu repositorio y asígnalas a Copilot. Algunas ideas:

- Crear un formulario de interés de patrocinadores en la página de detalles del juego.
- Implementar paginación en la página de lista de juegos.
- Añadir validación de entradas y gestión de errores a los ayudantes de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. En estas lecciones:

- **Has inspeccionado los archivos de instrucciones personalizadas que incluye este repositorio** para observar su efecto en el resultado del agente en la nube.
- **Has asignado incidencias al agente en la nube de Copilot** y has observado cómo prepara el entorno, planifica y ejecuta el trabajo de forma asincrónica.
- **Has creado y utilizado un agente personalizado** de accesibilidad para añadir los modos de alto contraste y claro.
- **Has utilizado la página de agentes de Copilot como mission control** para supervisar y dirigir la sesión de accesibilidad mientras estaba en curso.
- **Has revisado e iterado sobre las solicitudes de incorporación de cambios del agente en la nube**, etiquetando a `@copilot` para solicitar cambios y aprobar flujos de trabajo.

## Revisar y próximos pasos

Has completado el recorrido del agente en la nube. Si quieres seguir explorando, los demás recorridos complementan lo que has practicado aquí:

- 🖥️ **[Recorrido de VS Code](../../vscode/)** — explora el modo agente de Copilot Chat y la integración de MCP directamente desde tu IDE.
- 💻 **[Recorrido de CLI](../../cli/)** — realiza dos cambios revisados desde tu terminal con los modos Plan y Autopilot, habilidades de agente, un agente QA personalizado, Playwright MCP, Agent Merge y un puente opcional mediante `/delegate` al agente en la nube.

En tu propio repositorio, prueba estas ideas de seguimiento:

- Asigna al agente en la nube una incidencia de refactorización o cobertura de pruebas.
- Crea un agente personalizado para otro ámbito.
- Configura `copilot-setup-steps.yml` para una pila tecnológica distinta.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas del flujo de trabajo de configuración del agente en la nube de Copilot][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube de Copilot][agent-firewall]

---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
