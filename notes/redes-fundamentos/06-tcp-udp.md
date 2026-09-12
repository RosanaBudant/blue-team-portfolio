# TCP e UDP — Camada de Transporte

## UDP (User Datagram Protocol)

- Não orientado à conexão, sem recuperação de erros, checksum opcional.
- Usado quando entrega rápida importa mais que entrega garantida (voz/vídeo
  em tempo real, DNS, DHCP).
- Cabeçalho simples: porta origem, porta destino, tamanho, checksum.
- Portas variam de **0 a 65535**; 0–1023 são reservadas para serviços
  padrão (HTTP, SMTP, DNS...).

## TCP (Transmission Control Protocol)

- Orientado à conexão, entrega confiável fim-a-fim: recupera dados
  perdidos/duplicados, reordena dados fora de ordem.
- Unidade de dados: **segmento**. Comunicação full-duplex.
- Mecanismos principais:
  - **Números de sequência**: cada byte do stream é numerado.
  - **Retransmissão**: se não chega ACK a tempo, reenvia.
  - **Controle de fluxo**: janela deslizante — o emissor não manda mais
    dados do que o receptor consegue processar.
  - **Controle de erros**: checksum por segmento; segmento danificado é
    descartado e retransmitido.
  - **Controle de congestionamento**: ajusta a janela de transmissão
    conforme a rede confirma (ACK) os dados.

### Three-way handshake (abertura de conexão)

```
Host 1 → SYN        → Host 2
Host 1 ← SYN+ACK     ← Host 2
Host 1 → ACK         → Host 2
```

### Encerramento de conexão

```
Host 1 → FIN     → Host 2
Host 1 ← ACK     ← Host 2
Host 1 ← FIN+ACK ← Host 2
Host 1 → ACK     → Host 2
```

Como o TCP é full-duplex, cada lado finaliza sua "metade" de forma
independente (**Half Close**) — um lado pode ainda enviar dados depois de
receber um FIN do outro.

### Estados relevantes (útil pra ler netstat/pcap)

`LISTEN → SYN_SENT/SYN_RCVD → ESTABLISHED → FIN_WAIT → CLOSE_WAIT →
TIME_WAIT → CLOSED`

## Ângulo de segurança

- **SYN Flood**: ataque de negação de serviço que explora o handshake —
  o atacante manda muitos SYN sem completar o ACK final, esgotando a
  tabela de conexões meio-abertas do servidor. Reconhecível em captura por
  um volume alto de SYN sem SYN-ACK/ACK correspondente vindos de múltiplas
  origens (spoofing) ou de poucas origens em alta frequência.
- Portas bem conhecidas (0–1023) sendo acessadas de forma incomum, ou
  conexões TCP presas em `SYN_SENT`/`SYN_RCVD` por muito tempo, são sinais
  clássicos de reconhecimento de rede (scan) ou tentativa de exploração.
- Tráfego UDP sem padrão de request-response esperado (ex: muitos pacotes
  saindo sem resposta) pode indicar varredura de portas ou exfiltração via
  UDP.
