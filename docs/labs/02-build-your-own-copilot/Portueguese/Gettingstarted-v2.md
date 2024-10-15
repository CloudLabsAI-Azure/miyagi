## Introdução ao laboratório

1. Após a configuração do ambiente, o seu navegador carregará uma máquina virtual (JumpVM). Utilize essa máquina virtual durante todo o workshop para realizar o laboratório. Você pode consultar o número na parte inferior do guia de laboratório para alternar entre diferentes exercícios.

   ![](../Media/gettingstartedpagenew1-v2.png)

1. Para obter os detalhes do ambiente de laboratório, você pode selecionar a guia **Detalhes do Ambiente**. Além disso, as credenciais também serão enviadas para o seu endereço de e-mail registrado. Você também pode abrir o Guia de Laboratório em uma janela separada e completa, selecionando a opção **Dividir Janela** no canto inferior direito. Além disso, pode iniciar, parar e reiniciar máquinas virtuais na guia **Recursos**.

   ![](../Media/gettingstartedpagenew2-v2.png)

 > Você verá o valor SUFFIX no guia **Detalhes do Ambiente**, utilize-o sempre que vir SUFFIX ou DeploymentID nas etapas do laboratório.

## Faça login no Portal do Azure

1. Minimize o **Docker Desktop**, clicando no botão **Minimizar**.

   ![](../Media/miyagi-image1.png)

 > **Observação:** Se você encontrar o erro "Falha na atualização do WSL" no aplicativo Docker Desktop, clique no botão **Reiniciar** para reabrir o aplicativo Docker Desktop a partir da área de trabalho.

   ![](../Media/docker-issue.png)

1. No JumpVM, clique no atalho do Portal do Azure no navegador Microsoft Edge, que é criado no ambiente de trabalho.

   ![](../Media/gettingstartpage3.png)

1. Na guia **Entrar no Microsoft Azure**, verá a tela de login. Insira o seguinte e-mail ou nome de usuário e clique em **Avançar**.

     * **E-mail/Nome de usuário**: **<inject key="AzureAdUserEmail"></inject>**

       ![](../Media/miyagi-image2.png)

1. Agora, digite a seguinte senha e clique em **Entrar**.

    * **Senha**: **<inject key="AzureAdUserPassword"></inject>**

      ![](../Media/miyagi-image3.png)

1. Se você vir o pop-up **Permanecer conectado?**, selecione **Não**.

   ![](../Media/miyagi-image4.png)

1. Se uma janela pop-up **Bem-vindo ao Microsoft Azure** aparecer, selecione **Cancelar** para ignorar o tour.

   ![](../Media/miyagi-image5.png)

1. Agora que você verá o Painel do Portal do Azure, clique em **Grupos de recursos** no painel de navegação para ver os grupos de recursos.

   ![](../Media/miyagi-image6.png)

1. Em **Grupos de recursos**, clique em **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** grupo de recursos.

   ![](../Media/miyagi-image7.png)

1. No grupo de recursos **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, verifique os recursos nele presentes.

   ![](../Media/miyagi-image8.png)


> [!IMPORTANTE]<br>
> **Para uma experiência mais fluida durante o laboratório prático, é importante rever minuciosamente as instruções e as notas complementares. Isso o ajudará a navegar pelas tarefas com facilidade e confiança.**
