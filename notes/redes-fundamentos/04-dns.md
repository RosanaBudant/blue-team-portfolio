# DNS — Domain Name System

## Função

Mapeia nomes simbólicos (fáceis de lembrar, ex: `www.pucrs.br`) para
endereços IP e vice-versa. Roda sobre a **porta 53**. Definido nas RFCs
1034/1035.

## Hierarquia

Estrutura em árvore, sem repositório central único:
- **Root Name Servers** — topo da hierarquia
- **TLD (Top Level Domain)** — `.com`, `.org`, `.br`...
- **Servidores de Autoridade** — responsáveis por um domínio específico
  (ex: servidor da PUCRS responde por `pucrs.br`)

Um domínio/subdomínio é agrupado em **zonas**, cada uma com administração
independente. A resolução de nomes pode ser **iterativa** (o resolver
pergunta a cada nível) ou **recursiva** (um servidor faz o trabalho de
perguntar aos outros por você).

## Resource Records (RRs) principais

| Tipo | Função |
|---|---|
| A | Endereço IPv4 |
| AAAA | Endereço IPv6 |
| CNAME | Nome canônico (apelido) |
| MX | Servidor de e-mail |
| NS | Servidor de nomes |
| PTR | Resolução reversa (IP → nome) |
| SOA | Autoridade da zona (parâmetros de refresh, retry, expire, TTL) |

## Ferramentas de troubleshooting

- `nslookup` — consulta registros de um domínio (`set type=mx`, `set type=ns` etc.)
- `whois` — consulta dados de registro de um domínio

## Segurança — o ponto mais relevante pra Blue Team

O DNS nasceu pensando em disponibilidade, não em segurança:
- Consultas e respostas trafegam em **texto claro** (sem criptografia nativa).
- Não há autenticação nativa da origem da resposta.

**Ataques clássicos:**
- **Cache Poisoning (envenenamento de cache)**: um atacante injeta uma
  resposta falsa antes da resposta legítima chegar (ex: fazendo
  `www.banco.com.br` resolver pro IP do atacante). Como o servidor guarda
  isso em cache, o efeito se propaga para todos os usuários que consultam
  aquele servidor.
- **DNS Tunneling**: uso do protocolo DNS para exfiltrar dados ou criar
  canal de comando-e-controle (C2), escondendo tráfego dentro de consultas
  DNS aparentemente legítimas — é um padrão clássico de detecção em Blue
  Team (muitas consultas incomuns para o mesmo domínio, nomes de subdomínio
  muito longos/aleatórios).

**Mitigações:**
- **DNSSEC**: garante autenticação de origem e integridade da resposta
  (mas **não** criptografa a consulta — não resolve confidencialidade).
- **DoH (DNS over HTTPS)** e **DoT (DNS over TLS)**: criptografam o canal
  de consulta, impedindo que o provedor de internet (ou um atacante na
  rede) veja quais domínios estão sendo resolvidos.

## Ligação com o projeto de pcap-analysis

Esse é o tópico mais aplicável direto ao projeto de análise de PCAP: dá
pra capturar uma resolução DNS normal, identificar os campos de
query/response, e depois comparar com um cenário simulado de tunneling ou
volume anômalo de consultas.
