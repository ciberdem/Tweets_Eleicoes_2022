# Tweets_Eleicoes_2022 - Pipeline de Processamento de Dados 

Contexto:
As disputas eleitorais têm sido impactadas diretamente pelo fenômeno das redes sociais.  Esses ambientes se tornaram férteis para observar fenômenos como a ultra polarização das discussões políticas, a radicalização e a manipulação de fatos dentro de “bolhas” de influência. 
Torna-se importante entender, ao longo do debate político, como os grupos se formam e se relacionam dentro das redes sociais, quem são seus principais influenciadores, como se posicionam e como se dá a dinâmica de discussão entre eles em relação a eventos que acontecem fora das redes.
O ano de 2022 é considerado um dos períodos eleitorais mais polarizados da história brasileira. A pesquisa "Monitoramento de discussões políticas no Twitter durante as Eleições de 2022 no Brasil: polarização, agrupamento e principais atores" (publicação em breve), desenvolvida no âmbito do CIBERDEM e do Programa de Pós-Graduação em Computação Aplicada da Universidade Presbiteriana Mackenzie , teve como objetivo propor a construção de um pipeline de extração e processamento dos dados do Twitter a partir de eventos políticos relevantes durante o processo eleitoral para presidência do Brasil em 2022.
O pipeline é estruturado como um processo que atua em conjunto com programas desenvolvidos em Python para extração e tratamento dos dados obtidos do Twitter e a visualização dos dados com uso da ferramenta de análise de redes sociais Gephi (https://gephi.github.io/).
O pipeline permite gerar visualizações dos principais atores, agrupamentos de perfis e os diferentes pontos de discussão dentro desses grupos, evidenciando o movimento da polarização nas redes a partir das discussões sobre a ocorrência e divulgação dos fatos ao longo do tempo.
Nesse repositório se encontra disponível os arquivos fontes utilizados para execução da pipeline.
Lista de Arquivos do Pipeline:
1.	Extrai_tweets - Módulo de extração dos Tweets - Passo 1 (Notebook Jupyter)
2.	IDs_Lista_Distribuicao_Twitter.txt - Arquivo com os IDs das listas de distribuição usadas para conseguir a lista de usuários e executar a categorização (necessita "hidratação" a partir do Twitter)
3.	Twitter_contas_br_2022_exemplo.txt - Exemplo do arquivo com os usuários extraídos das listas, com a categorização a partir da presença em cada lista e pela declaração de voto (Pro_Bolsonaro, Pro_Lula e Neutro/Indefinido)
4.	Gera_Visao_Geral_Modularidades: Módulo de análise das modularidades identificadas pelo processamento dos dados extraídos.
5.	Gera_maiores_modularidade_inbound: Módulo de análise detalhada de cada modularidade e seus subgrupos.
6.	GeraPDF_Geral_Modularidade: Módulo ilustrativo da geração de arquivos PDF para exposição dos resultados.
7.	Datasets – Extrações de 2022/2023
No diretório \Datasets_Desidratados se encontram os arquivos extraídos a partir da execução do Pipeline ao longo de 2022 e em janeiro de 2023.
Esses arquivos têm a seguinte estrutura de dados: 
 
A lista completa dos datasets se encontra no arquivo Execução do Pipeline - Lista de Arquivos coletados em 2022, com o nome dos arquivos, meses e datas de extração e um link para a notícia que motivou a pesquisa. 
Para recuperação de todos os dados do tweets será necessário fazer a “reidratação” da informação a partir dos IDs apresentados nos arquivos. Para isso o Twitter possui uma página com a referência de uso para as APIs necessárias para recuperação dos dados (https://developer.twitter.com/en/docs/api-reference-index).
Observação: a partir do ano de 2023 o Twitter mudou seu modelo de acesso as APIs, passando a cobrar para o uso (https://developer.twitter.com/en/docs/twitter-api).
Howto 
 
Passo A: Preparação:
1.	Reidratar os IDs listados no arquivo "IDs_Lista_Distribuicao_Twitter.txt", de maneira a se conseguir as informações como Nome da Lista, Usuários participantes etc.
2.	A partir da reidratação do arquivo, extrair os usuários e salvar a informação no formato do Arquivo "twitter_contas_br_2022_v3_exemplo.txt".
3.	Fazer a classificação dessas contas a partir da declaração de voto de cada usuário. Para isso a partir da lista de perfis extraídos das listas de distribuição, houve uma visita à timeline de cada um dos perfis no Twitter, e observado a posição voto autodeclarada em cada um deles (pró Lula ou pró Bolsonaro), gerando dessa maneira a categorização dos perfis. Caso não houvesse uma declaração explicita do usuário, ele foi categorizado como “Neutro/Indeciso”. 
4.	Fazer o Download da versão mais recente da ferramenta de análise de dados grafos Gephi - https://gephi.org/
Passo B: Extração dos dados
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Extrai_tweets
2.	Identificar a notícia/acontecimento que se quer explorar (Ex. Sites de Informação, Portais, Jornais, etc)
3.	Observar e selecionar seu comportamento na timeline do Twitter (Ex: hashtags e/ou termos se destacando dentro do Trend Topics)
4.	Fazer a configuração da query de extração com os termos escolhidos (Ex: termo, período, número máximo de tweets a serem recuperados, etç)
5.	Configurar os diretórios, data da execução do processo, diretório de armazenamento dos arquivos etc.
6.	Executar o processo de extração
Passo C: Processamento via Gephi
A partir dos arquivos de nodes e edges gerados após a execução do passo B:
1.	Importar os arquivos para o Gephi, sendo que para o de tipo de gráfico deve ser escolhida a opção “dirigido”, por se tratar de um estudo de mensagens enviadas e replicadas por usuários no Twitter e como a estratégia de mesclagem dos edges deve ser configurada a opção de "Don't Merge".
2.	Executar os cálculos: Grau Médio, Grau Ponderado Médio, Diâmetro da Rede, Densidade do Grafo, HITS, PageRank, Componentes Conectados, Centralidade de Autovetor, Coeficiente de Clustering Médio e Modularidade.
3.	Gerar visões de rede para os dados, exportando para o diretório indicado no passo B.
4.	Ir para a aba "Laboratório de Dados" e, a partir da visão geral dos dados, gerar arquivos de saída com os dados gerais e as 4 maiores modularidades calculadas.
Passo D: Visão Geral das Modularidades
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Gera_Visao_Geral_Modularidades
2.	Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos, etc.
3.	Executar o processo de análise
Passo E: Visão detalhada das maiores Modularidades (a quantidade pode ser configurada) 
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Gera_maiores_modularidade_inbound
2.	Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos etc.
3.	Executar o processo de análise
Passo F: Geração de relatório - PDF (opcional)
1.	Dentro do script configurar as variáveis de ambiente com os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos etc. - Tese_GeraPDF_Geral_Modularidade_v2023
2.	Executar o script de geração de relatório, que irá gerar uma visão agrupada em formato PDF, a partir dos arquivos gerados nas outras etapas. 
3.	É importante frisar que esse script mostra apenas uma forma de como gerar uma visão das análises e pode ser modificado e configurado para entregar a informação desejada, servindo de referência de como apresentar os resultados da análise. 
Resumo das Etapas: 
 
Observações:
(*) - A partir de 2023 o Twitter passou a cobrar para todo acesso as suas APIs, removendo acessos gratuitos anteriores (Ex: pesquisadores). Portanto para conseguir um token de acesso terá que ser utilizado um plano pago disponibilizado pelo Twitter.
Referências:
xxxx

BERTANHA, M., ARAUJO, R.M., SILVA, L.J., Linha do Tempo: Eleições Presidenciais 2022 https://ciberdem.mack.com.br/index.php/linha-do-tempo-eleicoes-presidenciais-2022/
Equipe e contatos:
Luciano José da Silva - luciano.jose-silva@outlook.com (pesquisador principal)
Renata Mendes de Araujo – renata.araujo@mackenzie.br
Manuela de Caria Bertanha - manuela.bertanha@mackenzista.com.br
Ana Grasielle Dionisio Correa - ana.correa@mackenzie.br
Livia Alabarse dos Santos - liviaalabarse.santos@mackenzista.com.br
Orlando Bisacchi Coelho – orlando.coelho@mackenzie.br
Apoio:
O conteúdo deste repositório foi desenvolvido em parceria com a equipe do Projeto HEIWA – Mineração e Visualização de Discussões em Redes Sociais, desenvolvido no âmbito do CIBERDEM, financiado pela FAPESP.
A elaboração da Linha do Tempo contou com o apoio do CNPq.
*********************************************************
Grupo de Pesquisa e Inovação em Ciberdemocracia (CIBERDEM)
Programa de Pós-Graduação em Computação Aplicada
Faculdade de Computação e Informática
Universidade Presbiteriana Mackenzie


