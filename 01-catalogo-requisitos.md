# Catálogo de Requisitos: IA Local para Documentos (Offline-first, Egresso Auditado)

**Versão:** 0.2 · **Papel:** documento de referência para Fase 2 e 3, **não é escopo do MVP**.

> Para o escopo do MVP e das conversas de discovery, use [04-mvp-matriz.md](04-mvp-matriz.md). Este catálogo completo existe para que nada importante seja esquecido quando o projeto crescer.
**Escopo:** plataforma de IA capaz de processar documentos locais (PDF, DOC/DOCX, XLS/XLSX, PPT, MSG/EML, XML fiscal, imagens digitalizadas, entre outros) sem submissão a plataformas de IA em nuvem externa, com suporte a consultas externas **expressamente solicitadas** e **integralmente auditadas**.
**Verticais prioritárias:** jurídico, compliance, administrativo/público, contábil, fiscal. Secundárias: trabalhista/RH, saúde, seguros, engenharia, imobiliário.

---

## 1. Contexto e premissas

O documento parte de cinco premissas que condicionam todos os requisitos abaixo. Se alguma delas for rejeitada no debate, os requisitos marcados como dependentes precisam ser revistos.

**P1. O dado documental é o ativo, não o modelo.** O valor está no acervo (contratos, processos, notas fiscais, políticas, demonstrações) e nos derivados dele. O modelo é substituível; o acervo não é. Toda decisão arquitetural deve proteger o acervo primeiro.

**P2. "Offline" é o modo padrão, não uma restrição.** A instalação nasce sem rota de saída para serviços de IA. Habilitação de egresso é ato administrativo explícito, versionado e reversível.

**P3. Existe um perímetro de dados ampliado.** Não é só o arquivo. Texto extraído, OCR, chunks, vetores de embedding, cache de prompt, prompt em si, histórico de conversa, logs, traces e métricas derivadas são todos o mesmo dado sob a mesma classificação. Qualquer requisito que fale em "não sai do ambiente" aplica-se a todo esse conjunto.

**P4. A consulta externa é um ato jurídico, não um detalhe técnico.** Enviar conteúdo de cliente a terceiro pode violar sigilo profissional, segredo de justiça, sigilo fiscal/bancário e LGPD simultaneamente. Por isso o egresso precisa de finalidade, autorização, registro e possibilidade de reconstrução, como qualquer ato com efeito jurídico.

**P5. Qualidade local é requisito de negócio, não aspiração.** Se o modelo local entregar resultado pior que o usuário obteria colando o texto no ChatGPT, ele vai colar o texto no ChatGPT. A contenção do egresso só se sustenta se a experiência local for boa o suficiente. Isso torna avaliação contínua (R22) e adaptação ao domínio (R23) requisitos essenciais, não desejáveis.

---

## 2. Convenções de indexação e leitura

- **R** = requisito. Numeração contínua R1..R40, agrupada em seis blocos temáticos.
- **E** = especificação. Numeração **reiniciada dentro de cada requisito** (E1..En). Portanto "E6" isolado não identifica nada; a referência sempre inclui o requisito.
- **Referência cruzada** entre especificações de requisitos diferentes é escrita como: *conforme especificação E4 do requisito R38*. Referências dentro do mesmo requisito aparecem como *conforme E4*.
- **D** = decisão de arquitetura ou de política, registrada em [03-registro-decisoes.md](03-registro-decisoes.md) e referenciada como *conforme decisão D1*. Decisões fechadas substituem parâmetros que antes eram "a definir"; decisões abertas permanecem na seção 12.
- **Prioridade** segue MoSCoW adaptado:
  - **Essencial.** sem isso a solução não atende à premissa central (soberania, auditabilidade, sigilo). Não há MVP sem isso.
  - **Importante.** necessário para operação real em produção, pode entrar na primeira onda de entrega.
  - **Desejável.** agrega valor, entra em fase posterior.
  - **Futuro.** direcional, registrado para não ser esquecido.
- Cada especificação é escrita para ser **verificável**: teste, inspeção de configuração, demonstração ou evidência documental.

---

## 3. Mapa de requisitos (visão geral)

| Bloco | Requisitos | Tema |
|---|---|---|
| I | R1 a R8 | Governança, conformidade e soberania |
| II | R9 a R16 | Conhecimento documental (ingestão, extração, busca) |
| III | R17 a R23 | Modelos, orquestração e qualidade de resposta |
| IV | R24 a R30 | Segurança, isolamento e infraestrutura |
| V | R31 a R36 | Verticais, integrações e pessoas |
| VI | R37 a R40 | Economia, implantação e evolução |

| ID | Requisito | Bloco | Prioridade |
|---|---|---|---|
| R1 | Soberania documental e confidencialidade por padrão | I | Essencial |
| R2 | Conformidade legal e regulatória | I | Essencial |
| R3 | Sigilo profissional e informação sensível | I | Essencial |
| R4 | Controle de egresso e consultas externas auditadas | I | Essencial |
| R5 | Solicitação expressa e consentimento qualificado | I | Essencial |
| R6 | Auditoria, rastreabilidade e cadeia de custódia | I | Essencial |
| R7 | Identidade, papéis e autorização | I | Essencial |
| R8 | Governança e gestão de riscos de IA | I | Importante |
| R9 | Ingestão multi-formato | II | Essencial |
| R10 | OCR, ICR e extração de layout | II | Essencial |
| R11 | Normalização, versionamento e deduplicação | II | Importante |
| R12 | Classificação e taxonomia documental | II | Importante |
| R13 | Extração estruturada e enriquecimento | II | Importante |
| R14 | Indexação e busca híbrida | II | Essencial |
| R15 | Recuperação aumentada com grounding e citação | II | Essencial |
| R16 | Ciclo de vida, retenção e descarte | II | Importante |
| R17 | Runtime de modelos locais | III | Essencial |
| R18 | Orquestração de agentes e fluxos | III | Importante |
| R19 | Qualidade de resposta e anti-alucinação | III | Essencial |
| R20 | Gateway técnico de IA externa | III | Essencial |
| R21 | MLOps local e ciclo de vida de modelos | III | Importante |
| R22 | Avaliação contínua e benchmarking | III | Essencial |
| R23 | Adaptação ao domínio | III | Importante |
| R24 | Criptografia e proteção de dados | IV | Essencial |
| R25 | Isolamento e segregação multi-tenant | IV | Essencial |
| R26 | Infraestrutura e aceleração | IV | Essencial |
| R27 | Desempenho e escalabilidade | IV | Importante |
| R28 | Disponibilidade, backup e continuidade | IV | Importante |
| R29 | Observabilidade e SLOs | IV | Importante |
| R30 | Administração e configuração | IV | Importante |
| R31 | Integrações jurídicas e processuais | V | Importante |
| R32 | Integrações contábeis, fiscais e ERP | V | Importante |
| R33 | Integrações de produtividade e GED | V | Desejável |
| R34 | Casos de uso por vertical | V | Importante |
| R35 | Experiência do usuário e acessibilidade | V | Essencial |
| R36 | Capacitação e gestão de mudança | V | Importante |
| R37 | Custo total de propriedade e economicidade | VI | Importante |
| R38 | Topologia e modos de implantação | VI | Essencial |
| R39 | Suporte, manutenção e atualização normativa | VI | Importante |
| R40 | Extensibilidade e roadmap | VI | Desejável |

---

# BLOCO I: Governança, conformidade e soberania

## R1. Soberania documental e confidencialidade por padrão

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** É o requisito fundante. Define o que não pode acontecer em nenhuma circunstância, independentemente de configuração, plugin, integração ou versão. Todos os demais requisitos técnicos existem para tornar este verificável.

**Especificações**

- **E1. Perímetro de dados formalmente definido.** Inventário publicado do que constitui "dado documental": arquivo original, texto extraído, resultado de OCR, tabelas e células, metadados, chunks, embeddings e índice vetorial, cache de prompt e de resposta, histórico de conversa, logs de consulta, traces de execução e métricas que permitam reconstruir conteúdo. Todos herdam a mesma classificação de sensibilidade do original.
- **E2. Pipeline padrão integralmente local.** Ingestão, antivírus, conversão de formato, OCR, chunking, geração de embeddings, indexação, recuperação, reranking, inferência e geração de resposta ocorrem em infraestrutura sob controle do cliente, sem dependência de serviço externo.
- **E3. Zero telemetria de terceiros por padrão.** Nenhum componente (biblioteca, runtime de modelo, agente, coletor) envia métricas, relatórios de falha, prompts, nomes de arquivo, contadores de uso ou identificadores de instalação para o fabricante. Toda telemetria é local e opcional.
- **E4. Operação air-gapped plena.** O sistema opera completamente sem rota de saída à internet, incluindo instalação, ativação de licença, atualização de software, atualização de modelos e suporte técnico remoto, *conforme especificação E5 do requisito R38*.
- **E5. Vedação de treinamento com dados do cliente.** Configuração e contrato garantem que nenhum dado do cliente é usado para treinar, ajustar ou avaliar modelos de terceiros. Modelos locais não retêm estado entre sessões nem entre tenants, *conforme especificação E4 do requisito R25*.
- **E6. Inventário de dependências e teste de "phone home".** Cada versão publica SBOM (software bill of materials) e a lista de endpoints externos que o software é capaz de acionar. A esteira de release executa teste automatizado de rede que falha o build se houver conexão não declarada.
- **E7. Residência de dados e jurisdição declaradas.** Contrato e configuração declaram onde os dados residem fisicamente e sob qual jurisdição. Replicação para região não autorizada é bloqueada tecnicamente, não apenas por política.
- **E8. Rótulo de sensibilidade na origem.** Todo artefato carrega classificação (público, interno, restrito, sigiloso) desde a ingestão, e essa classificação condiciona recuperação, exibição e egresso.
- **E9. Ambiente de demonstração com dados sintéticos.** Existe modo de avaliação comercial e de treinamento que opera com acervo sintético, sem exigir exposição de dados reais do cliente.
- **E10. Verificação independente.** O cliente ou auditor terceiro pode executar a suíte de verificação de confinamento (captura de tráfego, inspeção de processos, checklist) sem depender da palavra do fornecedor.

---

## R2. Conformidade legal e regulatória

**Prioridade:** Essencial · **Verticais:** todas, com peso em compliance e saúde

**Racional.** A solução trata dados pessoais e, em várias verticais, dados sensíveis e protegidos por sigilo legal. Precisa ser operável *dentro* do regime jurídico, não apenas "com aviso de privacidade".

**Especificações**

- **E1. Base legal e finalidade registradas por tratamento.** Cada fluxo de tratamento declara base legal (LGPD, Lei 13.709/2018, art. 7º ou art. 11 para dados sensíveis), finalidade e categoria de titulares. O registro é mantido no próprio sistema e exportável.
- **E2. Mapeamento de dados pessoais e sensíveis.** A plataforma identifica e classifica dados pessoais e dados pessoais sensíveis nos documentos ingeridos, com relatório de incidência por acervo, por cliente e por vertical.
- **E3. Direitos do titular operacionalizáveis.** Busca por titular, exportação em formato estruturado, correção e eliminação, com propagação efetiva para índice textual, índice vetorial, cache e logs, *conforme especificação E5 do requisito R16*.
- **E4. Minimização e limitação de retenção.** O sistema permite configurar retenção por classe documental e por base legal, e bloqueia retenção indeterminada por padrão.
- **E5. Avaliação de impacto (DPIA/RIPD) suportada por evidência.** O sistema produz os insumos técnicos da avaliação: categorias de dados, volumes, fluxos, destinatários, medidas de segurança e histórico de incidentes.
- **E6. Transferência internacional sob controle.** No modo padrão não há transferência internacional. No modo com egresso habilitado, cada destino externo é registrado com país, subprocessadores e base legal, *conforme especificação E2 do requisito R4*.
- **E7. Requisitos setoriais mapeados.** Mínimo exigido: regulamentação de segurança cibernética de instituições financeiras (Resolução CMN 4.658/2018) e normas de PLD/FT do Banco Central; guarda de prontuário eletrônico (Lei 13.787/2018 e regulamentação do CFM); sigilo fiscal (CTN, art. 198); sigilo bancário (LC 105/2001); uso de IA no Judiciário (Resolução CNJ 332/2020); contratações públicas (Lei 14.133/2021) e processo eletrônico no setor público.
- **E8. Normas técnicas adotadas como referencial.** ISO/IEC 27001 (segurança da informação), ISO/IEC 27701 (privacidade) e ISO/IEC 42001 (sistema de gestão de IA), além do NIST AI Risk Management Framework como modelo de risco.
- **E9. Regulação de IA acompanhada.** Mapeamento contínuo do marco legal de IA em tramitação no Brasil (PL 2338/2023) e do Regulamento (UE) 2024/1689 para operações com exposição a contrapartes europeias. Requisitos de transparência e de supervisão humana são implementados desde já, independentemente da entrada em vigor.
- **E10. Registro de operações de tratamento gerado automaticamente.** O sistema mantém e exporta o inventário de operações (ROPA) atualizado a partir da configuração real, não de planilha paralela.

---

## R3. Sigilo profissional e informação sensível

**Prioridade:** Essencial · **Verticais:** jurídico, compliance, contábil, saúde

**Racional.** Vai além da LGPD: aqui o dano não é só ao titular, é à relação profissional e ao processo. O sigilo advocatício, o segredo de justiça e o sigilo fiscal têm regimes próprios e consequências disciplinares e processuais.

**Especificações**

- **E1. Sigilo advocatício protegido por desenho.** O sistema impede tecnicamente a revelação de informação de cliente a terceiro, inclusive por egresso. Envio externo de conteúdo de cliente exige anuência registrada do cliente ou base legal expressa, *conforme especificação E4 do requisito R5*.
- **E2. Segredo de justiça com isolamento próprio.** Documentos marcados como sigilosos (CPC, art. 189) recebem índice separado, bloqueio de egresso por padrão e controle de acesso por vínculo ao processo, não apenas por perfil.
- **E3. Informação privilegiada de mercado.** Suporte a marcação de informação privilegiada e a controle de "wall-crossing" para equipes que operam temas societários e de capitais.
- **E4. Sigilo fiscal e bancário.** Documentos fiscais e extratos com sigilo legal recebem classificação própria e restrição de recuperação cruzada entre entidades do mesmo grupo.
- **E5. Segredo industrial e NDA de due diligence.** Data rooms e acervos de due diligence são isolados por operação, com registro de quem acessou o quê e quando, e com expiração automática ao final do projeto.
- **E6. Prontuário e dado de saúde.** Tratamento com isolamento reforçado, controle de acesso por vínculo assistencial e observância do prazo legal de guarda.
- **E7. Compartimentação por cliente, processo e assunto.** O acesso é concedido por vínculo explícito, não por pertencimento a área. A ausência de vínculo impede a recuperação, inclusive em busca semântica.
- **E8. Proteção contra exfiltração em exportações.** Exportações carregam marca d'água identificadora do usuário e do momento, e exportações em massa disparam revisão ou bloqueio conforme política.

---

## R4. Controle de egresso e consultas externas auditadas

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Este é o requisito que define a expressão "parcialmente online". Não basta ter um botão de "usar IA externa": é preciso que o caminho seja único, visível, minimizado, autorizado, registrado e reconstruível. A postura correta é negação por padrão com liberação excepcional e observável.

**Especificações**

- **E1. Negação por padrão.** Nenhuma rota de saída para serviços de IA externos está ativa na instalação. Habilitação é ato administrativo explícito, versionado, com prazo e responsável identificado, *conforme especificação E1 do requisito R38*.
- **E2. Catálogo fechado de destinos homologados.** Existe lista formal de provedores externos permitidos, cada um com endpoint, país de processamento, política de retenção, subprocessadores, base de transferência internacional e data de revisão. Destino fora do catálogo é tecnicamente inalcançável, não apenas não recomendado. O catálogo é limitado a **dois provedores no primeiro ciclo de habilitação**, *conforme decisão D1*.
- **E3. Broker de egresso como caminho único.** Todo tráfego para modelo externo passa por um gateway que aplica política, inspeciona payload, aplica redação e registra. Não existe chamada direta de componente de aplicação, script ou notebook ao provedor.
- **E4. Bloqueio em camadas independentes.** A política é aplicada simultaneamente em: camada de aplicação, proxy de saída, firewall/DNS corporativo e política de rede do orquestrador de containers. Um bypass em uma camada é contido pelas demais.
- **E5. Pré-visualização obrigatória do payload.** Antes do envio, o usuário vê exatamente o que sairá: texto integral, trechos citados, metadados, nome do destino e país. Sem confirmação sobre a prévia visualizada, não há envio.
- **E6. Minimização e redação automática.** O gateway aplica mascaramento de dados pessoais e sensíveis, remoção de metadados do arquivo e, quando a finalidade permitir, substituição de nomes e identificadores por placeholders com reversão local na resposta.
- **E7. Autorização em camadas por classe de conteúdo.** C2 depende de política prévia aprovada pelo responsável da área; C3 de política prévia aprovada pelo sócio responsável, com alçada nominal; C4 exige quatro olhos por consulta, com decisão do sócio responsável pelo caso. O DPO define a política, detém poder de veto e de revogação e audita, mas não aprova caso a caso. Nenhum aprovador aprova a própria solicitação, *conforme especificação E4 do requisito R7*, e *conforme especificação E5 do requisito R7*. C4 não admite trilha de urgência, *conforme decisão D4*.
- **E8. Justificativa vinculada obrigatória.** Todo egresso exige finalidade declarada e vínculo a cliente e a processo ou projeto. Consulta sem vínculo é negada.
- **E9. Cotas e limites de escopo.** Tetos configuráveis por consulta (volume de caracteres), por usuário/dia, por cliente e por processo. Anomalia de volume gera alerta e bloqueio, não apenas relatório. Valores iniciais por classe de payload: C2 com 100 consultas por usuário/mês; C3 com 30 consultas e 150 mil caracteres por usuário/mês; C4 com 5 consultas por usuário/mês; C0 e C1 sem cota de governança, sujeitas apenas a limite de custo, *conforme decisão D1*.
- **E10. Autorização com prazo e revogação.** Autorizações têm janela de validade. Autorização permanente só existe quando concedida por política explícita, nunca por uso repetido. A habilitação do egresso é concedida por cliente, tem prazo inicial de **90 dias**, renovação por decisão registrada e revisão contratual obrigatória em **12 meses**; ao término sem renovação, o broker retorna automaticamente ao estado negado, *conforme decisão D1*.
- **E11. Registro imutável do egresso.** Para cada envio, registro encadeado por hash contendo: hash do payload, destino, provedor, versão do modelo externo declarada, horário, solicitante, aprovador, política aplicada, transformações de redação executadas e resposta recebida.
- **E12. Marcação permanente do conteúdo derivado.** Toda resposta proveniente de modelo externo é armazenada com rótulo de proveniência externa, destacada visualmente na interface e identificada em qualquer exportação posterior, *conforme especificação E5 do requisito R15*.
- **E13. Retorno controlado ao acervo.** Resposta externa não é automaticamente indexada no acervo local. Ela entra como documento de origem externa, em coleção separada e identificada, sujeita a curadoria.
- **E14. Interruptor geral de emergência.** Comando único desativa todo o egresso, com efeito em segundos e registro de quem acionou, quando e por quê.
- **E15. Distinção entre consulta sem conteúdo e consulta com conteúdo.** Pergunta genérica, sem dados do cliente no payload, tem fluxo simplificado. Qualquer payload que contenha conteúdo documental exige nível superior de autorização. A classificação do payload é feita pelo gateway, não autodeclarada pelo usuário.
- **E16. Suíte de testes de exfiltração.** Conjunto automatizado e periódico de tentativas de vazamento por prompt injection, imagem markdown com URL, link, exfiltração por DNS, uso indevido de ferramentas de agente e encoding alternativo. Resultado auditável e com prazo de correção definido.
- **E17. Contratos e DPAs por destino.** Cada provedor homologado tem instrumento contratual com vedação de treinamento, retenção zero ou mínima declarada, região de processamento e obrigação de notificação de incidente em prazo compatível com o dever de comunicação do controlador.
- **E18. Modo simulação.** Execução em branco que mostra o que seria enviado, quais redações ocorreriam e quais políticas disparariam, sem realizar o envio. Permite treinar usuários e validar políticas antes de habilitar.

---

## R5. Solicitação expressa e consentimento qualificado

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Complementa R4 pelo lado do ato humano. O requisito central é que a consulta externa seja sempre um ato positivo, informado e atribuível a alguém, nunca um comportamento automático do sistema.

**Especificações**

- **E1. Ato positivo inequívoco.** Nenhuma consulta externa ocorre por ação implícita, por fallback automático, por degradação de qualidade, por timeout do modelo local ou por padrão de configuração.
- **E2. Proibição de fallback silencioso.** Se o modelo local não atende ao caso, o sistema informa a limitação de forma explícita e oferece a alternativa externa. Ele nunca a executa por conta própria. Esta é a especificação mais violada em produtos comerciais e deve ser testada especificamente.
- **E3. Declaração de ciência registrada.** O usuário declara ciência do que será compartilhado, com quem, em qual país e sob qual retenção, antes do primeiro envio em cada contexto.
- **E4. Anuência do cliente quando exigida.** Para acervos de cliente, o compartilhamento com terceiro só ocorre com registro de anuência contratual ou autorização específica do cliente, mantido no dossiê do cliente.
- **E5. Granularidade da autorização.** A autorização é concedida por consulta, por sessão, por processo ou por política de cliente, nunca de forma global e irrestrita. A granularidade é escolhida na concessão e exibida no momento do uso. O vínculo entre classe de conteúdo e granularidade é o fixado pela *decisão D1* e detalhado na matriz de decisão de egresso: política prévia por cliente para C2 e C3, autorização individual com quatro olhos para C4, *conforme decisão D4*.
- **E6. Revogação a qualquer tempo.** Usuário, gestor, DPO e administrador podem revogar autorizações vigentes, com efeito imediato e registro.
- **E7. Registro completo do consentimento.** Quem consentiu, quando, em qual escopo, com qual prazo, qual texto foi apresentado e qual versão da política estava vigente.
- **E8. Bloqueio por perfil.** Perfis sem alçada não veem sequer a opção de consulta externa. A existência do recurso não é publicizada a quem não pode usá-lo.
- **E9. Educação no ponto de decisão.** A interface apresenta, no momento da escolha, o risco concreto daquele caso (por exemplo: "este documento contém dado de saúde e está marcado como sigiloso"), e não um aviso genérico.

---

## R6. Auditoria, rastreabilidade e cadeia de custódia

**Prioridade:** Essencial · **Verticais:** todas, com peso em jurídico, compliance e setor público

**Racional.** Sem trilha confiável não há como demonstrar conformidade, defender-se em auditoria nem sustentar a validade de uma peça produzida com apoio de IA. A trilha precisa resistir à tentação de alteração por quem tem acesso administrativo.

**Especificações**

- **E1. Log inviolável.** Registros de auditoria são append-only, com encadeamento por hash ou armazenamento WORM. Nem administrador do sistema apaga ou edita evento já gravado; exclusão de log é, ela própria, um evento registrado.
- **E2. Trilha por documento.** Para cada documento: quem ingeriu, quando, de onde, quem acessou, em qual consulta, com qual finalidade e em qual resposta foi utilizado.
- **E3. Trilha por resposta.** Cadeia completa resposta → trecho citado → página → documento → hash do original, reconstruível a posteriori.
- **E4. Trilha de egresso dedicada.** Visão consolidada de todas as consultas externas, com filtros por cliente, usuário, período, destino e resultado, *conforme especificação E11 do requisito R4*.
- **E5. Retenção de log compatível com obrigações.** Prazos distintos por tipo de evento, respeitando prazo processual, prazo fiscal (regra geral de cinco anos) e prazos setoriais, sem descarte prematuro nem retenção indefinida.
- **E6. Exportação para SIEM/SOC.** Integração padronizada para envio de eventos a plataforma corporativa de monitoramento, em formato estruturado.
- **E7. Integridade do original.** Hash criptográfico do arquivo calculado na ingestão e reverificado sob demanda; divergência gera alerta de possível adulteração.
- **E8. Reconstrução de consulta.** Capacidade de reexecutar uma consulta histórica com as mesmas versões de modelo, índice, prompt e parâmetros, produzindo resultado comparável para fins de demonstração.
- **E9. Relatórios para terceiros.** Geração de relatório de auditoria para DPO, auditoria externa, órgãos de controle e, quando aplicável, para o Judiciário e para o cliente.
- **E10. Proteção do próprio log.** O log não se torna um novo vetor de vazamento: conteúdo sensível é referenciado por identificador e hash, não replicado em claro no evento de auditoria.

---

## R7. Identidade, papéis e autorização

**Prioridade:** Essencial · **Verticais:** todas

**Especificações**

- **E1. Autenticação corporativa.** Integração com provedor de identidade do cliente via SAML 2.0 ou OpenID Connect, com MFA obrigatório para perfis administrativos e para alçada de egresso.
- **E2. Autorização híbrida RBAC + ABAC.** Papéis definem o que o perfil pode fazer; atributos (cliente, processo, sensibilidade, vertical, vínculo) definem sobre o que. A decisão final é sempre combinada, nunca apenas por papel.
- **E3. Perfis de referência.** Administrador de plataforma, curador de acervo, advogado, paralegal, analista de compliance, contador, auditor, DPO/encarregado, leitor restrito, conta de serviço de integração.
- **E4. Segregação de funções.** Quem configura política de egresso não é quem aprova egresso. Quem administra a plataforma não acessa conteúdo de cliente por padrão.
- **E5. Alçadas de egresso.** Alçadas explícitas e nomeadas: solicitar, aprovar, revogar, vetar e auditar consulta externa. A alçada é por cliente e por classe de conteúdo, *conforme especificação E7 do requisito R4*. O DPO detém veto e revogação sem alçada de aprovação; o sócio responsável aprova C3 e C4 do seu caso; todo caso com acesso a C4 tem no mínimo dois aprovadores designados na abertura; a alçada expira em 4 horas úteis com resultado negativo por omissão, *conforme decisão D4*.
- **E6. Delegação e substituição temporária.** Delegação com prazo, registrada, para ausências, sem transferência permanente de alçada.
- **E7. Contas de serviço com escopo mínimo.** Automações e integrações usam credenciais próprias, com escopo restrito e rotação periódica, e nunca herdam alçada humana.
- **E8. Revisão periódica de acessos.** Recertificação trimestral (ou semestral, conforme política) com evidência de aprovação do gestor de cada área.
- **E9. Ciclo de vida do acesso.** Provisionamento e desprovisionamento automáticos a partir do diretório corporativo; desligamento revoga acesso em minutos, incluindo sessões ativas.

---

## R8. Governança e gestão de riscos de IA

**Prioridade:** Importante · **Verticais:** todas

**Racional.** Requisito de processo, não de software, mas precisa de suporte no software para não virar documento morto.

**Especificações**

- **E1. Papéis e comitê formalizados.** Patrocinador executivo, proprietário do sistema, encarregado de dados, segurança da informação, representante de cada vertical e responsável por qualidade de modelo, com atribuições escritas.
- **E2. Inventário de casos de uso com classificação de risco.** Cada caso de uso registrado com finalidade, verticais atendidas, dados envolvidos, grau de autonomia e classificação de risco.
- **E3. Aprovação prévia para caso de alto risco.** Casos que afetam direito de terceiro, prazo processual, obrigação fiscal ou decisão sobre pessoa exigem aprovação formal antes de entrar em operação.
- **E4. Supervisão humana obrigatória.** Todo ato com efeito jurídico, contábil ou fiscal tem revisão humana identificada. O sistema registra quem revisou, quando e com qual resultado.
- **E5. Vedação de decisão automatizada vinculante.** O sistema não decide, sozinho, questão que afete direito, prazo, crédito, sanção ou obrigação de terceiro. Ele sugere, fundamenta e submete.
- **E6. Registro de decisão e racional.** Para atos relevantes, o sistema guarda a recomendação da IA, a decisão humana, a justificativa e o responsável.
- **E7. Canal de contestação.** Mecanismo para que terceiro afetado ou revisor interno conteste resultado produzido com apoio de IA, com registro de tratamento.
- **E8. Alinhamento a referencial de gestão de IA.** Estrutura compatível com ISO/IEC 42001 e com o NIST AI RMF, com evidências mapeadas por controle.
- **E9. Política de uso aceitável.** Documento assinado por cada usuário no primeiro acesso e reapresentado a cada versão relevante, com registro de aceite.

---

# BLOCO II: Conhecimento documental

## R9. Ingestão multi-formato

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** A qualidade de tudo que vem depois depende de a ingestão não perder informação. Um contrato convertido mal, uma tabela achatada ou uma nota fiscal lida pela metade contaminam busca, extração e resposta.

**Especificações**

- **E1. Cobertura de formatos primária.** PDF (nativo e digitalizado), DOC, DOCX, XLS, XLSX, PPT, PPTX, MSG, EML, TXT, CSV, RTF, ODT, ODS, ODP, HTML, XML de documentos fiscais (NF-e, NFS-e, CT-e, MDF-e), JSON e Markdown.
- **E2. Cobertura secundária.** TIFF multipágina, PDF/A, DJVU, imagens isoladas (JPG, PNG), arquivos compactados (ZIP, TAR, 7z) com varredura recursiva e controle de profundidade, e formatos setoriais conforme vertical (por exemplo DICOM em saúde e DWG em engenharia).
- **E3. Sanitização antes do parsing.** Todo arquivo passa por antivírus e por desarme de conteúdo (content disarm and reconstruction) antes de ser interpretado, com registro do resultado da verificação.
- **E4. Limites e quarentena.** Limites configuráveis de tamanho por arquivo, número de páginas, profundidade de compactação, tempo de processamento e número de objetos embutidos. Excesso vai para quarentena com notificação, nunca para falha silenciosa.
- **E5. Canais de entrada.** Upload pela interface, pasta monitorada em rede, API, conector de caixa de e-mail com anexos, conectores de GED e captura a partir de sistemas integrados, *conforme especificação E7 do requisito R33*.
- **E6. Registro de origem e custódia.** Cada documento guarda custodiante, canal de entrada, usuário ou serviço responsável, data e hora, e origem física ou lógica.
- **E7. Preservação do original.** O arquivo original é imutável e mantido separado dos derivados processados. Todo derivado referencia o original por hash.
- **E8. Proteção contra arquivos hostis.** Defesa específica contra zip bomb, entidade externa XML (XXE), macro maliciosa, PDF com JavaScript, arquivo poliglota e caminho relativo malicioso. Cada defesa tem teste próprio.
- **E9. Duas camadas de metadados.** Metadados nativos do formato (autor, criação, revisão, aplicativo) e metadados de negócio capturados na ingestão (cliente, processo, vertical, tipo), ambos pesquisáveis.
- **E10. Ingestão idempotente com fila.** Reprocessamento do mesmo arquivo não duplica registro. Falhas entram em fila de reprocessamento com backoff e contador de tentativas.
- **E11. Ingestão de volume histórico.** Capacidade de carga inicial em massa (acervo legado) com relatório de progresso, estimativa de conclusão e tratamento de itens problemáticos isolados.

---

## R10. OCR, ICR e extração de layout

**Prioridade:** Essencial · **Verticais:** jurídico, administrativo, fiscal, contábil

**Racional.** Nas verticais alvo, a maior parte do acervo real é digitalizada: peças processuais escaneadas, notas fiscais em papel, certidões, contratos assinados fisicamente. OCR ruim é a causa raiz mais comum de resposta errada em sistemas de RAG corporativo.

**Especificações**

- **E1. OCR local com modelos em português.** Motor de OCR executado no ambiente do cliente, com modelo treinado ou ajustado para português do Brasil, incluindo acentuação e caracteres próprios.
- **E2. Detecção automática de documento digitalizado.** Classificação por página entre página com camada de texto confiável e página que exige OCR, evitando re-OCR desnecessário e evitando confiar em camada de texto de qualidade duvidosa.
- **E3. Preservação de estrutura.** Extração que mantém ordem de leitura, colunas, tabelas, cabeçalho, rodapé, numeração de página e notas. Documento de duas colunas lido em ordem errada produz resposta errada.
- **E4. Tabelas convertidas em estrutura.** Tabelas extraídas como estrutura de linhas e colunas, não como texto corrido, com preservação de valores numéricos, alinhamento decimal e unidades.
- **E5. Manuscrito e baixa qualidade.** Tratamento explícito de manuscrito, carimbo, assinatura, documento torto, baixa resolução e ruído, com resultado marcado como incerto quando aplicável.
- **E6. Marcação de confiança por trecho.** Cada trecho reconhecido carrega escore de confiança. Trechos abaixo do limiar vão para fila de revisão humana e são sinalizados na resposta que os utilizar.
- **E7. Multilíngue.** Suporte a documentos em outros idiomas, com detecção automática e escolha de modelo de OCR correspondente.
- **E8. Re-OCR versionado.** Possibilidade de reprocessar um documento com versão nova de motor ou modelo, mantendo as duas versões disponíveis e registrando qual versão gerou cada resposta histórica.
- **E9. Vedação de OCR externo por padrão.** O reconhecimento ocorre localmente. Uso de serviço externo de OCR é tratado como egresso e segue integralmente o disposto em R4, inclusive pré-visualização e autorização.
- **E10. Métricas de acurácia por tipo documental.** Medição periódica de acurácia por classe de documento da vertical (contrato, petição, certidão, nota fiscal, balanço, demonstrativo), com meta declarada e relatório de desvio.

---

## R11. Normalização, versionamento e deduplicação

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Normalização textual.** Tratamento consistente de acentuação, hifenização entre linhas, espaços, numeração de página, cabeçalho repetido e caracteres de controle, preservando o texto original como referência.
- **E2. Detecção de duplicatas exata e aproximada.** Identificação por hash criptográfico e por similaridade de conteúdo, com decisão configurável entre consolidar, manter ou marcar como versão.
- **E3. Versionamento de documento.** Múltiplas versões do mesmo documento convivem, com identificação de qual é vigente, qual é histórica e qual foi substituída.
- **E4. Reconhecimento de retificação e aditivo.** Um aditivo contratual ou uma retificação de obrigação acessória é vinculado ao documento original, e o sistema sabe qual prevalece para cada efeito.
- **E5. Linhagem completa.** Todo derivado sabe de qual original veio, com qual versão de pipeline foi produzido e quando.
- **E6. Exclusão lógica.** Documento removido vira tombstone imediatamente em busca e recuperação, sem apagar a evidência de auditoria associada.
- **E7. Idempotência de pipeline.** Reexecutar o pipeline sobre o mesmo insumo produz o mesmo resultado e não gera duplicidade de chunks, vetores ou citações.

---

## R12. Classificação e taxonomia documental

**Prioridade:** Importante · **Verticais:** todas

**Racional.** Classificar corretamente é o que permite aplicar política de acesso, escolher o extrator adequado e recuperar com precisão. Sem classificação, a política de sigilo não tem onde se ancorar.

**Especificações**

- **E1. Taxonomia configurável por vertical.** Estrutura de classes e subclasses editável, com conjuntos de referência para jurídico (petição, contrato, parecer, procuração, certidão, decisão, laudo), compliance (política, denúncia, relatório de investigação), administrativo (edital, contrato administrativo, portaria, ofício), contábil (balanço, DRE, nota explicativa, razão, conciliação) e fiscal (NF-e, guia, obrigação acessória, apuração).
- **E2. Classificação híbrida.** Combinação de regras determinísticas, modelo de classificação supervisionado e modelo de linguagem local, com pesos configuráveis e fallback explícito entre as abordagens.
- **E3. Classificação de sensibilidade e sigilo.** Além do tipo documental, o sistema classifica sensibilidade, incidência de dado pessoal, incidência de dado sensível e indicação de sigilo legal.
- **E4. Extração de entidades.** Identificação de partes, CPF e CNPJ com validação de dígito, datas, valores monetários, números de processo conforme padrão CNJ, números de nota fiscal, cláusulas, tributos e prazos.
- **E5. Rotulagem humana como insumo.** Correções de classificação feitas por usuário alimentam conjunto de avaliação e realimentam o modelo, com controle de qualidade e sem promessa de treinamento automático, *conforme especificação E4 do requisito R23*.
- **E6. Incerteza explícita.** Classificação abaixo do limiar de confiança vai para fila de revisão e é usada com aviso, nunca silenciosamente.
- **E7. Versionamento de taxonomia e de modelo.** Mudança de taxonomia é versionada, com registro de impacto sobre documentos já classificados e possibilidade de reclassificação em lote.

---

## R13. Extração estruturada e enriquecimento

**Prioridade:** Importante · **Verticais:** contábil, fiscal, jurídico, administrativo

**Racional.** É o que transforma documento em dado utilizável por ERP, planilha e sistema processual. Sem extração confiável, a plataforma continua sendo só um buscador sofisticado.

**Especificações**

- **E1. Esquema por tipo documental.** Cada tipo tem esquema formal de campos obrigatórios e opcionais, validável e versionado.
- **E2. Extração com âncora de origem.** Todo campo extraído aponta para página, coordenada e trecho que o originou, permitindo conferência imediata.
- **E3. Validação de consistência.** Regras de negócio aplicadas na extração: soma de itens conferindo com total, data de vencimento posterior à de emissão, CNPJ válido, alíquota dentro de faixa plausível, sequência de numeração coerente.
- **E4. Tratamento de tabelas e séries.** Extração de demonstrativos contábeis, apurações fiscais e planilhas com preservação de séries temporais e de hierarquia de contas.
- **E5. Cruzamento entre documentos.** Capacidade de comparar o mesmo fato em fontes distintas, como nota fiscal contra registro no SPED contra lançamento no razão, apontando divergências.
- **E6. Saída consumível.** Exportação em JSON, CSV, planilha e via API, com esquema estável e versionado para integração com ERP, sistema processual e ferramenta de BI.
- **E7. Revisão e aprovação de extração.** Fluxo de conferência humana para campos de alto impacto, com registro de aprovador e de divergência entre extração e correção.
- **E8. Extração reprocessável e auditável.** Reexecutar extração com versão nova de modelo gera nova versão do resultado sem sobrescrever a anterior, preservando histórico.

---

## R14. Indexação e busca híbrida

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** É o coração da utilidade. Busca puramente vetorial erra em número de processo, CNPJ e termo jurídico exato; busca puramente lexical erra em paráfrase. As verticais alvo exigem as duas, com filtros de governança aplicados no próprio índice.

**Especificações**

- **E1. Busca híbrida nativa.** Combinação de índice lexical (BM25) e índice vetorial denso, com fusão de resultados configurável e reranking posterior.
- **E2. Embeddings gerados localmente.** Nenhum texto é enviado a serviço externo para vetorização no modo padrão.
- **E3. Múltiplos modos de consulta.** Busca por linguagem natural, por palavra-chave exata, por entidade (parte, CNPJ, número de processo), por intervalo de datas e por valor monetário.
- **E4. Reranking local.** Modelo de reranking executado no ambiente do cliente para ordenar os candidatos recuperados.
- **E5. Filtros de governança aplicados no índice.** A restrição por tenant, cliente, processo, sensibilidade e data é aplicada na camada de índice, não apenas filtrada depois na aplicação. Um erro de aplicação não pode produzir vazamento entre acervos.
- **E6. Facetas e navegação.** Refinamento por tipo documental, cliente, período, vertical, classificação e custodiante.
- **E7. Busca em números e tabelas.** Consultas sobre valores, datas e séries extraídas, não apenas sobre texto.
- **E8. Reindexação incremental e total.** Atualização incremental em tempo próximo ao real, e reindexação completa planejada para troca de modelo de embedding, *conforme especificação E6 do requisito R21*.
- **E9. Escala comprovada.** Operação demonstrável com acervo de milhões de páginas, com latência declarada e medida nessa escala.
- **E10. Busca federada entre acervos autorizados.** Um usuário com vínculo a múltiplos acervos consulta todos em uma pergunta, com resultados identificados por acervo de origem.

---

## R15. Recuperação aumentada com grounding e citação

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Para as verticais alvo, uma resposta sem fonte não é resposta: é risco. O requisito é que a plataforma prefira dizer "não encontrei" a produzir algo plausível e errado.

**Especificações**

- **E1. Resposta ancorada.** Toda afirmação factual sobre o acervo é sustentada por trecho recuperado, e o sistema não afirma fato documental sem âncora.
- **E2. Citação obrigatória e navegável.** Cada afirmação traz referência a documento, página e trecho, com abertura do original no ponto exato ao clique.
- **E3. "Não encontrado" como resposta de primeira classe.** A ausência de base suficiente produz resposta explícita de não encontrado, com sugestão de reformulação ou de ampliação de escopo. A taxa de abstenção correta é medida, *conforme especificação E7 do requisito R19*.
- **E4. Declaração de cobertura.** A resposta informa sobre qual acervo, período e escopo foi produzida, e sinaliza quando a pergunta aparenta extrapolar a base disponível.
- **E5. Distinção visual entre origem local e externa.** Conteúdo produzido com apoio de modelo externo é visualmente distinto e rotulado, *conforme especificação E12 do requisito R4*.
- **E6. Comparação multi-documento.** Comparação estruturada entre contratos, versões, propostas ou apurações, com apontamento de divergências e referência a cada fonte.
- **E7. Estratégia de chunking configurável.** Segmentação ajustável por tipo documental, com preservação de contexto de cláusula, seção e página, e não por tamanho fixo cego.
- **E8. Escopo de consulta controlado pelo usuário.** Escolha explícita entre pesquisar todo o acervo autorizado, um cliente, um processo ou um conjunto de documentos selecionados.
- **E9. Memória de conversa com contenção.** Histórico de conversa é mantido com política de retenção própria e não é usado para enriquecer consulta de outro usuário ou de outro acervo.
- **E10. Sumarização com limites declarados.** Sumários de documento ou conjunto indicam o que foi lido, o que foi omitido por limite de contexto e qual a cobertura efetiva.

---

## R16. Ciclo de vida, retenção e descarte

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Política de retenção por classe.** Prazos definidos por tipo documental e por base legal, com valores de referência para prazo fiscal, prazo processual, prazo contratual e prazo de guarda de prontuário.
- **E2. Descarte seguro verificado.** Eliminação que alcança original, derivados, chunks, vetores, cache, réplicas e backups dentro da janela definida, com verificação posterior.
- **E3. Suspensão de descarte por litígio.** Marcação de preservação legal (legal hold) que sobrepõe a política de retenção e bloqueia descarte automático, com registro de quem solicitou e por qual motivo.
- **E4. Exportação e portabilidade.** Exportação completa do acervo de um cliente em formato aberto e documentado, incluindo metadados e linhagem.
- **E5. Eliminação a pedido do titular.** Eliminação de dados de titular específico propagada para índice, vetores e cache, com certificado de execução, *conforme especificação E3 do requisito R2*.
- **E6. Expurgo de cache e log.** Expiração automática de cache de prompt e de resposta, e de logs que contenham conteúdo, respeitando os prazos de auditoria.
- **E7. Certificado de descarte.** Documento verificável, com hash e carimbo de tempo, atestando o que foi eliminado e quando.

---

# BLOCO III: Modelos, orquestração e qualidade

## R17. Runtime de modelos locais

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** A escolha de runtime e de família de modelo define o custo de hardware, a latência e a qualidade possível. Precisa ser substituível: o modelo de hoje não será o de daqui a doze meses.

**Especificações**

- **E1. Modelo de linguagem local plugável.** Suporte a famílias abertas com licença compatível com uso comercial, executadas por runtime local (por exemplo llama.cpp, Ollama, vLLM ou TGI), sem dependência de provedor de API.
- **E2. Modelo de embedding local.** Vetorização com modelo multilíngue adequado a português, com versão fixada e registrada por índice.
- **E3. Modelo de reranking local.** Cross-encoder executado localmente para ordenação de candidatos.
- **E4. Modelos especializados locais.** OCR, análise de layout, reconhecimento de entidade e classificação executados localmente, sem chamada externa.
- **E5. Quantização com trade-off declarado.** Perfis de quantização documentados com impacto medido em qualidade e em memória, para que a escolha seja informada e não acidental.
- **E6. Portabilidade de hardware.** Execução em CPU, GPU NVIDIA, GPU AMD, Apple Silicon e aceleradores neurais quando disponíveis, com perfil de implantação por combinação.
- **E7. Inferência em lote e em fluxo.** Processamento em lote para ingestão e extração, e resposta em fluxo para interação, com fila separada para cada tipo de carga.
- **E8. Isolamento de execução de modelo.** Runtime confinado em processo ou container com permissões mínimas e sem acesso à rede no modo air-gapped.
- **E9. Troca de modelo sem interrupção.** Substituição de modelo em operação com drenagem gradual, possibilidade de reverter e registro de qual versão atendeu cada requisição.
- **E10. Licenciamento verificado.** Cada peso de modelo tem licença registrada e verificada quanto a uso comercial, redistribuição e restrição de finalidade, com parecer jurídico arquivado.

---

## R18. Orquestração de agentes e fluxos

**Prioridade:** Importante · **Verticais:** jurídico, compliance, contábil

**Especificações**

- **E1. Orquestração com estado.** Fluxos multi-etapa com estado persistido, retomada após falha e histórico de execução consultável.
- **E2. Ferramentas controladas.** Catálogo fechado de ferramentas disponíveis ao agente (busca no acervo, extração de campo, cálculo, comparação, geração de minuta, consulta a sistema integrado), cada uma com escopo e permissão próprios.
- **E3. Limites de execução.** Tetos de iterações, de tempo, de tokens e de chamadas a ferramentas por execução, com interrupção limpa ao atingir o limite.
- **E4. Aprovação humana em pontos de decisão.** Pontos de parada configuráveis onde o fluxo aguarda revisão e aprovação antes de prosseguir.
- **E5. Fluxos de referência por vertical.** Conjunto entregue pronto: revisão de contrato, due diligence em data room, análise de peça processual, conciliação contábil, conferência de obrigação acessória, triagem de denúncia.
- **E6. Reprodutibilidade.** Parâmetros determinísticos (temperatura, semente, versão de modelo, versão de prompt) registrados por execução, permitindo reprodução fiel.
- **E7. Degradação graciosa.** Falha de uma ferramenta não derruba o fluxo: o sistema informa a etapa comprometida e entrega o resultado parcial com o escopo declarado.
- **E8. Rastreamento por execução.** Traço completo de cada execução, com etapas, ferramentas chamadas, insumos e saídas, disponível para auditoria.
- **E9. Isolamento de execução de código.** Quando houver geração e execução de código, o ambiente é efêmero, sem rede e sem acesso ao acervo além do escopo da tarefa.
- **E10. Vedação de egresso implícito por ferramenta.** Nenhuma ferramenta do agente pode acionar serviço externo. Egresso só existe pelo broker, *conforme especificação E3 do requisito R4*.

---

## R19. Qualidade de resposta e anti-alucinação

**Prioridade:** Essencial · **Verticais:** todas, crítico em jurídico e fiscal

**Racional.** Na advocacia e na área fiscal, uma citação de julgado inexistente ou de dispositivo revogado destrói a credibilidade de toda a plataforma. Este requisito é o que separa uma ferramenta de demonstração de uma ferramenta de produção.

**Especificações**

- **E1. Portões de qualidade por tarefa.** Fidelidade ao documento, aderência ao contexto recuperado, precisão de citação, correção de abstenção e completude são medidas por vertical e por caso de uso, e convertidas em cinco portões com consequência definida: Q1 integridade de citação em 100%, Q2 extração validável em 99,5% e 100% em campos com validação algorítmica, Q3 classificação em 95% top-1 e 99% top-3, Q4 fidelidade em 95% com zero afirmação sem âncora, Q5 abstenção correta em 85% com no máximo 2% de erro confiante. Tarefa que não atinge o portão **não é oferecida em Modo A**, *conforme decisão D2*.
- **E2. Validação de citação contra o índice.** Toda referência produzida é verificada contra o acervo real. Citação que não corresponde a trecho existente é sinalizada e a resposta é bloqueada ou rebaixada.
- **E3. Vedação de citar fonte não recuperada.** O sistema não produz referência a jurisprudência, súmula, dispositivo legal, artigo ou precedente que não esteja na base local ou em fonte previamente validada.
- **E4. Verificação de vigência normativa.** A base de legislação carrega estado de vigência, e o sistema sinaliza quando a norma citada está revogada, alterada ou com eficácia suspensa.
- **E5. Cálculo determinístico fora do modelo.** Prazos processuais, contagem de dias úteis, correção monetária, juros, tributos e encargos são calculados por componente determinístico auditável, nunca por geração de linguagem, com o cálculo apresentado em memória.
- **E6. Verificação por segunda passagem.** Camada de verificação que confronta a resposta com os trechos-fonte e aponta afirmações sem sustentação, aplicada por padrão em casos de alto risco.
- **E7. Limiares de confiança e aviso.** Escore de confiança por resposta, com aviso explícito ao usuário quando abaixo do limiar e recomendação de revisão integral. A defasagem tolerada em relação ao modelo de referência em nuvem é de até 5 pontos percentuais em extração e classificação, 10 em recuperação e resumo e 20 em raciocínio e redação, este último condicionado a revisão humana obrigatória, *conforme especificação E4 do requisito R8*, com meta de convergência para 10 pontos em 18 meses, *conforme decisão D2*.
- **E8. Rotulagem de conteúdo gerado por IA.** Saídas trazem marcação de origem gerada por IA, e exportações carregam essa marcação, atendendo a deveres de transparência.
- **E9. Retroalimentação de erros.** Mecanismo de registro de erro pelo usuário, com triagem, causa raiz e entrada no conjunto de avaliação, *conforme especificação E1 do requisito R22*.
- **E10. Conjunto dourado por vertical.** Base de perguntas e respostas de referência, revisada por especialista, usada como critério de liberação de versão.

---

## R20. Gateway técnico de IA externa

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** R4 define o que deve acontecer; R20 define como construir. Separar os dois permite que a política mude sem reescrever a integração, e que a integração mude sem reabrir a política.

**Especificações**

- **E1. Motor de política externo à aplicação.** Regras de egresso escritas em linguagem de política declarativa (por exemplo OPA ou Cedar), versionadas em repositório e avaliadas pelo gateway, não codificadas em condicionais de aplicação.
- **E2. Adaptadores por provedor.** Interface comum de requisição e resposta, com adaptador específico por provedor, permitindo troca de provedor sem alteração de política.
- **E3. Normalização de metadados.** Versão de modelo, janela de contexto, custo por token, região e política de retenção declarada, padronizados e registrados em cada chamada.
- **E4. Cache de resposta externa com política.** Cache opcional, com prazo, escopo por cliente e expiração automática, jamais compartilhado entre acervos distintos.
- **E5. Controle de custo e cota.** Medição e limite de gasto por provedor, por cliente e por período, com bloqueio ao atingir o teto e alerta antecipado.
- **E6. Resiliência.** Timeout, tentativa com recuo exponencial, disjuntor por provedor e fila de reenvio, sem nunca transformar falha em envio duplicado silencioso.
- **E7. Registro de versão e data de corte.** Para cada chamada, registro da versão do modelo externo efetivamente utilizada e da data de corte de conhecimento declarada.
- **E8. Modo sem conteúdo do cliente.** Fluxo separado para consulta de conhecimento geral, com verificação automática de que o payload não contém conteúdo documental antes de classificar como consulta simples.
- **E9. Testes de contrato e verificação contínua.** Testes automatizados por adaptador e verificação periódica de que o provedor mantém as condições contratadas, com alerta em mudança.
- **E10. Desativação granular.** Desligamento por provedor, por modelo, por cliente ou global, com efeito imediato e registro.

---

## R21. MLOps local e ciclo de vida de modelos

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Registro de modelos.** Catálogo com versão, hash do peso, licença, origem, data de incorporação e casos de uso aprovados.
- **E2. Distribuição offline.** Atualização de modelo por mídia física ou repositório interno, com verificação de assinatura e integridade, adequada a ambiente air-gapped.
- **E3. Reversão.** Retorno à versão anterior em uma operação, com preservação do índice e dos artefatos compatíveis.
- **E4. Portão de qualidade.** Modelo só é promovido após aprovação no conjunto de avaliação da vertical e sem regressão nas métricas definidas em R19.
- **E5. Versionamento de prompt.** Prompts tratados como código, com versionamento, revisão e histórico de mudanças e de resultados associados.
- **E6. Acoplamento entre modelo de embedding e índice.** Troca de modelo de embedding dispara reindexação planejada, com janela de convivência e registro de qual índice atendeu cada consulta, *conforme especificação E8 do requisito R14*.
- **E7. Avaliação comparativa interna.** Comparação entre versões candidatas com o mesmo conjunto de avaliação antes da promoção.
- **E8. Governança de mudança.** Toda mudança de modelo, prompt ou índice passa por aprovação registrada e comunicação aos usuários afetados.

---

## R22. Avaliação contínua e benchmarking

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Sem medição, a decisão sobre qual modelo usar, qual hardware comprar e se a qualidade é suficiente vira opinião. Em ambiente offline, onde não se pode trocar de modelo por API em um clique, medir é ainda mais crítico.

**Especificações**

- **E1. Conjunto de avaliação por vertical e por tarefa.** Base revisada por especialista, com perguntas, respostas esperadas, fontes corretas e casos de abstenção obrigatória.
- **E2. Avaliação automática e amostragem humana.** Métricas automáticas em toda liberação, complementadas por revisão humana amostral com critério estatístico declarado.
- **E3. Teste de regressão obrigatório.** Nenhuma mudança de modelo, prompt, índice ou pipeline é promovida sem execução e aprovação no conjunto de regressão.
- **E4. Comparativo de modelos locais.** Avaliação periódica de modelos candidatos no acervo real do cliente, com relatório de qualidade, latência, memória e custo por perfil de hardware.
- **E5. Métricas de negócio.** Tempo médio de análise, taxa de retrabalho, número de achados em due diligence, redução de tempo de elaboração de peça, taxa de aceitação de sugestão.
- **E6. Relatório periódico de qualidade.** Publicação mensal com métricas, incidentes, causas e ações, acessível a gestão e a auditoria.
- **E7. Detecção de deriva.** Monitoramento de mudança no mix documental e no padrão de perguntas, com alerta quando a distribuição se afasta do conjunto de avaliação.
- **E8. Avaliação de egresso.** Medição do ganho real obtido nas consultas externas, para que a exceção ao padrão offline seja justificada por resultado e não por hábito. A medição compara execução com e sem egresso no mesmo conjunto dourado e é o dado que decide a revisão do regime, *conforme decisão D1*.
- **E9. Referência de comparação declarada e versionada.** Todo relatório de defasagem registra a versão do modelo local, a versão do modelo de referência, a data, o conjunto dourado utilizado e o tamanho da amostra. Comparar com "o melhor modelo disponível" sem fixar versão produz número que não se reproduz no trimestre seguinte, *conforme especificação E7 do requisito R19*.
- **E10. Portão de qualidade como critério de liberação.** Nenhuma vertical ou tarefa entra em produção sem atingir os portões de *especificação E1 do requisito R19*; falha em duas avaliações consecutivas retira a tarefa do escopo de Modo A, *conforme decisão D2*.

---

## R23. Adaptação ao domínio

**Prioridade:** Importante · **Verticais:** jurídico, contábil, fiscal

**Especificações**

- **E1. Glossários e dicionários de domínio.** Vocabulário jurídico, contábil e fiscal com sinônimos, expressões consagradas, siglas e correção de termos, aplicado na indexação e na consulta.
- **E2. Modelos de tarefa e exemplos por vertical.** Conjunto de instruções e exemplos de referência para cada tarefa típica (resumir peça, extrair cláusula, comparar apuração), versionado e avaliado.
- **E3. Ajuste fino local quando justificado.** Capacidade de ajuste fino ou de adaptadores leves executados localmente, quando houver volume, base legal e ganho demonstrado em avaliação.
- **E4. Vedação de treinamento sem base legal.** Nenhum ajuste de modelo usa dado de cliente sem base legal específica, avaliação de impacto e anonimização ou pseudonimização verificada.
- **E5. Base de conhecimento interna.** Políticas, teses, modelos de peça, pareceres anteriores e material de referência indexados separadamente do acervo de cliente, com origem identificada.
- **E6. Atualização normativa e jurisprudencial.** Base de legislação e de jurisprudência atualizada por processo controlado, com data de referência visível e trilha de origem. No MVP, este é o requisito R17 de [04-mvp-matriz.md](04-mvp-matriz.md), com pipeline de sincronização por commit a partir de repositório público, segmentação por artigo e proveniência em cada citação.
- **E7. Personalização por organização.** Ajuste de taxonomia, prompts, limiares e políticas por escritório, departamento ou empresa, sem contaminar configuração de outro.

---

# BLOCO IV: Segurança, isolamento e infraestrutura

## R24. Criptografia e proteção de dados

**Prioridade:** Essencial · **Verticais:** todas

**Especificações**

- **E1. Criptografia em repouso.** Criptografia de volume somada a criptografia por objeto, com chave por acervo ou por tenant quando exigido.
- **E2. Criptografia em trânsito.** TLS obrigatório entre todos os componentes e autenticação mútua entre serviços internos.
- **E3. Gestão de chaves.** Armazenamento em módulo dedicado (KMS ou HSM) no ambiente do cliente, com rotação periódica, separação de deveres e registro de uso.
- **E4. Proteção do índice vetorial.** Vetores tratados como dado sensível, com criptografia em repouso e controle de acesso equivalente ao do texto que os originou.
- **E5. Proteção de backup.** Backups cifrados, com chave distinta da chave de produção e teste de restauração.
- **E6. Prevenção de perda de dados local.** Detecção de dados pessoais e sensíveis em saídas, com bloqueio ou alerta configurável em exportação, cópia e envio.
- **E7. Sanitização de ambiente de teste.** Ambiente de homologação opera com dados sintéticos ou anonimizados, com verificação de que não houve importação indevida de produção.
- **E8. Destruição criptográfica.** Eliminação de acervo que inclui destruição da chave correspondente, tornando dados irrecuperáveis de forma verificável.

---

## R25. Isolamento e segregação multi-tenant

**Prioridade:** Essencial · **Verticais:** jurídico, contábil, compliance

**Racional.** Escritórios de advocacia e empresas de auditoria guardam acervos de clientes concorrentes no mesmo sistema. Um vazamento cruzado é falha catastrófica, não incidente menor.

**Especificações**

- **E1. Multi-tenant com namespace por tenant.** Separação lógica rigorosa em armazenamento, índice, cache e logs, com identificador de tenant obrigatório em toda consulta.
- **E2. Isolamento físico opcional.** Possibilidade de instância ou cluster dedicado para cliente de alto sigilo, quando contratualmente exigido.
- **E3. Isolamento de índice por escopo.** Índices separados por cliente, processo ou conjunto sigiloso, com impossibilidade técnica de consulta cruzada não autorizada, *conforme especificação E5 do requisito R14*.
- **E4. Sessão de modelo sem estado compartilhado.** Nenhum contexto, cache ou memória de conversa é compartilhado entre usuários, sessões ou tenants.
- **E5. Segregação de segredo de justiça.** Acervo sigiloso em partição própria, com política de acesso e de egresso mais restritiva que a política geral, *conforme especificação E2 do requisito R3*.
- **E6. Isolamento de rede e de carga de trabalho.** Namespaces de rede, políticas de tráfego entre serviços e limites de recurso por tenant.
- **E7. Defesa contra vazamento por cache e por prompt.** Chaves de cache incluem tenant e escopo; nenhum cache semântico é compartilhado entre acervos.
- **E8. Testes de isolamento auditáveis.** Suíte que tenta, de forma sistemática, acessar acervo de outro tenant por busca, por citação, por API e por manipulação de identificador, com resultado reportado.

---

## R26. Infraestrutura e aceleração

**Prioridade:** Essencial · **Verticais:** todas

**Especificações**

- **E1. Perfis de implantação definidos.** Perfil de piloto (estação de trabalho com GPU única), perfil de departamento (servidor com GPU), perfil corporativo (cluster com GPU e separação de cargas), cada um com especificação de hardware publicada.
- **E2. Dimensionamento por volume.** Fórmula publicada relacionando páginas indexadas, usuários simultâneos, consultas por hora e tamanho de modelo ao hardware necessário.
- **E3. Suporte a múltiplos ambientes.** Operação em servidor físico, máquina virtual, contêiner e nuvem privada dedicada, com o mesmo pacote de instalação.
- **E4. Requisitos de rede documentados.** Lista de portas, protocolos e destinos necessários, com a informação explícita de que no modo padrão não há destino externo.
- **E5. Instalação offline.** Pacote de instalação completo, com todas as dependências, verificável por assinatura, instalável sem acesso à internet.
- **E6. Consumo e refrigeração.** Consumo elétrico estimado por perfil, requisitos de refrigeração e de espaço em rack, para planejamento predial.
- **E7. Alternativa sem GPU.** Modo de operação apenas em CPU, com desempenho e limitações declarados, viabilizando piloto de baixo custo e validação de conceito.
- **E8. Compatibilidade com o parque existente.** Suporte a Linux e Windows Server, com requisitos de virtualização e de armazenamento declarados.

---

## R27. Desempenho e escalabilidade

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Objetivos de nível de serviço declarados.** Metas publicadas para latência de busca, tempo até o primeiro token, tempo total de resposta e throughput de ingestão, medidas em hardware de referência.
- **E2. Escala horizontal.** Capacidade de adicionar nós de indexação e de inferência sem redesenho, com distribuição de carga e particionamento do índice.
- **E3. Filas com prioridade.** Separação entre cargas interativas e cargas de lote, com prioridade para o usuário em interação e limites para ingestão em massa.
- **E4. Cache semântico.** Reaproveitamento de respostas para consultas equivalentes dentro do mesmo escopo, com invalidação ao atualizar o acervo.
- **E5. Planejamento de pico.** Dimensionamento e teste para picos previsíveis do negócio: fechamento fiscal, prazo processual concentrado, auditoria anual, campanha de due diligence.
- **E6. Testes de carga com evidência.** Relatório de teste de carga reproduzível, por perfil de implantação, disponível ao cliente antes da contratação.
- **E7. Degradação controlada.** Ao atingir limite, o sistema reduz funcionalidade de forma previsível e informada, em vez de falhar de modo opaco.

---

## R28. Disponibilidade, backup e continuidade

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Metas de recuperação por criticidade.** RPO e RTO definidos e acordados por classe de serviço, com distinção entre acervo, índice, configuração e log de auditoria.
- **E2. Backup completo e incremental.** Cobertura de originais, derivados, índice, configuração, modelos e logs, com verificação de integridade após cada execução.
- **E3. Restauração testada.** Teste periódico de restauração documentado, com tempo medido e relatório de sucesso, não apenas promessa.
- **E4. Operação degradada.** Capacidade de manter busca e consulta ao acervo mesmo com indisponibilidade do componente de geração de linguagem.
- **E5. Continuidade e sítio secundário.** Plano de continuidade com procedimento de ativação e, quando exigido, réplica em sítio secundário dentro da jurisdição autorizada.
- **E6. Independência do fornecedor no núcleo.** O acervo, o índice e os derivados permanecem legíveis e exportáveis sem o fornecedor, evitando aprisionamento e garantindo continuidade em caso de descontinuidade comercial.

---

## R29. Observabilidade e SLOs

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Métricas em três camadas.** Infraestrutura (CPU, memória, GPU, disco, rede), aplicação (requisições, erros, latência) e pipeline de conhecimento (fila de ingestão, taxa de OCR, cobertura de índice).
- **E2. Traço de consulta ponta a ponta.** Visualização do caminho completo de uma consulta, com tempo por etapa, documentos recuperados e decisões de política aplicadas.
- **E3. Logs estruturados sem dado pessoal por padrão.** Registro com estrutura padronizada, mascarando conteúdo sensível e permitindo correlação por identificador.
- **E4. Alertas acionáveis.** Alertas para falha de ingestão, tentativa de egresso negada, degradação de latência, esgotamento de disco, falha de backup e anomalia de acesso.
- **E5. Painéis por tenant e por vertical.** Visões separadas para operação, gestão e auditoria, com filtro por cliente e por área.
- **E6. Painel dedicado de egresso.** Visão consolidada das consultas externas com solicitante, aprovador, destino, volume e resultado, *conforme especificação E4 do requisito R6*.
- **E7. Custo unitário visível.** Custo por documento processado, por consulta e por usuário ativo, disponível para gestão.

---

## R30. Administração e configuração

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Console administrativo completo.** Gestão de usuários, acervos, taxonomias, políticas, modelos e integrações em interface única, com registro de toda alteração.
- **E2. Política como código.** Toda regra de acesso e de egresso versionada em repositório, revisável por diferença e promovível por esteira controlada, *conforme especificação E1 do requisito R20*.
- **E3. Aprovação de mudança de política.** Alteração de política de egresso, de retenção ou de sensibilidade exige aprovação de segundo ator e entra em vigor com registro de quem autorizou.
- **E4. Gestão de vocabulário controlado.** Manutenção de taxonomia, glossário, sinônimos e modelos de documento pelo próprio cliente, sem dependência do fornecedor.
- **E5. Simulação de política.** Recurso que responde "o que aconteceria se" para uma consulta, um documento ou um usuário, antes de publicar a mudança.
- **E6. Exportação de configuração.** Exportação integral da configuração para auditoria, comparação entre ambientes e reconstrução após incidente.
- **E7. Interface multilíngue.** Console e interface disponíveis em português e inglês no mínimo, com estrutura preparada para outros idiomas.

---

# BLOCO V: Verticais, integrações e pessoas

## R31. Integrações jurídicas e processuais

**Prioridade:** Importante · **Verticais:** jurídico, administrativo

**Especificações**

- **E1. Captura de sistemas processuais.** Integração com PJe, e-SAJ e portais de tribunais superiores para captura de peças e movimentações de acesso público, respeitando limites de uso e termos dos provedores.
- **E2. Integração com gestão de escritório.** Conectores para sistemas de gestão jurídica usuais do mercado, com sincronização de cliente, processo, prazo e documento.
- **E3. Diários oficiais e publicações.** Captura de publicações e vinculação automática ao processo e ao responsável.
- **E4. Cálculo de prazos.** Componente determinístico de contagem de prazo com calendário de feriados nacional, estadual e forense, com memória de cálculo auditável, *conforme especificação E5 do requisito R19*.
- **E5. Assinatura e certificação digital.** Integração com padrão ICP-Brasil e com a Lei 14.063/2020 para assinatura de documentos produzidos na plataforma.
- **E6. Base própria de teses e precedentes.** Indexação do acervo interno de pareceres, teses e precedentes do escritório, separado do acervo de cliente e com origem identificada.
- **E7. Distinção rigorosa entre público e sigiloso.** Documento obtido de fonte pública e documento sigiloso têm tratamento distinto de indexação, recuperação e egresso, com marcação na origem.

---

## R32. Integrações contábeis, fiscais e ERP

**Prioridade:** Importante · **Verticais:** contábil, fiscal

**Especificações**

- **E1. Conectores de ERP.** Integração com sistemas de gestão empresarial usuais do mercado para leitura de razão, plano de contas, lançamentos e cadastros.
- **E2. Leitura de documentos fiscais eletrônicos.** Interpretação de NF-e, NFS-e, CT-e e MDF-e, com extração de itens, impostos, totais e chave de acesso.
- **E3. Obrigações acessórias do SPED.** Leitura e conferência de ECD, ECF, EFD ICMS/IPI, EFD Contribuições, EFD-Reinf e eSocial, conforme Decreto 6.022/2007 e atos correlatos.
- **E4. Conciliação automatizada.** Cruzamento entre documento, escrituração e razão, com apontamento de divergência e fila de tratamento.
- **E5. Apuração e conferência com cálculo determinístico.** Verificação de apuração de tributos por componente de cálculo auditável, nunca por geração de linguagem, *conforme especificação E5 do requisito R19*.
- **E6. Reforma tributária.** Suporte à transição para IBS e CBS nos termos da EC 132/2023 e da LC 214/2025, com parametrização por competência e convivência entre regimes.
- **E7. Preparação para auditoria e fiscalização.** Geração de dossiê organizado por exigência, com documentos, extrações e trilha de conferência.
- **E8. Sigilo fiscal preservado.** Documentos sob sigilo fiscal recebem classificação própria e restrição de recuperação cruzada mesmo dentro do mesmo grupo econômico, *conforme especificação E4 do requisito R3*.

---

## R33. Integrações de produtividade e GED

**Prioridade:** Desejável · **Verticais:** todas

**Especificações**

- **E1. Repositórios corporativos de arquivo.** Conectores para SharePoint, OneDrive, Google Drive e compartilhamentos de rede, com sincronização incremental.
- **E2. Correio eletrônico.** Captura de caixa funcional e de anexos, com preservação de cabeçalhos, conversa e cadeia de custódia.
- **E3. GED e processo eletrônico.** Conectores para sistemas de gestão documental e de processo administrativo eletrônico amplamente usados no setor público.
- **E4. Herança de permissão da origem.** O acesso ao documento indexado respeita a permissão do repositório de origem, sem ampliar acesso por conta da indexação.
- **E5. Detecção de remoção e alteração na origem.** Sincronização que identifica exclusão e alteração no repositório de origem e reflete no índice com trilha.
- **E6. API pública e webhooks.** Interface programática documentada, com autenticação, limite de uso e eventos para integração por terceiros.
- **E7. Conectores de pasta monitorada.** Monitoramento de diretório local ou de rede, com regras de inclusão, exclusão e estabilização de arquivo em escrita.

---

## R34. Casos de uso por vertical

**Prioridade:** Importante · **Verticais:** todas

**Racional.** Requisito de escopo funcional: define o que o produto precisa saber fazer em cada vertical, para que a avaliação de qualidade tenha alvo concreto.

**Especificações**

- **E1. Jurídico: revisão e comparação contratual.** Análise de contrato contra padrão do escritório, extração de cláusulas críticas, apontamento de desvio e matriz de risco.
- **E2. Jurídico: análise de peça e elaboração de minuta.** Leitura de peças processuais, resumo com linha do tempo e elaboração assistida de minuta apoiada no acervo interno.
- **E3. Jurídico: due diligence em data room.** Varredura de acervo de operação societária, com identificação de contingências, contratos relevantes e pendências.
- **E4. Jurídico: gestão de prazos e obrigações contratuais.** Extração de prazos, garantias, obrigações de fazer e gatilhos de renovação, com alerta antecipado.
- **E5. Jurídico: pesquisa sobre acervo próprio.** Consulta a pareceres, teses e precedentes internos, com citação de origem interna e distinção de fonte pública externa.
- **E6. Compliance: conheça seu cliente e prevenção à lavagem.** Análise documental de cadastro, identificação de beneficiário final, verificação de sanções e de pessoa exposta politicamente, com relatório e trilha.
- **E7. Compliance: políticas, denúncias e investigação.** Indexação de políticas internas, triagem de denúncia, apoio à investigação com preservação de sigilo e cadeia de custódia.
- **E8. Compliance: privacidade e atendimento ao titular.** Mapeamento de dados pessoais no acervo, resposta a requisição de titular e produção de insumos para avaliação de impacto.
- **E9. Administrativo: licitações e contratos administrativos.** Análise de edital, verificação de requisitos de habilitação, apoio à elaboração de proposta e gestão de contrato conforme Lei 14.133/2021.
- **E10. Administrativo: processo administrativo e pareceres.** Apoio à instrução processual, recuperação de precedentes administrativos internos e elaboração de minuta de parecer.
- **E11. Contábil: leitura de demonstrações.** Extração de demonstrações contábeis, notas explicativas e comparativo entre exercícios, com validação de consistência.
- **E12. Contábil: auditoria e papéis de trabalho.** Apoio a testes de substantivo, seleção de amostra documental, conferência de saldos e montagem de papéis de trabalho.
- **E13. Fiscal: conferência de obrigações e risco de autuação.** Verificação de obrigações acessórias, identificação de inconsistência e avaliação de exposição.
- **E14. Fiscal: crédito e tese tributária.** Recuperação de crédito, análise de tese aplicável ao caso e quantificação com cálculo auditável.
- **E15. Outras verticais.** Trabalhista e RH (acordos, convenções, processos), saúde (prontuário e protocolo com isolamento reforçado), seguros (apólice, sinistro, regulação), engenharia e imobiliário (contrato, memorial, matrícula).

---

## R35. Experiência do usuário e acessibilidade

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Vinculado à premissa P5: se a experiência local for pior que a alternativa em nuvem, o usuário contorna a política. A usabilidade é, aqui, um controle de segurança.

**Especificações**

- **E1. Integração ao fluxo de trabalho.** Acesso por navegador, aplicação desktop e complementos para editor de texto, planilha e cliente de e-mail, evitando que o usuário saia do ambiente para consultar.
- **E2. Leitura lado a lado.** Visualização simultânea de documento original e resposta, com destaque do trecho citado e navegação por página.
- **E3. Indicador permanente de modo.** A interface informa, de forma sempre visível, se a interação está em modo local ou com participação externa, sem depender de o usuário lembrar.
- **E4. Transparência sobre limites.** Mensagens claras quando a base não cobre a pergunta, quando a confiança é baixa e quando há alternativa disponível, sem jargão técnico.
- **E5. Desempenho percebido.** Tempo até o primeiro token compatível com uso interativo, com indicação de progresso durante etapas longas de OCR e análise.
- **E6. Acessibilidade.** Conformidade com WCAG 2.2 nível AA, navegação por teclado, compatibilidade com leitor de tela e contraste adequado.
- **E7. Idioma.** Interface e modelos em português do Brasil, com capacidade de processar e responder em outros idiomas quando o acervo exigir.
- **E8. Onboarding curto.** Primeiro uso produtivo em menos de trinta minutos, com acervo de exemplo e roteiro guiado.

---

## R36. Capacitação e gestão de mudança

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Trilha de treinamento por perfil.** Conteúdo distinto para usuário final, curador de acervo, administrador e aprovador de egresso, com avaliação de aprendizagem.
- **E2. Política de uso aceitável assinada.** Termo com o que é permitido, o que é proibido, o que constitui egresso e qual a responsabilidade do usuário, *conforme especificação E9 do requisito R8*.
- **E3. Rede de multiplicadores.** Papéis de referência por área, com materiais e canal de dúvidas.
- **E4. Medição de adoção.** Indicadores de uso ativo, retenção de usuários, distribuição por vertical e motivos de não adesão.
- **E5. Comunicação sobre limites e riscos.** Material recorrente sobre o que a IA local faz bem, o que faz mal e o que exige verificação humana obrigatória.
- **E6. Laboratório seguro de prática.** Ambiente com acervo sintético para treinar sem risco de exposição de dado real, *conforme especificação E9 do requisito R1*.

---

# BLOCO VI: Economia, implantação e evolução

## R37. Custo total de propriedade e economicidade

**Prioridade:** Importante · **Verticais:** todas

**Racional.** A pergunta que decide a compra raramente é "é seguro?". É "quanto custa comparado a colar texto no ChatGPT?". O requisito é tornar essa comparação possível com número, não com discurso.

**Especificações**

- **E1. Comparativo estruturado de custo.** Modelo aberto comparando custo de infraestrutura própria (aquisição, depreciação, energia, refrigeração, espaço, operação) com custo de consumo de API externa equivalente em volume. A depreciação de hardware com GPU é calculada em **três anos**, não em cinco: o ciclo útil para acompanhar modelos abertos competitivos é mais curto que o de servidor tradicional, e usar cinco anos superestima a vantagem do on-premise em cerca de 40%, *conforme decisão D3*.
- **E2. Custo unitário.** Custo por página indexada, por documento processado, por consulta e por usuário ativo, medido e não estimado.
- **E3. Custo de curadoria humana.** Reconhecimento explícito de que revisão, rotulagem e correção consomem horas e precisam entrar na conta.
- **E4. Previsibilidade.** Demonstração de que o custo é previsível e não indexado a preço de terceiro, que é a principal vantagem econômica do modelo local.
- **E5. Rateio interno.** Modelo de rateio por vertical, departamento ou cliente, para cobrança interna e decisão de expansão.
- **E6. Sensibilidade a escala.** Curva de custo mostrando em qual volume o modelo local passa a ser mais barato que a alternativa externa, e em qual volume deixa de ser.
- **E7. Custo da não conformidade.** Comparação com o custo de um incidente de vazamento, de uma autuação por sigilo ou de uma sanção por tratamento irregular, como parte do argumento econômico.

---

## R38. Topologia e modos de implantação

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** Os modos de operação são o vocabulário comum entre jurídico, segurança e tecnologia. Sem eles, cada área fala de um produto diferente.

**Especificações**

- **E1. Modo A: air-gapped integral.** Nenhuma rota externa, nenhum egresso, atualização por mídia física. É o modo padrão de referência, o modo de fábrica na instalação e o modo contratual na assinatura, e o que define o teto de garantia, *conforme decisão D1*.
- **E2. Modo B: local com egresso auditado.** Núcleo idêntico ao Modo A, com broker de egresso habilitado por política, com catálogo fechado de destinos e todos os controles de R4 ativos.
- **E3. Modo C: nuvem privada dedicada.** Execução em nuvem privada ou VPC dedicada do cliente, sob sua conta e sua jurisdição, com as mesmas garantias de isolamento. É o modo do piloto e uma exceção comercial, nunca o padrão de instalação, *conforme decisão D3*.
- **E4. Modo D: híbrido.** Acervo e índice locais, com possibilidade de processamento pesado em ambiente controlado do cliente, sem saída para IA de terceiro.
- **E5. Atualização e instalação offline.** Pacote completo e verificável, instalável e atualizável sem internet, com procedimento documentado, *conforme especificação E4 do requisito R1*.
- **E6. Licenciamento offline.** Mecanismo de licença que funcione sem consulta a servidor externo e sem degradação indevida por falta de conectividade.
- **E7. Contrato adequado ao modo.** Cada modo tem instrumento contratual próprio, com cláusulas de confidencialidade, de auditoria, de notificação de incidente e de subprocessadores compatíveis.
- **E8. Portabilidade entre modos.** Migração entre modos sem perda de acervo, índice, configuração ou histórico de auditoria.
- **E9. Faixas de implantação com regra objetiva de passagem.** Piloto em nuvem privada na conta do cliente até aproximadamente 50 mil páginas e 15 usuários; produção departamental em servidor on-premise entre 50 mil e 2 milhões de páginas e 15 a 100 usuários; produção com requisito de air-gap sempre on-premise. A passagem da primeira para a segunda faixa é disparada quando o custo projetado de 24 meses em nuvem exceder o custo total de aquisição do servidor equivalente, calculado com cotação real, *conforme decisão D3*.

---

## R39. Suporte, manutenção e atualização normativa

**Prioridade:** Importante · **Verticais:** todas

**Especificações**

- **E1. Níveis de serviço de suporte.** Severidades definidas, com prazo de primeira resposta e de contorno, e canal adequado a ambiente sem acesso remoto.
- **E2. Atualização de software em ambiente isolado.** Pacote de atualização com assinatura, notas de versão, procedimento de reversão e janela acordada.
- **E3. Atualização de base legal e jurisprudencial.** Processo periódico de atualização, com data de referência visível e trilha de origem de cada norma ou precedente incorporado.
- **E4. Tratamento de vulnerabilidade.** Acompanhamento de vulnerabilidades conhecidas nas dependências, com prazo de correção por severidade e comunicação ao cliente.
- **E5. Ciclo de vida declarado.** Prazo de suporte por versão, política de fim de vida e plano de migração comunicado com antecedência.
- **E6. Documentação operacional.** Runbooks de instalação, operação, backup, restauração, incidente e auditoria, mantidos atualizados.
- **E7. Resposta a incidente.** Procedimento conjunto com o cliente, com papéis definidos, prazo de comunicação e registro de lição aprendida.

---

## R40. Extensibilidade e roadmap

**Prioridade:** Desejável · **Verticais:** todas

**Especificações**

- **E1. API e kit de desenvolvimento.** Interface programática documentada, com cliente de referência e exemplos por vertical.
- **E2. Modelo de extensão.** Mecanismo formal para adicionar extrator, conector, ferramenta de agente ou modelo, sem alterar o núcleo e sem contornar as políticas de segurança.
- **E3. Novos formatos e conectores.** Processo de homologação de formato e de conector, com critérios de aceitação e testes de segurança.
- **E4. Novos modelos.** Processo de avaliação e promoção de modelo, compatível com R21 e R22.
- **E5. Novas verticais.** Processo para incorporar taxonomia, extratores, casos de uso e conjunto de avaliação de uma nova vertical.
- **E6. Governança de roadmap.** Instância de discussão com clientes para priorização, com registro de decisão e comunicação de retorno.

---

## 10. Matriz de dependências entre requisitos

Relações em que a ausência de um requisito impede ou compromete o outro.

| Requisito | Depende criticamente de | Por quê |
|---|---|---|
| R4 | R7, R20, R24, R25 | Política de egresso sem identidade, gateway, criptografia e isolamento não é aplicável |
| R5 | R4, R35 | Consentimento sem broker e sem interface clara vira aviso ignorado |
| R6 | R24, R29 | Log inviolável exige criptografia e observabilidade |
| R15 | R14, R17, R19 | Sem busca, modelo local e verificação, a resposta não tem âncora |
| R19 | R15, R22 | Anti-alucinação depende de citação e de medição contínua |
| R22 | R19, R21 | Avaliação depende de métricas definidas e de versionamento de modelo |
| R25 | R14, R24 | Isolamento exige filtro no índice e criptografia por escopo |
| R31, R32 | R13, R19 | Integração vertical sem extração estruturada e cálculo determinístico gera erro em escala |
| R34 | R12, R13, R15 | Caso de uso depende de classificação, extração e recuperação |
| R37 | R22, R29, R38 | Custo só é calculável com medição e modo de implantação definidos |
| R38 | R1, R4, R26 | Modo de operação é a materialização dos requisitos de soberania |

---

## 11. Fatiamento sugerido

**MVP: o mínimo que já é defensável** (~16 requisitos)
R1, R4, R5, R6, R7, R9, R10, R14, R15, R17, R19, R24, R25, R26, R35, R38.
Entrega: ingestão multi-formato com OCR, busca híbrida, resposta com citação, egresso bloqueado por padrão com broker e trilha de auditoria. É a menor configuração que sustenta a afirmação "não sai do ambiente e, quando sair, fica registrado".

**Onda 2: operação real** (~12 requisitos)
R2, R3, R8, R11, R12, R16, R18, R20, R21, R22, R28, R29, R30.
Entrega: conformidade operacionalizável, classificação, extração básica, ciclo de vida, MLOps e observabilidade. É o que permite passar de piloto a produção.

**Onda 3: valor por vertical** (~8 requisitos)
R13, R23, R27, R31, R32, R34, R36, R39.
Entrega: extração estruturada rica, adaptação ao domínio, integrações verticais e casos de uso completos.

**Onda 4: evolução**
R33, R37, R40.
Entrega: ecossistema, conectores amplos, modelo econômico refinado e extensibilidade.

---

## 12. Pontos para debate e decisões abertas

Itens em que a resposta correta depende de contexto que não está no pedido e que mudam materialmente o projeto. Cada um traz a tensão e o que muda conforme a escolha.

**Decididas.** D1 a D4 foram fechadas e os parâmetros resultantes já estão propagados nas especificações acima. O registro completo, com opções consideradas, justificativa e critério de reversão de cada uma, está em [03-registro-decisoes.md](03-registro-decisoes.md).

- **D1. Egresso é exceção governada.** Exceção por cliente, prazo de 90 dias, no máximo dois provedores homologados e cotas por classe de conteúdo. Refletida em R4 (E2, E9, E10), R5/E5, R38/E1 e R22/E8.
- **D2. Qualidade medida por cinco portões por tarefa.** Tarefa que não atinge o portão não é oferecida em Modo A. Refletida em R19 (E1, E7) e R22 (E9, E10).
- **D3. Três faixas de implantação com regra objetiva de passagem.** Nuvem privada para piloto, on-premise para departamento, on-premise obrigatório para air-gap, com depreciação de GPU em três anos. Refletida em R37/E1 e R38 (E3, E9).
- **D4. Aprovação em camadas por classe.** Sócio decide o caso, DPO define política e veta, aprovador nunca aprova a própria solicitação, C4 sem trilha de urgência. Refletida em R4/E7 e R7/E5.

**Em aberto.**

**D5. O acervo de cliente pode ser usado para ajuste de modelo?**
Ganho de qualidade real, mas exige base legal, avaliação de impacto e anonimização verificada. *Recomendação: não no MVP; habilitar apenas com contrato específico e por cliente, conforme R23/E4.*

**D6. Qual o escopo de integração com sistemas processuais?**
Captura de dado público de tribunal é de baixo risco; acesso a processo sigiloso com credencial do cliente muda a natureza do sistema. *Decisão contratual e jurídica, não técnica.*

**D7. Quem é o controlador dos dados no egresso?**
Quando o conteúdo do cliente vai a um provedor externo por solicitação do usuário, a cadeia controlador-operador precisa estar escrita antes do primeiro uso. *Decisão jurídica com impacto direto no desenho de R4/E17.*

**D8. Qual a postura sobre citação de jurisprudência?**
Indexar bases públicas de jurisprudência em ambiente air-gapped exige processo de atualização e verificação de vigência. Sem isso, o sistema cita precedente revogado, que é pior que não citar. *Recomendação: no MVP, responder apenas com base no acervo do cliente e declarar essa limitação de forma explícita.*

**D9. Multi-tenant forte ou instância dedicada?**
Multi-tenant reduz custo e simplifica operação, mas concentra risco. Escritórios com clientes concorrentes costumam exigir instância dedicada. *Recomendação: multi-tenant no MVP com isolamento testado por R25/E8, e instância dedicada como opção comercial.*

**D10. Qual o prazo de retenção do log de egresso?**
Curto demais compromete defesa em auditoria; longo demais cria um segundo acervo sensível. *Recomendação: alinhar ao prazo prescricional aplicável por vertical, com o log contendo hash e referência em vez de conteúdo, conforme R6/E10.*

---

## 13. Riscos e lacunas conhecidas

- **Risco de contorno humano.** O maior risco não é técnico: é o usuário copiar o documento e colar em ferramenta externa não homologada. Mitigação está em R35 (experiência) e R36 (cultura), não em R4. Se apenas R4 for implementado, o vazamento acontece por fora do sistema.
- **Qualidade de OCR em acervo legado.** Acervos com décadas de digitalização ruim produzem respostas erradas com aparência de corretas. Mitigação em R10/E6 e R19/E7.
- **Deriva de modelo.** Atualização de modelo promovida sem regressão adequada degrada silenciosamente. Mitigação em R21/E4 e R22/E3.
- **Custo de curadoria subestimado.** Projetos de IA documental costumam falhar por falta de gente para curar taxonomia, revisar extração e manter o conjunto de avaliação. Explicitado em R37/E3.
- **Fonte normativa desatualizada.** Base legal desatualizada produz resposta confiante e errada. Mitigação em R19/E4 e R39/E3.
- **Lacuna identificada, não coberta por requisito próprio:** não há requisito específico para *análise de imagem e vídeo* (audiências gravadas, laudos fotográficos, plantas). Se a vertical jurídica ou de engenharia exigir, será necessário um R41.
- **Lacuna identificada, não coberta por requisito próprio:** não há requisito para *detecção de fraude documental* (documento adulterado, assinatura falsificada, metadado inconsistente). Relevante em compliance e seguros; candidato a R42.
- **Lacuna identificada, não coberta por requisito próprio:** não há requisito para *transcrição de áudio* (audiências, reuniões, atendimento). Candidato a R43, com implicações próprias de egresso.

---

## 14. Fora de escopo desta versão

- Substituição de sistema de gestão processual, ERP ou GED: a plataforma integra, não substitui.
- Emissão de documentos fiscais: a plataforma lê e confere, não emite.
- Assinatura digital como serviço de certificação: integra com ICP-Brasil, não é autoridade certificadora.
- Treinamento de modelo de base próprio: usa modelos abertos existentes, com ajuste leve quando autorizado.
- Consultoria jurídica automatizada sem advogado responsável: vedado por R8/E5.
