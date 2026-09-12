# Pós-Exploração

Fase que acontece depois que um atacante (ou pentester) já obteve acesso
inicial a um sistema. O objetivo aqui é entender o que ele tenta fazer em
seguida — essencial para saber o que procurar numa investigação de
incidente.

## Persistência

Depois do acesso inicial, manter esse acesso é prioridade — reinícios de
sistema, trocas de senha ou detecção parcial não devem derrubar o
atacante. Técnicas comuns:

- **Shells bind e reverso**: formas de manter um canal de controle remoto
  aberto com o sistema comprometido (bind = o sistema comprometido fica
  "escutando"; reverso = o sistema comprometido é quem inicia a conexão
  de volta ao atacante — útil para atravessar firewalls que bloqueiam
  conexões de entrada).
- **Comando e controle (C2)**: infraestrutura usada pelo atacante para
  enviar instruções a sistemas comprometidos, muitas vezes disfarçada
  como tráfego legítimo (ex: usando serviços cloud populares como canal).
- **Tarefas agendadas, novos serviços/daemons, novas contas de usuário**:
  formas de garantir que o acesso sobreviva a uma reinicialização.

## Movimento lateral

Depois de garantir persistência num ponto de apoio, o atacante tenta se
mover para outros sistemas da rede — reconhecimento interno, reuso de
credenciais e exploração adicional. Isso só é possível na escala que for
porque a rede não está bem segmentada; **segmentação de rede** é
justamente o controle que limita o alcance de um movimento lateral mesmo
depois de um comprometimento inicial.

### "Living off the land"

Uma técnica relevante: em vez de instalar ferramentas maliciosas novas
(que teriam mais chance de ser detectadas por antivírus), o atacante usa
utilitários **legítimos já presentes no sistema** (PowerShell, WMI,
utilitários administrativos nativos) para realizar as mesmas tarefas.
Isso é chamado de "malware sem arquivo" — não há binário malicioso novo
para uma assinatura de antivírus detectar, o que torna a detecção
comportamental (ver `notes/introducao-ciberseguranca/06-siem-soc-csirt.md`)
muito mais relevante do que detecção baseada em assinatura nesse cenário.

## Escalada de privilégios

- **Vertical**: um usuário comum ganha privilégios de administrador/root.
- **Horizontal**: um usuário ganha acesso a recursos de outro usuário do
  mesmo nível de privilégio (não a privilégios mais altos, mas a dados
  que não deveriam ser dele).

## Cobrindo rastros

Antes de encerrar, um atacante tenta apagar evidências: remover contas
criadas, arquivos temporários, logs relevantes, e reverter qualquer
configuração alterada. Isso reforça por que **logs centralizados e
protegidos contra alteração** (enviados imediatamente para um SIEM, fora
do alcance do sistema comprometido) são essenciais — se o único registro
de um evento vive no próprio host comprometido, o atacante pode apagá-lo.

## Ângulo de detecção (Blue Team) — o mais direto pra este portfólio

- Conexões de saída incomuns (um host de usuário comum iniciando conexão
  para uma porta externa não usual) podem indicar um shell reverso ou
  beacon de C2.
- Criação de novas contas de usuário ou novas tarefas agendadas fora da
  janela normal de mudança é um sinal clássico de persistência — e é
  exatamente o tipo de evento que o **Wazuh** (via monitoramento de log e
  FIM) está posicionado para capturar.
- Tempo de permanência de um atacante numa rede ("dwell time") depende
  diretamente da velocidade de detecção dessas atividades — quanto mais
  cedo a persistência e o movimento lateral forem identificados, menor a
  janela de exfiltração de dados.
- Esse módulo é a ponte conceitual mais clara para os `incident-reports/`
  do portfólio: cada relatório de incidente pode ser estruturado seguindo
  esse ciclo (acesso inicial → persistência → movimento lateral →
  exfiltração → limpeza de rastros) e mapeado no MITRE ATT&CK.
