# Dispositivos de Segurança e Detecção

## Firewalls

Controlam/filtram o que entra e sai de um dispositivo ou rede. Tipos:

| Tipo | Filtra por |
|---|---|
| Camada de rede | Endereços IP origem/destino |
| Camada de transporte | Portas e estado da conexão |
| Camada de aplicação | Aplicativo/serviço específico |
| Sensível ao contexto | Usuário, dispositivo, papel, perfil de ameaça |
| Proxy | Conteúdo web (URLs, domínios, tipo de mídia) |
| Proxy reverso | Protege/distribui acesso a servidores web (fica na frente deles) |
| NAT firewall | Oculta endereços privados da rede interna |
| Baseado em host | Roda no próprio sistema operacional, filtra por processo |

## Varredura de portas (Port Scanning)

Processo de sondar um host em busca de portas abertas, usado tanto por
atacantes (reconhecimento) quanto por administradores (auditoria de
segurança). Ferramenta clássica: **Nmap/Zenmap**. Respostas possíveis:

- **Aberta/Aceita**: porta acessível
- **Fechada/Negada**: nada rodando ali
- **Filtrada/Bloqueada**: firewall está impedindo o acesso

## IDS vs. IPS

- **IDS (Intrusion Detection System)**: analisa tráfego contra uma base de
  assinaturas/regras, mas **só detecta e alerta** — não bloqueia nada.
  Geralmente fica fora do caminho direto do tráfego (recebe uma cópia
  espelhada via switch) para não adicionar latência.
- **IPS (Intrusion Prevention System)**: além de detectar, **bloqueia**
  ativamente o tráfego que corresponde a uma assinatura maliciosa. Exemplo
  clássico: Snort (versão comercial: Cisco Sourcefire).
- **Ataque de dia zero**: explora uma vulnerabilidade antes que exista uma
  correção/assinatura conhecida — por definição, é o tipo de ataque mais
  difícil pra um IDS/IPS baseado em assinatura detectar, o que reforça a
  importância de detecção comportamental (ver próximo tópico).

## Proteção contra malware

Soluções corporativas (ex: Cisco AMP) analisam arquivos em massa e
correlacionam com bases de ameaças conhecidas para identificar
comportamentos de ameaças persistentes avançadas (APTs), indo além da
detecção por assinatura simples.

## Boas práticas de segurança organizacional (resumo)

Avaliação de risco → política de segurança → segurança física → backups
testados → patches em dia → controle de acesso → resposta a incidentes
testada → ferramenta de monitoramento/SIEM → dispositivos de rede
atualizados → proteção de endpoint → treinamento de usuários →
criptografia de dados sensíveis.

## Relevância direta pro Wazuh

O Wazuh atua como uma camada de **detecção baseada em host** (HIDS/EDR) que
complementa o que firewall/IDS de rede enxergam: monitoramento de
integridade de arquivos, análise de logs, detecção de rootkits e
configuração de segurança — o que se encaixa diretamente no "Proteção
contra malware" e na parte de detecção do ciclo descrito acima.
