# Tweets_Eleicoes_2022

Ao longo dos ´ultimos vinte anos as disputas eleitorais tˆem sido impactadas diretamente
pelo fenˆomeno das redes sociais. Os pol´ıticos que souberam interagir com os diferentes
grupos de eleitores, atrav´es das redes, tiveram impactos positivos em suas campanhas.
No entanto, esse ambiente tamb´em se tornou f´ertil para fenˆomenos negativos como a ultra
polariza¸c˜ao das discuss˜oes pol´ıticas, com grupos radicais manipulando como os fatos s˜ao
absorvidos dentro de suas “bolhas” de influˆencia, impactando diretamente os rumos das
campanhas eleitorais. O Brasil n˜ao ficou alheio a essa condi¸c˜ao. Por exemplo, o ano
de 2022 ´e considerado um dos per´ıodos eleitorais mais polarizados da hist´oria brasileira.
Entender como esses grupos se formam e se relacionam dentro das redes sociais, quem s˜ao
seus principais influenciadores e visualizar como o posicionamento eleitoral desses perfis
impactaram a maneira como os eventos do ano eleitoral brasileiro de 2022 foram discutidos
dentro de suas “bolhas”. As informa¸c˜oes coletadas tornaram-se importantes para ajudar
no entendimento da dinˆamica das redes no processo democr´atico no Brasil.Dentro deste
contexto, esta pesquisa tem como objetivo colaborar com esse entendimento, atrav´es da
proposta de constru¸c˜ao de um pipeline de extra¸c˜ao e processamento dos dados do Twitter
durante eventos pol´ıticos relevantes no Brasil em 2022, sendo esse constitu´ıdo de um
processo estruturado que atua em conjunto com programas desenvolvidos em Python e
uma ferramenta de An´alise de Redes Sociais. Ap´os sua execu¸c˜ao, foi poss´ıvel gerar visualiza
¸c˜oes dos principais atores, agrupamentos de perfis e os diferentes pontos de discuss˜ao
dentro desses grupos, evidenciando o movimento da polariza¸c˜ao nas redes a partir das
discuss˜oes sobre a ocorrˆencia e divulga¸c˜ao dos fatos ao longo do tempo. Para apoiar a
visualiza¸c˜ao dos resultados da execu¸c˜ao desse processo ´e apresentado um estudo de caso
com dados extra´ıdos do Twitter durante os eventos de 8 de janeiro de 2023 em Bras´ılia.












Lista de Arquivos do Pipeline:

1. Tese_Extrai_tweets_v2023 - Módulo de extração dos Tweets - Passo 1 (Notebook Jupyter)

2. IDs_Lista_Distribuicao_Twitter.txt - Arquivo com os IDs das listas de distribuição usadas para conseguir a lista de usuários e executar a categorização (necessita "hidratação" a partir do Twitter)

3. twitter_contas_br_2022_v3_exemplo.txt - Exemplo do arquivo com os usuários extraidos das listas, com a categorização a partir da presença em cada lista e também pela declaração de voto (Pro_Bolsonaro, Pro_Lula e Neutro/Indefinido)
