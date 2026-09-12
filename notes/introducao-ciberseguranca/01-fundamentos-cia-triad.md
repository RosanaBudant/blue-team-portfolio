# Fundamentos: CIA Triad e o Cubo de McCumber

## Por que começar por aqui

Antes de falar de ataques específicos, toda análise de segurança parte de
um objetivo: o que exatamente está sendo protegido? O Cubo de McCumber
(John McCumber, 1991) organiza isso em três dimensões que se cruzam.

## Dimensão 1 — Princípios (CIA Triad)

- **Confidencialidade**: impedir que dados sensíveis sejam acessados por
  quem não tem autorização. Ferramentas: criptografia, autenticação forte,
  autenticação de dois fatores.
- **Integridade**: garantir que dados/processos não sejam alterados de
  forma indevida (intencional ou acidental). Ferramentas: hash, checksum.
- **Disponibilidade**: garantir que usuários autorizados consigam acessar
  sistemas e dados quando precisam. Ameaçada diretamente por ataques de
  negação de serviço (DoS/DDoS).

## Dimensão 2 — Estados do dado

- **Em processamento** (sendo usado ativamente por uma aplicação)
- **Em armazenamento / repouso** (em disco, backup, etc.)
- **Em trânsito** (trafegando na rede)

## Dimensão 3 — Medidas de proteção

- Tecnologia, políticas/práticas, e educação/treinamento das pessoas.

## Como isso se conecta ao resto do portfólio

Cada projeto aqui pode ser mapeado num desses eixos: uma análise de PCAP
foca em dados **em trânsito**; o Wazuh monitora integridade de arquivos
(**integridade**, dados **em repouso**) e detecta anomalias que ameaçam a
**disponibilidade**. Vale usar esse vocabulário nos relatórios de incidente
pra deixar claro qual princípio de segurança foi violado em cada caso.
