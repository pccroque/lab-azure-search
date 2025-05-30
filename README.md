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


**Carregar documentos no Armazenamento do Azure**

1. No painel de menu à esquerda, selecione **Contêineres**.
2. Selecione **+ Contêiner**. Um painel no seu lado direito é aberto.
3. Insira as seguintes configurações e clique em **Criar:**<br>
   **Nome:** coffee-reviews<br>
   **Nível de acesso público:** contêiner (acesso de leitura anônimo para contêineres e blobs)<br>
   **Avançado:** *sem alterações*.<br>

4. Em uma nova guia do navegador, baixe as *avaliações de café compactadas* de e extraia os arquivos para a pasta de *avaliações*. https://aka.ms/mslearn-coffee-reviews<br>
5. No portal do Azure, selecione seu contêiner coffee-reviews. No contêiner, selecione **Carregar**.<br>
6. No painel **Carregar blob**, selecione **Selecionar um arquivo.**<br>
7. Na janela Explorer, selecione **todos** os arquivos na pasta de revisões, selecione **Abrir** e, em seguida, selecione **Carregar**.<br>
8. Após a conclusão do carregamento, você pode fechar o painel **Carregar blob**. Seus documentos agora estão em seu contêiner *de armazenamento de avaliações de café*.<br>

**Indexar os documentos**

Depois de ter os documentos armazenados, você pode usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente de importação de dados. Com esse assistente, você pode criar automaticamente um índice e um indexador para fontes de dados com suporte. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

1. No portal do Azure, navegue até o recurso do Azure AI Search. Na página Visão geral, selecione Importar dados.
2. Na página Conectar-se aos seus dados, na lista Fonte de Dados, selecione Armazenamento de Blobs do Azure. Preencha os detalhes do armazenamento de dados com os seguintes valores:
Fonte de dados: Armazenamento de Blobs do Azure
Nome da fonte de dados: coffee-customer-data
Dados a serem extraídos: conteúdo e metadados
Modo de análise: Padrão
Cadeia de conexão: *Selecione Escolher uma conexão existente. Selecione sua conta de armazenamento, selecione o contêiner coffee-reviews e clique em Selecionar.
Autenticação de identidade gerenciada: nenhuma
Nome do contêiner: essa configuração é preenchida automaticamente depois que você escolhe uma conexão existente.
Pasta Blob: deixe em branco.
Descrição: Comentários sobre Fourth Coffee shops.
3. Selecione Avançar: Adicionar habilidades cognitivas (opcional).
4. Na seção Anexar Serviços de IA, selecione o recurso de serviços de IA do Azure.
5. Na seção Adicionar enriquecimentos:
   * Altere o nome do conjunto de habilidades para coffee-skillset.
   * Marque a caixa de seleção Ativar OCR e mesclar todo o texto em merged_content campo.
      Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecido.
   * Certifique-se de que o campo Dados de origem esteja definido como merged_content.
   * Altere o nível de granularidade de enriquecimento para Páginas (partes de 5000 caracteres).
   * Não selecione Habilitar enriquecimento incremental
   * Selecione os seguintes campos enriquecidos:

| Habilidade cognitiva | Parâmetro | Nome do campo |
| ---------------------------------- | ---------------- | ----------------- |
| Extrair nomes de locais            |        	 	     | Locais |
| Extrair frases-chave               |	 	              | frases-chave |
| Detectar sentimento                |	                 | sentimento |
| Gerar tags a partir de imagens     |	 	              | tags de imagem |
| Gerar legendas a partir de imagens |	 	              | legenda da imagem |


6. Em **Salvar enriquecimentos em um repositório de conhecimento**, selecione:

   *  Projeções de imagem
   *  Documentos
   *  Páginas
   *  Frases-chave
   *  Entidades
   *  Detalhes da imagem
   *  Referências de imagem

7. Selecione **Escolher uma conexão existente**. Escolha a conta de armazenamento que você criou anteriormente.
8. Selecione **Projeções de blob do Azure: Documento**. Uma configuração para *Nome do contêiner* com o contêiner de *armazenamento de conhecimento* preenchido automaticamente é exibida. Não altere o nome do contêiner.
9. Selecione **Avançar: Personalizar índice de destino**. Altere **o nome do índice** para **coffee-index**.
10. Certifique-se de que a **chave** esteja definida como **metadata_storage_path**. Deixe o **nome do Suggester** em branco e o **modo de pesquisa** preenchido automaticamente.
11. Revise as configurações padrão dos campos de índice. Selecione **filtrável** para todos os campos que já estão selecionados por padrão. Os nomes de campo que precisam ser marcados como *filtráveis* incluem: conteúdo, locais, frases-chave, sentimento, merged_content, texto, layoutText, imageTags, imageCaption.
12. Selecione **Avançar: Criar um indexador**.
13. Altere o **nome do indexador** para **coffee-indexer**.
14. Deixe o **Agendamento** definido como **Uma vez**.
15. Expanda as **opções avançadas**. Certifique-se de que a opção **Chaves de Codificação de Base 64** esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
16. Selecione **Enviar** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
    * Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
    * Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
    * Mapeia os campos extraídos para o índice.
17. Retorne à página de recursos do Azure AI Search. No painel esquerdo, em **Gerenciamento de Pesquisa**, selecione **Indexadores**. Selecione o **indexador de café recém-criado**. Aguarde um minuto e selecione **&orarr; Atualize** até que o **Status** indique sucesso.
18. Selecione o nome do indexador para ver mais detalhes.


**Consultar o índice**

Use o Gerenciador de pesquisa para escrever e testar consultas. O gerenciador de pesquisa é uma ferramenta integrada ao portal do Azure que oferece uma maneira fácil de validar a qualidade do índice de pesquisa. Você pode usar o Gerenciador de Pesquisa para escrever consultas e revisar resultados em JSON.

1. Na página *Visão geral* do serviço de Pesquisa, selecione **Gerenciador de pesquisa** na parte superior da tela.
2. Observe como o índice selecionado é o *índice de café* que você criou. Abaixo do índice selecionado, altere a exibição para **a exibição JSON**.

No campo **Editor de consultas JSON**, copie e cole:
```
{
    "search": "*",
    "count": true
}
```
   1. Selecione **Pesquisar**. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count. O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.
   2. Agora vamos filtrar por localização. No campo **Editor de consultas JSON**, copie e cole:
```
   código
   {
      "search": "locations:'Chicago'",
      "count": true
   }
```
   3. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra as revisões com um local de Chicago. Você deve ver no **campo.3@odata.count**
   4. Agora vamos filtrar por sentimento. No campo **Editor de consultas JSON**, copie e cole:
```
   código
   {
      "search": "sentiment:'negative'",
      "count": true
   }
```   
   5. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra as revisões com um sentimento negativo. Você deve ver no campo.1@odata.count

      **Nota**
      Veja como os resultados são classificados por . Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quão próximos os resultados correspondem à consulta
      fornecida. @search.score

   6. Um dos problemas que podemos querer resolver é por que pode haver certas revisões. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. Qual você acha que pode ser a causa da revisão?


**Examinar o repositório de conhecimento**

Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o *assistente para Importar dados*, você também criou um repositório de conhecimento. Dentro do repositório de conhecimento, você verá que os dados enriquecidos extraídos pelas habilidades de IA persistem na forma de projeções e tabelas.

   1. No portal do Azure, navegue de volta para sua conta de armazenamento do Azure.
   2. No painel de menu à esquerda, selecione **Contêineres**. Selecione o contêiner do **repositório de conhecimento**.
   3. Você verá uma lista de pastas. Há uma pasta para todos os metadados de cada documento de revisão. **Selecione qualquer uma das pastas**. Na pasta, clique no arquivo **objectprojection.json.**
   4. Selecione **Editar** para ver o JSON produzido para um dos documentos do armazenamento de dados do Azure.
   5. Selecione a trilha de navegação do blob de armazenamento na parte superior esquerda da tela para retornar aos *Contêineres* da conta de armazenamento.
   6. Em *Contêineres*, selecione o contêiner *coffee-skillset-image-projection*. Selecione qualquer um dos itens.
   7. Selecione qualquer um dos *.jpg* arquivos. Selecione **Editar** para ver a imagem armazenada do documento. Observe como todas as imagens dos documentos são armazenadas dessa maneira.
   8. Selecione a trilha de navegação do blob de armazenamento na parte superior esquerda da tela para retornar aos *Contêineres* da conta de armazenamento.
   9. Selecione **Navegador de armazenamento** no painel esquerdo e selecione **Tabelas**. Há uma tabela para cada entidade no índice. Selecione a tabela *coffeeSkillsetKeyPhrases*.

Veja as frases-chave que o repositório de conhecimento conseguiu capturar do conteúdo nas avaliações. Muitos dos campos são chaves, portanto, você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.
















