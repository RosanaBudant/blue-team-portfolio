# Reconhecimento e Varredura de Vulnerabilidades

## Reconhecimento passivo vs. ativo

- **Passivo**: coleta informação sem interagir diretamente com o alvo —
  OSINT (fontes públicas: registros de domínio, redes sociais, certificados
  SSL, vazamentos), escuta de tráfego. Não gera tráfego suspeito, por isso
  é o tipo de atividade mais difícil de detectar via monitoramento de rede.
- **Ativo**: envia sondas diretamente ao alvo (varredura de portas,
  enumeração de hosts/usuários/serviços) para obter respostas. Gera
  tráfego que pode ser detectado — é aqui que o Blue Team tem mais chance
  de perceber um reconhecimento em andamento.

## Varredura de portas (nível conceitual)

Uma varredura de portas testa quais serviços estão escutando num host,
variando o nível de "ruído" gerado:

- **SYN scan** (semi-aberta): não completa o handshake TCP — mais furtiva,
  gera menos log no alvo.
- **Connect scan**: completa a conexão TCP inteira — mais fácil de
  detectar (mais log gerado, mais chance de disparar IDS).
- **UDP scan**: mais lenta e ambígua (a ausência de resposta pode
  significar "aberta" ou "filtrada").
- Ferramentas ajustam a **velocidade/agressividade** da varredura — quanto
  mais lenta e espaçada, mais furtiva e mais difícil de diferenciar de
  tráfego legítimo.

## Enumeração

Depois de identificar hosts/portas ativas, o próximo passo é extrair mais
detalhes: usuários, grupos, compartilhamentos de rede, versões de
serviço. Em ambientes Windows isso frequentemente usa o protocolo **SMB**
(porta 445) — consultas mal configuradas podem revelar usuários, grupos e
compartilhamentos existentes sem credenciais.

## Varredura de vulnerabilidades

Um scanner de vulnerabilidades automatizado segue, em geral, este ciclo:
1. Descoberta de hosts/portas (equivalente a um port scan)
2. Identificação de versão do serviço rodando em cada porta
3. Correlação com uma base de vulnerabilidades conhecidas
4. Geração de relatório — sujeito a **falsos positivos**, que sempre
   precisam de validação manual antes de virar um achado reportável

### Tipos de varredura

| Tipo | Características |
|---|---|
| Não autenticada | Vê só o que é exposto externamente; mais falsos positivos |
| Autenticada | Usa credenciais para inspecionar o sistema por dentro; mais precisa |
| De descoberta | Foco em mapear a superfície de ataque |
| Completa | Ativa todas as verificações disponíveis |
| Furtiva | Reduz agressividade para não disparar alarmes |
| De conformidade | Verifica aderência a um framework regulatório (ex: PCI DSS) |

## Ângulo de detecção (Blue Team)

- Reconhecimento ativo deixa rastro: múltiplas conexões TCP incompletas
  (SYN sem ACK final) vindas do mesmo IP em curto intervalo, ou varredura
  sequencial de portas em vários hosts, são padrões clássicos que um
  IDS/SIEM pode sinalizar.
- Consultas SMB anônimas bem-sucedidas (enumeração de usuários/grupos/
  compartilhamentos sem autenticação) indicam configuração insegura e
  merecem alerta — é um dos primeiros pontos que um pentester (ou
  atacante real) explora depois de ganhar acesso à rede interna.
- Correlacionar OSINT vazado (ex: funcionários publicando fotos de crachás,
  estrutura de e-mail exposta) com treinamento de conscientização é uma
  medida preventiva que reduz a eficácia do reconhecimento passivo contra
  a organização.
