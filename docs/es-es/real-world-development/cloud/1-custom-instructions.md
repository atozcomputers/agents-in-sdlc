---
title: "Ejercicio 1 - Instrucciones personalizadas (Agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental cuando se trabaja con IA generativa. Si una tarea debe realizarse de una manera determinada o Copilot necesita conocer información de contexto, debes asegurarte de que tenga acceso a esa información. Los [archivos de instrucciones][instruction-files] permiten proporcionar esas indicaciones para que Copilot entienda no solo *qué* quieres que haga, sino *cómo* quieres que lo haga.

En este ejercicio:

- explorarás cómo el contexto específico del proyecto, las directrices de programación y los estándares de documentación llegan a Copilot mediante instrucciones personalizadas del repositorio y archivos de instrucciones con ámbito por ruta;
- añadirás un nuevo estándar para todo el repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no ejecutarás una indicación *antes/después*: el agente en la nube de Copilot trabaja de forma asincrónica en incidencias de GitHub, por lo que es más difícil demostrar el efecto uno al lado del otro en tiempo real. Verás la influencia de tu archivo de instrucciones más adelante en este recorrido, al revisar las solicitudes de incorporación de cambios que genera el agente en la nube.

## Archivos de instrucciones

### Escenario

Como corresponde a cualquier equipo de desarrollo responsable, Tailspin Toys dispone de directrices y requisitos para las prácticas de desarrollo. Estos incluyen:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz debe usar el modo oscuro y transmitir una apariencia moderna.
- Debe añadirse documentación al código mediante comentarios TSDoc.
- Debe añadirse un bloque de comentarios al principio de cada archivo que describa para qué sirve.

Mediante los archivos de instrucciones garantizarás que Copilot disponga de la información correcta para realizar las tareas conforme a estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas permiten proporcionar contexto y preferencias a Copilot, de modo que pueda comprender mejor tu estilo de programación y tus requisitos. Esta funcionalidad puede ayudarte a dirigir a Copilot para obtener sugerencias y fragmentos de código más relevantes. Puedes especificar las convenciones de programación que prefieras, las bibliotecas que utilices e incluso los tipos de comentarios que quieras incluir en el código. Puedes crear instrucciones para todo el repositorio o para tipos específicos de archivos, a fin de proporcionar contexto para una tarea.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un único archivo de instrucciones que se envía a Copilot para **todas** las solicitudes del repositorio. Debe contener información a nivel del proyecto: contexto relevante para la mayoría de las solicitudes de chat o CLI que envíes a Copilot. Puede incluir la pila tecnológica utilizada, una descripción general de lo que se está creando, las mejores prácticas y otras directrices globales.
- Los archivos `.github/instructions/*.instructions.md` se pueden crear para tareas o tipos de archivos específicos. Puedes utilizarlos para proporcionar directrices sobre lenguajes concretos (como TypeScript o Astro) o sobre tareas como crear un componente de interfaz o un nuevo conjunto de pruebas unitarias.

> [!NOTE]
> Cuando trabajas en tu IDE, los archivos de instrucciones solo se usan para la generación de código en Copilot Chat, no para las finalizaciones de código ni las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan los archivos de nivel de repositorio y `*.instructions.md` (con frontmatter `applyTo`) al generar código.
>
> Por último, Copilot [admite archivos de instrucciones con otros estándares][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Mejores prácticas para gestionar archivos de instrucciones

Una conversación completa sobre cómo crear archivos de instrucciones queda fuera del alcance de este taller. No obstante, los ejemplos incluidos en el proyecto muestran un enfoque representativo. A alto nivel:

- Mantén las instrucciones de `copilot-instructions.md` centradas en las directrices del proyecto, como la descripción de lo que se está creando, la estructura del proyecto y los estándares globales de programación.
- Usa archivos `*.instructions.md` para proporcionar instrucciones específicas para tipos de archivos (pruebas unitarias, componentes de Astro, la capa de datos) o para tareas concretas.
- Utiliza lenguaje natural. Mantén las indicaciones claras. Proporciona ejemplos de cómo debe verse el código y cómo no debe verse.

No existe una única forma correcta de crear archivos de instrucciones, igual que no existe una única forma correcta de utilizar IA. Mediante la experimentación descubrirás qué funciona mejor para tu proyecto.

> [!TIP]
> Cada proyecto que use GitHub Copilot debe tener una colección sólida de archivos de instrucciones. Al explorar los incluidos en este proyecto, observarás que hay archivos para numerosos tipos de tareas, como [actualizaciones de interfaz][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada interfaz los expone de forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI); la lección correspondiente de cada interfaz lo indicará cuando resulte relevante.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio lleno de archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas de este proyecto

Dedica un momento a leer los archivos de instrucciones que incluye este repositorio: hay un archivo principal `copilot-instructions.md` y una colección de archivos `*.instructions.md` para diversas tareas. Ábrelos en tu editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Explora el archivo y observa la breve descripción del proyecto, así como secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, presta atención a las indicaciones anidadas de **GitHub Actions Workflows**. Estas se aplican a todas las interacciones que tengas con Copilot.
3. Abre la carpeta `.github/instructions` y examínala. Verás instrucciones para archivos de Astro, la capa de datos de Drizzle, pruebas y mucho más.
4. Abre `.github/instructions/unit-tests.instructions.md`. Observa el campo `applyTo` al principio: establece un patrón glob (relativo a la raíz del repositorio) que determina a qué archivos se aplican las instrucciones. Aquí coincidirá con cualquier archivo de pruebas de TypeScript (por ejemplo, uno que cumpla `**/*.test.ts`).
5. Examina las instrucciones específicas para crear pruebas unitarias de este proyecto.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Fíjate en los enlaces a otros archivos de instrucciones (como `unit-tests.instructions.md`) y a archivos existentes del proyecto. Esto permite dividir conjuntos grandes de instrucciones en archivos reutilizables más pequeños y dirigir a Copilot hacia ejemplos que puede seguir al generar código. Las rutas son relativas al archivo de instrucciones y no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero aún no exige documentación dentro del código. En los siguientes pasos añadirás reglas para comentarios TSDoc y encabezados de comentarios en los archivos.

## Añadir un nuevo estándar al repositorio

El siguiente paso es la única edición que realizarás aquí: añade una regla para todo el proyecto que indique que la documentación debe integrarse en el código mediante comentarios TSDoc y un encabezado de comentario a nivel de archivo. El agente en la nube recogerá esta regla al trabajar en las incidencias que le asignes más adelante en este recorrido.

Antes de editar, crea una rama para trabajar (el agente en la nube leerá tus instrucciones desde cualquier rama a la que apunte la incidencia, pero aun así debes confirmar los cambios de forma limpia):

1. Desde el terminal del codespace, crea y cambia a una rama nueva:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como hemos indicado anteriormente, `.github/copilot-instructions.md` está diseñado para proporcionar información a nivel del proyecto a Copilot. Vamos a asegurarnos de que los estándares de programación del repositorio estén documentados para mejorar las sugerencias de código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Localiza la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Observa cómo documenta los estándares de programación del proyecto, pero todavía no incluye una regla sobre documentación dentro del código, razón por la cual el ayudante generado no tenía comentarios de documentación.
3. Añade las siguientes líneas de Markdown justo debajo de los estándares existentes para indicar a Copilot que añada encabezados de comentario en los archivos y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como viste en la lección anterior, puedes crear archivos de instrucciones a nivel del repositorio (`.github/copilot-instructions.md`) para directrices globales, o archivos `*.instructions.md` para lenguajes, tipos de archivos o tareas específicas. El archivo a nivel del repositorio es el lugar adecuado para estándares del proyecto, como la regla de comentarios de documentación que acabas de añadir.

## Confirmar, enviar y combinar la actualización de instrucciones

El agente en la nube lee los archivos de instrucciones de la rama a la que apunta la incidencia. Al asignar una incidencia a Copilot en el siguiente ejercicio, Copilot creará una rama a partir de `main`, así que los cambios de instrucciones deben llegar a `main` para que el agente en la nube pueda recogerlos.

1. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Abre una solicitud de incorporación de cambios desde `custom-instructions-cloud` hacia `main` en github.com y combínala. El agente en la nube leerá estas instrucciones al trabajar en las incidencias asignadas en el siguiente ejercicio.

> [!TIP]
> Si prefieres trabajar directamente en `main` para este taller, puedes omitir la rama y confirmar directamente en `main`. La rama aparece aquí para que el taller refleje cómo gestionarías el trabajo en un proyecto real.

## Resumen y próximos pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones de este proyecto y has añadido un nuevo estándar para todo el repositorio en `.github/copilot-instructions.md`. Verás que este estándar se aplica en las solicitudes de incorporación de cambios que genere el agente en la nube durante el resto de este recorrido.

A continuación, [asignarás tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para la personalización de GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [5 consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
