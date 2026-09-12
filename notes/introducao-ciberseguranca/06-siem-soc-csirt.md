# Detecção Comportamental, SIEM, SOC e CSIRT

## Segurança baseada em comportamento

Em vez de depender só de assinaturas conhecidas, analisa o fluxo normal de
comunicação numa rede e sinaliza **desvios do padrão** como possíveis
ameaças — essencial contra ataques novos ou desconhecidos (dia zero).

- **Honeypot**: sistema-isca que simula ser um alvo atraente, para captar
  e estudar o comportamento de um atacante em um ambiente controlado,
  sem risco para os sistemas reais.
- **NetFlow**: tecnologia que coleta metadados sobre os fluxos de tráfego
  (quem, quando, como) passando por switches/roteadores/firewalls,
  permitindo estabelecer uma linha de base de comportamento "normal" da
  rede — desvios dessa linha de base geram alerta.

## Teste de Penetração (Pentest)

Avaliação autorizada e estruturada de um sistema em busca de
vulnerabilidades exploráveis. Etapas clássicas:

1. **Planejamento**: reconhecimento (footprinting), coleta de informação
   sobre o alvo.
2. **Varredura**: reconhecimento ativo — port scanning, verificação de
   vulnerabilidades, enumeração de contas/sistemas.
3. **Obter acesso**: exploração efetiva (payloads, engenharia social,
   falhas de configuração, quebra de Wi-Fi etc.).
4. **Manter acesso**: o pen tester tenta permanecer despercebido (usando
   as mesmas técnicas de backdoor/rootkit que um atacante real usaria),
   pra avaliar até onde conseguiria ir.
5. **Análise e relatório**: recomendações concretas de melhoria de
   produto, política e treinamento.

## SIEM e DLP

- **SIEM (Security Information and Event Management)**: coleta e
  correlaciona logs e alertas de segurança de múltiplas fontes na rede,
  em tempo real e histórico, para permitir detecção precoce de incidentes.
  **É exatamente o papel que o Wazuh cumpre neste portfólio.**
- **DLP (Data Loss Prevention)**: monitora e protege dados sensíveis nos
  três estados (em uso, em trânsito, em repouso) para evitar vazamento ou
  exfiltração.

## CSIRT (Computer Security Incident Response Team)

Equipe dedicada a receber, analisar e responder a incidentes de segurança.
Times maduros (como o da Cisco) também atuam de forma proativa: avaliação
de ameaças, planejamento de mitigação, e colaboração com organizações
externas de resposta a incidentes (ex: FIRST, CERT).

### Manual de segurança (Playbook)

Conjunto padronizado de processos de detecção e resposta, cobrindo:
identificação/automação de resposta a ameaças comuns, definição clara do
que é tráfego normal de entrada/saída, estatísticas resumidas e
correlação de eventos entre fontes de dados diferentes — a lógica por
trás de qualquer plataforma de SIEM/SOC, incluindo o Wazuh.

## Gestão de risco (resumo do ciclo)

Definir o risco → classificar gravidade (impacto financeiro/operacional)
→ responder (eliminar, mitigar, transferir ou aceitar) → monitorar
continuamente.

## Relevância direta pro portfólio

Esse é o tópico que dá o "porquê" conceitual do projeto `blue-team-lab/`:
o Wazuh atua como SIEM, e os `incident-reports/` que serão produzidos a
partir dele seguem exatamente essa lógica de playbook — identificação,
linha do tempo, evidências, e recomendação.
