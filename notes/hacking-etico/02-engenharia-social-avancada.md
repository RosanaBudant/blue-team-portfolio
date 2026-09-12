# Engenharia Social (aprofundado)

## Variações de phishing

| Técnica | Alvo / característica |
|---|---|
| Phishing | Massa, e-mail genérico com link/anexo malicioso |
| Spear phishing | Direcionado a um indivíduo/grupo específico, com contexto pesquisado sobre a vítima (nomes de colegas, projetos reais) |
| Whaling | Direcionado a executivos/C-level, com aparência mais formal e "corporativa" |
| Vishing | Mesma lógica, por telefone (voz) |
| Smishing | Mesma lógica, por SMS |

## Outras técnicas de manipulação

- **Pretexting**: construir uma história/identidade falsa para justificar
  um pedido de informação ou acesso.
- **Watering hole**: comprometer um site que o alvo costuma visitar,
  injetando código malicioso que só afeta visitantes daquele perfil
  específico — ataque direcionado e mais difícil de detectar porque não
  mira a vítima diretamente, mira um lugar que ela frequenta.
- **USB deixado ("USB drop")**: deixar pendrives infectados em locais que
  a vítima frequenta, contando com a curiosidade humana para que alguém
  conecte o dispositivo. Estudos mostram que a maioria das pessoas conecta
  um pendrive encontrado sem hesitar.

## Ataques físicos

- **Tailgating/Piggybacking**: seguir uma pessoa autorizada para entrar
  num espaço restrito sem credencial própria.
- **Busca em lixo (dumpster diving)**: procurar informações sensíveis
  descartadas incorretamente (papéis, mídias não destruídas).
- **Espionagem visual (shoulder surfing)**: observar diretamente o que a
  vítima digita ou visualiza.
- **Clonagem de crachá**: replicar um cartão de acesso físico, muitas
  vezes com informações de design obtidas de fotos postadas em redes
  sociais.

## Métodos de influência (o "porquê" funciona)

Engenheiros sociais exploram gatilhos psicológicos comuns: autoridade
(fingir ser alguém com poder de decisão), urgência (criar pressão de
tempo para evitar verificação), prova social, reciprocidade e simpatia.
Reconhecer esses gatilhos em uma comunicação suspeita é a base de qualquer
treinamento de conscientização.

## Ângulo de detecção e mitigação (Blue Team)

- E-mails de phishing frequentemente compartilham indicadores técnicos
  reconhecíveis: domínio do remetente muito parecido mas não idêntico ao
  legítimo (typosquatting), cabeçalhos de e-mail com origem inconsistente
  com o remetente exibido, links que não correspondem ao texto exibido.
- Simulações periódicas de phishing (com consentimento e escopo definidos)
  são a forma mais direta de medir o nível de exposição real de uma
  organização a esse vetor — e geram dados concretos para justificar
  investimento em treinamento.
- Contra ataques físicos, controles simples (vestíbulos de acesso,
  destruição segura de documentos, política de crachás visíveis) têm
  custo-benefício muito melhor do que soluções puramente tecnológicas.
- Como esse vetor ataca pessoas e não sistemas, a melhor "detecção" nem
  sempre é técnica: um processo claro de "como reportar algo suspeito" e
  cultura de segurança são controles tão importantes quanto um filtro de
  e-mail.
