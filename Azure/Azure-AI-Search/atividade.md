# Azure Cognitive Search

Numma rede nacional de cafés você é solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a pesquisa de insights sobre as experiências do cliente. 
Você decide criar um índice de Pesquisa de IA do Azure usando dados extraídos de avaliações de clientes.

Resumo

- Criar recursos do Azure
- Extrair dados de uma fonte de dados
- Enriqueça dados com habilidades de IA
- Usar o indexador do Azure no portal do Azure
- Consultar seu índice de pesquisa

Para isso voce devera criar um mecanismo de busca, um recurso de IA e uma storage account para reunir as informacoe.

1. Criar um novo resoure group do tipo Azure AI Search e selecione o princing basic.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/36bd6e87-0c87-4325-aad5-f93b1d578455"  width="700px" />
</div> 


2.Criar Recurso de IA do mesmo grupo do Search Service.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/c372f9ba-fc85-4a58-b94c-3ee66c906890" width="700px" />
</div> 

3.Criar um Servico do Zero em Storage Accounts


<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/028693e9-2e2c-4314-abdb-c1f73682611b" width="700px"/>
</div> 

LRS - Opções de redundância, sao as replicas dos dados armazenados dentro do storage acconunts.

4.Liberar nas configurações acessos anônimos. Clique em Salvar após a mudança!

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/ad841de2-c062-4edb-b23a-1a00b85f5567" width="700px"/>
</div> 

5. Criar um novo container de nível remoto, depois selecione Upload e carregue os arquivos.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/704b7f94-07c2-4f2d-b070-9b78babd3c66" width="700px" />
</div> 

Após criar nosso mecanismo de busca, um recurso de IA e uma storage account para reunir as informacoes…


6.Abra o mecanismo de busca, no AI Search e importe os dados.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/024e7ed6-3e7d-4579-a523-156a10322112" width="700px"/>
</div> 

Na página **Conectar aos seus dados**, na lista **Fonte de Dados**, selecione **Armazenamento de Blobs do Azure**. Conclua os detalhes do armazenamento de dados com os seguintes valores:

- **Fonte de dados**: Armazenamento de Blobs do Azure
- **Nome da fonte de dados**: coffee-customer-data
- **Dados a serem extraídos**: conteúdo e metadados
- **Modo de análise**: Padrão
- **Cadeia de** conexão: *Selecione **Escolher uma conexão existente**. Selecione sua conta de armazenamento, selecione o contêiner de **revisões de café** e clique em **Selecionar**.
- **Autenticação de identidade gerenciada**: Nenhuma
- **Nome do contêiner**: *essa configuração é preenchida automaticamente depois que você escolhe uma conexão existente*.
- **Pasta Blob**: *deixe isso em branco*.
- **Descrição**: Comentários a Fourth Coffee shops.

Selecione **Avançar: Adicionar habilidades cognitivas (Opcional).**

7. Na seção **Anexar Serviços Cognitivos**, selecione seu recurso de serviços de IA do Azure.

Na seção **Adicionar enriquecimentos**:

- Altere o **nome do Skillset** para **coffee-skillset**.
- Marque a caixa **de seleção Habilitar OCR e mesclar todo merged_content texto em campo**.
- Selecion os seguintes campos de acordo com a imagem.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/793e289f-3c7f-4d76-a8f2-6fe8311cf5c0" width="700px"/>
</div> 

8. Em **Salvar enriquecimentos em um repositório de conhecimento**, selecione:
- Image projections
- Documents
- Pages
- Key phrases
- Entities
- Image details
- Image references

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/f3bf108e-7ddb-4390-b5b4-0af0ff5e1c30" width="700px" />
</div> 

Selecione projeções de blob do Azure: Documento. Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do contêiner de armazenamento de conhecimento. Não altere o nome do contêiner.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/f7203ea6-2f25-4873-82f4-aa081dd813f9" width="700px"/>
</div> 

10. Selecione **Avançar: Personalizar índice de destino**. **Altere o nome do índice** para **coffee-index**.
    
    1.Verifique se a **chave** está definida como **metadata_storage_path**. Deixe o **nome do Sugeridor** em branco e **o modo de Pesquisa** preenchido automaticamente.
    
    2.Revise as configurações padrão dos campos de índice. Selecione **filtrável** para todos os campos que já estão selecionados por padrão.

  <div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/27a8e003-4b21-4957-ac4c-b2b5d91e7ee4" width="700px"/>
    </div


12. Selecione **Avançar: Criar um indexador**.**Altere o nome do indexador** para **coffee-indexer**.
    
    11.1 Deixe a **Agenda** definida como **Uma vez/Once**.
    
    11.2 Expanda as **opções Avançadas**. Verifique se a opção **Base-64 Encode Keys** está selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
    
    11.3 Selecione **Enviar** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
    
    - Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
    - Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
    - Mapeia os campos extraídos para o índice.

    ## CONSULTAR O INDICE

    <div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/7d0efe1c-53d5-4e21-8f74-4f0b279da0ec" width="700px"/>
    </div> 
    
    <div align="center">
    <img src="(https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/f6999f4e-319c-49ad-bdae-98cc4a1b4f0a" width="700px"/>
    </div> 

    12. O campo **Editor de consultas JSON**, copie e cole:

    ```
    json
    {
    "search": "*","count": true
    }

    ```

    Selecione **Pesquisar**. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo **@odata.count.** O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.
    
    <div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/0f973e70-3632-4707-938c-88697029a925" width="700px"/>
    </div> 

    13. Agora vamos filtrar por localização. No campo **Editor de consultas JSON**, copie e cole:
    
    ```
    json{
     "search": "locations:'Chicago'","count": true
    }
    
    ```

    Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra por revisões com um local de Chicago. Você deve ver no campo.`3@odata.count`
   <div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/ceafa344-fb35-4ae7-9c62-799e03016d20" width="700px"/>
    </div> 

   14. Agora vamos filtrar por **sentimento**. No campo **Editor de consultas JSON**, copie e cole:

    ```json
        { "search": "sentiment:'negative'", "count": true
        }
    ```
Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra por avaliações com um sentimento negativo. Você deve ver no campo.`1@odata.count`

> Nota Veja como os resultados são classificados por . Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quanto os resultados correspondem à consulta dada.@search.score

