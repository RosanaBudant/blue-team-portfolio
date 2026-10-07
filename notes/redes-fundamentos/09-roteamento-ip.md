# Roteamento IP e Tabelas de Roteamento

## O que é roteamento IP

É o processo de enviar um datagrama através de múltiplas redes físicas até o destino. Envolve decidir **qual rota seguir**, considerando fatores como carga da rede, tamanho do datagrama, tipo de serviço e menor caminho.

## Roteamento direto vs. indireto

- **Direto**: origem e destino estão na mesma rede física — o pacote vai direto de host a host, sem passar por roteador intermediário
- **Indireto**: origem e destino estão em redes diferentes — o pacote precisa passar por pelo menos um roteador (R) no meio do caminho

## Tabela de roteamento

Cada roteador mantém uma tabela armazenando informações sobre redes de destino possíveis e como alcançá-las. Estrutura básica:

| Rede Destino | Máscara | Saída |
|---|---|---|
| Rede diretamente conectada | Máscara da rede | "Direto via [interface]" |
| Rede alcançável via outro roteador | Máscara da rede | IP do próximo salto (next-hop) |
| `0.0.0.0` | `-` (ou `0.0.0.0`) | Rota padrão (default) |

**Lógica prática:** se a rede de destino está diretamente conectada a uma interface do roteador, a saída é "direto via [interface]". Se não está diretamente conectada, a saída aponta para o IP do próximo roteador no caminho (next-hop) — por exemplo, R1 sabe chegar nas redes 20.0.0.0 e 10.0.0.0 diretamente, mas para alcançar redes mais distantes (30.0.0.0, 40.0.0.0, 50.0.0.0), encaminha o tráfego para o IP do roteador vizinho (ex: 20.0.0.5), que por sua vez sabe o próximo passo.

Cada roteador do caminho só precisa saber o **próximo salto**, não a rota completa até o destino final — esse processo se repete roteador a roteador até o pacote chegar.

## Rota Default (rota padrão)

Entrada especial na tabela (`0.0.0.0`) usada para **reduzir o tamanho da tabela de roteamento**: em vez de listar explicitamente o endereço de toda rede possível que a máquina pode alcançar, qualquer destino que não tenha uma entrada específica na tabela é enviado por essa rota — tipicamente usada para encaminhar tráfego "para fora" da rede local (ex: para a internet).

> Em hosts finais (não roteadores), a tabela costuma ser simples: uma entrada para a rede local (acesso direto) e uma rota default apontando para o **gateway padrão (DG)** — o roteador responsável por tudo que não é da rede local.

## Conexão com Blue Team

Entender tabela de roteamento é a base para interpretar **topologia de rede** em uma investigação — por exemplo, ao analisar tráfego suspeito no Wireshark, saber por onde um pacote deveria passar normalmente ajuda a identificar rotas anômalas, hops inesperados ou tentativas de desviar tráfego (ex: ataques de rota ou spoofing).
