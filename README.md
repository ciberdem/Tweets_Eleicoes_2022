# Tweets_Eleicoes_2022

Ao longo dos últimos vinte anos as disputas eleitorais têm sido impactadas diretamente pelo fenômeno das redes sociais. Os políticos que souberam interagir com os diferentes grupos de eleitores, através das redes, tiveram impactos positivos em suas campanhas.

No entanto, esse ambiente também se tornou fértil para fenômenos negativos como a ultra polarização das discussões políticas, com grupos radicais manipulando como os fatos são absorvidos dentro de suas “bolhas” de influência, impactando diretamente os rumos das campanhas eleitorais. O Brasil não ficou alheio a essa condição. Por exemplo, o ano de 2022 ´e considerado um dos períodos eleitorais mais polarizados da história brasileira.

Entender como esses grupos se formam e se relacionam dentro das redes sociais, quem são seus principais influenciadores e visualizar como o posicionamento eleitoral desses perfis impactaram a maneira como os eventos do ano eleitoral brasileiro de 2022 foram discutidos dentro de suas “bolhas”. As informações coletadas tornaram-se importantes para ajudar no entendimento da dinâmica das redes no processo democrático no Brasil. Dentro deste contexto, a pesquisa "Monitoramento de discussões políticas no Twitter durante as Eleições de 2022 no Brasil: polarização, agrupamento e principais atores" tem como objetivo colaborar com esse entendimento, através da proposta de construção de um pipeline de extração e processamento dos dados do Twitter durante eventos políticos relevantes no Brasil em 2022, sendo esse constituído de um processo estruturado que atua em conjunto com programas desenvolvidos em Python e uma ferramenta de Análise de Redes Sociais. 

Após sua execução, foi possível gerar visualizações dos principais atores, agrupamentos de perfis e os diferentes pontos de discussão dentro desses grupos, evidenciando o movimento da polarização nas redes a partir das discussões sobre a ocorrência e divulgação dos fatos ao longo do tempo. Para apoiar a visualização dos resultados da execução desse processo ´e apresentado um estudo de caso com dados extraídos do Twitter durante os eventos de 8 de janeiro de 2023 em Brasília.













Lista de Arquivos do Pipeline:

1. Tese_Extrai_tweets_v2023 - Módulo de extração dos Tweets - Passo 1 (Notebook Jupyter)

2. IDs_Lista_Distribuicao_Twitter.txt - Arquivo com os IDs das listas de distribuição usadas para conseguir a lista de usuários e executar a categorização (necessita "hidratação" a partir do Twitter)

3. twitter_contas_br_2022_v3_exemplo.txt - Exemplo do arquivo com os usuários extraidos das listas, com a categorização a partir da presença em cada lista e também pela declaração de voto (Pro_Bolsonaro, Pro_Lula e Neutro/Indefinido)
