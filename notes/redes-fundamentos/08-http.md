# HTTP e HTTPS

## HTTP (HyperText Transfer Protocol)

- Modelo cliente/servidor de requisição-resposta. Usa **TCP**, porta **80**.
- Evoluiu de HTTP/0.9 (só GET, sem headers) até HTTP/1.1 (headers,
  persistência de conexão, mais métodos) e HTTP/2 (multiplexação,
  compressão de headers, sobre uma única conexão TCP).
- **HTTP/3** roda sobre **QUIC**, que por sua vez roda sobre **UDP** — uma
  mudança relevante pra quem analisa tráfego, já que HTTP deixa de estar
  sempre associado a TCP.

### Métodos principais

`GET` (obter recurso), `POST` (enviar dados), `PUT` (enviar/substituir
recurso), `DELETE` (remover), `HEAD` (só cabeçalhos), `OPTIONS` (métodos
suportados), `PATCH` (atualização parcial), `CONNECT` (túnel, usado para
HTTPS via proxy).

### Códigos de status

| Faixa | Significado |
|---|---|
| 1xx | Informacional |
| 2xx | Sucesso |
| 3xx | Redirecionamento |
| 4xx | Erro do cliente |
| 5xx | Erro do servidor |

## HTTPS (HTTP + TLS/SSL)

- Adiciona uma camada de criptografia (SSL, sucedido por TLS) sobre o HTTP.
  Roda tradicionalmente na porta **443**.
- Garante:
  - **Confidencialidade**: todo o conteúdo da mensagem é criptografado
    (inclusive cabeçalhos).
  - **Integridade**: um MAC (Message Authentication Code) detecta se a
    mensagem foi alterada em trânsito.
  - **Autenticidade do servidor**: via certificado digital emitido por uma
    Autoridade Certificadora (CA), que confirma que a chave pública
    apresentada realmente pertence ao domínio.
- Fluxo simplificado: o servidor envia sua chave pública + certificado; o
  cliente valida o certificado com a CA; as duas partes negociam uma chave
  simétrica para a sessão (assimétrica só no início, por custo de
  processamento).

## Ângulo de segurança

- Sem validação de certificado (ou com o usuário ignorando avisos do
  navegador), é possível um ataque de **man-in-the-middle**, onde um
  atacante se passa pelo servidor legítimo.
- Em análise de tráfego, HTTP em texto claro expõe totalmente
  URLs, headers e corpo da requisição — útil para investigação, mas
  também é exatamente o que um atacante consegue capturar se interceptar
  a rede (daí a importância de identificar tráfego HTTP não migrado para
  HTTPS num ambiente).
- Contra HTTPS, a inspeção de tráfego (Wireshark/IDS tradicional) só
  enxerga metadados (IP, porta, SNI do TLS) — não o conteúdo. Isso é
  relevante para justificar por que soluções de Blue Team modernas (como
  o Wazuh) atuam também no nível do host (logs, EDR) e não só na rede.
