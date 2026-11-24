---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Probablemente haya muy pocas organizaciones que no tengan dificultades con la deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que requiere actualizaciones o solicitudes de funcionalidades que llevan mucho tiempo en el backlog porque simplemente no había tiempo para implementarlas. El agente en la nube de GitHub Copilot está diseñado para realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Cuando termina su trabajo, genera una PR borrador lista para que una persona desarrolladora la revise. Esto permite descargar tareas tediosas y acelerar el proceso de desarrollo, además de liberar a las personas desarrolladoras para que se concentren en asuntos de mayor alcance.

Explorarás lo siguiente con el agente en la nube de Copilot:

- personalizar el entorno para generar código;
- garantizar que las operaciones se realizan de forma segura;
- la importancia de asignar ámbitos claros a las incidencias;
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica que le gustaría solucionar. Los contratistas que crearon inicialmente la primera versión del sitio dejaron la documentación en un estado poco satisfactorio — de hecho, está prácticamente ausente. Como primer paso, les gustaría que se añadieran comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño está listo para mejorar el descubrimiento de juegos. Les gustaría que la página de detalles de cada juego mostrase juegos relacionados — otros títulos de la misma categoría — para que las personas puedan seguir navegando. Todavía no necesitan una implementación pulida; solo quieren algo que puedan utilizar para las pruebas de aceptación de la experiencia de usuario. Actualmente, esto bloquea el trabajo, pero hay otros asuntos de mayor prioridad.

Estos son ejemplos de tareas que pueden quedar postergadas rápidamente y que son idóneas para asignar al agente en la nube de Copilot. El agente podrá trabajar en ellas de forma asincrónica, permitiendo a las personas desarrolladoras centrarse en otras tareas y volver después para revisar el trabajo de Copilot y asegurarse de que todo sea correcto.

## Presentación del agente en la nube de GitHub Copilot

[El agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano, de manera muy similar a una persona desarrolladora. Y, al igual que ocurre con una persona desarrolladora, se puede trabajar de varias formas, incluso [asignando una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Cuando se asigna, Copilot crea una solicitud de incorporación de cambios en borrador para seguir el progreso, prepara un entorno y comienza a trabajar en la tarea. Puedes consultar la sesión de Copilot mientras sigue en curso o después de que haya terminado. Cuando esté lista para que la revises, te etiquetará en la solicitud de incorporación de cambios.

## Importancia de las instrucciones con un alcance adecuado

GitHub Copilot no hace magia: no puedes omitir la reflexión. Incluso las operaciones aparentemente sencillas adquieren complejidad al profundizar en ellas, por lo que debes [prestar atención al ámbito de las tareas asignadas al agente en la nube][cloud-agent-best-practices]. Trátalo como a una persona que programa en pareja con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque sobre la marcha. Los fundamentos del desarrollo de software no cambian al incorporar IA generativa.

## Instrucciones personalizadas en este repositorio

Los ejercicios anteriores presentaron las instrucciones personalizadas y cómo orientan a Copilot. Si ya has realizado el ejercicio práctico de instrucciones personalizadas, habrás visto `.github/copilot-instructions.md` en acción; si no, este es un buen momento para echarle un vistazo rápido. Antes de asignar trabajo al agente en la nube, examina en modo solo lectura los archivos de instrucciones incluidos en este repositorio para identificar su efecto posteriormente.

Abre los siguientes archivos en la interfaz web de GitHub de tu repositorio o en un codespace si ya tienes uno en ejecución:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, especialmente las expectativas sobre las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observa el frontmatter `applyTo`, que limita estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes la incidencia `Code lacks documentation` al agente en la nube en la siguiente sección, busca en la solicitud de incorporación de cambios resultante comentarios TSDoc, convenciones de TypeScript y encabezados de comentario: proceden de estos archivos de instrucciones. Haremos referencia a ello de nuevo al revisar PR en un ejercicio posterior.

## Configurar el entorno de desarrollo para el agente en la nube de Copilot

Crear código, independientemente de quién participe, suele requerir un entorno específico y la ejecución de scripts de configuración para asegurarse de que todo esté en buen estado. Esto también se aplica al asignar tareas a Copilot, que las realiza de forma similar a una persona ingeniera de software.

El agente en la nube utiliza [GitHub Actions][github-actions] como entorno para realizar su trabajo. Puedes personalizarlo creando un [flujo de trabajo de configuración especial][setup-workflow], configurado en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que Copilot empiece a trabajar. Así tendrá acceso a las herramientas de desarrollo y las dependencias necesarias. Ya ha sido preconfigurado para el laboratorio y permite incluir esta oportunidad de aprendizaje. Garantiza que Copilot tenga acceso a Node.js, las dependencias del proyecto, los binarios del navegador para las pruebas de extremo a extremo y la base de datos SQLite migrada y poblada para la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite ejecutar el flujo de trabajo desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Define los permisos mínimos necesarios para *tus pasos*. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si necesitas clonar el repositorio en el flujo de configuración, por ejemplo para instalar dependencias, necesitarás el permiso `contents: read`. Si no clonarlo en este flujo, Copilot lo hará automáticamente después de completarse los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración del frontend / aplicación — toda la aplicación ahora es Astro + Drizzle/libSQL
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      # Instalar las dependencias de JavaScript
      - name: Install JavaScript dependencies
        run: npm ci

      # Instalar los navegadores de Playwright
      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrar y poblar la base de datos SQLite local para que las compilaciones y pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

Tiene el aspecto de cualquier otro archivo de flujo de trabajo de GitHub, pero presenta algunos aspectos clave:

- Contiene un único trabajo llamado `copilot-setup-steps`. GitHub Actions ejecuta este trabajo antes de que Copilot empiece a trabajar en la solicitud de incorporación de cambios.
- Observa el desencadenador `workflow_dispatch`, que permite ejecutar manualmente el flujo de trabajo desde la pestaña **Actions** del repositorio. Esto es útil para comprobar que el flujo de trabajo se ejecuta correctamente sin esperar a que lo haga Copilot.

## Añadir documentación

Aunque todo el mundo entiende la importancia de la documentación, la mayoría de los proyectos tienen información obsoleta o carecen de ella por completo. Este es el tipo de deuda técnica que suele quedar sin abordar, lo que ralentiza la productividad y dificulta mantener el código o incorporar a nuevas personas al equipo. Afortunadamente, Copilot destaca en la creación de documentación, y esta es una incidencia perfecta para asignarla al agente en la nube. Trabajará en segundo plano para generar la documentación necesaria. En un ejercicio posterior volverás a revisar su trabajo.

1. Navega a tu repositorio en github.com desde una pestaña nueva del navegador.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para crearla.
5. Establece el **Title** como `Code lacks documentation`.
6. Establece el **Description** con:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lateral derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

10. Selecciona la pestaña **Pull Requests**.
11. Abre la solicitud de incorporación de cambios recién generada (PR), cuyo título será similar a `[WIP]: Code lacks documentation`. Si no aparece una PR nueva en la lista, espera uno o dos minutos y actualiza la ventana del navegador.
12. Al cabo de unos minutos, Copilot habrá creado una lista de tareas.

> [!NOTE]
> La lista de tareas de Copilot puede tardar varios minutos en aparecer en la PR. Copilot está preparando su entorno (ejecutando el flujo de trabajo indicado anteriormente), analizando el proyecto y determinando cuál es el mejor enfoque para resolver el problema.

13. Revisa la lista y las tareas que va a completar.
14. Desplázate por el historial de la solicitud de incorporación de cambios y verás una actualización que indica que Copilot ha comenzado a trabajar en la incidencia.
15. Selecciona el botón **View session**.

  ![Vista de sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la ventana para ver el indicador actualizado.

16. Observa que puedes desplazarte por la sesión en directo y ver cómo Copilot resuelve el problema: explora el código, comprende el estado, se detiene a razonar y decidir el plan adecuado y, además, crea código.

Esto tardará varios minutos. Uno de los objetivos principales del agente en la nube es permitirle realizar tareas de forma asincrónica y liberarnos para centrarnos en otras actividades. Aprovecharemos esa función asignando otra tarea al agente en la nube y dedicándonos a escribir código para añadir funcionalidades a la aplicación.

## Añadir una sección de juegos relacionados a la página de detalles

Como hemos señalado, una de las grandes ventajas del agente en la nube es la posibilidad de dividir el trabajo: puedes concentrarte en un conjunto de tareas mientras él se ocupa de otro. Aunque añadir una sección de juegos relacionados para el equipo de diseño podría no llevar mucho tiempo, ese tiempo podría dedicarse a otras tareas. ¡Vamos a asignarlo al agente en la nube!

1. Vuelve a tu repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para utilizar la plantilla en blanco.
5. Establece el **Title** como: `Show related games on the game details page`
6. Establece el **Description** con:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecciona **Create** para crear la incidencia.
8. En el lateral derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Poco después, verás unos 👀 en el primer comentario de la incidencia, lo que indica que Copilot está trabajando.

![Copilot utiliza el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

¡Copilot está trabajando diligentemente en tu segunda solicitud! El agente en la nube funciona de manera similar a una persona ingeniera de software, así que no necesitas supervisarlo activamente; revisa su trabajo cuando haya terminado. Ahora vamos a crear y utilizar agentes personalizados.

## Resumen y próximos pasos

Esta lección ha explorado [el agente en la nube de GitHub Copilot][copilot-agents]. Con el agente en la nube puedes asignar incidencias a Copilot para que las realice de forma asincrónica. Puedes usar Copilot para abordar deuda técnica, crear nuevas funcionalidades o migrar código de un framework a otro.

Has explorado estos conceptos:

- personalizar el entorno para generar código;
- garantizar que las operaciones se realizan de forma segura;
- la importancia de asignar ámbitos claros a las incidencias;
- asignar incidencias a Copilot.

Con el agente en la nube trabajando en segundo plano, ahora podemos crear y utilizar agentes personalizados. [El agente en la nube también puede utilizar servidores MCP][cloud-agent-mcp] y dispone de instrucciones personalizadas, que hemos explorado en módulos anteriores.

## Recursos

- [Acerca del agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas del flujo de trabajo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
