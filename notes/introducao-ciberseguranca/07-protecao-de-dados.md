# Protegendo Dados e Dispositivos

## Proteção de dispositivos pessoais

- **Firewall ativado** — software ou de hardware no roteador, sempre atualizado
- **Antivírus/antispyware** instalado e atualizado, baixando software só de fontes confiáveis
- **SO e navegador atualizados** — configurações de segurança em nível médio/alto, patches aplicados regularmente
- **Proteção por senha** em todos os dispositivos (PC, celular, tablet), com dados sensíveis criptografados
- **Dispositivos IoT** são mais vulneráveis — raramente recebem atualizações de segurança, então o ideal é isolá-los numa rede separada da rede principal

## Wi-Fi

- Trocar **SSID** e senha padrão do roteador (hackers conhecem os padrões de fábrica)
- Habilitar criptografia **WPA2** — mas atenção à vulnerabilidade **KRACK** (Key Reinstallation Attack), que pode comprometer até redes com WPA2 ativo
- Mitigação: manter firmware de roteadores/dispositivos atualizado, preferir conexão cabeada quando possível, usar **VPN** confiável em redes sem fio
- **Wi-Fi público:** evitar compartilhamento de arquivos ativo, exigir autenticação com criptografia, e sempre usar VPN para evitar interceptação (eavesdropping)

## Senhas

**Diretrizes do NIST:**
- Mínimo 8 caracteres (sem máximo baixo — até 64)
- Sem exigência forçada de maiúsculas/números/símbolos (regras de composição)
- Sem expiração periódica obrigatória
- Permitir visualizar a senha ao digitar (reduz erro)
- Não usar dicas de senha nem perguntas secretas como autenticação

**Frase secreta > senha tradicional:** mais fácil de lembrar e mais resistente a força bruta/dicionário (ex: "Umgato queAm4vcachorro").

## Criptografia e backup

- **Criptografia** converte dados para formato ilegível sem a chave — não impede interceptação, só impede leitura do conteúdo
- No Windows, o **EFS (Encrypting File System)** criptografa arquivos/pastas vinculados à conta do usuário
- **Backup:** pode ser local (HD externo, NAS, pendrive) ou em nuvem (ex: AWS) — nuvem protege contra perda física (incêndio, roubo), mas depende de acesso à conta
- **Deletar não é apagar de verdade:** um arquivo "excluído" continua recuperável até ser sobrescrito. Ferramentas como SDelete (Windows) ou shred (Linux) sobrescrevem os dados; a única garantia total é destruição física da mídia

## Quem é dono dos seus dados

Antes de aceitar Termos de Serviço de qualquer plataforma, vale checar:
- O que a política de uso de dados diz sobre coleta/compartilhamento
- Quais configurações de privacidade você pode controlar
- O que acontece com seus dados após encerrar a conta

## Proteção de privacidade online

- **Autenticação de dois fatores (2FA):** soma senha + um segundo fator (objeto físico, biometria, código por SMS/e-mail). Reduz risco, mas não elimina (ainda vulnerável a phishing/malware avançado)
- **OAuth (Open Authorization):** permite login em serviço de terceiros usando credenciais de outra conta (ex: "Entrar com Google"), sem expor a senha original
- **Navegação privada** remove cookies e histórico local ao fechar a janela, mas não impede todas as formas de rastreamento (ex: fingerprinting, roteadores intermediários registrando tráfego)
