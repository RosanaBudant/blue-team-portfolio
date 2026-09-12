# IPv4 — Protocolo e Endereçamento

## O protocolo IP

- Criado por Robert Kahn e Vint Cerf (1973). Serviço **não orientado à
  conexão** e **não confiável** (não garante entrega) — a confiabilidade,
  quando necessária, é responsabilidade de camadas superiores (TCP).
- Unidade de dados: **datagrama**.

### Campos principais do cabeçalho (relevantes pra leitura de pacote)

- **TTL (Time to Live)**: número máximo de saltos (roteadores) que o
  datagrama pode atravessar antes de ser descartado; decrementado a cada
  roteador. Útil pra estimar "distância" de rede e detectar spoofing (TTL
  inconsistente com a origem alegada).
- **Protocolo**: indica o protocolo da camada superior (TCP, UDP, ICMP...).
- **Identificação / Flags / Offset do Fragmento**: controlam fragmentação
  e remontagem de datagramas grandes que precisam ser divididos para
  caber no MTU de cada rede no caminho.
- **Checksum do cabeçalho**: verifica integridade só do cabeçalho (dados
  não são cobertos — cada protocolo superior faz seu próprio checksum).
- **Endereços IP origem e destino**: 32 bits cada, não são alterados
  durante o trajeto (exceto quando há NAT no caminho).

## Endereçamento — classes clássicas

| Classe | Faixa (1º octeto) | Uso |
|---|---|---|
| A | 0–127 | Poucas redes, muitos hosts |
| B | 128–191 | Redes/hosts intermediários |
| C | 192–223 | Muitas redes, poucos hosts (256) |
| D | 224–239 | Multicast |
| E | 240–255 | Reservado/experimental |

*(Hoje o uso de classes fixas foi substituído por CIDR/máscaras de tamanho
variável, mas entender as classes ajuda a interpretar máscaras "clássicas".)*

## Endereços especiais

- **Endereço de rede**: todos os bits de host em 0 (ex: `192.168.1.0`)
- **Endereço de broadcast**: todos os bits de host em 1 (ex: `192.168.1.255`)
- **Loopback**: `127.0.0.1`
- **Faixas privadas (RFC 1918)**: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`

## Máscara de sub-rede

A máscara define quais bits identificam a rede (1) e quais identificam o
host (0). Sub-redes menores permitem dividir um bloco maior em segmentos
independentes (ex: `/24` → `/25` divide 256 endereços em 2 blocos de 128).

## Ângulo de segurança

- Saber calcular rapidamente rede/broadcast/faixa útil de uma sub-rede é
  essencial pra interpretar regras de firewall, ACLs e alertas de IDS que
  vêm expressos em CIDR.
- TTL anômalo (muito diferente do esperado pro SO/rede de origem) é um
  indicador clássico de **IP spoofing**.
- Fragmentação excessiva ou incomum pode ser usada para evadir IDS
  (fragmentation attack) — vale observar em capturas quando os
  fragmentos não remontam de forma limpa.
