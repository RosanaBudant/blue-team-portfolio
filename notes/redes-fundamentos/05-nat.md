# NAT — Network Address Translator

## Por que existe

O IPv4 tem quantidade limitada de endereços. O NAT (RFC 1631) permite que
uma rede interna use um conjunto de endereços privados diferentes dos
usados para acessar a Internet, traduzindo entre eles num roteador de
borda.

**Faixas de endereços privados (não roteáveis na Internet):**
- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

## Características comuns

- **Alocação transparente**: liga endereços privados a endereços públicos e vice-versa.
- **Roteamento transparente**: traduz o cabeçalho IP para conter um
  endereço roteável do próprio NAT-router.

## Tipos

| Tipo | Descrição |
|---|---|
| NAT Estático | Tradução 1:1 fixa; não economiza endereços |
| NAT Dinâmico | Tradução baseada nas conexões ativas |
| NAPT / IP Masquerading | Tradução m:1 (muitos IPs privados → 1 IP público, trocando também a porta). É a técnica mais usada hoje. |

## Ângulo de segurança

- O NAT **oculta o layout da rede interna** — quem está do lado de fora só
  enxerga o IP público do roteador, não os hosts internos individuais. Isso
  dá uma camada extra de proteção "por obscuridade" (não substitui firewall).
- Do ponto de vista de análise forense/Blue Team: numa rede com NAT, todo
  tráfego externo de múltiplos hosts internos aparece com o **mesmo IP de
  origem** (o do NAT-router) — só muda a porta de origem. Isso é
  fundamental para não confundir múltiplos hosts internos com uma única
  máquina ao investigar logs de firewall ou proxy.
