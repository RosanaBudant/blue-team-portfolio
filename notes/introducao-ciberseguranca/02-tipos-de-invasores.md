# Tipos de Invasores e Origem das Ameaças

## Classificação por intenção (hat colors)

- **White hat**: invade sistemas com autorização prévia, pra identificar
  falhas e reportar ao dono. É a base ética do pentest e do trabalho de
  Blue/Red Team.
- **Gray hat**: encontra vulnerabilidades sem autorização; pode ou não
  reportar, dependendo do que for mais conveniente pra ele — às vezes
  publica a falha antes de avisar o responsável, o que pode dar tempo pra
  outros atacantes explorarem.
- **Black hat**: explora vulnerabilidades para ganho pessoal, financeiro
  ou político, sem autorização e sem intenção de ajudar.

## Por nível de sofisticação

- **Script kiddies**: pouca experiência técnica, usam ferramentas prontas
  ou tutoriais encontrados online. Menos sofisticados, mas ainda podem
  causar dano real.
- **Hackers organizados**: grupos com alto nível de coordenação —
  hacktivistas (motivação política/ideológica), cibercriminosos
  profissionais (crime como serviço), e agentes patrocinados por Estados
  (ataques direcionados, bem financiados, geralmente ligados a espionagem
  ou sabotagem).

## Ameaças internas vs. externas

- **Internas**: funcionários, terceirizados ou parceiros com acesso
  legítimo, que — de forma acidental ou intencional — manipulam dados de
  forma incorreta, introduzem malware (ex: pendrive infectado) ou
  comprometem sistemas internos. É uma superfície de ataque
  frequentemente subestimada, já que o agente já está "dentro" do
  perímetro de rede.
- **Externas**: atacantes fora da organização, explorando vulnerabilidades
  de rede ou usando engenharia social para conseguir acesso.

## Guerra cibernética

Ataques patrocinados por Estados vão além do roubo de dados — podem ter
como alvo infraestrutura crítica (energia, água, indústria). O caso mais
citado é o **Stuxnet**, malware voltado a sabotar equipamentos industriais
(centrífugas de enriquecimento de urânio no Irã), demonstrando que malware
pode causar dano físico, não só digital.

## Relevância para Blue Team

Saber classificar "quem" está por trás de um ataque ajuda a estimar
sofisticação e motivação — um script kiddie tende a usar ferramentas
conhecidas e assinaturas fáceis de detectar; um agente patrocinado por
Estado tende a usar técnicas customizadas e evasão mais elaborada. Isso
influencia diretamente a priorização de um alerta.
