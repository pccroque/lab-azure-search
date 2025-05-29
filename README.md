# lab-azure-search

Este laboratório tem como objetivo aplicar técnicas de organização e pesquisa de documentos por meio da ingestão de dados e indexação utilizando ferramentas de inteligência artificial.
Foram abordados três passos principais: ingestão de conteúdo para IA, criação de índices inteligentes e exploração prática dos dados organizados.

*Explorar um índice (UI) do Azure AI Search*
Vamos imaginar que você trabalhe para a Fourth Coffee, uma rede nacional de cafés. Você é solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a pesquisa de insights sobre as experiências do cliente. Para isso, Usaremos o Azure AI Search com os dados extraídos de avaliações de clientes.

**Recursos do Azure necessários:**
A solução para criar o Fourth Coffee requer os seguintes recursos na assinatura do Azure:
- Um recurso do Azure AI Search, que gerenciará a indexação e a consulta.
- Um recurso de serviços de IA do Azure, que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.
- Uma conta de armazenamento com contêineres de blob, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.

**Criar um recurso do Azure AI Search**
1. Entre no *portal do Azure*.
2. Clique no botão **+ Criar um recurso**, pesquise Azure AI Search e crie um recurso Azure **AI Search** com as seguintes configurações: 

**Assinatura:** sua assinatura do Azure.  
**Grupo de recursos:** selecione ou crie um grupo de recursos com um nome exclusivo.  
**Nome do serviço:** um nome exclusivo.  
**Local:** Colocar West US 2 (Fora do Brasil mais barato).  
**Tipo de preço:** Básico   

3. Selecione **Examinar + criar** e, depois de ver a resposta **Validação bem-sucedida**, selecione **Criar**.
4. Após a conclusão da implantação, selecione **Ir para o recurso**. Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

**Criar um recurso de serviços de IA do Azure**  

Você precisará provisionar um recurso de **serviços de IA do Azure** que esteja no mesmo local que o recurso de Pesquisa de IA do Azure. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

1. Retorne à home page do portal do Azure. Clique no botão **+Criar um recurso** e pesquise os *serviços de IA do Azure*.
   Selecione **criar** um plano de **serviços de IA do Azure**. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:  

**Assinatura:** sua assinatura do Azure.  
**Grupo de recursos:** o mesmo grupo de recursos que o recurso do Azure AI Search.  
**Região:** o mesmo local que o recurso do Azure AI Search.  
**Nome:** Um nome exclusivo.  
**Tipo de preço:** Standard S0  

Ao marcar esta caixa, **reconheço que li e entendi todos os termos abaixo:** Selecionado  
2. Selecione **Examinar + criar**. Depois de ver a resposta **Validação aprovada**, selecione **Criar**.  
3. Aguarde a conclusão da implantação e exiba os detalhes da implantação.  

**Criar uma conta de armazenamento**
1. Retorne à home page do portal do Azure e selecione o botão **+ Criar um recurso**.
2. Pesquise a conta de armazenamento e crie um recurso **de conta de armazenamento** com as seguintes configurações:

**Assinatura:** sua assinatura do Azure.  
**Grupo de recursos:** o mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços de IA do Azure.  
**Nome da conta de armazenamento:** um nome exclusivo.  
**Local:** escolha qualquer local disponível.  
**Desempenho:** Padrão  
**Redundância:** LRS (armazenamento com redundância local)  

3. Clique em **Revisar** e, em seguida, clique em **Criar**. Aguarde a conclusão da implantação e vá para o recurso implantado.
4. Na conta de Armazenamento do Azure que você criou, no painel de menu à esquerda, selecione **Configuração**.
5. Altere a configuração de *Permitir acesso anônimo ao Blob* para **Habilitado** e selecione **Salvar**.




