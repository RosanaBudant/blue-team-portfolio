# Blue Team Portfolio — Rosana Schreiner Budant

## Quem sou

Estudante de Ciência da Computação (PUCRS, previsão de conclusão em dez/2027), com experiência prática em suporte técnico e redes (TCP/IP, DNS, troubleshooting) e formação complementar em segurança da informação (Hacker do Bem, Cisco Networking Academy, Acadi-TI Prime).

## Objetivo profissional

Migrar da experiência em suporte técnico e redes para uma posição de entrada em **Blue Team / SOC / Segurança da Informação**, aplicando conhecimento de monitoramento, detecção e resposta a incidentes.

## Tecnologias e ferramentas

`TCP/IP` `DNS` `Wireshark` `Linux` `Windows` `Windows Event Logs` `Wazuh (SIEM)` `MITRE ATT&CK` `Python` `SQL` `Git/GitHub`

## Estrutura deste repositório

| Pasta | Conteúdo | Status |
|---|---|---|
| [`notes/`](./notes) | Resumos de estudo: introdução à cibersegurança, fundamentos de redes, sensibilização para a segurança digital e hacking ético | Em andamento |
| [`incident-reports/`](./incident-reports) | Relatórios de incidentes simulados no laboratório, com linha do tempo, evidências e mapeamento MITRE ATT&CK | 1 incidente publicado |
| `blue-team-lab/` | Documentação do laboratório de detecção (arquitetura e configuração) | Em breve |
| `pcap-analysis/` | Análises de captura de tráfego (Wireshark) | Em breve |
| `system-investigations/` | Investigações em sistemas Linux e Windows (processos, logs, eventos) | Em breve |

## Laboratório atual

- **SIEM:** Wazuh 4.9 (instalação all-in-one) em uma VM Ubuntu
- **Endpoint monitorado:** VM Windows 7 com agente Wazuh, enviando Windows Event Logs
- **Rede:** VirtualBox com adaptador host-only entre as VMs, isolado de sistemas reais

Os incidentes de `incident-reports/` são gerados de propósito nesse ambiente, detectados no Wazuh e investigados.

## Como reproduzir

Cada pasta de projeto terá seu próprio README com o passo a passo do ambiente e como reproduzir a investigação.

## Aprendizados

Este portfólio é atualizado conforme avanço nos estudos. Cada projeto reflete o que aprendi na prática, não só em teoria.

---

## Aviso

As notas em `notes/` são resumos pessoais de estudo, elaborados a partir de cursos da Cisco Networking Academy (Introduction to Cybersecurity, Ethical Hacker e Sensibilização para a Segurança Digital) e da disciplina de Laboratório de Redes (PUCRS). Não reproduzem o material original.

📫 [LinkedIn](https://linkedin.com/in/rosana-budant) · [GitHub](https://github.com/RosanaBudant)
