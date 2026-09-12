# Fundamentos de Redes

Notas de estudo produzidas a partir da disciplina de Laboratório de Redes
(PUCRS) e material complementar (Cisco Networking Academy / Womakers),
organizadas por tópico e com foco no que é mais relevante para análise de
tráfego e Blue Team.

## Índice

1. [Modelos OSI e TCP/IP](./01-modelos-osi-tcpip.md)
2. [Protocolos de Aplicação — Fundamentos](./02-protocolos-aplicacao.md)
3. [DHCP](./03-dhcp.md)
4. [DNS](./04-dns.md)
5. [NAT](./05-nat.md)
6. [TCP e UDP](./06-tcp-udp.md)
7. [IPv4 — Protocolo e Endereçamento](./07-ipv4-enderecamento.md)
8. [HTTP e HTTPS](./08-http.md)

Cada arquivo termina com uma seção **"Ângulo de segurança"**, conectando o
conceito de redes ao que é observável/detectável numa análise de Blue Team
(Wireshark, IDS, SIEM).

## Próximos passos

Os tópicos de DNS, DHCP e TCP/UDP aqui servem de base teórica direta para
o projeto prático em [`pcap-analysis/`](../../pcap-analysis).
