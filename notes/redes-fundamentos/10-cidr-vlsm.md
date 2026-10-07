# CIDR e VLSM

## CIDR (Classless Inter-Domain Routing)

Notação que usa um **prefixo** para indicar quantos bits da máscara de sub-rede são fixos (de rede), em vez de escrever a máscara completa.

**Exemplos:**
- `192.168.1.1/255.255.255.0` → `192.168.1.1/24` (24 bits de "1" na máscara: `11111111.11111111.11111111.00000000`)
- `152.13.160.0/255.255.224.0` → `152.13.160.0/19` (19 bits de "1": `11111111.11111111.11100000.00000000`)

Quanto maior o prefixo, menor o número de hosts disponíveis naquela sub-rede (mais bits "gastos" com a identificação da rede, menos sobram para hosts).

## VLSM (Variable Length Subnet Mask)

Permite criar **sub-redes de tamanhos diferentes dentro de uma mesma rede**, em vez de dividir tudo em blocos iguais — essencial para não desperdiçar endereços IP quando os setores de uma rede têm necessidades de tamanho muito diferentes.

### Exemplo prático (passo a passo)

Bloco recebido: `192.168.2.0/24`, para endereçar 3 prédios + 2 links ponto a ponto entre eles:
- 1º prédio: 50 hosts
- 2º prédio: 28 hosts
- 3º prédio: 15 hosts
- 2 links ponto a ponto (1º↔3º e 2º↔3º), cada um precisando de 2 endereços de host (uma interface em cada ponta)

**Regra geral:** sempre começar pela sub-rede que precisa de **mais hosts** e ir alocando em ordem decrescente — isso evita desperdício de endereços.

| Necessidade | Cálculo | Prefixo | Sub-rede resultante | Intervalo de endereços |
|---|---|---|---|---|
| 50 hosts | 50 < 2⁶ (64) → 32−6 = 26 | /26 | 192.168.2.0/26 | 0 a 63 |
| 28 hosts | 28 < 2⁵ (32) → 32−5 = 27 | /27 | 192.168.2.64/27 | 64 a 95 |
| 15 hosts | 15 < 2⁴ não cabe (16−2=14<15) → usa 2⁵ (32) → 32−5 = 27 | /27 | 192.168.2.96/27 | 96 a 127 |
| Link 1 (2 hosts) | 2 < 2² (4) → 32−2 = 30 | /30 | 192.168.2.128/30 | 128 a 131 |
| Link 2 (2 hosts) | 2 < 2² (4) → 32−2 = 30 | /30 | 192.168.2.132/30 | 132 a 135 |

**Como calcular o prefixo:** encontrar o menor expoente *n* tal que `2ⁿ` seja maior que o número de hosts necessário (contando endereço de rede e broadcast); o prefixo é `32 − n`.

**Atenção ao caso de 15 hosts:** `2⁴ = 16`, mas descontando endereço de rede e broadcast sobram só 14 hosts utilizáveis — não é suficiente para 15, então é preciso subir para `2⁵ = 32` (prefixo /27), mesmo "desperdiçando" mais endereços do que o estritamente necessário.

## Conexão com Blue Team

Saber calcular CIDR/VLSM é essencial para **ler e interpretar diagramas de rede** durante uma investigação — por exemplo, ao analisar logs de firewall ou tráfego de rede, reconhecer rapidamente a que sub-rede um IP pertence ajuda a identificar se um host é interno, de outro segmento, ou potencialmente externo/suspeito. Também é básico para configurar corretamente o ambiente de laboratório (ex: VMs do Blue Team Lab) em sub-redes isoladas.
