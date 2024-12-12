# Machine-Learning-na-Pratica-DIO--AI900
Criando um modelo de aprendizado de maquina automatizado-DIO-AI900

# CONFIGURAÇÕES INICIAIS

NOME: mslearn-bike-rental
NOVO NOME: mslearn-bike-rental
DESCRIÇÃO: Aprendizado de maquina automatizado para previvão de locação de bicicletas
TAGS: N/D

# TIPO DE TAREFA E DADOS

Selecionar o tipo de tarefa: Regressão
Selecionar o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações

   Tipo de dados:
   
   Nome: locação de bicicletas
   Descrição: dados historicos de locação de bicicletas
   Tipo: tabela (tabelavel)

   Fonte de dados
   Web: https://aka.ms/bike-rentals

   baixar e extrair a pasta que contem os arquivos necessarios

   Destino de armazenamento:
      Armazenamento: Azure Blob Storage
      Nome: woekspaceblobstore

Selecionar (CRIAR)
Após a criação do tipo de dado, selecione (locação de bicicletas) para continuar e submeter  no serviço de ML AUTOMAZIDO

# CONFIGURAÇÃO DA TAREFA

Tipo de tarefa: Regressão
Tipo de dados: Locação de bicicletas
Coluna alvo: Locação (inteiro)

Configuração adicional:
   Metrica Primaria: NormalizedRootMeanSquaredError 
   Explicar melhor modelo: Não selecionar
   Habilitar o empilhamento de conjunto: Não selecionar
   Use todos os modelos suportados: Não selecionar 
   Modelos permitidos: Selecione apenas RandomForest e LightGBM (caso queira testar outros modelos o tempo de execução tera aumento no serviço)

# LIMITES

  Tentativa de testes: 3
  Tentativa de testes simultaneos: 3
  Máximo de nós : 3
  Limite da pontução metrica : 0.085 (ao atigir o valor delimitado ou menor  no erro da raiz quadrada normalizada o serviço ira terminar)
  Tempo de experimento: 15
  Tempo de interação: 15
  Permitir o termino antecipado: selecionado

# VALIDAÇÃO E TESTE

Tipo de validação : Train-validation split
% de validação dos dados: 10
Teste conjunto de dados : nenhum

# CALCULAR

Selecione o tipo de calculo: Serveless
Tipo de maquina virtual: CPU
Nível máquina virtual: Dedicado
Tamanho maquina virtual:Standard_DS3_V2*
Numero de instancias: 1

Obs: Se a sua assinatura do Azure restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível

Submeta o trabalho de treino, ele iniciara automaticamente

Espere pelo termino , pode demorar um pouco

Na guia Visão geral do trabalho automatizado de aprendizado de máquina, observe o melhor resumo do modelo
Selecione abaixo de  "Nome do Algoritmo" o para visualizar o melhor modelo e seus detalhes.
Selecione a guia Métricas e selecione os gráficos de residuals e  predicted_true se ainda não estiverem selecionados.   

# IMPLANTAR E TESTE DO MODELO
Na guia (Model) para o melhor modelo treinado pelo seu trabalho automatizado de aprendizado de máquina,Selecione Implantar e usar a opção de ponto de extremidade em tempo real para implantar o modelo com as seguintes configurações:

  Máquina virtual: Standard_DS3_v2
  Contagem de instâncias: 3
  Ponto final: Novo
  Nome do endpoint: Deixe o padrão ou certifique-se de que é globalmente único
  Nome de implantação: Deixe o padrão
  Inferência de coleta de dados: Desativado
  Modelo do pacote: Desativado

  Espere a implementação começar- pode demorar alguns segundos.
  O status de Implantação para o endpoint predict-rentals será indicado na parte principal da página como (Executando).

 Aguarde que o status de Implantação mude para Bem-Sucedido. Isso pode levar de 5 a 10 minutos
  
  Testando o serviço

No Azure Machine Learning studio, no menu esquerdo, selecione Endpoints e abra o ponto de extremidade predict-locação em tempo real.

Na pagina predict-locação , olhe a guia de testes

No painel de Input data to test endpoint, substitua o modelo JSON com os seguintes dados de entrada:

# {
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
} # 

Revise os resultados do teste, que incluem um número previsto de aluguel com base nos recursos de entrada
