# Métodos de Ataque

## Engenharia social

Manipula a pessoa (não a tecnologia) para obter acesso ou informação.
Explora confiança, urgência, autoridade ou vaidade.

- **Pretexting**: o atacante inventa uma história/identidade falsa para
  justificar o pedido de dados sensíveis (ex: se passar por suporte
  técnico pedindo confirmação de senha).
- **Tailgating**: seguir uma pessoa autorizada de perto para entrar num
  local físico restrito sem precisar de credencial própria.
- **Quid pro quo**: oferecer algo em troca da informação (ex: "ajuda
  técnica" em troca da senha).

## Negação de Serviço (DoS e DDoS)

- **DoS**: sobrecarrega um sistema/recurso até torná-lo indisponível para
  usuários legítimos.
- **DDoS**: a mesma ideia, mas distribuída — usando uma **botnet** (rede
  de máquinas infectadas, "zumbis", controladas remotamente via um
  servidor de comando e controle). Isso torna o ataque mais difícil de
  bloquear, já que o tráfego malicioso vem de milhares de origens
  diferentes e se mistura com tráfego legítimo.

## Ataques On-Path (Man-in-the-Middle)

O atacante se posiciona entre duas partes de uma comunicação (ex: cliente
e servidor web) para interceptar, ler ou alterar os dados sem que nenhuma
das partes perceba.

- **Man-in-the-Mobile (MitMo)**: variação voltada a dispositivos móveis,
  usada por exemplo para interceptar SMS de autenticação em dois fatores.

## SEO Poisoning

Manipular resultados de mecanismos de busca para posicionar sites
maliciosos em posições altas de pesquisas populares, atraindo vítimas para
páginas com malware ou golpes de engenharia social.

## Ataques de senha

| Técnica | Como funciona |
|---|---|
| Força bruta | Testa todas as combinações possíveis até acertar |
| Dicionário | Testa palavras comuns/conhecidas como senha |
| Password spraying | Testa poucas senhas muito comuns contra muitas contas diferentes (evita bloqueio por tentativas excessivas numa única conta) |
| Rainbow table | Compara o hash da senha-alvo com uma tabela pré-computada de hashes conhecidos, evitando recalcular cada tentativa |
| Interceptação de tráfego (sniffing) | Captura senhas transmitidas sem criptografia diretamente da rede |

## Relevância para Blue Team

- DDoS e password spraying deixam padrões de tráfego reconhecíveis
  (volume anômalo, tentativas de login distribuídas) — bons candidatos
  pra regras de detecção no Wazuh/SIEM.
- Interceptação de tráfego reforça por que capturar e analisar PCAP (ver
  `pcap-analysis/`) é relevante: protocolos sem criptografia expõem
  credenciais literalmente em texto claro pra quem estiver capturando o
  tráfego.
