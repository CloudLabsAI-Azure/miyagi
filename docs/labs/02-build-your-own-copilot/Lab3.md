# Laboratorio 4 - Exponer Open AI a través de APIM

### Duración estimada: 60 minutos

En este laboratorio, profundizará en la configuración y verificación de API en Azure API Management, centrándose en la integración del servicio Azure OpenAI. Esto implica configurar API HTTP, garantizar una configuración correcta y obtener una URL de puerta de enlace para un acceso externo y una integración sin problemas. También explorará la creación de políticas, la definición de roles y la administración de suscripciones para operar las API de forma segura. Este laboratorio destaca las prácticas recomendadas en la administración de API, garantizando una autenticación, autorización y pruebas operativas robustas dentro del completo ecosistema de Azure.

## Objetivos del laboratorio
Podrá completar las siguientes tareas:

- Tarea 1: Verificar el servicio implementado API Management y crear una API.
- Tarea 2: Crear Políticas y Roles de API Management
- Tarea 3: Actualizar la Imagen de Docker para el servicio de Recomendación
- Tarea 4: Revisión del servicio de Recomendación de AKS 
- Tarea 5: Configurar Event Hub Logging y Validar la Entrada

## Tarea 1: Verificar el servicio implementado API Management y crear una API

En esta tarea, configurará una API HTTP en Azure API Management para interactuar con el servicio Azure OpenAI. Esto garantiza que la API esté configurada correctamente y proporciona una URL de puerta de enlace para el acceso externo y la integración con otros servicios.

1. Navegue al Portal de Azure, abra el Grupo de recursos llamado **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  y seleccione el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

   ![](./Media/api-select.png)

1. En el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en **API** **(1)** en la sección APIs del menú izquierdo y seleccione **HTTP** **(2)** en Definir una nueva API para crear una API HTTP.

   ![](./Media/lab3-t1-s2.png)

1. Introduzca los siguientes valores en el panel Crear una API HTTP:
   
   | **Parameter**        | **Values**           | 
   | -------------------- | -------------------- | 
   | API Type **(1)**     | **Basic**            | 
   | Display name **(2)** | **miyagi-api**       |
   | Name **(3)**         | **miyagi-api**       |
   | Web service URL **(4)** | Ingrese el punto final de Azure OpenAI Endpoint  **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | API URL suffix **(5)** | **openai** |
   | Click on  **(6)** | **Create** |

   ![](./Media/apim1.png)

1. Una vez creada la API, haga clic en **Información general** **(1)** en el menú de la izquierda, copie la **URL de la Puerta de Enlace** **(2)** del servicio API Management. Péguela en el Bloc de notas para usarlo más adelante.

   ![](./Media/api-product6.png)


>**¡Felicitaciones** por completar la tarea! Ahora es el momento de validarla. Aquí están los pasos:
> - Pulse el botón Validar para la tarea correspondiente.
> - Si recibe un mensaje de éxito, puede proceder a la siguiente tarea. De lo contrario, lea atentamente el mensaje de error y vuelva a intentar el paso, siguiendo las instrucciones de la guía de laboratorio.
> - Si necesita ayuda, contáctenos en cloudlabs-support@spektrasystems.com. Estamos disponibles las 24 horas del día, los 7 días de la semana para ayudarle.

<validation step="5385328b-c6b7-4d03-9fcc-c2d33d96d9cd" />

## Tarea 2: Crear Políticas y Roles de API Management

En este laboratorio, configurará políticas de API, definirá roles y suscripciones, e integrará la API de Azure OpenAI Service en Azure API Management. Esto garantiza la correcta autenticación, autorización y pruebas operativas de los puntos de conexión de la API.

1. En el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en **API** **(1)**, luego clic en los **three dots** **(2)** al lado de miyagi-api, seleccione **Import** **(3)**, y haga clic en **OpenAPI** **(4)**.

   ![](./Media/api-openi-import.png)

   ![](./Media/api-05.png)

2. En la ventana emergente de **Import from OpenAPI specification** pegue el siguiente enlace en el **textbox** **(1)** de la especificación OpenAPI, y entonces haga clic en **Import** **(2)**. 

   ```
   https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
   ```

   ![](./Media/apim3.png)

3. Ahora debería ver una serie de APIs en Azure OpenAI Service API.
   
    ![](./Media/apim4.png)

4. En la API **api-key**, navegue a la pestaña **Configuración** **(1)** y actualice la URL del servicio web **<inject key="OpenAIEndpoint" enableCopy="true"/>** **(2)**.

   ![](./Media/miyagi-image161n.png)

5. En la API **Azure OpenAI Service API** navegue a la pestaña **Settings** **(1)** y actualice el **Header Name** con el valor **api-key** **(2)** y haga clic en **Save** **(3)**.

   ![](./Media/azure-open-api-setting.png)

6. En el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en **Productos** **(1)** en APIs del menú izquierdo y haga clic en **+ Agregar** **(2)**.

   ![](./Media/api-product1-1.png)

7. En la ventana **Agregar producto**, especifique **OpenAi** **(1)** como **Nombre para mostrar** y **OpenAI** **(2)** como **Descripción**. En el menú **API**, haga clic en el **Signo más** **(3)**, seleccione **Azure OpenAI Service API** **(4)**, presione Intro y haga clic en **Crear** **(5)**.

   ![](./Media/productSpan-1.png)

   ![](./Media/productSpan-2.png)

8. En el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en **Suscripciones** **(1)** en APIs del menú izquierdo y haga clic en **+ Agregar suscripción** **(2)**.

   ![](./Media/api-product3.png)

9. En **Agregar suscripción**, ingrese el Nombre como **aoai-test** **(1)**, establezca el Nombre para mostrar como **AOAI Test** **(2)**, y haga clic en **Crear** **(3)**.

   ![](./Media/api-product4.png)

10. Una vez creada la suscripción, haga clic en los **tres puntos** **(1)** al lado de la clave recién creada y haga clic en **Mostrar u ocultar claves** **(2)**. Copie la clave **principal de suscripción** **(3)** y guárdela para más adelante.

    ![](./Media/api-product5.png)

11. Navegue a **Azure OpenAI** en el Portal de Azure, seleccione el recurso Azure OpenAI **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**.

12. En **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**, seleccione **Control de acceso (IAM)** **(1)**, haga clic en **+ Agregar** **(2)**, y seleccione **Agregar asignación de roles** **(3)**.

    ![](./Media/sp25.png)
   
13. En la pestaña **Agregar asignación de rol**, busque **Cognitive Services User (1)** en la barra de búsqueda, seleccione **Usuario de Servicios Cognitivos (2)** y haga clic en **Siguiente (3)**.

    ![](./Media/sp26.png)

14. En la pestaña **Miembros**, seleccione **Identidad administrada** **(1)**, haga clic en **+ Seleccionar miembros** **(2)**.

    ![](./Media/apim-role-0.png)

15. En la ventana emergente de selección de identidad administrada, para **Suscripción (1)** acepte el valor predeterminado y luego en **Identidad administrada** seleccione **Servicio de API Management** **(2)**, elija **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)** y luego haga clic en **Seleccionar** **(4)**.

    ![](./Media/sp27.png)

16. Haga clic en **Siguiente**.

    ![](./Media/apim-role-1-1.png)

17. En la pestaña **Revisar y asignar** haga clic en **Revisar y asignar**.

      ![](./Media/namespace3-1.png)

18. Vuelva al **servicio API Management** en el Portal de Azure, seleccione el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**.

19. En el servicio **API Management**, seleccione **API** **(1)**, elija la API **Azure OpenAI Service API** **(2)** creada en el paso anterior, seleccione **Todas las Operaciones** **(3)** y haga clic en **Editor de código de política** **(4)** en **Procesamiento entrante**.

      ![](./Media/sp28.png)

20. En el editor de código, copie la siguiente política para sobrescribir solo las etiquetas **entrantes** **(1)**, reemplace **&lt;&lt;Azure_OpenAI_Endpoint&gt;&gt;** con **<inject key="OpenAIEndpoint" enableCopy="true"/>** **(2)** del administrador de API que copió el Paso 4 de la Tarea 1 y haga clic en **Guardar** **(3)**.

      ```
      <inbound>
         <base />
         <set-header name="api-key" exists-action="delete" />
         <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
         <set-header name="Authorization" exists-action="override">
            <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
         </set-header>
         <set-backend-service base-url="<<Azure_OpenAI_Endpoint>>openai" />
      </inbound>
      ```

    ![](./Media/api-inbound.png)

    >**Nota**: Asegúrese de pegar los valores de **OpenAIEndpoint** y eliminar cualquier duplicación de **https://**.

21. En API Management, haga clic en **Test** **(1)**, seleccione Creates a **completion for the chat message** **(2)**, ingrese el nombre de la implementación gpt-35-turbo **<inject key="CompletionModel" enableCopy="true"/>** **(3)** en el campo deployment-id, ingrese **2024-08-01-preview** **(4)** en el campo api-version, y haga clic en **Enviar**. 

     ![](./Media/sp29.png)

22. Desplácese hasta la sección **Request body** **(1)**, reemplace el código existente con el código a continuación y haga clic en **Send** **(2)**.

      ```
      {"model":"gpt-4","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
      ```

      ![](./Media/new-api-body.png)

23. Desplácese hacia abajo en la respuesta y debería ver una respuesta `200` y un mensaje devuelto por su servicio OpenAI.

    ![](./Media/api-product8.png)

## Tarea 3: Actualizar la Imagen de Docker para el servicio de Recomendación

En esta tarea, actualizará la configuración del servicio de recomendaciones, reconstruirá la imagen de Docker, la enviará a ACR y se asegurará de que la imagen actualizada esté lista para su implementación dentro del entorno de Azure.

1. Navegue a Visual Studio Code, expanda el directorio **Miyagi/services(1)/recommendation-service(2)/dotnet(2)** y seleccione **appsettings.json(4)**.

   ![](./Media/open-appsettings.png)

1. En el archivo `appsettings.json`, debe reemplazar el valor **endpoint** que tiene el **punto de conexión del recurso OpenAI** con la **URL de la Puerta de Enlace del API** que copió en el Paso 4 de la Tarea 1, el valor **apiKey** con la **clave de suscripción** que se copió in el Paso 10 de la Tarea 2 y guarde el archivo.

   ![](./Media/api-update.png)

1. Desde el Explorador, navegue a la ruta `Miyagi/services/recommendation-service/dotnet/` **(1)**. Haga clic derecho en la carpeta `dotnet` y seleccione **Abrir en Terminal Integrada** **(2)** en la pestaña de opciones para abrir la terminal con la ruta requerida.

   ![](./Media/lab3-t2-s3.png)

1. Ahora, necesita reconstruir la imagen docker para el servicio de recomendación ejecutando el siguiente comando docker. Asegúrese de utilizar el mismo nombre de la imagen docker que se creó anteriormente para el servicio de recomendación.

   ```
   docker build . -t miyagi-recommendation
   ```

    >**Nota**: Este comando crea una imagen Docker llamada Miyagi-recommendation a partir del Dockerfile y los archivos asociados en el directorio actual.

1. Ejecute el siguiente comando para iniciar sesión en ACR.

    ```
    docker login <inject key="AcrLoginServer" enableCopy="true"/> -u <inject key="AcrUsername" enableCopy="true"/> -p <inject key="AcrPassword" enableCopy="true"/>
    ```

    >**Nota**: El comando docker login <inject key="AcrLoginServer" enableCopy="false"/> -u <inject key="AcrUsername" enableCopy="false"/> -p <inject key="AcrPassword" enableCopy="false"/> se usa para autenticar el cliente de Docker con el Azure Container Registry (ACR) especificado mediante el nombre de usuario y la contraseña proporcionados. Esta autenticación es necesaria para realizar operaciones como enviar y recibir imágenes de contenedor del ACR.

1. Ejecute el siguiente comando para agregar la etiqueta.

   ```
   docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   >**Note**: El comando docker push <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest carga una imagen de Docker desde su equipo local al Azure Container Registry (ACR) especificado. Al ejecutar este comando, la imagen miyagi-recommendation:latest está disponible en el ACR, lo que permite su uso en diversas implementaciones y servicios de Azure.

1. Una vez que haya iniciado sesión en ACR, ejecute el siguiente comando para enviar la imagen docker actualizada del servicio de recomendación al registro del contenedor.

   ```
   docker push <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   >**Nota**: El comando docker push <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest carga la imagen de Docker miyagi-recommendation:latest en el Azure Container Registry (ACR) especificado. Esto hace que la imagen esté disponible en el ACR para su uso en implementaciones y otras operaciones.

## Tarea 4: Revisión del servicio de Recomendación de AKS 

En esta tarea, administrará el ciclo de vida de la implementación del servicio de recomendaciones en Azure Kubernetes Service (AKS), lo que incluye iniciar y detener el servicio, así como verificar su funcionalidad después de la revisión.

1. Navegue al Portal de Azure, abra el Grupo de Recursos denominado **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  y seleccione el servicio de Kubernetes **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

   ![](./Media/kub1.png)

1. En la pestaña Información general del panel del servicio de Kubernetes **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en el botón **Detener**.

   ![](./Media/sp30.png)

   > **Nota**: Espere hasta que el servicio de Kubernetes se detenga por completo. 

1. En la pestaña Información general del panel del servicio de Kubernetes **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>**, haga clic en el botón **Iniciar**.

   ![](./Media/sp31.png)

1. Una vez que se inicie el servicio de Kubernetes, seleccione **Servicios y entradas(1)** en recursos de Kubernetes y haga clic en **Extension IP(2)** de miyagi-recommendation-service.

   ![](./Media/sp32.png)

1. Esto navegará a una nueva pestaña con la página web de **miyagi-recommendation-service**.

   ![](./Media/kub5.png)

## Tarea 5: Configurar Event Hub Logging y Validar la Entrada

En esta tarea, configurará el registro de Event Hub para API Management, configurará los componentes necesarios en Azure, implementará la configuración de registro mediante una plantilla Bicep y validará la integración mediante pruebas y monitoreo.

1. En el Portal de Azure, busque y seleccione **Event Hubs**, seleccione **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](./Media/sp56.png)

2. En la pestaña Espacios de nombres de Event hub **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, en el menú de la izquierda seleccione **Control de acceso (IAM)** **(1)** , haga clic en **+ Agregar** **(2)**, y seleccione **Agregar asignación de roles** **(3)**.

   ![](./Media/sp34.png)

3. En la pestaña **Agregar asignación de rol**, busque **Remitente de datos de Azure Event Hubs (1)** en la barra de búsqueda, seleccione **Remitente de datos de Azure Event Hubs (2)** y haga clic en **Siguiente (3)**.

   ![](./Media/sp35.png)

4. En la pestaña **Miembros**, seleccione **Identidad administrada** **(1)**, haga clic en **+ Seleccionar miembros** **(2)**.

   ![](./Media/miyagi-image82.png)

5. En la ventana emergente Selección de identidades administradas, para **Suscripción deje el valor predeterminado (1)**, en el menú desplegable Identidad administrada elija **Servicio de gestión de API** **(2)**, seleccione **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)**, haga clic en **Seleccionar** **(4)**. 

   ![](./Media/sp36.png)

6. Haga clic en **Siguiente**.

7. En la pestaña **Revisar y asignar** haga clic en **Revisar y asignar**.

   ![](./Media/namespace3-2.png)

8. En la pestaña Espacio de nombres de Event hub **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, en el menú de la izquierda seleccione **Event Hubs** **(1)** en Entidades y haga clic en **miyagi-event-<inject key="DeploymentID" enableCopy="false"/> (2)**

   ![](./Media/sp37.png)

9. En la **Instancia de Event Hubs** de **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, en el menú de la izquierda seleccione **Políticas de acceso compartido** **(1)** en Configuración, haga clic en **apimLoggerAccessPolicy** **(2)** y copie la **Cadena de conexión principal** **(3)** y péguela en un bloc de notas.

   ![](./Media/sp38.png)

10. Abra el **bloc de notas** de LabVM y copie y pegue el siguiente código, actualizando **&lt;&lt;API_MANAGEMENT_NAME&gt;&gt;** con el nombre **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** y **&lt;&lt;EVENT_HUB_CONNECTION_STRING&gt;&gt;** con el valor copiado en el paso anterior.

    ```
    resource existingApiManagement 'Microsoft.ApiManagement/service@2023-03-01-preview' existing = {
       name: '<<API_MANAGEMENT_NAME>>'
     }
     
     resource ehLoggerWithConnectionString 'Microsoft.ApiManagement/service/loggers@2023-05-01-preview' = {
       name: 'AOAILogger'
       parent: existingApiManagement
       properties: {
         loggerType: 'azureEventHub'
         description: 'Event hub logger with connection string'
         credentials: {
           connectionString: '<<EVENT_HUB_CONNECTION_STRING>>'
           name: 'ApimEventHub'
         }
       }
     }
    ```

    ![](./Media/bicepfile1.png)

11. En la barra de menú del bloc de notas seleccione **Archivo** y haga clic en **Guardar como**.

12. En **Guardar como** navegue a la ruta `C:\LabFiles\miyagi` **(1)**, ingrese el nombre de archivo **aoai-logger.bicep** **(2)**, guarde el tipo como **Todos los archivos** **(3)** y haga clic en **Guardar/Save** **(4)**.

    ![](./Media/bicepfile2-1.png)

13. En LabVM abra la terminal de PowerShell y ejecute el siguiente comando para iniciar sesión en el **Portal de Azure**.

    ```
    az login
    ```

14. Esto lo redireccionará a la **página de inicio de sesión de Microsoft**, seleccione su cuenta de Azure **<inject key="AzureAdUserEmail"></inject>**, y regrese de vuelta a **PowerShell**.

    ![](./Media/sp23.png)

15. Ejecute el siguiente comando para cambiar el directorio a la carpeta raiz `miyagi` en la terminal y ejecutar el archivo bicep.
   
    ```
    cd C:\LabFiles\miyagi
    az deployment group create --resource-group <inject key="rgname" enableCopy="true"/> --template-file .\aoai-logger.bicep
    ```

    > **Nota**: Esta secuencia de comandos navega al directorio C:\LabFiles\miyagi que contiene el archivo Bicep y luego implementa los recursos definidos en ese archivo en el grupo de recursos de Azure especificado.
    
16. Navegue al Portal de Azure, abra el Grupo de recursos denominado **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  y seleccione el servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

    ![](./Media/lab3-t1-s1.png)

17. En servicio API Management **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** en el menú de la izquierda haga clic en **APIs** **(1)** y seleccione **Azure OpenAI Service API** **(2)** que fue creado en un paso anterior, seleccionando **All operations** **(3)** y en **Outbound processing** haga clic en el **Policies(4)**.

    ![](./Media/sp39.png)

18. En el editor de código copie la siguiente política para sobrescribir las etiquetas **salientes** únicamente y haga clic en **Guardar**.

      ```
      <outbound>
         <base />
         <choose>
            <when condition="@(!context.Variables.GetValueOrDefault<bool>("isStream"))">
                  <log-to-eventhub logger-id="AOAILogger" partition-id="0">@{
                  var responseBody = context.Response.Body?.As<JObject>(true);
                  return new JObject(
                     new JProperty("prompt_tokens", responseBody["usage"]["prompt_tokens"].ToString()),
                     new JProperty("total_tokens", responseBody["usage"]["total_tokens"].ToString())
                  ).ToString();
            }</log-to-eventhub>
            </when>
         </choose>
      </outbound>
      ```

      ![](./Media/apmi-output.png)

19. Ahora abra la interfaz de usuario de Miyagi en una pestaña separada del navegador, haga clic en **Personalize**, seleccione su **Asesor Financiero Favorito (1)**, elija **GPT-4 (2)** para **Reasoning Engine** de la lista. Luego, haga clic en **Personalize (3)** y repita los mismos pasos seleccionando diferentes **Asesores Financieros Favoritos** de 6 a 7 veces para generar registros adicionales. 

    ![](./Media/miyagi-image126.png)

    >**Note**: Please ensure that the localhost is running in the VS code or else follow the steps in **Page 4 - Lab 2 - Task 4 - Steps 1 & 2**

20. Vuelva a Event Hubs, seleccione el recurso Event Hub **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](./Media/sp37.png)

21. En el Espacio de nombres Event Hub **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, en el menú de la izquierda seleccione **Event Hubs** **(1)** en **Entidades** y haga clic en **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**

    ![](./Media/namespace4.png)

22. En la Instancia de Event Hubs **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, en el menú de la izquierda seleccione **Procesar datos** **(1)**, desplácese hacia abajo hasta localizar **Procese sus datos de Event Hub usando Stream Analytics Query Language** y haga clic en **Iniciar** **(2)**.

    ![](./Media/sp40.png)


23. Haga clic en **Consulta de lenguaje de consulta** y en Query de Event hub, debería ver información de registro de los tokens utilizados.

    ![](./Media/event-hub-data.png)

## Resumen

En esta práctica de laboratorio, configuró un servicio API Management para administrar las APIs de manera eficiente. Inicialmente, se implementó el servicio y se creó una API dentro de él. Posteriormente se establecieron reglas y roles para controlar el acceso a la API. El registro de Event Hub se configuró para monitorear el uso de API de manera efectiva. Por último, se realizó una validación de entradas para garantizar que la API manejara varias entradas correctamente. En general, este proceso garantizó la gestión efectiva, la seguridad y el monitoreo del rendimiento de las API, contribuyendo a un ecosistema de API seguro y bien organizado.

### Ha completado con éxito el laboratorio. Ahora haga clic en **Siguiente** en la esquina inferior derecha para pasar a la página siguiente.
