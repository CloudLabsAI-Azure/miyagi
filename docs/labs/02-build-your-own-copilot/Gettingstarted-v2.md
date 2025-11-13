# Cree Aplicaciones Inteligentes con la Pila Copilot de Microsoft y Azure OpenAI

### Duración Total Estimada: 4 horas

## Descripción General

En este laboratorio, obtendrá una sólida comprensión de los conceptos básicos de la IA Generativa, Azure Open AI, los patrones de Recuperación de Generación Aumentada (RAG), Semantic Kernel y cómo utilizar estos conceptos para crear su propio Copilot para las necesidades de su negocio. También explorará casos de uso que muestran experiencias de productos Copilot. Utilizando la Pila Copilot de Microsoft y casos de uso prácticos, este laboratorio lo guiará en la visualización y creación de sistemas inteligentes que integran modelos fundacionales que dan como resultado una productividad mejorada y experiencias de producto hiperpersonalizadas.

## Objetivo

- **Verificar y Recuperar los valores de los Recursos de Azure**: Este ejercicio práctico tiene como objetivo verificar y recuperar los valores para asegurar la configuración y la conectividad adecuadas de los recursos de Azure.
- **Ejecutar la Aplicación Miyagi Localmente**: Este ejercicio práctico tiene como objetivo configurar la aplicación Miyagi, implementar el servicio de recomendación, desplegar el frontend localmente, optimizar la recuperación de datos con Azure AI Search y explorar la aplicación y el servicio para lograr una experiencia de usuario personalizada.
- **Contenedorización de la Interfaz de Usuario de Miyagi y el servicio de Recomendación en Azure Kubernetes Service (AKS)**: Este ejercicio práctico tiene como objetivo contenerizar y desplegar Miyagi UI y los servicios de recomendación en AKS, configurar Kubernetes, enviar imágenes de Docker a ACR y verificar la implementación a través de puntos de conexión del servicio.
- **Explorar y Verificar la interfaz de usuario de Miyagi y el servicio de Recomendación contenedorizados en AKS**: Este ejercicio práctico tiene como objetivo implementar y verificar Miyagi UI y los servicios de recomendación en AKS, probando APIs y accediendo a la Interfaz de Usuario a través de los puntos de conexión Ingress para asegurar su funcionalidad. Este ejercicio mejora la comprensión de la gestión y el enrutamiento del tráfico dentro de los entornos de Kubernetes.
- **Exponer Open AI a través de APIM**: Este ejercicio práctico tiene como objetivo verificar y crear APIs en el servicio APIM para actualizar la imagen de Docker para el servicio de recomendación, asegurando la optimización y el mantenimiento de las aplicaciones en contenedores.
- **Comenzando con su propio Copiloto**: Este ejercicio práctico tiene como objetivo integrar Modelos de Lenguaje Grande (LLM) con lenguajes como C#, Python y Java, permitiendo la creación de complementos que se pueden encadenar fácilmente.
  
## Prerrequisitos

Los participantes deberían contar con:

- Comprensión de los conceptos básicos de la IA generativa
- Familiaridad con Azure Open AI
- Experiencia con Semantic Kernel

## Arquitectura

La arquitectura de Miyagi utiliza IA para interacciones de usuario hiperpersonalizadas, transformando aplicaciones con habilidades avanzadas de Semantic Kernel y prompt engineering. Cuenta con microservicios escalables y una columna vertebral basada en eventos, que evoluciona con nuevos modelos de IA. El frontend ofrece experiencias personalizadas similares a Microsoft Copilot.

Integra Azure Functions, AKS y Apache Kafka para una comunicación fluida, con datos administrados por Cosmos DB y Azure Storage. Miyagi ejemplifica la IA avanzada y los servicios Azure para aplicaciones inteligentes preparadas para el futuro.

## Diagrama de Arquitectura

   ![](../../Lab-Scenario-Preview/sk-memory-orchestration-1.png)

## Explicación de Componentes

La arquitectura de este laboratorio incluye los siguientes componentes clave:

- **Azure OpenAI**: Azure OpenAI integra los modelos de lenguaje de OpenAI en la nube de Microsoft Azure, permitiendo soluciones de IA escalables para el procesamiento del lenguaje natural y la automatización.
- **AI Search**: Es un servicio en la nube que permite capacidades de búsqueda potentes y flexibles, incluyendo la búsqueda de texto completo y las funciones impulsadas por IA.
- **Azure Functions**: Ejecuta código en respuesta a eventos sin administrar servidores. Escala automáticamente en función de la demanda.
- **AKS (Azure Kubernetes Service)**: Servicio administrado de Kubernetes para la orquestación y el escalado de contenedores.
- **Apache Kafka**: Maneja la transmisión de datos en tiempo real y el procesamiento de eventos.
- **Cosmos DB**: Base de datos multimodelo distribuida globalmente con baja latencia y alta disponibilidad.
- **Azure Storage**: Almacenamiento escalable para blobs, archivos, colas y tablas.
- **Bing Search**: Le permite agregar funciones de búsqueda de Bing a sus aplicaciones. Proporciona APIs para búsquedas web, de imágenes, videos y noticias.

## Introducción al laboratorio

¡Bienvenido a su taller "Crea aplicaciones inteligentes con Copilot Stack y Azure OpenAI" de Microsoft! Hemos preparado un entorno perfecto para que explores y aprendas sobre los servicios de Azure. Empecemos por aprovechar al máximo esta experiencia:

## Comenzando con el Laboratorio

Una vez configurado el ambiente, su navegador cargará una máquina virtual (LabVM), utilice esta máquina virtual durante todo el taller para realizar el laboratorio. Puede ver el número en la parte inferior de la guía de laboratorio para cambiar a diferentes ejercicios en la guía de laboratorio.

   ![](./Media/sp48.png)

### Máquina Virtual y Guía de Laboratorio

Su máquina virtual es su herramienta principal durante el taller. La guía de laboratorio es su hoja de ruta hacia el éxito.

## Explorando los recursos de su laboratorio

Para comprender mejor los recursos y credenciales de su laboratorio, diríjase a la pestaña **Ambiente**.

   ![](./Media/sp49.png)
   
   > Verá el valor SUFFIX en la pestaña **Ambiente**; úselo dondequiera que vea SUFFIX o DeploymentID en los pasos del laboratorio.

## Uso de la función de ventana dividida

Para mayor comodidad, puede abrir la guía de laboratorio en una ventana separada seleccionando el botón **Ventana dividida** en la esquina superior derecha.

   ![](./Media/sp50.png)

## Administre su máquina virtual

Puede iniciar, detener o reiniciar su máquina virtual según sea necesario desde la pestaña **Recursos**. ¡Su experiencia está en sus manos!

   ![](./Media/2025-05-23-3.png)

## Guía de laboratorio: Acercar/Alejar

Para ajustar el nivel de zoom de la página del entorno, haga clic en el icono **A↕ : 100%**, ubicado junto al temporizador en el entorno de laboratorio.

   ![](./Media/sp51.png)

## Iniciar Sesión en el Portal de Azure

1. Minimice **Docker Desktop** haciendo clic en el botón **Minimizar**.

   ![](./Media/11-10-24(11).png)

   > **Nota:** Si encuentra un error de actualización de WSL en la aplicación Docker Desktop, haga clic en **Quit** y vuelva a abrir la aplicación Docker Desktop desde el escritorio.

   ![](./Media/11-10-24(12).png)

   > Si se encuentra con el problema "A WSL distro Docker Desktop relies on has exited unexpectedly.", esto generalmente sucede como resultado de que una entidad externa finalizó WSL, haga clic en el botón **Restart**.

   ![](./Media/11-10-24(13).png)   

1. En LabVM, haga clic en el acceso directo al Portal de Azure del navegador Microsoft Edge, el cual se ha creado en el escritorio.

   ![](./Media/10-10-25.png)

1. En la pestaña **Iniciar sesión en Microsoft Azure**, verá la pantalla de inicio de sesión. Ingrese el siguiente correo electrónico o nombre de usuario y haga clic en **Siguiente**. 

   * **Correo electrónico/Nombre de usuario**: **<inject key="AzureAdUserEmail"></inject>**

     ![](./Media/sp1.png)
     
1. Ahora ingrese la siguiente contraseña y haga clic en **Iniciar sesión**.
   
   * **Contraseña**: **<inject key="AzureAdUserPassword"></inject>**

     ![](./Media/sp2.png)

     > **Nota**: Si se le solicita MFA, siga los pasos resaltados en - [Pasos para continuar con la configuración de MFA si la opción "Preguntar más tarde" no está visible](#Pasos-para-continuar-con-la-configuración-de-MFA-si-la-opción-Preguntar-más-tarde-no-está-visible)  
   
1. Si ve la ventana emergente **¿Permanecer conectado?**, seleccione **No**.

   ![](./Media/sp3.png)

1. Si aparece una ventana emergente **Bienvenido a Microsoft Azure**, seleccione **Cancelar** para omitir el recorrido.

    ![](./Media/11-10-24(7).png)
   
1. Ahora verá el Panel del Portal de Azure, haga clic en **Grupos de recursos** en el panel Navegar para ver los grupos de recursos.

   ![](./Media/11-10-24(15).png)

1. En **Grupos de recursos**, haga clic en el grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](./Media/11-10-24(16).png)

1. En el grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, verifique los recursos presentes.

   ![](./Media/11-10-24(17).png)

## Pasos para continuar con la configuración de MFA si la opción Preguntar más tarde no está visible

> **Nota:** Continúe con los ejercicios si la MFA ya está habilitada o la opción no está disponible.

1. En el mensaje **"Se requiere más información"**, seleccione **Siguiente**.

1. En la página **"Mantenga su cuenta segura"**, seleccione **Siguiente** dos veces.

1. **Nota:** Si no tiene la aplicación Microsoft Authenticator instalada en su dispositivo móvil:

    - Abra **Google Play Store** (Android) o **App Store** (iOS).
    - Busque **Microsoft Authenticator** y pulse **Instalar**.
    - Abra la aplicación **Microsoft Authenticator**, seleccione **Agregar cuenta** y luego elija **Cuenta profesional o educativa**.

1. Se mostrará un **código QR** en la pantalla de su computadora.

1. En la aplicación Authenticator, seleccione **Escanear un código QR** y escanee el código que aparece en la pantalla.

1. Después de escanear, haga clic en **Siguiente** para continuar.

1. En su teléfono, ingrese el número que se muestra en la pantalla de su computadora en la aplicación Authenticator y seleccione **Siguiente**.

1. Si se le solicita que mantenga la sesión iniciada, puede hacer clic en **No**.

1. Si aparece la ventana emergente **Bienvenido a Microsoft Azure**, haga clic en **Cancelar** para omitir la visita guiada.

1. Ahora, haga clic en **Siguiente** en la esquina inferior derecha para pasar a la página siguiente.

> [!IMPORTANTE]<br>
> **Para una experiencia más fluida durante la práctica de laboratorio, es importante revisar detenidamente tanto las instrucciones como las notas que las acompañan. Esto le ayudará a realizar las tareas con facilidad y confianza**.

Este laboratorio práctico lo guiará para crear sistemas inteligentes con la pila Copilot de Microsoft, aprovechando los patrones de IA Generativa y RAG para una mayor productividad y experiencias personalizadas.

## Contacto de Soporte
 
El equipo de soporte de CloudLabs está disponible las 24 horas del día, los 7 días de la semana, los 365 días del año, por correo electrónico y chat en vivo para garantizar una asistencia sin inconvenientes en cualquier momento. Ofrecemos canales de soporte dedicados, diseñados específicamente tanto para estudiantes como para instructores, garantizando que todas sus necesidades sean atendidas de forma rápida y eficiente.

Contactos de Soporte para Estudiantes:

- Soporte por Correo Electrónico: cloudlabs-support@spektrasystems.com
- Soporte por Chat En Vivo: https://cloudlabs.ai/labs-support

Ahora, haga clic en **Siguiente** en la esquina inferior derecha para pasar a la página siguiente.

   ![](./Media/next-page-2.png)

## ¡¡Feliz Aprendizaje!!
