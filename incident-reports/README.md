# Incident Reports

Relatórios de incidentes **simulados** no laboratório de Blue Team ([`blue-team-lab/`](../blue-team-lab)): Wazuh como SIEM, com endpoints Windows e Linux enviando logs. Cada incidente é gerado de propósito, detectado no SIEM, investigado e documentado.

Os relatórios seguem a mesma estrutura:

1. Resumo (host, conta, origem, severidade)
2. Linha do tempo
3. Evidências (campos do evento e prints)
4. Análise
5. Mapeamento MITRE ATT&CK
6. Impacto
7. Resposta (o que seria feito num cenário real)
8. Lições e próximos passos

## Índice

| # | Incidente | Host | Regra Wazuh | MITRE (sugerido pelo Wazuh) | Severidade |
|---|---|---|---|---|---|
| 01 | [Falhas de logon interativo na Windows 7](./01-logon-failure-windows7) | `windows7-agent` | 60122 | T1531 (Account Access Removal) | Nível 5 |

## Observação

Os incidentes são simulações em ambiente isolado, sem sistemas ou dados reais. Quando o mapeamento MITRE padrão do Wazuh difere da técnica que melhor descreve o comportamento observado, o relatório registra as duas e explica a diferença.
