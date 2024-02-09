
# Aprendizado de Máquina com Azure Machine Learning

Voce vera um resumo de passos para treinar e avaliar um modelo com Azure Machine Learning.

Esse exercicio utiliza um conjunto de dados históricos de aluguel de bicicletas para treinar um modelo.[Conjunto de Dados](https://aka.ms/bike-rentals).

O modelo prevê o número de aluguéis de bicicletas esperados em um determinado dia, com base em características sazonais e meteorológicas.

## Criar um espaço de trabalho do Aprendizado de Máquina do Azure

Para usar o Aprendizado de Máquina do Azure, você precisa provisionar um espaço de trabalho do Aprendizado de Máquina do Azure em sua assinatura do Azure. Em seguida, você poderá usar o estúdio para trabalhar com os recursos em seu espaço de trabalho.

1. Entre no [Azure portal](https://portal.azure.com) e `https://portal.azure.com` use suas credenciais da Microsoft.

1. Selecione **+ Create a resource**, procure por *Machine Learning* na barra de pesquisa, e crie um novo recurso com as seguitnes configurações:
    - **Subscription**: *sua assinatura do Azure*.
    - **Resource group**: *crie ou selecione um grupo de recursos*.
    - **Name**: *Insira um nome exclusivo para seu espaço de trabalho*.
    - **Region**: *Selecione a região geográfica mais próxima*.
    - **Storage account**: *observe a nova conta de armazenamento padrão que será criada para seu espaço de trabalho*.
    - **Key vault**: *Observe o novo cofre de chaves padrão que será criado para seu espaço de trabalho*.
    - **Application insights**: *observe o novo recurso padrão de insights de aplicativo que será criado para seu espaço de trabalho*.
    - **Container registry**: *Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner)*.

1. Selecione **Review + create** e, em seguida, selecione **Create**.
Aguarde até que seu espaço de trabalho seja criado (pode levar alguns minutos) e vá para o recurso implantado.

<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/205cafa4-2298-4f17-aa15-777861359ea1" width="700px" />
</div>

1. Selecione **Launch studio** (ou abra uma nova guia do navegador e navegue até [https://ml.azure.com](https://ml.azure.com?azure-portal=true),e entre no estúdio do Aprendizado de Máquina do Azure usando sua conta da Microsoft).

1. No estúdio de Aprendizado de Máquina do Azure, você deve ver seu espaço de trabalho recém-criado. Caso contrário, selecione **All workspaces** de trabalho no menu à esquerda e, em seguida, selecione o espaço de trabalho que você acabou de criar.

## Usar o aprendizado de máquina automatizado para treinar um modelo

1. No [Azure Machine Learning studio](https://ml.azure.com?azure-portal=true), exiba a página **Automated ML** (em **Authoring**).

1. Crie um novo trabalho de ML automatizado com as seguintes configurações, usando **Next** conforme necessário para progredir pela interface do usuário:

    **Configurações básicas**:

    - **Nome do trabalho:**: mslearn-bike-automl
    - **Novo nome do experimento:**: mslearn-bike-rental
    - **Descrição:**: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
    - **Tags:**: *nenhuma*

   **Tipo de tarefa & data:**:

    - **Selecionar tipo de tarefa:**: Regression
    - **Selecionar conjunto**: crie um novo conjunto de dados com as seguintes configurações:
        - **Tipo de dados:**:
            - **Name**: bike-rentals
            - **Description**: Dados históricos de aluguer de bicicletas
            - **Type**: Tabular
        - **Fonte de dados:**:
            - Select **From web files**
        - **Web URL**:
            - **Web URL**: `https://aka.ms/bike-rentals`
            - **Ignorar validação de dados:**: *não selecione*
        - **Configurações**:
            - **Formato de arquivo:**: Delimitado
            - **Delimitador**: Vírgula
            - **Codificação**: UTF-8
            - **Cabeçalhos de coluna:**: Somente o primeiro arquivo tem cabeçalhos
            - **Pular linhas:**:Nenhum
            - **O conjunto de dados contém dados de várias linhas**: *não selecione*
        - **Esquema**:
            - Incluir todas as colunas diferente de  **Path**
            - Revisar os tipos detectados automaticamente

        Selecione **Create**. Depois que o conjunto de dados for criado, selecione o conjunto de dados de **bike-rentals** para continuar a enviar o trabalho de ML automatizado.

    **Configurações da tarefa:**:

    - **Tipo de tarefa**: Regressão
    - **Conjunto de dados:**: bike-rentals
    - **Coluna de destino:**: Rentals (integer)
    - **Definições de configuração adicionais:**:
        - **Métrica primária:**: Normalized root mean squared error
        - **Explicar melhor modelo:**: *Unselected*
        - **Use todos os modelos suportados:**: <u>Un</u>selected. *Nãoselecionado. Você restringirá o trabalho para tentar apenas alguns algoritmos específicos.*
        - **Modelos permitidos:**: *Selecione apenas **RandomForest** e **LightGBM** — normalmente você gostaria de tentar o maior número possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.*
    - **Limites**: *Expanda esta seção*
        - **Máximo de tentativas:**: 3
        - **Máximo de tentativas simultâneas:**: 3
        - **Nós máximos:s**: 3
        - **Limiar de**: pontuação métrica: 0,085 *(de modo que, se um modelo atingir uma pontuação métrica quadrática média normalizada de 0,085 ou menos, o trabalho termina.)*
        - **Tempo limite:**: 15
        - **Tempo limite de iteração:**: 15
        - **Habilitar rescisão antecipada:**: *SSelecionado*
    - **Validação e teste**:
        - **Tipo de validação:**: Divisão de validação de treinamento
        - **Porcentagem de dados de validação:**: 10
        - **Conjunto de dados de teste:**: Nenhum

    **Computação:**:

    - **Selecione o tipo de computação:**: Serverless
    - **Tipo de máquina virtual:**: CPU
    - **Camada de máquina virtual:**: Dedicado
    - **Tamanho da máquina virtual:**: Standard_DS3_V2\*
    - **Número de instâncias:**: 1

    \* *Se sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.*

1. Envie o trabalho de treinamento. Ele começa automaticamente.

## Overview

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo treinado.

1. Na guia **Visão geral** do trabalho de aprendizado de máquina automatizado, observe o melhor resumo do modelo.
   
<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/ce1b1d15-2d6d-48af-a3c0-8ebf0f4b986c" width="700px" />
</div>


    > **Nota**
    > Nota Você pode ver uma mensagem sob o status "Aviso: pontuação de saída especificada pelo usuário atingida...". Esta é uma mensagem esperada. Continue para a próxima etapa.
  
1. Selecione o texto em **Nome do algoritmo** para o melhor modelo para exibir seus detalhes.

1. Selecione a guia **Métricas** tab and select the **gráficos de resíduos** e **predicted_true** se ainda não estiverem selecionados. 

    Analise os gráficos que mostram o desempenho do modelo. O gráfico **resíduos** mostra os *resíduos* (as diferenças entre os valores previstos e reais) como um histograma. O gráfico **predicted_true** compara os valores previstos com os valores verdadeiros. 

## Implantar e testar o modelo

1. Na guia **Modelo** para obter o melhor modelo treinado pelo seu trabalho de aprendizado de máquina automatizado, selecione **Implantar**  e usar a opção **Web service** para implantar o modelo com as seguintes configurações:
    - **Nome**: predict-rentals
    - **Descrição:**: Prever aluguéis de ciclos
    - **Tipo de computação:**:  Instância de Contêiner do Azure
    - **Habilitar autenticação:**: *Selecionado*

1. Aguarde o início da implantação - isso pode levar alguns segundos. O **status de implantação** para o ponto de extremidade **de aluguel de previsão** será indicado na parte principal da página como *Em execução..*
1. Aguarde até que o **status Implantar** seja alterado para Bem-sucedido. Isso pode levar de 5 a 10 minutos.

## Testar o serviço implantado

Agora você pode testar seu serviço implantado.

1. No estúdio do Aprendizado de Máquina do Azure, no menu à esquerda, selecione Pontos de extremidade e abra o ponto de **extremidade**   em tempo real de **aluguéis de previsão.**

1. Na página de ponto de extremidade em tempo real de  **aluguéis de previsão** exiba a guia **Teste.**

1. No painel Dados de entrada **para testar o ponto de extremidade** substitua o modelo JSON pelos seguintes dados de entrada:

    ```JSON
    {
      "Inputs": { 
        "data": [
          {
            "day": 1,
            "mnth": 1,   
            "year": 2022,
            "season": 2,
            "holiday": 0,
            "weekday": 1,
            "workingday": 1,
            "weathersit": 2, 
            "temp": 0.3, 
            "atemp": 0.3,
            "hum": 0.3,
            "windspeed": 0.3 
          }
        ]    
      },   
      "GlobalParameters": 1.0
    }
    ```

1. Clique no botão **Testar.**
   
<div align="center">
    <img src="https://github.com/Mouretz/DIO-Bootcamp-Certificacao-Azure-AI900/assets/104279399/4269cae8-4f49-4432-a7c2-0ddb4f904af5" width="700px" />
</div>

1. Analise os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada - semelhante a este:

    ```JSON
    {
      "Results": [
        335.84926542932226
      ]
    }
    ```

    O painel de teste pegou os dados de entrada e usou o modelo treinado para retornar o número previsto de aluguéis.

Por fim , utilizamos um conjunto de dados de dados históricos de aluguel de bicicletas com base em características sazonais e meteorológicas. O modelo prevê o número de aluguéis de bicicletas esperados em um determinado dia.