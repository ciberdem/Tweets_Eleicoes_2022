# Tweets_Eleicoes_2022 - Pipeline de Processamento de Dados 

Contexto:

Ao longo dos últimos vinte anos as disputas eleitorais têm sido impactadas diretamente pelo fenômeno das redes sociais. Os políticos que souberam interagir com os diferentes grupos de eleitores, através das redes, tiveram impactos positivos em suas campanhas.

No entanto, esse ambiente também se tornou fértil para fenômenos negativos como a ultra polarização das discussões políticas, com grupos radicais manipulando como os fatos são absorvidos dentro de suas “bolhas” de influência, impactando diretamente os rumos das campanhas eleitorais. O Brasil não ficou alheio a essa condição. Por exemplo, o ano de 2022 ´e considerado um dos períodos eleitorais mais polarizados da história brasileira.

Entender como esses grupos se formam e se relacionam dentro das redes sociais, quem são seus principais influenciadores e visualizar como o posicionamento eleitoral desses perfis impactaram a maneira como os eventos do ano eleitoral brasileiro de 2022 foram discutidos dentro de suas “bolhas”. As informações coletadas tornaram-se importantes para ajudar no entendimento da dinâmica das redes no processo democrático no Brasil. Dentro deste contexto, a pesquisa "Monitoramento de discussões políticas no Twitter durante as Eleições de 2022 no Brasil: polarização, agrupamento e principais atores" tem como objetivo colaborar com esse entendimento, através da proposta de construção de um pipeline de extração e processamento dos dados do Twitter durante eventos políticos relevantes no Brasil em 2022, sendo esse constituído de um processo estruturado que atua em conjunto com programas desenvolvidos em Python e uma ferramenta de Análise de Redes Sociais. 

Após sua execução, foi possível gerar visualizações dos principais atores, agrupamentos de perfis e os diferentes pontos de discussão dentro desses grupos, evidenciando o movimento da polarização nas redes a partir das discussões sobre a ocorrência e divulgação dos fatos ao longo do tempo. Para apoiar a visualização dos resultados da execução desse processo ´e apresentado um estudo de caso com dados extraídos do Twitter durante os eventos de 8 de janeiro de 2023 em Brasília.

Nesse diretório se encontra disponível os arquivos fontes utilizados para execução da pipeline de extração.

Lista de Arquivos do Pipeline:
1.	Tese_extrai_tweets_v2023 - Módulo de extração dos Tweets - Passo 1 (Notebook Jupyter)

2.	IDs_Lista_Distribuicao_Twitter.txt - Arquivo com os IDs das listas de distribuição usadas para conseguir a lista de usuários e executar a categorização (necessita "hidratação" a partir do Twitter)

3.	twitter_contas_br_2022_v3_exemplo.txt - Exemplo do arquivo com os usuários extraídos das listas, com a categorização a partir da presença em cada lista e pela declaração de voto (Pro_Bolsonaro, Pro_Lula e Neutro/Indefinido)

4.	Tese_Gera_Visao_Geral_Modularidades_v2023: Módulo de análise das modularidades identificadas pelo processamento dos dados extraídos.

5.	Tese_trabalha_maiores_modularidade_inbound_v2023: Módulo de análise detalhada de cada modularidade e seus subgrupos.

6.	Tese_GeraPDF_Geral_Modularidade_v2023: Módulo ilustrativo da geração de arquivos PDF para exposição dos resultados.

Howto de Execução
![image](https://github.com/ciberdem/Tweets_Eleicoes_2022/assets/142453499/0c1f8f6f-8290-45c9-b5ee-335bec914624)

Preparação:

1. Reidratar os IDs listados no arquivo "IDs_Lista_Distribuicao_Twitter.txt", de maneira a se conseguir as informações como Nome da Lista, Usuários participantes, etc.
2. A partir da reidratação do arquivo extrair os usuários e salvar a informação no formato do Arquivo "twitter_contas_br_2022_v3_exemplo.txt".
3. Fazer a classificação dessas contas a partir da declaração de voto de cada usuário.
4. Fazer o Download da versão mais recente da ferramenta de análise de dados grafos Gephi - https://gephi.org/

Passo A: Extração dos dados

1. Configurar o token de acesso provido pelo Twitter (*) no módulo Tese_extrai_tweets_v2023
2. Identificar a notícia/acontecimento que se quer explorar (Ex: Sites de Informação, Portais, Jornais, etc)
3. Observar e selecionar seu comportamento na timeline do Twitter (Ex: hashtags e/ou termos se destacando dentro do Trend Tópics)
4. Fazer a configuração da query de extração com os termos escolhidos (Ex: Termo, Período, nro máx de tweets a serem recuperados, etç)
5. Configurar os diretórios, data da execução do processo, diretório de armazenamento dos arquivos, etc.
6. Executar o processo de extração

Passo B: Processamento via Gephi

A partir dos arquivos de Nodes e Edges gerados após a execução do passo A:

1. Importar para o Gephi como um gráfico difigido e com a estratégia de mesclagem dos Edges configurada para "Don't Merge".
2. Executar os cálculos: Grau Médio, Grau Ponderado Médio, Diametro da Rede, Densidade do Grafo, HITS, PageRank, Componentes Conectados, Centralidade de Auto Vetor, Coeficiente de Clustering Médio e Modularidade.
3. Gerar visões de rede para os dados e exportando para o diretório indicado no passo A. 
4. Ir para a aba "Laboratório de Dados" e a partir das visão geral dos dados gerar arquivos de saída com os dados gerais e as 4 maiores modularidades calculadas.

Passo C: Visão Geral das Modularidades

1. Configurar o token de acesso provido pelo Twitter (*) no módulo Tese_Gera_Visao_Geral_Modularidades_v2023
2. Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos, etc.
3. Executar o processo de análise

Passo D: Visão detalhada de Modularidades

1. Configurar o token de acesso provido pelo Twitter (*) no módulo Tese_trabalha_maiores_modularidade_inbound_v2023
2. Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos, etc.
3. Executar o processo de análise

Passo D: Geração de relatório - PDF (opcional)

1. Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos, etc. - Tese_GeraPDF_Geral_Modularidade_v2023
2. Executar o processo de análise

Observações:

(*) - A partir de 2023 o Twitter passou a cobrar para todo acesso as suas APIs, removendo acessos gratuitos que haviam antes (Ex: pesquisadores). Portanto para conseguir um token de acesso terá que ser utilizado um plano pago disponibilizado pelo Twitter na época. 

(**) - O Pipeline foi construido no intuito de suprir uma lacuna existente hoje que é a de existir um processo padronizado para visualização de discussões políticas dentro da esfera das redes sociais, providenciando para isso a extração, processamento e apresentação dos dados de análise. Ele foi criado a partir de estudo das necessidades, uso de exemplo de códigos disponíveis na Internet e integração com uma ferramenta Open Source (Gephi).  
