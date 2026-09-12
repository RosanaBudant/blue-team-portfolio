# Modelos OSI e TCP/IP

## Por que isso importa pra Blue Team

Toda análise de tráfego (Wireshark, IDS, SIEM) parte de "em que camada esse
problema está acontecendo?". Saber separar camada de rede (IP), transporte
(TCP/UDP) e aplicação (HTTP, DNS...) é o que permite ler um alerta e saber
se é um problema de roteamento, de uma sessão TCP anômala, ou de conteúdo
malicioso dentro de uma requisição HTTP.

## Modelo OSI (7 camadas)

Modelo de referência conceitual (ISO), usado mais para linguagem comum entre
profissionais do que como implementação real.

| Camada | Função | Unidade de dados |
|---|---|---|
| 7 - Aplicação | Serviços ao usuário (e-mail, web, arquivos) | Dados |
| 6 - Apresentação | Tradução, criptografia, compressão | Dados |
| 5 - Sessão | Controle de diálogo entre sistemas | Dados |
| 4 - Transporte | Entrega processo-a-processo (portas) | Segmento |
| 3 - Rede | Entrega origem-destino (endereçamento lógico, roteamento) | Pacote |
| 2 - Enlace | Entrega nó-a-nó, endereçamento físico (MAC) | Quadro |
| 1 - Física | Transmissão de bits no meio físico | Bit |

A camada de Enlace, no contexto de redes locais (padrão IEEE 802), é
subdividida em duas subcamadas:
- **LLC** (Logical Link Control) — independente da tecnologia de rede local
- **MAC** (Medium Access Control) — controla o acesso ao meio (quem transmite quando)

## Modelo TCP/IP (o que realmente roda na Internet)

Mais enxuto, 4 camadas, é o que efetivamente foi implementado:

| Camada TCP/IP | Equivalente OSI | Protocolos típicos |
|---|---|---|
| Aplicação | 5, 6, 7 | HTTP, DNS, DHCP, SMTP |
| Transporte | 4 | TCP, UDP |
| Rede | 3 | IP, ICMP, ARP |
| Interface de Rede | 1, 2 | Ethernet, Wi-Fi (802.11) |

## Ligação com os outros tópicos deste repositório

- `03-dhcp.md`, `04-dns.md`, `08-http.md` → camada de Aplicação
- `06-tcp-udp.md` → camada de Transporte
- `07-ipv4-enderecamento.md` → camada de Rede
- `05-nat.md` → opera na camada de Rede, traduzindo endereços IP
