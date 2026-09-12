# Exploração de Redes Cabeadas e Sem Fio

## Vulnerabilidades baseadas em rede (visão geral)

Vários serviços clássicos de rede carregam riscos conhecidos quando mal
configurados ou desatualizados:

- **SMB**: permite enumeração de usuários/grupos/compartilhamentos quando
  mal configurado (ver `01-reconhecimento-e-varredura.md`).
- **DNS**: suscetível a envenenamento de cache (ver `notes/redes-fundamentos/04-dns.md`).
- **SNMP/SMTP/FTP legados**: costumam expor informação em texto claro ou
  aceitar autenticação anônima/fraca quando não configurados com cuidado
  (ex: FTP sem TLS, comunidade SNMP padrão "public").

## Ataques de credenciais em ambiente Windows/AD

- **Pass-the-hash**: como o Windows armazena senhas como hash (não como
  texto puro), um atacante que já obteve o hash de um sistema comprometido
  pode reutilizá-lo para se autenticar em outro sistema, sem nunca
  precisar "quebrar" a senha original.
- **Kerberos (Golden/Silver Ticket, Kerberoasting)**: ataques que abusam
  do protocolo de autenticação do Active Directory para forjar ou extrair
  tickets de acesso, muitas vezes explorando hashes de contas de serviço
  com criptografia fraca ou senhas previsíveis.

Esses ataques reforçam por que **rotação de credenciais**, **política de
senha forte para contas de serviço** e **segmentação de rede** são
controles centrais em ambiente corporativo — eles não impedem o
comprometimento inicial, mas limitam o quanto um atacante consegue se
mover depois dele.

## Ataques on-path (Man-in-the-Middle)

- **ARP spoofing/poisoning**: o atacante forja respostas ARP para se
  passar pelo gateway (ou outro host) na rede local, fazendo o tráfego da
  vítima passar por ele antes de seguir ao destino real. É a base técnica
  mais comum para interceptar tráfego numa LAN.
- Esse tipo de ataque acontece na camada 2 e é limitado ao segmento de
  rede local — outro motivo pra segmentação (VLANs) ser relevante como
  controle defensivo.

## Vulnerabilidades sem fio

| Ataque | Descrição |
|---|---|
| AP Rogue | Ponto de acesso não autorizado plugado na rede |
| Evil Twin (gêmeo maligno) | AP falso configurado com o mesmo nome/aparência da rede legítima, para capturar credenciais dos usuários que se conectam por engano |
| Deauth/Desassociação | Força a desconexão de um cliente legítimo (DoS local ou para empurrá-lo a se conectar a um Evil Twin) |
| Wardriving | Mapeamento de redes Wi-Fi vulneráveis percorrendo uma área física |
| Ataques a protocolos antigos (WEP) | WEP tem falhas criptográficas conhecidas e é considerado inseguro; WPA/WPA2/WPA3 sucessivamente corrigiram essas falhas |

## Ângulo de detecção (Blue Team)

- **ARP spoofing** é detectável monitorando associações IP↔MAC
  inconsistentes na rede (uma ferramenta de detecção de ARP spoofing ou
  um IDS de rede configurado para isso sinaliza quando o MAC associado ao
  IP do gateway muda inesperadamente).
- Múltiplas tentativas de autenticação SMB anônimas ou falhas de logon
  vindo de um mesmo host merecem virar regra de alerta.
- **Redes sem fio** devem ser monitoradas quanto ao aparecimento de SSIDs
  duplicados (possível Evil Twin) e picos de frames de desautenticação
  (possível ataque de deauth) — muitos controladores de Wi-Fi corporativos
  já reportam isso nativamente.
- Esse tópico conecta diretamente com o projeto `pcap-analysis/`: uma
  captura de ARP spoofing ou de handshake WPA malformado é um exemplo
  concreto e reproduzível em laboratório controlado.
