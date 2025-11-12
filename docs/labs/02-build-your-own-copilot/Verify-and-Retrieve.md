# Laboratorio 1 - Verificar y Recuperar los valores de los Recursos de Azure (opcional)

### Duración estimada: 20 minutos

En esta tarea, se verifican y recuperan valores específicos, incluidos el punto de conexión, la cadena de conexión y la clave para los recursos designados.

   - Azure OpenAI : **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** 
   - Cuenta de Azure Cosmos DB : **cosmos-<inject key="DeploymentID" enableCopy="false"/>**
   - Servicio Search : **acs-<inject key="DeploymentID" enableCopy="false"/>**

1. Para verificar los nombres de los modelos implementados para "**deploymentOrModelId**" y para "**embeddingDeploymentOrModelId**" siga los pasos a continuación:
   
      - En la página de inicio del Portal de Azure, haga clic en **Grupos de Recursos** en el panel Navegar.

          ![](./Media/sp4.png)

      - Desde la página Grupos de Recursos, haga clic en **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

         ![](./Media/sp5.png)

      - En **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, en la pestaña **Información general (1)** seleccione **OpenAIService-<inject key="DeploymentID" enableCopy="false"/> (2)**.

        ![](./Media/11-10-24(18).png)

      - En la página **Información general de OpenAI** **(1)**, haga clic en el botón **Ir al portal de la fundición de IA de Azure (2)** para ir al **Portal de Azure AI Foundry**.

           ![](./Media/sp6.png) 
   
      - En el **Portal de Azure AI Foundry**, en el panel de navegación izquierdo, seleccione **Implementaciones**, en la sección **Recursos compartidos**.

           ![](./Media/sp7.png)

      - En la hoja **Implementaciones** **(1)** de Azure AI Foundry, haga clic en el nombre de la implementación **miyagi-CompletionModel-<inject key="DeploymentID" enableCopy="false"/>** y verifique el **nombre de la implementación** del modelo gpt-4.1 **(2)**.

          ![](./Media/sp8.png)
        
          ![](./Media/sp9.png)
      
      -  Vuelva a la página **Implementaciones (1)**.

      - En la hoja Implementaciones de Azure AI Foundry, haga clic en el nombre de implementación **miyagi-EmbeddingModel-<inject key="DeploymentID" enableCopy="false"/>** y verifique el **nombre de implementación** del modelo **text-embedding-ada-002 (2)**.
        
          ![](./Media/sp10.png)

         ![](./Media/sp11.png)

1. Para verificar los valores para "**endpoint**" y "**apiKey**", siga los pasos a continuación:

   -  Vuelva a la pestaña que muestra **Portal de Azure**. 

   -  En la hoja **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** en la sección **Administración de Recursos**, seleccione **Claves y punto de conexión (1)**, verifique **Clave 1 (2)** y **Extremo (3)**.
     
      ![](./Media/sp12.png)

1. Para verificar los valores para  "**azureCognitiveSearchEndpoint**" y  "**azureCognitiveSearchApiKey**", siga los pasos a continuación:
   
   - Vuelva al grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

   - En la página **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, seleccione **acs-<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

      ![](./Media/sp13.png)
 
   - En la hoja **acs-<inject key="DeploymentID" enableCopy="false"/>**, verifique la **URL**.
   
      ![](./Media/sp52.png)

   - En la hoja **acs-<inject key="DeploymentID" enableCopy="false"/>**, en la sección **Configuración**, selecciona **Clave (1)** y verifica el valor de la **Clave de administrador principal (2)**.
   
      ![](./Media/image-rg-14.png)

1. Para verificar los valores de "**cosmosDbUri**" y "**cosmosDbName**," por favor siga los pasos a continuación:

   - Vuelva a la página del grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, seleccione **cosmos-<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

     ![](./Media/select-cosmosdb.png)

   - En **cosmos-<inject key="DeploymentID" enableCopy="false"/>** verifique la **URL**.
     
     ![](./Media/image-rg-16.png)

   - En **cosmos-<inject key="DeploymentID" enableCopy="false"/>** en **Configuración**, seleccione **Claves (1)** y verifique el valor de la **CADENA DE CONEXIÓN PRINCIPAL de Cosmos DB (2)**.

     ![](./Media/cs.png)

1. Para obtener los valores de  "**blobServiceUri**", por favor siga los pasos a continuación:

   - Vuelva a la página del grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, seleccione **miyagiblobstorge<inject key="DeploymentID" enableCopy="false"/>** de la lista de recursos.

     ![](./Media/select-storage.png)

   - En la cuenta de almacenamiento **miyagiblobstorge<inject key="DeploymentID" enableCopy="false"/>**, del menú de la izquierda seleccione **Puntos de conexión** **(1)** en Configuración y verifique **Blob service** **(1)** en Blob service.

     ![](./Media/sp53.png)

## Resumen
En este laboratorio, verificará y recuperará valores de configuración como el punto de conexión, la cadena de conexión y la clave para diversos recursos de Azure, como OpenAI Service, Cosmos DB y Cognitive Search. Esto garantiza una configuración y conectividad correctas. Los pasos implican acceder al Portal de Azure, navegar a grupos de recursos específicos y verificar los valores requeridos.

### Ahora haga clic en **Siguiente** en la esquina inferior derecha para pasar a la página siguiente.


   ![](./Media/next-page-2.png)
