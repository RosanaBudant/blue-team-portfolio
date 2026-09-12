# DHCP — Dynamic Host Configuration Protocol

## O que resolve

Automatiza a entrega dos parâmetros necessários pro TCP/IP funcionar numa
máquina que acabou de entrar na rede:
- Endereço IP
- Máscara de rede
- Gateway padrão
- Servidores DNS

Sem isso, cada máquina precisaria de configuração manual — inviável em
redes grandes e gera inconsistência.

## Características

- Extensão do BOOTP, usa **UDP**: servidor na porta **67**, cliente na porta **68**.
- Servidor mantém dois tipos de banco: endereços estáticos (reservados) e
  uma faixa dinâmica disponível para concessão temporária (lease).
- **Renovação do lease**: aos 50% do tempo de concessão o cliente tenta
  renovar via unicast direto com o servidor (Renewal); aos 87,5% tenta
  renovar via broadcast com qualquer servidor (Rebinding); aos 100% perde o IP.
- **Relay Agent**: reencapsula os pedidos broadcast do cliente em mensagens
  direcionadas quando o servidor DHCP está em outra sub-rede.

## DHCP + DNS + IPAM (DDI)

- O IPAM (IP Address Management) dá visibilidade centralizada de quem está
  usando qual IP, permitindo auditoria: "qual dispositivo usou esse IP nesse
  horário" — informação essencial em investigação de incidente.
- Com DDNS (Dynamic DNS), quando o DHCP atribui um IP, o próprio DHCP ou o
  dispositivo pode atualizar automaticamente o registro DNS correspondente.

## Ângulo de segurança (Blue Team)

- **DHCP Starvation**: um atacante pode esgotar o pool de IPs disponíveis
  fazendo várias requisições DHCP Discover com MACs falsos, negando serviço
  a clientes legítimos.
- **Rogue DHCP Server**: um servidor DHCP não autorizado na rede pode
  responder antes do servidor legítimo, entregando gateway/DNS forjados
  (abre caminho pra man-in-the-middle).
- No Wireshark, tráfego DHCP normal segue o ciclo **Discover → Offer →
  Request → Ack (DORA)**; uma investigação sobre isso deve procurar por
  volume anômalo de Discovers ou mais de um servidor respondendo a mesma
  requisição.
