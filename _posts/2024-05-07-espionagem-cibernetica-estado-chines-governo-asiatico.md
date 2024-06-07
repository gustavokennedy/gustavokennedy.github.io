![Espionagem cibernética apoiada pelo Estado chinês tem como alvo o governo do sudeste asiático](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiM4DNz5tdSeHXIrC4JzPseSDf7tBvSPRxTJEhfQBaB6UsWf38cZ-w0PU9vPd6nMbj_6RwwEdkL9okCR5gHLaMZpmu4pykUKVxLbMMl_9FGVkeLEIQS-LN0wtozjKVhxOJ2GHSBecros2GEWKkPkMI0y2O7XGIcBzj49565q8B6a6Ii9Lyd_9CHg7PDKNW7/s728-rw-e365/net.png)

## Espionagem cibernética apoiada pelo Estado chinês tem como alvo o governo do sudeste asiático

Uma organização governamental não identificada de alto perfil no Sudeste Asiático emergiu como alvo de uma operação de espionagem cibernética "complexa e de longa duração" patrocinada pelo Estado chinês, codinome Crimson Palace .

“O objetivo geral por trás da campanha era manter o acesso à rede alvo de ciberespionagem em apoio aos interesses do Estado chinês”, disseram os pesquisadores da Sophos Paul Jaramillo, Morgan Demboski, Sean Gallagher e Mark Parsons em um relatório compartilhado com o The Hacker News.

“Isso inclui acessar sistemas críticos de TI, realizar reconhecimento de usuários específicos, coletar informações militares e técnicas confidenciais e implantar vários implantes de malware para comunicações de comando e controle (C2).”

O nome da organização governamental não foi divulgado, mas a empresa disse que o país é conhecido por ter repetidos conflitos com a China por território no Mar da China Meridional , levantando a possibilidade de que possam ser as Filipinas, que têm sido alvo do Estado chinês. grupos patrocinados como o Mustang Panda no passado.

O Crimson Palace compreende três grupos de intrusão , alguns dos quais compartilham as mesmas táticas, embora haja evidências de atividades mais antigas que remontam a março de 2022 -

Cluster Alpha (março de 2023 - agosto de 2023), que exibe algum grau de semelhança com atores rastreados como BackdoorDiplomacy , REF5961 , Worok e TA428
Cluster Bravo (março de 2023), que tem pontos em comum com Unfading Sea Haze , e
Cluster Charlie (março de 2023 - abril de 2024), que se sobrepõe ao Earth Longzhi , um subgrupo dentro do APT41
A Sophos avaliou que esses grupos de atividades sobrepostas provavelmente faziam parte de uma campanha coordenada orquestrada sob a direção de uma única organização.

O ataque é notável pelo uso de malware não documentado como PocoProxy, bem como uma versão atualizada do EAGERBEE , junto com outras famílias de malware conhecidas como NUPAKAGE , PowHeartBeat , RUDEBIRD, DOWNTOWN (PhantomNet) e EtherealGh0st (também conhecido como CCoreDoor).

![Imagem Clusters](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiA_py7aOIEYJEEj5Pk_3lxqQrO9mak9gNpKGql3pK6ggDzH1rLsRulCX1C6-mD-scdFLkVIlShrpwmAbzMl24a3VWE2jGpRkPEb1LcBPcUn5DemYXSKb6NgDTZMtRaqzC96rl62kV1vtFl5TzDbrg8fML1hY080zvLFnIDVLRKg4a6ot7nTkwzce6LpExV/s728-rw-e365/cluster.png)

Outras características da campanha incluem o uso extensivo de carregamento lateral de DLL e táticas incomuns para permanecer fora do radar.

“Os atores da ameaça aproveitaram muitas novas técnicas de evasão, como sobrescrever DLL na memória para desconectar o processo do agente AV Sophos do kernel, abusar do software AV para carregamento lateral e usar várias técnicas para testar os métodos mais eficientes e evasivos de execução de suas cargas. ", disseram os pesquisadores.

Investigações adicionais revelaram que o Cluster Alpha se concentrou no mapeamento de sub-redes de servidores, enumeração de contas de administrador e realização de reconhecimento na infraestrutura do Active Directory, com o Cluster Bravo priorizando o uso de contas válidas para movimentação lateral e eliminando o EtherealGh0st.

A atividade associada ao Cluster Charlie, que ocorreu durante o período mais longo, envolveu o uso do PocoProxy para estabelecer persistência em sistemas comprometidos e a implantação do HUI Loader , um carregador personalizado usado por vários atores do nexo da China, para entregar o Cobalt Strike.

“Os clusters observados reflectem as operações de dois ou mais actores distintos que trabalham em conjunto com objectivos partilhados”, observaram os investigadores. “Os clusters observados refletem o trabalho de um único grupo com uma grande variedade de ferramentas, infraestrutura diversificada e múltiplos operadores”.

A divulgação ocorre no momento em que a empresa de segurança cibernética Yoroi detalha ataques orquestrados pelo ator APT41 (também conhecido como Brass Typhoon, HOODOO e Winnti) visando organizações na Itália com uma variante do malware PlugX (também conhecido como Destroy RAT e Korplug) conhecido como KEYPLUG .

“Escrito em C++ e ativo desde pelo menos junho de 2021, KEYPLUG tem variantes para plataformas Windows e Linux”, disse Yoroi . “Ele suporta vários protocolos de rede para tráfego de comando e controle (C2), incluindo HTTP, TCP, KCP sobre UDP e WSS, tornando-o uma ferramenta potente no arsenal de ataques cibernéticos do APT41.”

Também segue um comunicado do Centro Canadense de Segurança Cibernética alertando sobre o aumento dos ataques de hackers apoiados pelo Estado chinês, destinados a infiltrar-se no governo, em infraestruturas críticas e nos setores de pesquisa e desenvolvimento.

“A atividade de ameaças cibernéticas [da República Popular da China] supera outras ameaças cibernéticas de estados-nação em volume, sofisticação e amplitude de direcionamento”, disse a agência , destacando o uso de roteadores comprometidos para pequenos escritórios e escritórios domésticos (SOHO) e residências- técnicas fora da terra para conduzir atividades de ameaças cibernéticas e evitar a detecção.
