---
title: Configurar a redundância geográfica com o Replicação do SQL Server
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 54106ae635d44368542986c7c469560981f9888a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855839"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>Configurar a redundância geográfica com o Replicação do SQL Server


> [!IMPORTANT]  
> Se você quiser criar um farm de AD FS e usar SQL Server para armazenar os dados de configuração, poderá usar o SQL Server 2008 ou superior.
  
Se você estiver usando SQL Server como seu banco de dados de configuração do AD FS, poderá configurar a redundância de\-geográfica para seu farm de AD FS usando a replicação SQL Server. A redundância de\-geográfica replica dados entre dois sites distantes geograficamente para que os aplicativos possam mudar de um site para outro. Dessa forma, em caso de falha de um site, você ainda pode ter todos os dados de configuração disponíveis no segundo site. Para obter mais informações, consulte a "seção SQL Server de redundância geográfica" no [farm de servidores de Federação usando SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md).  
  
## <a name="prerequisites"></a>{1&gt;{2&gt;Pré-requisitos&lt;2}&lt;1}  
Instalar e configurar um farm do SQL Server. Para obter mais informações, consulte [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Na SQL Server inicial, verifique se o serviço SQL Server Agent está em execução e definido como início automático.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Criar a segunda réplica de \(\) SQL Server para redundância de\-geográfica  
  
1. Instalar SQL Server \(para obter mais informações, consulte [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Copie os arquivos de script CreateDB. SQL e SetPermissions. SQL resultantes para a réplica do SQL Server.  
  
2. Verifique se SQL Server Agent serviço está em execução e definido como início automático  
  
3. Execute **Export\-AdfsDeploymentSQLScript** no nó de AD FS primário para criar arquivos CreateDB. SQL e SetPermissions. Sql.  Por exemplo:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. Copie os scripts para o servidor secundário.  Abra o script CreateDB. SQL no **sql Management Studio** e clique em **executar**.
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. Abra o script SetPermissions. SQL no **sql Management Studio** e clique em **executar**.
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> Você também pode usar o seguinte na linha de comando. 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>Criar configurações de Publicador na SQL Server inicial  
  
1. No SQL Server Management Studio, em **replicação**, clique com o botão direito do mouse em **publicações locais** e escolha **nova publicação...** 
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. Na tela do assistente para nova publicação, clique em **Avançar**.</br>
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. Na página **distribuidor** , escolha servidor local como distribuidor e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. Na página pasta de **instantâneo** , insira \\\SQL1\repldata no lugar da pasta padrão. \(Observação: Talvez você precise criar esse compartilhamento por conta própria\).  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. Escolha **AdfsConfigurationV3** como o banco de dados de publicação e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. Em **tipo de publicação**, escolha **publicação de mesclagem** e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. Em **tipos de assinante**, escolha **SQL Server 2008 ou posterior** e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. Na página de **artigos** , selecione o nó **tabelas** para selecionar todas as tabelas e **des\-Verifique** se a tabela syncproperties \(esta não deve ser replicada\)</br>
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. Na página **artigos** , selecione o nó **funções definidas pelo usuário** para selecionar todas as funções definidas pelo usuário e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. Na página **problemas do artigo** , clique em **Avançar**.  
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. Na página **filtrar linhas da tabela** , clique em **Avançar**.  
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. Na página **agente de instantâneo** , escolha padrões de imediato e 14 dias, clique em **Avançar**.  
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    Talvez seja necessário criar uma conta de domínio para o SQL Agent. Use as etapas em [Configurar logon do SQL para a conta de domínio CONTOSO\\SQLAgent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) para criar o logon do SQL para esse novo usuário do AD e atribuir permissões específicas.  
  
13. Na página **segurança do agente** , clique em **configurações de segurança** e insira o nome de usuário\/senha de uma conta de domínio \(não um\) GMSA criado para o SQL Agent e clique em **OK**.  Clique em **Avançar**.  
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. Na página **ações do assistente** , clique em **Avançar**.   
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. Na página **concluir o assistente** , insira um nome para a publicação e clique em **concluir**. 
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. Depois que a publicação for criada, você deverá ver o status de êxito.  Clique em **Fechar**.
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. De volta ao SQL Server Management Studio, clique com o botão direito do mouse na nova publicação e clique em **iniciar o Replication Monitor**.  
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>Criar configurações de assinatura na SQL Server de réplica  
Certifique-se de que você criou as configurações do Publicador na SQL Server inicial conforme descrito acima e, em seguida, conclua o seguinte procedimento:  
  
1. Na SQL Server de réplica, no SQL Server Management Studio, em **replicação**, clique com o botão direito do mouse em **assinaturas locais** e escolha **nova assinatura...** . ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. Na página **Assistente de nova assinatura** , clique em **Avançar**.
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. Na página **publicação** , selecione o Publicador na lista suspensa.  Expanda **AdfsConfigurationV3** e selecione o nome da publicação criada acima e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. Na página **local do agente de mesclagem** , selecione **executar cada agente em seu assinante \(assinaturas pull\)** \(o\) padrão e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> Isso, juntamente com o tipo de assinatura abaixo, determina a lógica de resolução de conflitos. \(para obter mais informações, consulte [detectar e resolver conflitos de replicação de mesclagem](https://technet.microsoft.com/library/ms151191.aspx). </br>
 
5. Na página **assinantes** , selecione **AdfsConfigurationV3** como o banco de dados do assinante e clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. Na página **segurança do agente de mesclagem** , clique em **...** e insira o nome de usuário e a senha de uma conta de domínio \(não um\) GMSA criado para o SQL Agent usando a caixa reticências e clique em **Avançar**.
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. Em **agenda de sincronização**, escolha **executar continuamente** e clique em **Avançar**. 
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. Em **inicializar assinaturas**, clique em **Avançar**.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. Em **tipo de assinatura**, escolha **cliente** e clique em **Avançar**.  
  
   As implicações disso estão documentadas [aqui](https://technet.microsoft.com/library/ms151191.aspx) e [aqui](https://technet.microsoft.com/library/ms151170.aspx).  Essencialmente, pegamos a resolução de conflitos simples de "primeiro para o Publicador" e não precisamos republicar para outros assinantes.  
   ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. Na página **ações do assistente** , verifique se **a opção criar a assinatura** está marcada e clique em **Avançar**. 
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. Na página **concluir o assistente** , clique em **concluir**. 
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. Depois que a assinatura tiver concluído o processo de criação, você deverá ver o sucesso. Clique em **Fechar**. 
    ![configurar a redundância geográfica](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>Verificar o processo de inicialização e replicação  
  
1.  No SQL Server primário, clique com o botão direito do\-mouse no nó **replicação** e clique em **iniciar o Replication Monitor**.  
  
2.  No **Replication Monitor**, clique na publicação.  
  
3.  Na guia **todas as assinaturas** , clique com o botão direito do mouse e **exiba detalhes**.  
  
    Você deve ser capaz de ver muitas entradas em **ações** para a replicação inicial.  
  
4.  Além disso, você pode examinar o **SQL Server Agent\\nó trabalhos** para ver o trabalho\(s\) agendados para executar as operações da assinatura\/de publicação.  Somente os trabalhos locais são mostrados, portanto, certifique-se de verificar o Publicador e o Assinante para solução de problemas.  À direita\-clique em um trabalho e selecione **Exibir histórico** para exibir o histórico de execução e os resultados.  
  
## <a name="configure-sql-login-for-the-domain-account-contososqlagent"></a><a name="sqlagent"></a>Configurar o logon do SQL para a conta de domínio CONTOSO\\SQLAgent  
  
1.  Crie um novo logon no primário e na réplica SQL Server chamada CONTOSO\\SQLAgent \(o nome do novo usuário de domínio criado e configurado na página **segurança do agente** nos procedimentos acima.\)  
  
2.  Em SQL Server, à direita\-clique no logon que você criou e selecione Propriedades e, na guia **mapeamento de usuário** , mapeie esse logon para bancos de dados **AdfsConfiguration** e **AdfsArtifact** com as funções Public e DB\_genevaservice. Mapeie também esse logon no banco de dados de distribuição e adicione o BD\_função de proprietário para as tabelas de distribuição e adfsconfiguration.  Faça isso conforme aplicável no SQL Server primário e de réplica. Para obter mais informações, consulte [Replication Agent Security Model](https://technet.microsoft.com/library/ms151868.aspx).  
  
3.  Conceda à conta de domínio correspondente permissões de leitura e gravação no compartilhamento configurado como distribuidor.  Verifique se você definiu as permissões de leitura e gravação nas permissões de compartilhamento e nas permissões de arquivo local.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>Configurar AD FS nó\(s\) para apontar para o farm de réplica de SQL Server  
Agora que você configurou a redundância geográfica, os nós do farm de AD FS podem ser configurados para apontar para o farm de SQL Server de réplica usando os recursos de farm do AD FS "junção" padrão, seja da interface do usuário do assistente de configuração do AD FS ou usando o Windows PowerShell.  
  
Se você usar a interface do usuário do assistente de configuração do AD FS, selecione **Adicionar um servidor de Federação a um farm de servidores de Federação**. **Não selecione** **criar o primeiro servidor de Federação em um farm de servidores de Federação**.  
  
Se você usar o Windows PowerShell, execute **adicionar\-AdfsFarmNode**. **Não** execute **instalar\-AdfsFarm**.  
  
Quando solicitado, forneça o host e o nome da instância do SQL Server de réplica, **não** o SQL Server inicial.  
