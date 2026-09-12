# Protocolos de Aplicação — Fundamentos

## Arquiteturas de aplicação

- **Cliente-Servidor**: servidor sempre disponível, com IP fixo, atende
  requisições de clientes. Clientes não se comunicam diretamente entre si.
  Exemplos: Web, e-mail, SSH.
- **P2P (Peer-to-Peer)**: cada nó (peer) atua como cliente e servidor ao
  mesmo tempo. Altamente escalável, mas mais difícil de monitorar e
  controlar — relevante pra Blue Team, já que tráfego P2P foge do padrão
  "servidor central" e pode ser usado tanto por apps legítimos (torrents,
  blockchain) quanto como canal de exfiltração/C2 em malware.
- **Híbrida (P2P-C/S)**: servidor central intermedia, mas parte da
  comunicação acontece direto entre clientes (ex: Google Meet).

## Comunicação entre processos: Sockets

- Dois processos em hosts diferentes se comunicam trocando mensagens via
  **socket** — a interface entre a camada de aplicação e a de transporte.
- Para identificar unicamente um processo numa comunicação de rede, é
  preciso o par **endereço IP + porta** dos dois lados.

### Socket UDP
- Canal não confiável: não garante entrega nem ordem dos datagramas.
- Não mantém estado de conexão (não existe "conectado"/"desconectado").

### Socket TCP
- Canal confiável: garante entrega, ordem e ausência de duplicação.
- Mantém estado de conexão (o TCP sabe se está "escutando", "estabelecido" etc.).
- Implementa controle de fluxo e de congestionamento (ver `06-tcp-udp.md`).

## Relevância para monitoramento

Ao analisar uma captura de tráfego (Wireshark), a primeira pergunta é
"que tipo de socket é esse fluxo?" — UDP tende a ser sessões curtas e sem
handshake (DNS, DHCP), TCP tem sempre handshake (SYN/SYN-ACK/ACK) visível
antes dos dados. Reconhecer isso rapidamente já elimina hipóteses na hora
de investigar um alerta.
