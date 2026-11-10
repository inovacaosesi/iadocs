# Matriz de Requisitos: MVP

**Fase:** discovery / brainstorming · **Versão:** 1.0

Este é o documento de trabalho. Tudo aqui é hipótese para conversar, não compromisso contratual. Os números servem para dar concretude à discussão e serão recalibrados com o cliente no piloto.

---

## 1. Como este conjunto de documentos se relaciona

| Documento | Papel | Quando usar |
|---|---|---|
| **04-mvp-matriz.md** (este) | Matriz enxuta do MVP: 17 requisitos (M1 a M17), 90 especificações | Agora, no discovery |
| [03-registro-decisoes.md](03-registro-decisoes.md) | Hipóteses sobre as quatro decisões mais estruturantes | Como insumo de discussão |
| [02-matriz-decisao-egresso.md](02-matriz-decisao-egresso.md) | Como o egresso se comporta em cada classe de conteúdo | Quando for desenhar o egresso |
| [01-catalogo-requisitos.md](01-catalogo-requisitos.md) | Catálogo completo: 40 requisitos, ~349 especificações | Fase 2 e 3, como referência |
| [05-analise-de-gaps.md](05-analise-de-gaps.md) | Auditoria deste documento e do catálogo: 16 gaps priorizados | Antes de rever escopo ou numeração |

O catálogo completo não é escopo. Ele existe para garantir que nada importante seja esquecido quando o MVP crescer. No dia a dia do discovery, use este documento.

---

## 2. Premissas do MVP

Quatro, e só quatro.

1. **O MVP existe para provar uma coisa:** é possível trabalhar com o acervo sem expor o acervo, e quando algo sai, fica registrado. Tudo que não serve a essa prova fica para depois.
2. **Metas numéricas nascem no piloto, não no papel.** Definir 99,5% de acurácia antes de ver o acervo do cliente é chute com aparência de rigor.
3. **Escopo funcional é um caso de uso por vertical**, não a vertical inteira. Um caso de uso que funciona vale mais que cinco pela metade.
4. **Se o usuário contorna a solução, o MVP falhou.** Experiência ruim é falha de projeto, não problema de comportamento do usuário.

---

## 3. Visão geral

| ID | Requisito | Papel no MVP | Por que está aqui |
|---|---|---|---|
| M1 | Confidencialidade por padrão | Obrigatório | É a razão de existir do projeto |
| M2 | Consulta externa auditada | Obrigatório | É o diferencial de "parcialmente online" |
| M3 | Registro e auditoria | Obrigatório | Sem trilha não há como provar M1 e M2 |
| M4 | Acesso e permissões | Obrigatório | Não dá para separar acervo sem isso |
| M5 | Ingestão de documentos | Obrigatório | Nada acontece sem documento entrando |
| M6 | OCR e extração de texto | Obrigatório | A maior parte do acervo real é digitalizada |
| M7 | Busca | Obrigatório | Recuperar é pré-requisito de responder |
| M8 | Resposta com citação | Obrigatório | Resposta sem fonte é passivo, não produto |
| M9 | Modelo local | Obrigatório | É o motor de tudo |
| M10 | Qualidade mínima | Obrigatório | Piso, não bateria de metas |
| M11 | Segurança e isolamento | Obrigatório | Requisito de mesa para qualquer cliente |
| M12 | Infraestrutura | Obrigatório | Sem hardware definido não há piloto |
| M13 | Interface | Obrigatório | É o que decide se o usuário adota |
| M14 | Conformidade básica | Obrigatório | LGPD mínima, sem a qual não se assina |
| M15 | Modos de implantação | Obrigatório | Define o que se promete ao cliente |
| M16 | Caso de uso piloto | Obrigatório | MVP sem caso concreto vira demonstração |
| M17 | Atualização do corpus normativo | Obrigatório | O acervo do cliente tem o contrato, não tem a lei |

Dezessete requisitos próprios do MVP, numerados de M1 a M17. Tudo que estava no catálogo e não está aqui é Fase 2 ou 3, e a seção 5 diz onde encontrar.

---

## 4. Requisitos e especificações

Convenção: **E** numera dentro de cada **M**, e **M** é o identificador de requisito deste documento. O catálogo usa **R**. As duas séries são independentes e o identificador carrega o documento de origem: M é sempre da matriz de MVP, R é sempre do catálogo. Uma referência a requisito do catálogo dentro deste arquivo aparece qualificada, como *requisito R12 do catálogo*.

Marcações:
- sem marca = dentro do MVP
- **[a validar]** = depende de informação que ainda não temos
- **[Fase 2]** = registrado para não esquecer, fora do MVP

### M1. Confidencialidade por padrão

Se isso falhar, o projeto não tem razão de existir.

- **E1.** Todo o pipeline roda no ambiente do cliente: ingestão, OCR, indexação, busca, modelo e resposta.
- **E2.** A instalação nasce sem qualquer rota para serviço de IA externo.
- **E3.** Sem telemetria de terceiro. Se houver telemetria, é local e desligável.
- **E4.** Nada do acervo é usado para treinar modelo de terceiro.
- **E5.** Modo air-gapped funciona de ponta a ponta, com instalação e atualização por pacote offline.
- **E6 [a validar].** Inventário do que conta como "dado do cliente": além do arquivo, entram OCR, trechos, vetores, cache e logs.

### M2. Consulta externa auditada

É o "parcialmente online". Precisa ser visível, autorizado e registrado, sem virar burocracia que o usuário vai contornar.

- **E1.** Negado por padrão; habilitado por decisão explícita, com prazo.
- **E2.** Lista fechada de destinos permitidos, com país e política de retenção declarados.
- **E3.** Todo envio passa por um único ponto de saída, que registra. Não existe chamada direta.
- **E4.** O usuário vê o que será enviado antes do envio.
- **E5.** Nada é enviado automaticamente: se o modelo local não atende, o sistema avisa e oferece a opção, mas não executa.
- **E6.** Mascaramento simples de dado pessoal antes do envio, quando a finalidade permitir.
- **E7.** Registro de quem pediu, quem aprovou, o que foi enviado, para onde e quando.
- **E8.** Resposta de origem externa fica marcada e separada do acervo.
- **[Fase 2].** Aprovação em camadas por classe, cotas, catálogo com DPA por destino, interruptor de emergência, testes de exfiltração.

### M3. Registro e auditoria

- **E1.** Trilha por documento: quem acessou, quando, em qual consulta.
- **E2.** Trilha por resposta: resposta → trecho → página → documento.
- **E3.** Visão consolidada das consultas externas.
- **E4.** O log não pode ser apagado nem editado por administrador.
- **E5.** Exportação da trilha para auditoria e para o cliente.
- **E6 [a validar].** Prazo de retenção do log por vertical.
- **[Fase 2].** Encadeamento por hash, WORM, integração com SIEM, reconstrução de consulta.

### M4. Acesso e permissões

- **E1.** Login corporativo (SSO) e MFA para perfis administrativos.
- **E2.** Perfis básicos: administrador, curador de acervo, usuário, auditor.
- **E3.** Acesso por cliente e por processo, não apenas por área.
- **E4.** Perfil sem alçada não vê sequer a opção de consulta externa.
- **E5.** Desligamento de usuário revoga acesso em prazo curto.
- **[Fase 2].** RBAC+ABAC completo, delegação, segregação de funções, recertificação periódica.

### M5. Ingestão de documentos

- **E1.** Formatos do MVP: PDF com texto, PDF digitalizado, DOCX, XLSX, MSG/EML, TXT e CSV.
- **E2.** Entrada por upload na interface e por pasta monitorada.
- **E3.** Antivírus e quarentena para arquivo suspeito.
- **E4.** Original preservado imutável; todo derivado aponta para ele.
- **E5.** Metadados de negócio na entrada: cliente, tipo, data, responsável.
- **[a validar].** Volume inicial do acervo piloto, para dimensionar o resto.
- **[Fase 2].** XML fiscal, PPT, ODT/ODS, compactados, conectores de GED e e-mail.

### M6. OCR e extração de texto

- **E1.** OCR local com modelo em português.
- **E2.** Detecção automática entre página com texto e página que exige OCR.
- **E3.** Preservação de ordem de leitura e noção de tabela, para não embaralhar documento em colunas.
- **E4.** Trecho de baixa confiança é marcado e sinalizado na resposta que o usar.
- **E5 [a validar].** Qualidade mínima aceitável por tipo de documento, calibrada no piloto.
- **[Fase 2].** Manuscrito, tabela estruturada, re-OCR versionado, métricas por classe documental.

### M7. Busca

- **E1.** Busca por palavra-chave e por sentido, combinadas.
- **E2.** Filtros por cliente, tipo de documento e período.
- **E3.** Busca por entidade: parte, CNPJ, número de processo.
- **E4.** O resultado respeita o que o usuário pode ver, aplicado na própria busca.
- **[Fase 2].** Reranking, facetas, busca em valores e tabelas, escala acima do volume do piloto.

### M8. Resposta com citação

- **E1.** Toda resposta aponta o trecho e o documento que a sustenta.
- **E2.** Clicar na citação abre o documento na página certa.
- **E3.** "Não encontrei" é resposta aceitável e preferível a especular.
- **E4.** A resposta informa sobre qual acervo e período foi produzida.
- **E5.** Conteúdo de origem externa aparece visualmente distinto.
- **[Fase 2].** Comparação entre documentos, sumarização com escopo declarado, memória de conversa com política própria.

### M9. Modelo local

- **E1.** Modelo de linguagem aberto rodando localmente, com licença compatível com uso comercial.
- **E2.** Modelo de embedding também local.
- **E3.** Troca de modelo sem reinstalar a plataforma.
- **E4.** Perfil de hardware publicado para piloto e para produção.
- **E5 [a validar].** Qual modelo e qual quantização usar no piloto, decidido por teste no acervo real.
- **[Fase 2].** Reranker local, modelos especializados, portabilidade ampla de hardware, MLOps.

### M10. Qualidade mínima

Piso, não bateria de metas.

- **E1.** Conjunto pequeno de perguntas e respostas de referência por caso de uso piloto.
- **E2.** Toda citação é validada contra o acervo; citação inexistente bloqueia a resposta.
- **E3.** Cálculo de prazo, valor e tributo roda em componente determinístico, nunca no modelo.
- **E4.** Aviso explícito quando a confiança é baixa.
- **E5 [a validar].** Metas numéricas definidas com o cliente no início do piloto, não antes.
- **[Fase 2].** Portões formais por tarefa, avaliação contínua, benchmark entre modelos, detecção de deriva.

### M11. Segurança e isolamento

- **E1.** Criptografia em repouso e em trânsito.
- **E2.** Separação de acervo por cliente, com teste que tenta o acesso cruzado.
- **E3.** Backup criptografado com restauração testada.
- **E4.** Chaves gerenciadas no ambiente do cliente.
- **[Fase 2].** Segregação de segredo de justiça, instância dedicada, DLP, destruição criptográfica.

### M12. Infraestrutura

- **E1.** Perfil de piloto: uma máquina com GPU, instalada em dias.
- **E2.** Perfil de produção: servidor com GPU on-premise.
- **E3.** Instalação offline documentada, com procedimento de atualização.
- **E4 [a validar].** Dimensionamento por volume, fechado com o número real do piloto.

### M13. Interface

- **E1.** Acesso por navegador.
- **E2.** Documento e resposta lado a lado, com o trecho citado destacado.
- **E3.** Indicador sempre visível de "modo local" ou "com consulta externa".
- **E4.** Mensagem clara quando a base não cobre a pergunta.
- **[Fase 2].** Complementos de Word e Outlook, acessibilidade completa, multilíngue, onboarding guiado.

### M14. Conformidade básica

- **E1.** Registro de finalidade e base legal por fluxo de tratamento.
- **E2.** Identificação de dado pessoal no acervo.
- **E3.** Busca e eliminação por titular, com propagação ao índice e aos vetores.
- **[Fase 2].** ROPA automático, DPIA, requisitos setoriais, ISO 27001/27701/42001, mapeamento de regulação de IA.

### M15. Modos de implantação

- **E1.** Modo A: air-gapped integral, padrão de instalação e de contrato.
- **E2.** Modo B: local com egresso auditado habilitável.
- **E3.** Instalação, atualização e licenciamento offline em ambos.
- **[Fase 2].** Nuvem privada dedicada, híbrido, portabilidade entre modos, contrato por modo.

### M16. Caso de uso piloto

MVP sem caso concreto vira demonstração.

- **E1.** Um caso de uso por vertical escolhida, definido no discovery.
- **E2.** Conjunto de avaliação correspondente a esse caso de uso.
- **E3.** Usuários reais usando durante o piloto, não a equipe do projeto.
- **E4.** Métrica simples: tempo de tarefa e taxa de aceitação da resposta.
- **E5 [a validar].** Quais verticais entram no piloto: provavelmente uma entre jurídico e contábil-fiscal.

### M17. Atualização periódica do corpus normativo

O acervo do cliente tem o contrato, não tem a lei. Sem corpus normativo, a resposta cita o documento e para por aí.

Fonte proposta: o repositório público [ctresb/leis](https://github.com/ctresb/leis), com cerca de 2,7 mil estrelas e atualização recente. A estrutura favorece o trabalho: markdown com cabeçalho YAML contendo título, tipo, número, data, URN e fonte, organizado por esfera (federal, estaduais, municipais, reguladores, jurisprudência, tratados), com recibos SHA-256. Os textos normativos são atos oficiais, sem proteção autoral; os scripts do projeto estão em MIT.

- **E1.** Sincronização periódica com o repositório, registrando o commit coletado. A unidade de controle é o commit, não a data: assim o corpus é reproduzível meses depois.
- **E2.** Escopo por esfera: o MVP indexa Constituição, normas federais e normas de reguladores. Estaduais entram conforme a UF do cliente. Municipais apenas quando houver caso de uso que justifique: são milhares de municípios e a maior parte é ruído para o piloto.
- **E3.** Leitura de conteúdo, nunca execução. O pipeline lê os arquivos markdown e seus metadados; scripts, hooks e páginas do repositório não são executados. O repositório é entrada não confiável até prova em contrário.
- **E4.** Atualização incremental por diferença. Só o que mudou entre o commit anterior e o novo é reprocessado e reindexado.
- **E5.** Segmentação por artigo. Cada dispositivo é unidade recuperável, com hierarquia preservada (livro, título, capítulo, seção) e referência ao artigo no resultado. Segmentar por tamanho fixo quebra o artigo no meio e produz citação errada.
- **E6.** Proveniência em cada citação: título, tipo, número, data, URN e fonte vêm do cabeçalho, somados a commit, data de coleta e hash do arquivo.
- **E7.** Corpus separado do acervo do cliente, com índice próprio e identificação visual na resposta, que distingue o que veio da norma do que veio do documento.
- **E8.** Portão de curadoria. Alteração entra como pendente e vira ativa após revisão, ou por regra declarada que dispensa revisão quando a mudança é apenas de metadado.
- **E9.** Operação em air-gapped por espelho interno ou pacote assinado em mídia, com o mesmo controle de commit e hash.
- **E10.** Cobertura declarada. Consumo do arquivo de cobertura do projeto para saber o que ainda falta no corpus; norma ausente é declarada na resposta, não silenciada.
- **E11.** Origem não oficial sinalizada. A resposta declara que a fonte é agregação de terceiro e aponta a fonte original registrada no cabeçalho.
- **E12 [a validar].** Consolidação: verificar se o texto armazenado reflete a redação vigente ou a redação original. Se for a original, toda citação precisa ressalvar que pode haver alteração posterior.
- **E13 [a validar].** Frequência de sincronização e volume inicial, fechados no piloto.
- **[Fase 2].** Checklist de vigência, detecção de revogação, cruzamento com fonte oficial, ajuste fino do modelo sobre o corpus.

**Sobre chamar isso de aprendizado de máquina.** A automação em si é sincronização e indexação, não treinamento de modelo. O ganho aparece na recuperação: a norma passa a ser encontrada e citada porque está no índice. Ajustar os pesos do modelo ao corpus é caminho diferente, mais caro e mais arriscado, e fica em Fase 2. Vale manter a distinção porque ela muda expectativa, custo e prazo.

**O risco real desta fonte.** Três coisas precisam de verificação antes de confiar na citação: se o texto é a redação vigente ou a original; se a cobertura está completa na esfera escolhida; e como está a qualidade de OCR das normas convertidas de PDF. Um corpus amplo com texto desatualizado é pior que nenhum corpus, porque produz resposta confiante e errada. É por isso que a especificação E8 existe.

---

## 5. O que fica fora do MVP

Sem culpa. Estas coisas importam, só não agora.

| Tema | Requisito no catálogo completo | Fase |
|---|---|---|
| Classificação documental e taxonomia | R12 | 2 |
| Extração estruturada de campos | R13 | 2 |
| Orquestração de agentes e fluxos | R18 | 2 |
| Adaptação ao domínio, glossários | R23 | 2 |
| Observabilidade e SLOs | R29 | 2 |
| Administração e política como código | R30 | 2 |
| Integrações processuais (PJe, e-SAJ) | R31 | 3 |
| Integrações contábeis e fiscais (SPED, NF-e) | R32 | 3 |
| Casos de uso completos por vertical | R34 | 3 |
| Capacitação e gestão de mudança | R36 | 3 |
| Custo total e economicidade | R37 | 3 |
| Suporte, manutenção e atualização normativa | R39 | 3 |
| Extensibilidade e API pública | R40 | 3 |

Também ficam fora, e vale dizer em voz alta: ciclo de vida e descarte formal (R16), gestão de riscos de IA (R8), governança de egresso com testes de exfiltração, MLOps e avaliação contínua.

---

## 6. Critérios de "MVP pronto"

Curto, e verificável em conversa.

- Um usuário sobe um acervo real e faz uma pergunta, recebendo resposta com citação clicável que abre o documento na página certa.
- O sistema funciona sem internet, do início ao fim.
- Nenhum dado sai do ambiente sem ação explícita, comprovado por captura de tráfego durante o teste.
- Quando algo sai, existe registro consultável de quem pediu, o que saiu e para onde.
- Um caso de uso por vertical roda de ponta a ponta, com usuário real.
- O grupo piloto usou por duas semanas sem contornar a solução.
- Acervo de um cliente não é visível para outro, com teste que tentou.
- Uma pergunta que depende de lei recebe resposta citando o artigo, com origem, commit e data da coleta, visualmente distinta de uma citação do acervo do cliente.

Oito critérios. Se todos passarem, o MVP cumpriu o papel: provou a tese. A qualidade fina vem depois, com dado.

---

## 7. Pontos a validar no discovery

Perguntas abertas, sem resposta pronta. Valem uma conversa cada.

1. **Qual vertical entra no piloto?** Jurídico tem o caso mais claro e o risco mais alto. Contábil-fiscal tem volume maior e resultado mais mensurável. Escolher uma, não duas.
2. **Qual o acervo real disponível para o piloto?** Volume, formato e qualidade de digitalização definem metade das decisões técnicas.
3. **Qual a tolerância do cliente a erro?** A resposta muda de "erro com aviso é aceitável" para "só entrego com revisão integral", e isso muda o escopo.
4. **Quem é o dono do projeto do lado do cliente?** Sem patrocinador com poder de liberar acervo e usuário, o piloto não começa.
5. **Egresso está no piloto ou fica para a segunda onda?** Construir o broker é simples; construir a governança em volta, não. Pode ser mais saudável provar o modo offline primeiro.
6. **Hardware: já existe ou será comprado?** Uma GPU disponível hoje muda o cronograma mais que qualquer requisito.
7. **O corpus normativo entra no piloto, e com qual esfera?** É o item mais barato de entregar e o que mais muda a percepção de utilidade. Mas antes de expor citação de lei é preciso responder à E12 de M17: o texto da fonte é vigente ou original? Essa resposta define se a citação entra com ressalva ou entra firme.

---

## 8. Como evoluir

Quando o MVP passar nos critérios da seção 6, o catálogo completo volta a ser útil: cada requisito de M1 a M17 aqui mapeia para um ou mais requisitos de lá, e as especificações detalhadas já estão escritas. A seção 11 do catálogo traz o fatiamento em ondas, e a seção 12 as decisões que ainda estão em aberto.

O caminho natural é: um caso de uso provado, um vertical com avaliação calibrada, e então expansão por vertical em vez de expansão por funcionalidade.
