---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de comenzar los ejercicios del agente en la nube de Copilot, tienes que preparar todo. Crearás tu propia copia del repositorio de Tailspin Toys y un [codespace][codespaces] que podrás utilizar para editar los archivos de instrucciones y revisar el trabajo que genera el agente en la nube.

## Configurar el repositorio del laboratorio

Para crear una copia del repositorio del código que vas a crear, harás una instancia a partir de la [plantilla][template-repository]. La nueva instancia contendrá todos los archivos necesarios para el laboratorio y la utilizarás mientras realizas los ejercicios.

1. En una ventana nueva del navegador, navega hasta la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando el botón **Use this template** en la página del repositorio del laboratorio. Después, selecciona **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si estás realizando el taller como parte de un evento dirigido por GitHub o Microsoft, sigue las instrucciones proporcionadas por los mentores. En caso contrario, puedes crear el nuevo repositorio en una organización en la que tengas acceso a GitHub Copilot.

    ![Introduce la configuración del repositorio de plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio que has creado (**nombre-de-organizacion-o-usuario/nombre-del-repositorio**), ya que la utilizarás más adelante en el laboratorio.

## Crear un codespace

A continuación, utilizarás un codespace para completar los ejercicios del laboratorio.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que permite escribir, ejecutar y depurar código directamente desde el navegador. Ofrece un IDE completo con compatibilidad con varios lenguajes de programación, extensiones y herramientas.

1. Navega hasta el repositorio recién creado.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, el botón **+** para crear un codespace nuevo.

    ![Crear un codespace nuevo](../../../_images/ex0-create-codespace.png)

La creación del codespace tardará varios minutos, aunque sigue siendo mucho más rápido que tener que instalar manualmente todos los servicios. Puedes aprovechar este tiempo para explorar otras funciones de GitHub Copilot, a las que pasaremos a continuación.

> [!CAUTION]
> Volverás al codespace en un ejercicio posterior. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está diseñado para ejecutarse dentro de un codespace o de un [dev container][dev-containers] local. Ambos garantizan que el entorno tenga instalados todos los requisitos previos necesarios para ofrecer una experiencia fluida. Si prefieres ejecutarlo de forma local, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se solicite — VS Code creará el mismo dev container que utiliza el codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Resumen

¡Enhorabuena, has creado una copia del repositorio del laboratorio! También has iniciado el proceso de creación de tu codespace, que utilizarás mientras trabajas junto al agente en la nube de Copilot.

## Siguiente paso

Vamos a añadir instrucciones personalizadas que seguirá el agente en la nube. Continúa con el [Ejercicio 1 - Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general de GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
