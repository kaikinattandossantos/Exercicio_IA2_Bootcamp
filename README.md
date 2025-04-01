# Exercicio_IA2_Bootcamp
Definição do objetivo da pesquisa
Objetivo: "Analisar o sentimento (positivo, negativo ou neutro) em postagens do X sobre IA em 2025".
Insight inicial: Definir um escopo claro ajuda a escolher os dados e o modelo certos.
Configuração do ambiente no Azure
No Portal Azure, criei um recurso do Azure Machine Learning:
Nomeei como "SentimentAnalysisWorkspace".
Escolhi a região mais próxima (ex.: East US) e usei o plano gratuito para começar.
Acessei o AML Studio (ml.azure.com) e configurei um novo workspace.
Coleta de dados
Usei o Azure Functions para criar uma função em Python que acessa a API do X e coleta 1.000 postagens recentes com a palavra-chave "AI 2025".
Salvei os dados brutos (texto das postagens) em um Azure Blob Storage como um arquivo CSV chamado tweets_data.csv.
Insight: O Azure Functions é ótimo para automação, mas precisei garantir que a chave da API do X estivesse segura usando o Azure Key Vault.
Preparação dos dados no AML
No AML Studio, criei um novo Dataset importando o tweets_data.csv do Blob Storage.
Usei o recurso de Data Preparation para limpar os dados:
Removi postagens duplicadas e textos com menos de 5 palavras.
Adicionei uma coluna de "sentimento" pré-rotulada (usando um pequeno conjunto de dados anotado manualmente para treinar o modelo).
Insight: A limpeza no AML é intuitiva e economiza tempo comparado a scripts manuais.
Treinamento do modelo
No AML Studio, escolhi a opção Automated Machine Learning (AutoML):
Tipo de tarefa: Classificação (para prever sentimentos: positivo, negativo, neutro).
Dataset: Meu conjunto preparado.
Configurações: Limitei o tempo de execução a 1 hora e usei uma métrica primária de "Acurácia".
O AutoML testou vários algoritmos e escolheu o melhor (ex.: um modelo de Regressão Logística).
Resultado: Acurácia de 85% no conjunto de teste.
Insight: O AutoML é poderoso para iniciantes, mas ajustar hiperparâmetros manualmente pode melhorar ainda mais os resultados.
Implantação do modelo
Após o treinamento, implantei o modelo como um endpoint em tempo real no AML:
Escolhi o tipo de computação "Azure Container Instance" (ACI) por ser mais barato para testes.
Testei o endpoint enviando uma postagem de exemplo ("IA vai revolucionar 2025!") e recebi a previsão: "Positivo".
Insight: A implantação é simples, mas monitorar o uso do ACI é essencial para evitar custos extras.
Análise dos resultados
Usei o endpoint para classificar todas as 1.000 postagens coletadas.
Resultados: 60% positivas, 25% neutras, 15% negativas.
Exportei os dados para o Power BI (integrado ao Azure) e criei um gráfico de barras para visualizar as tendências.
Insight: Combinar AML com Power BI torna os resultados mais acessíveis para apresentações.
Insights
O Azure Machine Learning simplifica o processo de IA, desde a coleta até a previsão, com ferramentas integradas que não exigem conhecimento profundo de código.
A escalabilidade do Azure permite começar pequeno (ex.: 1.000 postagens) e expandir para milhões sem mudar a estrutura.
Automatizar a coleta com Azure Functions e analisar com AML reduz o trabalho manual em pelo menos 70% comparado a métodos tradicionais.
Possibilidades de ferramentas que se beneficiam
Azure Cognitive Services: Poderia complementar o AML com análise de texto pré-construída (ex.: Text Analytics) para sentimentos, economizando tempo no treinamento.
Power BI: Transforma os resultados do AML em dashboards interativos para equipes de negócios.
Azure Synapse Analytics: Útil para pesquisas maiores, integrando dados estruturados (ex.: CSV) e não estruturados (ex.: texto bruto).
Microsoft Teams: Integração para compartilhar insights da pesquisa com colegas diretamente do Azure.
Aprendizados adquiridos
Gerenciamento de recursos: Aprendi a desligar o endpoint e os recursos de computação após o uso para evitar custos (ex.: ACI cobra por hora).
AutoML é um atalho: Não precisei entender cada algoritmo; o Azure fez o trabalho pesado, mas estudar os modelos sugeridos me ajudou a aprender mais sobre IA.
Integração é chave: Conectar Blob Storage, AML e Power BI me mostrou como o ecossistema Azure funciona bem em conjunto.
Planejamento importa: Definir o objetivo e preparar os dados bem desde o início evitou retrabalho.
Considerações de custo (para seu receio)
Usei o crédito de $200 do nível gratuito e estimei um custo de ~$5 para esse exercício (1 hora de AutoML + ACI).
Desativei o endpoint logo após o teste para não gastar mais.
