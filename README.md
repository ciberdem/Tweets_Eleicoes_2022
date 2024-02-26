# Tweets_Eleicoes_2022 - Pipeline de Processamento de Dados 

## **Contexto:**

As disputas eleitorais têm sido impactadas diretamente pelo fenômeno das redes sociais.  Esses ambientes se tornaram férteis para observar fenômenos como a ultra polarização das discussões políticas, a radicalização e a manipulação de fatos dentro de “bolhas” de influência. 

Torna-se importante entender, ao longo do debate político, como os grupos se formam e se relacionam dentro das redes sociais, quem são seus principais influenciadores, como se posicionam e como se dá a dinâmica de discussão entre eles em relação a eventos que acontecem fora das redes.

O ano de 2022 é considerado um dos períodos eleitorais mais polarizados da história brasileira. A pesquisa "Monitoramento de discussões políticas no Twitter durante as Eleições de 2022 no Brasil: polarização, agrupamento e principais atores" (publicação em breve), desenvolvida no âmbito do [CIBERDEM](https://ciberdem.mack.com.br/) e do [Programa de Pós-Graduação em Computação Aplicada da Universidade Presbiteriana Mackenzie](https://www.mackenzie.br/pos-graduacao/mestrado-doutorado/sao-paulo-higienopolis/programa-de-pos-graduacao-em-computacao-aplicada-profissional) , teve como objetivo propor a construção de um pipeline de extração e processamento dos dados do Twitter a partir de eventos políticos relevantes durante o processo eleitoral para presidência do Brasil em 2022.

O pipeline é estruturado como um processo que atua em conjunto com programas desenvolvidos em Python para extração e tratamento dos dados obtidos do Twitter e a visualização dos dados com uso da ferramenta de análise de redes sociais Gephi (https://gephi.github.io/).

O pipeline permite gerar visualizações dos principais atores, agrupamentos de perfis e os diferentes pontos de discussão dentro desses grupos, evidenciando o movimento da polarização nas redes a partir das discussões sobre a ocorrência e divulgação dos fatos ao longo do tempo.

Nesse repositório se encontram disponíveis os arquivos fontes utilizados para execução do pipeline.

**Lista de Arquivos do Pipeline:**

1.	**Extrai_tweets** - Módulo de extração dos Tweets - Passo 1 (Notebook Jupyter)
2.	**IDs_Lista_Distribuicao_Twitter.txt** - Arquivo com os IDs das listas de distribuição usadas para conseguir a lista de usuários e executar a categorização (necessita "hidratação" a partir do Twitter)
3.	**Twitter_contas_br_2022_exemplo.txt** - Exemplo do arquivo com os usuários extraídos das listas, com a categorização a partir da presença em cada lista e pela declaração de voto (Pro_Bolsonaro, Pro_Lula e Neutro/Indefinido)
4.	**Gera_Visao_Geral_Modularidades:** Módulo de análise das modularidades identificadas pelo processamento dos dados extraídos.
5.	**Gera_maiores_modularidade_inbound:** Módulo de análise detalhada de cada modularidade e seus subgrupos.
6.	**GeraPDF_Geral_Modularidade:** Módulo ilustrativo da geração de arquivos PDF para exposição dos resultados.
7.	**Datasets – Extrações de 2022/2023**

No diretório **\Datasets_Desidratado**s se encontram os arquivos extraídos a partir da execução do Pipeline ao longo de 2022 e em janeiro de 2023.
Esses arquivos têm a seguinte estrutura de dados: 

![image](https://github.com/ciberdem/Tweets_Eleicoes_2022/blob/main/Dataset_Desidrat_estrutura_v1.jpg)

 
A lista completa dos **datasets** se encontra no arquivo **Execução do Pipeline - Lista de Arquivos coletados em 2022**, com o nome dos arquivos, meses e datas de extração e um link para a notícia que motivou a pesquisa. 

Para recuperação de todos os dados do tweets será necessário fazer a “**reidratação**” da informação a partir dos IDs apresentados nos arquivos. Para isso o _Twitter_ possui uma página com a referência de uso para as APIs necessárias para recuperação dos dados (https://developer.twitter.com/en/docs/api-reference-index).

**Observação**: a partir do ano de 2023 o _Twitter_ mudou seu modelo de acesso as APIs, passando a cobrar para o uso (https://developer.twitter.com/en/docs/twitter-api).

## **Howto** 

![image](https://github.com/ciberdem/Tweets_Eleicoes_2022/assets/142453499/81ac983e-b7c0-4ba9-a28c-54332f5790c4)

**Passo A: Preparação:**
1.	Reidratar os IDs listados no arquivo "IDs_Lista_Distribuicao_Twitter.txt", de maneira a se conseguir as informações como Nome da Lista, Usuários participantes etc.
2.	A partir da reidratação do arquivo, extrair os usuários e salvar a informação no formato do Arquivo "twitter_contas_br_2022_v3_exemplo.txt".
3.	Fazer a classificação dessas contas a partir da declaração de voto de cada usuário. Para isso a partir da lista de perfis extraídos das listas de distribuição, houve uma visita à timeline de cada um dos perfis no Twitter, e observado a posição voto autodeclarada em cada um deles (pró Lula ou pró Bolsonaro), gerando dessa maneira a categorização dos perfis. Caso não houvesse uma declaração explicita do usuário, ele foi categorizado como “Neutro/Indeciso”. 
4.	Fazer o Download da versão mais recente da ferramenta de análise de dados grafos Gephi - https://gephi.org/

**Passo B: Extração dos dados**
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Extrai_tweets
2.	Identificar a notícia/acontecimento que se quer explorar (Ex. Sites de Informação, Portais, Jornais, etc)
3.	Observar e selecionar seu comportamento na timeline do Twitter (Ex: hashtags e/ou termos se destacando dentro do Trend Topics)
4.	Fazer a configuração da query de extração com os termos escolhidos (Ex: termo, período, número máximo de tweets a serem recuperados, etç)
5.	Configurar os diretórios, data da execução do processo, diretório de armazenamento dos arquivos etc.
6.	Executar o processo de extração

**Passo C: Processamento via Gephi**
A partir dos arquivos de nodes e edges gerados após a execução do passo B:
1.	Importar os arquivos para o Gephi, sendo que para o de tipo de gráfico deve ser escolhida a opção “dirigido”, por se tratar de um estudo de mensagens enviadas e replicadas por usuários no Twitter e como a estratégia de mesclagem dos edges deve ser configurada a opção de "Don't Merge".
2.	Executar os cálculos: Grau Médio, Grau Ponderado Médio, Diâmetro da Rede, Densidade do Grafo, HITS, PageRank, Componentes Conectados, Centralidade de Autovetor, Coeficiente de Clustering Médio e Modularidade.
3.	Gerar visões de rede para os dados, exportando para o diretório indicado no passo B.
4.	Ir para a aba "Laboratório de Dados" e, a partir da visão geral dos dados, gerar arquivos de saída com os dados gerais e as 4 maiores modularidades calculadas.

**Passo D: Visão Geral das Modularidades**
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Gera_Visao_Geral_Modularidades
2.	Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos, etc.
3.	Executar o processo de análise

**Passo E: Visão detalhada das maiores Modularidades (a quantidade pode ser configurada)** 
1.	Configurar o token de acesso provido pelo Twitter (*) no módulo Gera_maiores_modularidade_inbound
2.	Configurar os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos etc.
3.	Executar o processo de análise

**Passo F: Geração de relatório - PDF (opcional)**
1.	Dentro do script configurar as variáveis de ambiente com os diretórios, nomes dos arquivos de entrada e saída, diretório de armazenamento dos arquivos etc. - Tese_GeraPDF_Geral_Modularidade_v2023
2.	Executar o script de geração de relatório, que irá gerar uma visão agrupada em formato PDF, a partir dos arquivos gerados nas outras etapas. 
3.	É importante frisar que esse script mostra apenas uma forma de como gerar uma visão das análises e pode ser modificado e configurado para entregar a informação desejada, servindo de referência de como apresentar os resultados da análise.

**Resumo das Etapas:**

![image](https://github.com/ciberdem/Tweets_Eleicoes_2022/assets/142453499/d6b36fd5-bb98-4a9e-8e70-1d391f7c8377)
 
**Observações:**
(*) - A partir de 2023 o Twitter passou a cobrar para todo acesso as suas APIs, removendo acessos gratuitos anteriores (Ex: pesquisadores). Portanto para conseguir um token de acesso terá que ser utilizado um plano pago disponibilizado pelo Twitter.

## **Referências:**

[BERTANHA, M., ARAUJO, R.M., SILVA, L.J., Linha do Tempo: Eleições Presidenciais 2022](https://ciberdem.mack.com.br/index.php/linha-do-tempo-eleicoes-presidenciais-2022/)

(outras referências em breve)

## **Equipe e contatos:**

Luciano José da Silva - luciano.jose-silva@outlook.com (pesquisador principal)

Renata Mendes de Araujo – renata.araujo@mackenzie.br

Manuela de Caria Bertanha - manuela.bertanha@mackenzista.com.br

Ana Grasielle Dionisio Correa - ana.correa@mackenzie.br

Livia Alabarse dos Santos - liviaalabarse.santos@mackenzista.com.br

Orlando Bisacchi Coelho – orlando.coelho@mackenzie.br

## Apoio:

O conteúdo deste repositório foi desenvolvido em parceria com a equipe do Projeto HEIWA – Mineração e Visualização de Discussões em Redes Sociais, desenvolvido no âmbito do CIBERDEM, financiado pela FAPESP.

A elaboração da Linha do Tempo contou com o apoio do CNPq.
*********************************************************
[Grupo de Pesquisa e Inovação em Ciberdemocracia (CIBERDEM)](https://d.docs.live.net/75628dacdeb58954/Documentos/ciberdem.mack.com.br)

[Programa de Pós-Graduação em Computação Aplicada](https://www.mackenzie.br/pos-graduacao/mestrado-doutorado/sao-paulo-higienopolis/programa-de-pos-graduacao-em-computacao-aplicada-profissionalhttps:/www.mackenzie.br/pos-graduacao/mestrado-doutorado/sao-paulo-higienopolis/programa-de-pos-graduacao-em-computacao-aplicada-profissional)

[Faculdade de Computação e Informática](https://www.mackenzie.br/universidade/unidades-academicas/fci)

[Universidade Presbiteriana Mackenzie](https://www.mackenzie.br/)

# Anexo:

## Lista de Arquivos coletados em 2022


| Mês de Coleta	| Pasta	| Arquivo	| Data	| Evento |
| -------------	| -----	| -------	| ----	| ------ |
|	Maio 2022	|	Raiz	|	Ciro	|	21/05/2022	|	https://g1.globo.com/politica/eleicoes/2022/noticia/2022/05/21/ciro-gomes-e-gregorio-duvivier-batem-boca-durante-debate-em-live.ghtml	|
|	Maio 2022	|	Raiz	|	Gregório	|	21/05/2022	|	https://g1.globo.com/politica/eleicoes/2022/noticia/2022/05/21/ciro-gomes-e-gregorio-duvivier-batem-boca-durante-debate-em-live.ghtml	|
|	Maio 2022	|	Raiz	|	BolsoMusk	|	20/05/2022	|	https://www.cnnbrasil.com.br/politica/elon-musk-tem-encontro-com-bolsonaro-no-interior-de-sao-paulo/	|
|	Maio 2022	|	Raiz	|	jair_vacina	|	20/05/2022	|	https://www1.folha.uol.com.br/equilibrioesaude/2022/05/mais-da-metade-das-criancas-vacinadas-contra-covid-pode-estar-com-2a-dose-atrasada.shtml	|
|	Maio 2022	|	Raiz	|	BNDES_3005	|	30/05/2022	|	https://noticias.uol.com.br/confere/ultimas-noticias/2022/05/30/empresa-ligada-a-shows-de-gusttavo-lima-nao-pegou-r-320-milhoes-com-bndes.htm	|
|	Junho 2022	|	Raiz	|	Datafolha_2306	|	23/06/2022	|	https://g1.globo.com/politica/eleicoes/2022/pesquisa-eleitoral/noticia/2022/06/23/datafolha-lula-tem-47percent-no-primeiro-turno-contra-28percent-de-bolsonaro.ghtml	|
|	Junho 2022	|	Raiz	|	Datafolha_2606	|	26/06/2022	|	https://www1.folha.uol.com.br/mercado/2022/06/datafolha-1-em-cada-4-brasileiros-diz-que-falta-comida-em-casa.shtml	|
|	Junho 2022	|	Raiz	|	Datafolha_2706	|	27/06/2022	|	https://www1.folha.uol.com.br/mercado/2022/06/datafolha-1-em-cada-4-brasileiros-diz-que-falta-comida-em-casa.shtml	|
|	Junho 2022	|	Raiz	|	Todoscombolsonaro	|	08/06/2022	|	https://www.poder360.com.br/governo/bolsonaro-volta-a-falar-que-pode-nao-cumprir-decisao-do-stf/	|
|	Junho 2022	|	Raiz	|	TSE	|	20/06/2022	|	https://g1.globo.com/politica/eleicoes/2022/noticia/2022/06/20/em-oficio-a-fachin-ministro-da-defesa-pede-reuniao-exclusiva-das-forcas-armadas-com-tecnicos-do-tse.ghtml	|
|	Junho 2022	|	Raiz	|	RodaViva	|	28/06/2022	|	https://www.poder360.com.br/governo/tarcisio-diz-que-coloca-a-cara-no-fogo-por-bolsonaro/	|
|	Junho 2022	|	Raiz	|	Nunes_marques	|	08/06/2022	|	https://oglobo.globo.com/politica/noticia/2022/06/apos-decisao-contra-francischini-ministros-do-stf-se-incomodam-com-silencio-sobre-caso-de-outro-bolsonarista.ghtml	|
|	Junho 2022	|	Raiz	|	Magno Malta	|	14/06/2022	|	https://veja.abril.com.br/coluna/maquiavel/barroso-aciona-o-stf-contra-magno-malta-apos-ser-acusado-de-agredir-mulher	|
|	Junho 2022	|	Raiz	|	Forças Armadas	|	10/06/2022	|	https://www.correiobraziliense.com.br/politica/2022/06/5014514-ministro-da-defesa-forcas-armadas-nao-se-sentem-devidamente-prestigiadas.html	|
|	Junho 2022	|	Raiz	|	Dom Phillips	|	12/06/2022	|	https://www.brasildefato.com.br/2022/06/12/desaparecimento-de-dom-philips-e-bruno-pereira-completa-uma-semana-sem-respostas	|
|	Junho 2022	|	Raiz	|	DanielaLima	|	22/06/2022	|	https://www.cnnbrasil.com.br/economia/amputar-a-lei-das-estatais-e-um-retrocesso-diz-michel-temer/	|
|	Junho 2022	|	Raiz	|	CiroNoflow	|	05/06/2022	|	https://www.youtube.com/watch?v=x6m1oUQMZSk	|
|	Junho 2022	|	Raiz	|	CasaGrande	|	15/06/2022	|	https://www.uai.com.br/app/noticia/series-e-tv/2022/06/13/noticias-series-e-tv,287505/no-encontro-casagrande-detona-governo-bolsonaro-perverso-e-muito-cruel.shtml	|
|	Junho 2022	|	Raiz	|	Bloomberg	|	12/06/2022	|	https://g1.globo.com/politica/noticia/2022/06/12/bolsonaro-pediu-a-biden-ajuda-para-conseguir-reeleicao-diz-agencia-bloomberg.ghtml	|
|	Junho 2022	|	Raiz	|	Bolsonaronacadeia	|	08/06/2022	|	https://www.cartacapital.com.br/politica/biden-discutira-eleicao-no-brasil-com-bolsonaro-que-insiste-em-fake-news-sobre-as-urnas/	|
|	Junho 2022	|	Crianca_Intercept	|	11 anos_CR_2006.csv	|	20/06/2022	|	https://oglobo.globo.com/brasil/noticia/2022/06/juiza-impede-aborto-de-menina-de-11-anos-que-engravidou-apos-ser-estuprada-em-sc.ghtml	|
|	Junho 2022	|	Crianca_Intercept	|	CriancaNaoEMae_CR_2006.csv	|	20/06/2022	|	https://oglobo.globo.com/brasil/noticia/2022/06/juiza-impede-aborto-de-menina-de-11-anos-que-engravidou-apos-ser-estuprada-em-sc.ghtml	|
|	Junho 2022	|	Crianca_Intercept	|	Juiza_CR_2006.csv	|	20/06/2022	|	https://oglobo.globo.com/brasil/noticia/2022/06/juiza-impede-aborto-de-menina-de-11-anos-que-engravidou-apos-ser-estuprada-em-sc.ghtml	|
|	Junho 2022	|	Crianca_Intercept	|	b_11 anos_CR_2006.csv	|	20/06/2022	|	https://oglobo.globo.com/brasil/noticia/2022/06/juiza-impede-aborto-de-menina-de-11-anos-que-engravidou-apos-ser-estuprada-em-sc.ghtml	|
|	Junho 2022	|	Crianca_Intercept	|	estuprada_CR_2006.csv	|	20/06/2022	|	https://oglobo.globo.com/brasil/noticia/2022/06/juiza-impede-aborto-de-menina-de-11-anos-que-engravidou-apos-ser-estuprada-em-sc.ghtml	|
|	Junho 2022	|	Petrobras	|	Petrobras_CR_1706.csv	|	17/06/2022	|	https://economia.uol.com.br/noticias/redacao/2022/06/17/petrobras-aumenta-preco-de-combustiveis.htm	|
|	Junho 2022	|	Petrobras	|	Petrobras_CR_2006.csv	|	20/06/2022	|	https://economia.uol.com.br/noticias/redacao/2022/06/20/presidente-da-petrobras-pede-demissao-da-companhia.htm	|
|	Junho 2022	|	Monark	|	Monark_2006_CR_2006.csv	|	20/06/2022	|	https://www.politize.com.br/paradoxo-da-tolerancia/	|
|	Junho 2022	|	Monark	|	Monark_CR_0506.csv	|	05/06/2022	|	https://noticias.uol.com.br/politica/ultimas-noticias/2022/06/03/jean-wyllys-e-condenado-a-pagar-indenizacao-para-kim-kataguiri.htm	|
|	Junho 2022	|	Milton Ribeiro	|	Milton Ribeiro_CR_2206.csv	|	22/06/2022	|	https://www.bbc.com/portuguese/brasil-61900067	|
|	Junho 2022	|	Milton Ribeiro	|	Milton Ribeiro_noite_CR_2206.csv	|	22/06/2022	|	https://www.bbc.com/portuguese/brasil-61900067	|
|	Junho 2022	|	Mark Ruffles	|	Mark Ruffles_CR_0906.csv	|	09/06/2022	|	https://noticias.uol.com.br/politica/ultimas-noticias/2022/06/09/bolsonaro-responde-mark-ruffalo-se-compara-capitao-america.htm	|
|	Junho 2022	|	Mark Ruffles	|	Mark Ruffles_CR_1006.csv	|	10/06/2022	|	https://www.uai.com.br/app/noticia/famosos/2022/06/08/interna-famosos,287132/mark-ruffalo-diz-que-e-preciso-escolher-entre-amazonia-ou-bolsonaro.shtml	|
|	Junho 2022	|	Dom e Bruno	|	Dom e Bruno_CR_1206	|	12/06/2022	|	https://br.ign.com/mark-ruffalo/99255/news/bolsonaro-chama-mark-ruffalo-de-ruffles-em-resposta-ao-ator-da-marvel	|
|	Junho 2022	|	Assedio_caixa	|	Caixa_CR_2806	|	28/06/2022	|	https://www.cartacapital.com.br/politica/funcionarias-denunciam-presidente-da-caixa-por-assedio-sexual-diz-site/	|
|	Junho 2022	|	Assedio_caixa	|	Caixa_CR_2906	|	29/06/2022	|	https://economia.uol.com.br/noticias/redacao/2022/06/28/funcionarias-denunciam-presidente-caixa-assedio-sexual.htm	|
|	Junho 2022	|	Assedio_caixa	|	Pedro Guimaraes_CR_2906	|	29/06/2022	|	https://www.cnnbrasil.com.br/economia/ministerio-publico-investiga-presidente-da-caixa-por-assedio-sexual/	|
|	Junho 2022	|	AbortoNão	|	AbortoNAO_2306	|	23/06/2022	|	https://g1.globo.com/sc/santa-catarina/noticia/2022/06/23/menina-de-11-anos-que-foi-estuprada-em-sc-consegue-fazer-aborto-diz-mpf.ghtml	|
|	Junho 2022	|	AbortoNão	|	AbortoNAO_2606	|	26/06/2022	|	https://g1.globo.com/sc/santa-catarina/noticia/2022/06/23/menina-de-11-anos-que-foi-estuprada-em-sc-consegue-fazer-aborto-diz-mpf.ghtml	|
|	Junho 2022	|	Outros	|	Bradesco_CR_0506	|	05/06/2022	|	https://www.metropoles.com/blog-do-noblat/aliado-de-lula-critica-presidente-do-bradesco-foi-uma-fala-golpista	|
|	Junho 2022	|	Outros	|	#CiroNoFlow_CR_0506	|	05/06/2022	|	https://www.youtube.com/watch?v=x6m1oUQMZSk	|
|	Junho 2022	|	Outros	|	Daniel_Silveira	|	04/06/2022	|	https://www.cnnbrasil.com.br/politica/moraes-bloqueia-conta-de-esposa-de-daniel-silveira-diz-deputado/	|
|	Junho 2022	|	Outros	|	Tiago_leifert	|	04/06/2022	|	https://www.uol.com.br/esporte/ultimas-noticias/2022/06/03/tiago-leifert-sobre-ter-que-votar-entre-lula-ou-bolsonaro-pode-atirar.htm	|
|	Julho 2022	|	Raiz	|	Alexandre Morais.csv	|	15/07/2022	|	https://oglobo.globo.com/politica/noticia/2022/07/alexandre-de-moraes-da-dois-dias-para-bolsonaro-se-manifestar-sobre-acusacoes-de-incitacao-a-violencia.ghtml	|
|	Julho 2022	|	Raiz	|	AugustoAras.csv	|	24/07/2022	|	https://noticias.uol.com.br/colunas/carolina-brigido/2022/07/26/chance-de-aras-ser-investigado-pelo-stf-e-praticamente-nula.htm	|
|	Julho 2022	|	Raiz	|	BTG Pesquisa.csv	|	24/07/2022	|	https://veja.abril.com.br/coluna/radar/lula-amplia-vantagem-sobre-bolsonaro-na-disputa-ao-planalto-diz-pesquisa	|
|	Julho 2022	|	Raiz	|	Capitolio.csv	|	22/07/2022	|	https://g1.globo.com/mundo/noticia/2022/07/22/trump-deve-ser-considerado-responsavel-por-ataque-ao-capitolio-diz-comite-do-congresso.ghtml	|
|	Julho 2022	|	Raiz	|	Daniela Lima.csv	|	13/07/2022	|	https://www.cnnbrasil.com.br/politica/lula-divide-psd-e-avanca-sobre-palanques-de-ciro-gomes/	|
|	Julho 2022	|	Raiz	|	Datafolha_2807.csv	|	28/07/2022	|	https://www.cnnbrasil.com.br/politica/pesquisa-datafolha-para-presidente-lula-47-bolsonaro-29-ciro-8/	|
|	Julho 2022	|	Raiz	|	Datafolha_governo.csv	|	01/07/2022	|	https://www.metropoles.com/brasil/eleicoes-2022/datafolha-lula-tem-43-e-bolsonaro-30-das-intencoes-de-voto-em-sp	|
|	Julho 2022	|	Raiz	|	Golpista.csv	|	22/07/2022	|	https://valor.globo.com/politica/noticia/2022/07/22/em-resposta-a-temer-dilma-chama-ex-vice-de-golpista-e-traidor.ghtml	|
|	Julho 2022	|	Raiz	|	Monark.csv	|	04/07/2022	|	https://www.otempo.com.br/entretenimento/monark-defende-humorista-leo-lins-e-e-novamente-atacado-na-internet-1.2694174	|
|	Julho 2022	|	Raiz	|	Pedro Guimaraes.csv	|	01/07/2022	|	https://www.cnnbrasil.com.br/economia/aliado-de-pedro-guimaraes-vice-presidente-da-caixa-renuncia-apos-denuncias-de-assedio/	|
|	Julho 2022	|	Raiz	|	Petista_foz.csv	|	11/07/2022	|	https://oglobo.globo.com/politica/eleicoes-2022/noticia/2022/07/tudo-o-que-se-sabe-sobre-o-assassinato-do-guarda-municipal-petista-morto-em-foz-do-iguacu.ghtml	|
|	Julho 2022	|	Raiz	|	SimoneTebet.csv	|	24/07/2022	|	https://www.uol.com.br/universa/noticias/redacao/2022/07/28/simone-tebet-direitos-reprodutivos.htm	|
|	Julho 2022	|	Raiz	|	Zambelli.csv	|	04/07/2022	|	https://oglobo.globo.com/blogs/sonar-a-escuta-das-redes/post/2022/07/carla-zambelli-se-exalta-em-podcast-apos-ser-questionada-sobre-orcamento-secreto.ghtml	|
|	Agosto 2022	|	Raiz	|	Alexandre_moraes_1708.csv	|	17/08/2022	|	https://www.tse.jus.br/comunicacao/radio/2022/agosto/ministro-alexandre-de-moraes-toma-posse-no-cargo-de-presidente-do-tse	|
|	Agosto 2022	|	Raiz	|	Aras_2408.csv	|	24/08/2022	|	https://www.correiobraziliense.com.br/politica/2022/08/5031683-empresarios-bolsonaristas-trocavam-mensagens-com-augusto-aras.html	|
|	Agosto 2022	|	Raiz	|	Ato_usp.csv	|	12/08/2022	|	https://noticias.uol.com.br/politica/ultimas-noticias/2022/08/11/carta-pela-democracia-leitura-sp.htm	|
|	Agosto 2022	|	Raiz	|	CiroNoRodaViva_1508.csv	|	15/08/2022	|	https://cultura.uol.com.br/noticias/51400_saiba-quem-e-ciro-gomes-candidato-a-presidencia-da-republica.html	|
|	Agosto 2022	|	Raiz	|	Ciro_JN_2308.csv	|	23/08/2022	|	https://g1.globo.com/jornal-nacional/noticia/2022/08/23/ciro-gomes-pdt-e-entrevistado-no-jornal-nacional.ghtml	|
|	Agosto 2022	|	Raiz	|	DebateNaBand_0708.csv	|	07/08/2022	|	https://www.metropoles.com/brasil/eleicoes-2022/debate-em-sp-e-marcado-por-troca-de-farpas-entre-haddad-e-tarcisio	|
|	Agosto 2022	|	Raiz	|	DebateNaBandrj_0708.csv	|	07/08/2022	|	https://www.poder360.com.br/partidos-politicos/candidatos-ao-governo-do-rj-fazem-debate-focado-em-temas-locais/	|
|	Agosto 2022	|	Raiz	|	DebateNaBandsp_0708.csv	|	07/08/2022	|	https://www.metropoles.com/brasil/eleicoes-2022/debate-em-sp-e-marcado-por-troca-de-farpas-entre-haddad-e-tarcisio	|
|	Agosto 2022	|	Raiz	|	Policia_federal_2308.csv	|	23/08/2022	|	https://cultura.uol.com.br/noticias/51788_saiba-quem-sao-os-empresarios-bolsonaristas-investigados-pela-policia-federal.html	|
|	Agosto 2022	|	Raiz	|	Vera_3008.csv	|	30/08/2022	|	https://www.terra.com.br/nos/quem-e-vera-magalhaes-jornalista-atacada-por-bolsonaro,ee372d6cd313645f5b4ce6f0605dd706sb1qich1.html	|
|	Setembro 2022	|	Raiz	|	Casagrande_3009.csv	|	30/09/2022	|	https://veja.abril.com.br/coluna/veja-gente/a-irritacao-de-casagrande-com-o-voto-de-neymar-em-bolsonaro	|
|	Setembro 2022	|	Raiz	|	Ciro_2209.csv	|	22/09/2022	|	https://www.em.com.br/app/noticia/politica/2022/09/22/interna_politica,1396836/ciro-sobre-lula-poder-corruptor-dele-nao-tem-limite-nao-o-conheco-mais.shtml	|
|	Setembro 2022	|	Raiz	|	CNN_1209.csv	|	12/09/2022	|	https://www.cnnbrasil.com.br/politica/a-cnn-lula-defende-indicacoes-de-aliados-investimentos-credito-e-recusa-magica-na-economia/	|
|	Setembro 2022	|	Raiz	|	Datafolha_0109.csv	|	01/09/2022	|	https://g1.globo.com/politica/eleicoes/2022/pesquisa-eleitoral/noticia/2022/09/01/datafolha-lula-oscila-de-47percent-para-45percent-bolsonaro-mantem-32percent-ciro-vai-a-9percent-e-tebet-sobe-para-5percent.ghtml	|
|	Setembro 2022	|	Raiz	|	Datafolha_0909.csv	|	09/09/2022	|	https://www.cnnbrasil.com.br/politica/pesquisa-datafolha-para-presidente-lula-tem-45-bolsonaro-34/	|
|	Setembro 2022	|	Raiz	|	Datafolha_2209.csv	|	22/09/2022	|	https://oglobo.globo.com/blogs/pulso/post/2022/09/lula-tem-50percent-dos-votos-validos-e-vitoria-no-primeiro-turno-continua-incerta-mostra-datafolha.ghtml	|
|	Setembro 2022	|	Raiz	|	DebateNaCultura_1309.csv	|	13/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/14/deputado-bolsonarista-douglas-garcia-ofende-jornalista-vera-magalhaes-durante-debate-de-candidatos-ao-governo-de-sp-na-tv-cultura.ghtml	|
|	Setembro 2022	|	Raiz	|	DebateNaGlobo_2909.csv	|	29/09/2022	|	https://www.poder360.com.br/eleicoes/leia-a-transcricao-do-debate-presidencial-da-globo/	|
|	Setembro 2022	|	Raiz	|	DebateNoSBT_2409.csv	|	24/09/2022	|	https://www.poder360.com.br/eleicoes/ausente-lula-vira-alvo-em-debate-presidencial-no-sbt/	|
|	Setembro 2022	|	Raiz	|	IPEC_1209.csv	|	12/09/2022	|	https://www.cnnbrasil.com.br/politica/pesquisa-ipec-para-presidente-lula-tem-46-bolsonaro-31/	|
|	Setembro 2022	|	Raiz	|	IPEC_1909.csv	|	19/09/2022	|	https://valor.globo.com/politica/eleicoes-2022/noticia/2022/09/19/ipec-lula-lidera-disputa-presidencial-com-47percent-contra-31percentde-bolsonaro.ghtml	|
|	Setembro 2022	|	Raiz	|	IPEC_2609.csv	|	26/09/2022	|	https://g1.globo.com/politica/eleicoes/2022/pesquisa-eleitoral/noticia/2022/09/26/ipec-lula-48percent-bolsonaro-31percent.ghtml	|
|	Setembro 2022	|	Raiz	|	Kirchner_0109.csv	|	01/09/2022	|	https://www.correiobraziliense.com.br/mundo/2022/09/5033918-brasileiro-tenta-assassinar-cristina-kirchner-vice-presidente-da-argentina.html	|
|	Setembro 2022	|	Raiz	|	ParanaPesquisas_1909.csv	|	19/09/2022	|	https://www1.folha.uol.com.br/poder/2022/09/parana-pesquisas-recebeu-r-27-milhoes-de-partido-de-bolsonaro-na-pre-campanha.shtml	|
|	Setembro 2022	|	Raiz	|	Pesquisa_BTG_1909.csv	|	19/09/2022	|	https://dinheirorural.com.br/pesquisa-btg-fsb-mostra-alta-de-lula-para-44-bolsonaro-tem-35-e-ciro-7/	|
|	Setembro 2022	|	Raiz	|	Quaest_2109.csv	|	21/09/2022	|	https://www.cnnbrasil.com.br/politica/bolsonaro-parece-ter-chegado-no-teto-diz-ceo-da-quaest/	|
|	Setembro 2022	|	Raiz	|	Rainha_0809.csv	|	08/09/2022	|	https://www.bbc.com/portuguese/internacional-62842329	|
|	Setembro 2022	|	Raiz	|	Vera_1409.csv	|	14/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/14/jornalista-vera-magalhaes-diz-que-deputado-douglas-garcia-agiu-deliberada-e-premeditadamente.ghtml	|
|	Setembro 2022	|	GovernoSP_2109	|	GovernoSP_2109_CR_2109.csv	|	21/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/22/pesquisa-datafolha-em-sao-paulo-haddad-tem-34percent-tarcisio-23percent-rodrigo-19percent-e-os-dois-estao-empatados-tecnicamente.ghtml	|
|	Setembro 2022	|	GovernoSP_2109/Haddad	|	GovernoSP_2109_CR_2109.csv	|	21/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/22/pesquisa-datafolha-em-sao-paulo-haddad-tem-34percent-tarcisio-23percent-rodrigo-19percent-e-os-dois-estao-empatados-tecnicamente.ghtml	|
|	Setembro 2022	|	GovernoSP_2109/Rodrigo	|	GovernoSP_2109_CR_2109.csv	|	21/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/22/pesquisa-datafolha-em-sao-paulo-haddad-tem-34percent-tarcisio-23percent-rodrigo-19percent-e-os-dois-estao-empatados-tecnicamente.ghtml	|
|	Setembro 2022	|	GovernoSP_2109/Garcia	|	GovernoSP_2109_CR_2109.csv	|	21/09/2022	|	https://g1.globo.com/sp/sao-paulo/eleicoes/2022/noticia/2022/09/22/pesquisa-datafolha-em-sao-paulo-haddad-tem-34percent-tarcisio-23percent-rodrigo-19percent-e-os-dois-estao-empatados-tecnicamente.ghtml	|
|	Outubro 2022	|	Democracia_0110\0110	|	Democracia_0110_CR_0110.csv	|	01/10/2022	|	https://www.tse.jus.br/comunicacao/noticias/2022/Outubro/na-vespera-do-1o-turno-presidente-do-tse-reafirma-seguranca-transparencia-e-confiabilidade-das-urnas	|
|	Outubro 2022	|	Democracia_0110\0210	|	Democracia_0110_CR_0110.csv	|	02/10/2022	|	https://www.tse.jus.br/comunicacao/noticias/2022/Outubro/eleitores-comecam-a-votar-nas-mais-de-472-mil-secoes-eleitorais-espalhadas-pelo-brasil	|
|	Outubro 2022	|	Democracia_0110\0310	|	Democracia_0110_CR_0110.csv	|	03/10/2022	|	https://www.correiobraziliense.com.br/opiniao/2022/10/5041501-artigo-as-urnas-eletronicas-sao-confiaveis-e-mostram-um-pais-conservador.html	|
|	Outubro 2022	|	RobertoJefferson_2310\1100_1500	|	RobertoJefferson_2310_CR_2310.csv	|	23/10/2022	|	https://agenciabrasil.ebc.com.br/geral/noticia/2022-10/roberto-jefferson-lancou-granada-contra-policiais-federais	|
|	Outubro 2022	|	RobertoJefferson_2310\1500_1800	|	RobertoJefferson_2310_CR_2310.csv	|	23/10/2022	|	https://www.conjur.com.br/2022-out-23/roberto-jefferson-preso-determinacao-alexandre/	|
|	Outubro 2022	|	Democracia_3010\2910	|	Democracia_3010_CR_3010.csv	|	29/10/2022	|	https://oglobo.globo.com/politica/eleicoes-2022/noticia/2022/10/bolsonaro-diz-que-respeitara-resultado-das-urnas-quem-tiver-mais-votos-leva-e-a-democracia.ghtml	|




