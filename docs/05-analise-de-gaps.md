# Análise de Gaps: O Que a Matriz Não Responde

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Papel:** auditoria dos documentos 01 a 04 contra o propósito declarado no README.

Este documento não propõe escopo novo por gosto de escopo. Ele responde a uma pergunta só: **o conjunto de requisitos existente sustenta a tese do produto e a operação do fornecedor que vende essa tese?** Onde a resposta é não, o gap está registrado com identificador, consequência e destino.

Nada aqui é compromisso. É lista de trabalho para a próxima rodada de conversa.

**Documentos irmãos:** [04-mvp-matriz.md](04-mvp-matriz.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [03-registro-decisoes.md](03-registro-decisoes.md) · [02-matriz-decisao-egresso.md](02-matriz-decisao-egresso.md)

---

## 1. Método

Quatro passos, e o terceiro é o que costuma faltar em análise de requisitos.

1. **Leitura integral** dos quatro documentos, do README e das cinco premissas P1 a P5 do catálogo.
2. **Verificação mecânica da numeração e das referências.** Contagem de requisitos e especificações, detecção de identificador duplicado, detecção de salto na sequência de E, e resolução de cada referência cruzada contra o requisito que ela cita.
3. **Confronto com o propósito declarado.** Para cada frase do README que afirma o que o produto faz, a pergunta: qual especificação torna essa frase verdadeira e verificável?
4. **Confronto com a pergunta do comprador.** O que um sócio, um DPO, um diretor de TI e um pregoeiro perguntam antes de assinar, e qual documento responde.

Os resultados do passo 2 são bons e vale dizer isso antes das críticas:

| Verificação | Resultado |
|---|---|
| Requisitos no catálogo | 40, na sequência R1 a R40, sem lacuna |
| Especificações no catálogo | 349, exatamente como o README declara |
| Requisitos e especificações no MVP | 17 e 90, exatos como o README declara |
| Numeração de E duplicada | nenhuma ocorrência |
| Salto na sequência de E dentro de um R | nenhuma ocorrência |
| Referências cruzadas "E* do requisito R*" | 47, todas resolvem para especificação existente |
| Referências a decisões D1 a D4 | 17, todas consistentes |

Um catálogo desse tamanho sem uma referência quebrada não é obra de sorte. A disciplina de indexação é o ativo aqui, e as críticas abaixo não são sobre forma.

---

## 2. Grupo A: integridade documental

### G1. Os dois documentos usaram o mesmo espaço de identificadores · **fechado em 10/11/2026**

**Status.** A matriz de MVP foi renumerada de **M1 a M17**, o catálogo manteve R1 a R40, e a convenção de indexação passou a exigir que o identificador carregue o documento de origem. O diagnóstico fica registrado abaixo como histórico, porque a razão de o erro ter acontecido é mais útil que a correção.

Este foi o gap mais grave, e o único que já produziu erro dentro do próprio repositório.

A matriz de MVP numerava seus 17 requisitos de R1 a R17. O catálogo numera 40 requisitos de R1 a R40. Eram espaços independentes que colidiam: **16 dos 17 identificadores do MVP apontavam para um requisito diferente no catálogo.**

| ID | Significava no MVP | Significa no catálogo |
|---|---|---|
| R2 | Consulta externa auditada | Conformidade legal e regulatória |
| R4 | Acesso e permissões | Controle de egresso |
| R7 | Busca | Identidade, papéis e autorização |
| R12 | Infraestrutura | Classificação e taxonomia documental |
| R16 | Caso de uso piloto | Ciclo de vida, retenção e descarte |
| R17 | Atualização do corpus normativo | Runtime de modelos locais |

A colisão apareceu materializada no arquivo 04: na seção 4, o cabeçalho `### R12. Infraestrutura` definia infraestrutura; na seção 5 do mesmo arquivo, a tabela de itens fora do MVP escrevia "Classificação documental e taxonomia | R12 | 2", usando R12 no sentido do catálogo. As duas frases conviviam no mesmo documento e se contradiziam. O mesmo acontecia com R16 e com R8.

O efeito prático, enquanto vigorou: toda referência a "requisito R4" exigia que o leitor adivinhasse de qual documento se estava falando. Em um conjunto que se apoia em rastreabilidade para sustentar confidencialidade e auditoria, isso era o oposto do que o projeto promete ao cliente.

**O que foi feito.** A matriz de MVP foi renumerada como M1 a M17, R1 a R40 ficou exclusivo do catálogo, e a convenção no README passou a declarar as duas séries e a regra de que o identificador carrega o documento de origem, com referência a requisito de outro arquivo sempre qualificada. A alternativa descartada era exigir a qualificação por extenso em toda referência, que resolveria o papel e manteria a armadilha para quem escrevesse depois.

### G2. Não existe matriz de rastreabilidade entre o MVP e o catálogo

O MVP diz que seus 17 requisitos saem do catálogo, mas não diz de qual requisito cada um saiu. A correspondência é inferível e não está escrita: M2 corresponde ao R4 do catálogo, M13 ao R35, M15 ao R38, M16 ao R34, e M17 ao R23 na especificação E6 somado ao R39 na E3.

Sem essa tabela, três coisas quebram na prática: uma mudança no catálogo não se propaga para o MVP de forma verificável; um cliente que pergunta "o que exatamente entrego nesta fase" recebe resposta por conversa e não por documento; e a expansão pós-piloto não sabe qual requisito do catálogo já foi parcialmente satisfeito.

**Recomendação.** Tabela de 17 linhas no arquivo 04, com colunas M, R de origem e observação de escopo parcial. Barato de fazer, e é o que transforma dois documentos em um sistema.

### G3. O mesmo MVP é descrito com dois tamanhos diferentes

O README e a matriz dizem que o MVP tem dezessete requisitos. A seção 11 do catálogo descreve a mesma coisa como "~16 requisitos", e lista exatamente dezesseis. As duas frases estão certas dentro do seu próprio documento e não reconciliam entre si, porque contam unidades diferentes: a matriz conta dezessete requisitos próprios, o catálogo conta dezesseis requisitos do catálogo que o MVP cobre. Um leitor que cruze os dois arquivos encontra 16 contra 17 e não tem como saber que a diferença é de unidade.

Some-se a isso que a seção 11 anuncia "~12 requisitos" na onda 2 e lista treze. São desvios pequenos e o tipo de coisa que ninguém conserta depois, porque cada um exige abrir dois arquivos.

**Recomendação.** Declarar a unidade em cada contagem, como "dezessete requisitos próprios do MVP" e "dezesseis requisitos do catálogo cobertos pelo MVP", e fazer as duas contagens fecharem por construção, isto é, como consequência do mapa de rastreabilidade do G2. Se o mapa existir, os números passam a ser derivados e não digitados.

### G4. Falta um glossário com estatuto de norma

"Acervo", "cliente", "tenant", "curador", "egresso", "documento derivado", "conjunto dourado" e "resposta" aparecem em todos os documentos e não são definidos em nenhum. A maior parte do tempo isso não incomoda. Incomoda exatamente nos pontos caros: "cliente" é a pessoa jurídica contratante, em R25, e é o cliente do escritório, em R3? A distinção muda quem tem direito de acesso. "Acervo" é o conjunto de originais ou o conjunto de originais mais derivados? Muda o escopo de backup, de eliminação e de egresso.

**Recomendação.** Seção 0 no catálogo com dez definições e uma regra de uso. É o documento mais chato e mais útil do conjunto.

---

## 3. Grupo B: lacunas de produto

Aqui a pergunta é diferente: qual especificação torna verdadeira cada frase do README? Onde não há, o gap é de requisito e não de redação.

### G5. O acervo do cliente é tratado como dado confiável, e deveria ser tratado como entrada hostil

O catálogo é rigoroso com o repositório normativo público: a especificação E3 do requisito M17, na matriz de MVP, diz que o repositório é "entrada não confiável até prova em contrário" e que scripts e hooks não são executados. A mesma regra não existe para o acervo do próprio cliente.

Ela é necessária. Um contrato de terceiro, um e-mail recebido, um anexo de licitação ou um PDF baixado da internet entram no acervo e passam a alimentar o contexto do modelo. Texto dentro de um documento pode instruir o modelo a ignorar a política de citação, a revelar o conteúdo de outro documento recuperado na mesma consulta ou a emitir conclusão favorável. Isso é injeção indireta de prompt, e o vetor é o próprio acervo — o dado que o cliente considera mais confiável.

O que existe hoje cobre o vizinho e não o caso. A especificação E16 do requisito R4 testa exfiltração por prompt injection, mas no fluxo de egresso. A especificação E10 do requisito R18 veda egresso por ferramenta de agente, o que impede o dano maior e não impede a resposta corrompida. Nada trata o texto ingerido como instrução não confiável no fluxo de recuperação.

**Recomendação.** Requisito próprio, com quatro especificações: separação entre conteúdo e instrução na montagem do contexto; detecção de padrão de injeção na ingestão com marcação do trecho; teste automatizado com corpus de documentos maliciosos plantados no acervo; e regra de que nenhuma instrução contida em documento altera política, citação ou permissão. As três primeiras são engenharia conhecida; a quarta é decisão de arquitetura e precisa ser tomada agora, porque retrofitar isso depois de o prompt estar espalhado pelo código é caro.

### G6. Implantação e tempo até valor não são requisito

O MVP promete instalação "em dias" e o catálogo tem perfis de hardware, pacote offline e carga histórica em massa. Nenhum documento define o que significa **acervo pronto para uso**: quanto do acervo precisa estar indexado, com qual qualidade, para a primeira pergunta valer a pena. Também não há processo de implantação — migração do acervo, janela, aceite, responsabilidades do cliente, tratamento do que falhou no OCR.

Esse é o gap com maior chance de matar o piloto por motivo não técnico. Um acervo de 200 mil páginas que leva seis semanas para indexar transforma um piloto de 30 dias em projeto de trimestre, e a percepção de valor chega depois do patrocinador perder a paciência.

**Recomendação.** Requisito de implantação com cinco especificações: critério de "acervo pronto" declarado e aceito antes do início; priorização de ingestão por caso de uso, para que o subconjunto que importa fique disponível primeiro; relatório de qualidade da carga inicial por classe documental; matriz de responsabilidades entre fornecedor e cliente; e prazo-alvo medido, não prometido, recalibrado por volume real. Conecta-se ao documento [07-sustentacao.md](07-sustentacao.md), porque quem executa isso é o time de implantação.

### G7. O acervo real é mais hostil que a lista de formatos

A especificação E1 do requisito R9 cobre dezenove extensões, da planilha ao XML fiscal. A especificação E8 cobre zip bomb, XXE, macro e PDF com JavaScript, que são ameaças de segurança. Falta a categoria mais comum e mais chata: **documento que não abre**.

PDF protegido por senha é rotina em acervo jurídico e societário. PDF com restrição de impressão e cópia, DOCX corrompido por conversão, planilha com cem mil linhas, scan em 72 dpi com camada de texto ilegível, arquivo com camada de texto presente e errada — pior que ausente, porque o pipeline confia nela. Hoje a resposta é quarentena e notificação, o que é correto como política e insuficiente como produto: o usuário precisa de uma fila de documentos que exigem ação dele, com o motivo em linguagem clara e um caminho de resolução.

**Recomendação.** Ampliar R9 com tratamento explícito de documento protegido, corrompido e de camada de texto não confiável, e uma fila de exceções com motivo classificado. É barato especificar agora e caro descobrir no acervo do cliente.

### G8. Isolamento de GPU não está especificado

A especificação E4 do requisito R25 garante que nenhuma sessão de modelo compartilha contexto, cache ou memória de conversa entre usuários e tenants. Ela fala de sessão e de aplicação. Não fala do que fica na memória da placa.

Em multi-tenant com GPU compartilhada, o cache de chave-valor e os buffers do runtime sobrevivem ao fim da requisição. Um pedido que reutilize memória não zerada pode, em tese, expor fragmento do processamento anterior. A probabilidade é baixa e a conversa com o DPO de um escritório que guarda acervo de clientes concorrentes não é sobre probabilidade.

**Recomendação.** Especificação de limpeza e isolamento de memória de acelerador verificável por teste, com escolha declarada entre três desenhos: processo de inferência dedicado por tenant, limpeza explícita entre requisições, ou GPU exclusiva para clientes de alto sigilo. A escolha é comercial e de custo, não só técnica, porque GPU exclusiva é o item mais caro da proposta de infraestrutura — ver [09-infraestrutura.md](09-infraestrutura.md).

### G9. Não há mecanismo de errata de resposta

Uma resposta errada sai do sistema, vira minuta, é protocolada. Depois alguém descobre o erro. O conjunto de requisitos cobre bloqueio de citação inexistente, aviso de baixa confiança e revisão humana obrigatória, mas nenhum deles cobre o que fazer **depois** que a resposta errada foi usada.

Faltam três coisas: identificação de que uma resposta específica foi retificada, notificação a quem a usou, e rastro do que foi protocolado com base nela. Isso é o mínimo do dever de cuidado em área regulada, e é também o que separa um fornecedor sério de um que descobre o problema junto com o cliente.

**Recomendação.** Requisito de errata com três especificações: marcação de resposta retificada com motivo e responsável; lista de usuários e exportações que consumiram aquela resposta; e notificação ativa a esses usuários. Depende de R3 no MVP, que já guarda resposta, trecho e documento — a peça que falta é a ligação resposta → consumo.

### G10. Não há evidência de segurança produzida por terceiro

O catálogo adota ISO/IEC 27001, 27701 e 42001 como referencial na especificação E8 do requisito R2, e exige verificação independente de confinamento na especificação E10 do requisito R1. Nenhuma das duas é atestado. Não há exigência de teste de intrusão periódico, de relatório de auditoria de terceiro nem de declaração de conformidade assinada.

Em venda para banco, seguradora, órgão público e grandes escritórios, o questionário de segurança vem antes da proposta comercial e pergunta exatamente isso: último pentest, data, escopo, criticidade dos achados e prazo de correção. Sem resposta, a conversa termina na área de segurança.

**Recomendação.** Requisito de evidência de segurança com três especificações: teste de intrusão anual ou por versão maior, com escopo declarado e relatório resumido ao cliente; política de divulgação de vulnerabilidade; e pacote de evidências renovável, pronto para questionário de segurança, reaproveitado em toda venda.

### G11. Licenças de software aberto e de corpus não são geridas

O produto é vendido como instalação no ambiente do cliente, o que é distribuição de software. A especificação E6 do requisito R1 exige SBOM, que é inventário de componentes e não análise de licença. A especificação E10 do requisito R17 verifica licença de peso de modelo. Ninguém verifica licença de biblioteca.

Componente com licença copyleft em um produto distribuído pode obrigar abertura de código — e o núcleo deste produto é justamente o que não se quer abrir. O mesmo vale para corpus normativo de terceiro: a especificação E11 do requisito M17 resolve a sinalização da origem não oficial na resposta, e não resolve atribuição, termos de uso nem responsabilidade por incorporar a base de outro ao produto.

**Recomendação.** Requisito próprio, com quatro especificações: política de licença por categoria de componente, com lista de bloqueio; varredura automática de licença no build, que falha a integração; inventário de corpus de terceiro com termos, atribuição e base de uso; e parecer arquivado por corpus incorporado. É requisito de uma tarde para especificar e de anos de dor para corrigir depois de virar contrato — ver [08-parcerias.md](08-parcerias.md), porque a mesma análise vale para o que o parceiro embute.

### G12. Não há plano para a hipótese de o fornecedor não existir amanhã

A especificação E6 do requisito R28 garante que acervo, índice e derivados permanecem legíveis e exportáveis sem o fornecedor. Isso resolve o sequestro de dados e não resolve a continuidade do software: quem corrige uma vulnerabilidade crítica no ano seguinte, quem mantém o pipeline normativo, quem dá suporte ao modelo que deixou de ser atualizado.

Cliente institucional faz essa pergunta sempre, e ela é mais desconfortável vindo de um fornecedor pequeno, que é o caso aqui.

**Recomendação.** Duas especificações e uma decisão. Especificações: depósito de código-fonte em regime de liberação por evento definido, e compromisso de suporte por prazo determinado após eventual descontinuidade, com preço de manutenção pré-acordado. Decisão: qual evento libera o escrow — falência, encerramento, ou interrupção de suporte por N versões. Vale entrar no registro de decisões como D11, não como nota de rodapé.

### G13. O conjunto dourado concentra sigilo fora do perímetro dos controles

Toda a governança do produto protege o acervo do cliente. O conjunto de avaliação, exigido na especificação E1 do requisito R22, é feito de perguntas e respostas derivadas de documentos reais do cliente, revisadas por especialista. Ele é, portanto, um segundo acervo sensível: menor, mais concentrado e frequentemente fora do escopo dos controles — mora em planilha, em repositório de teste ou no notebook do analista.

Ninguém especificou quem acessa o conjunto dourado, onde ele reside, por quanto tempo e como é eliminado ao fim do contrato.

**Recomendação.** Tratar o conjunto dourado como classe de dado com política própria: residência no ambiente do cliente quando contiver trecho real, acesso nominal, retenção limitada ao contrato e eliminação certificada. Encaixa como especificação adicional em R22 e como linha na política de retenção de R16.

### G14. Assinatura digital existente não é lida, só produzida

A especificação E5 do requisito R31 trata de assinar documento produzido na plataforma com ICP-Brasil. Nada trata de **verificar** assinatura de documento ingerido. Em acervo jurídico e de licitação, o documento chega assinado, e saber se a assinatura é válida, de quem é, quando foi aplicada e se o conteúdo foi alterado depois é informação de alto valor probatório.

**Recomendação.** Duas especificações: verificação de assinatura PAdES e CAdES na ingestão, com resultado registrado; e sinalização na resposta quando o documento citado tem assinatura inválida ou conteúdo alterado após a assinatura. Depende da especificação E7 do requisito R6, que já calcula hash do original.

---

## 4. Grupo C: a lacuna de negócio

### G15. Trinta e sete dos quarenta requisitos são técnicos, e o fornecedor não tem requisito nenhum

Esta é a lacuna mais ampla e a razão deste bloco de documentos existir.

O catálogo responde com precisão incomum como construir a plataforma. Não responde como o negócio que a constrói se sustenta: quanto custa, por quanto se vende, com que margem, com que time, vendido por quem, contra quem, para quem, e o que acontece quando o primeiro concorrente de bolso aparecer cobrando um décimo.

O que existe hoje e não cobre:

- **R37** calcula o custo total de propriedade **do cliente**. É argumento de venda, não modelo de receita. Nada define preço, empacotamento, métrica de cobrança, política de desconto ou reajuste.
- **R39** define níveis de serviço de suporte. Não define com quantas pessoas, com que cobertura e a que custo — e sustentação de produto instalado em cliente é o maior consumidor de margem nesse modelo.
- **R40** trata de extensibilidade técnica, não de ecossistema comercial.
- Nada trata de concorrência, de posicionamento, de parceiro de canal, de segmentação de cliente ou de margem.

A consequência é conhecida de quem vende software instalado no cliente: o produto tecnicamente excelente com modelo de negócio mal desenhado vira projeto de serviços com margem de 20%, um cliente grande que consome metade do time, e nenhuma capacidade de escalar. A tese do README —"trabalhar com o acervo sem expor o acervo"— só chega ao mercado se alguém souber vendê-la ao preço que paga o time que a sustenta.

**Destino.** Sete requisitos novos, registrados como **Bloco VII: negócio, mercado e operação sustentável**, com número continuando o catálogo a partir de R44 — R41, R42 e R43 estão reservados às lacunas de áudio, vídeo e fraude documental na seção 13 do catálogo, e não são reutilizáveis.

| Requisito | Tema | Documento |
|---|---|---|
| **R44** | Precificação e empacotamento comercial | [06-precificacao-e-escala.md](06-precificacao-e-escala.md) |
| **R45** | Escala de mercado e posicionamento de referência | [06-precificacao-e-escala.md](06-precificacao-e-escala.md) |
| **R46** | Sustentação com equipe enxuta | [07-sustentacao.md](07-sustentacao.md) |
| **R47** | Ecossistema de parcerias e canal | [08-parcerias.md](08-parcerias.md) |
| **R48** | Infraestrutura modular e elástica | [09-infraestrutura.md](09-infraestrutura.md) |
| **R49** | Inteligência competitiva | [10-concorrentes.md](10-concorrentes.md) |
| **R50** | Segmentação de mercado e margem | [11-publico-alvo-e-margem.md](11-publico-alvo-e-margem.md) |

Esses sete não substituem nada do que existe. R48 complementa R26 e R38 pelo lado do custo e da elasticidade; R46 complementa R39 pelo lado de quem executa; R44 complementa R37 pelo lado de quem recebe. Ao final da rodada, o catálogo passa a ter 47 requisitos e sete deles falam de negócio.

---

## 5. Priorização

Impacto é o dano de não fechar. Esforço é o custo de fechar agora, em discovery, não em implementação.

| Gap | Tema | Impacto | Esforço | Quando |
|---|---|---|---|---|
| ~~**G1**~~ | Colisão de identificadores | Alto | Baixo | **Fechado** |
| **G2** | Rastreabilidade MVP → catálogo | Alto | Baixo | Agora |
| **G5** | Acervo como entrada não confiável | Alto | Médio | Antes do piloto |
| **G6** | Implantação e tempo até valor | Alto | Médio | Antes do piloto |
| **G15** | Negócio, preço, margem e equipe | Alto | Alto | Agora, em paralelo |
| **G16** | Divergência de números entre os documentos de negócio | Alto | Baixo | Antes de qualquer proposta comercial |
| **G7** | Documento protegido e camada de texto ruim | Alto | Baixo | Antes do piloto |
| **G10** | Evidência de segurança de terceiro | Alto | Baixo | Antes da primeira venda institucional |
| **G8** | Isolamento de memória de GPU | Médio | Médio | Antes do primeiro cliente multi-tenant |
| **G9** | Errata de resposta | Médio | Médio | Fase 2 |
| **G11** | Licenças de software e corpus | Médio | Baixo | Antes da primeira distribuição |
| **G12** | Continuidade do fornecedor | Médio | Baixo | Antes do primeiro contrato grande |
| **G13** | Conjunto dourado como acervo sensível | Médio | Baixo | Antes do piloto |
| **G3** | Contagem do mesmo MVP com dois tamanhos | Baixo | Baixo | Agora, junto com G2 |
| **G4** | Glossário normativo | Baixo | Baixo | Junto com G1 |
| **G14** | Verificação de assinatura digital | Baixo | Médio | Fase 2 |

G1 está fechado. Dos sete itens de impacto alto que restam, cinco custam pouco para fechar em discovery. A recomendação de sequência é G2 com G3 e G4 na mesma passada, porque o mapa de rastreabilidade é o que faz as duas contagens do G3 fecharem por construção e o glossário evita a próxima ambiguidade de vocabulário; G15 em paralelo, porque é o bloco de documentos novos; G16 assim que G15 fechar, porque só existe divergência depois que existe número; e G5, G6, G7, G10 e G13 antes de o piloto começar.

---

## 6. O que não é gap

Lista curta do que parece faltar e está coberto. Serve para evitar que a próxima reunião rediscuta o que já está resolvido.

- **Fallback automático para nuvem quando o modelo local falha.** Vedado explicitamente pela especificação E2 do requisito R5, e é a vedação mais importante do conjunto.
- **Multi-tenant com isolamento testado.** Coberto por R25, incluindo a suíte de tentativa de acesso cruzado da especificação E8.
- **Vigência de norma citada.** Coberto por R39 na especificação E3 e por R19 na E4, com a decisão D8 aberta sobre jurisprudência — aberta de propósito, não por esquecimento.
- **Acessibilidade.** Coberto por WCAG 2.2 AA na especificação E6 do requisito R35. Vale acrescentar o modelo eMAG quando houver venda para órgão público, o que é ajuste de uma linha e não requisito novo.
- **Custo de curadoria humana.** Reconhecido e exigido na especificação E3 do requisito R37. O que falta não é o reconhecimento, é o número — e o número nasce no piloto.
- **Treinamento e gestão de mudança.** Coberto por R36, com trilha por perfil e laboratório com acervo sintético.
- **Vazamento por contorno humano.** Registrado como o risco número um na seção 13 do catálogo, com mitigação em R35 e R36. É risco aceito e medido, não lacuna.

---

## 7. Divergências entre os documentos de negócio

Os documentos 06 a 11 foram escritos em paralelo, sobre a mesma base de fatos, por autores diferentes. Três parâmetros saíram com valores incompatíveis entre si. Nenhum deles é erro de conta: são **modelos diferentes** para a mesma variável, e o conjunto fica inconsistente enquanto ninguém escolher um.

| Parâmetro | O que diz o documento 07 | O que dizem os documentos 06, 08 e 11 | Fator |
|---|---|---|---|
| **Time mínimo de sustentação** | 2,7 FTE, **R$ 55 mil/mês** | **R$ 105–125 mil/mês**, o time de cinco cabeças do anexo de fatos | 2× |
| **Custo de sustentação por cliente** | **R$ 13,9 mil/mês** com 10 clientes; R$ 7,3 mil com 50 | **15% da receita** no cenário base, o que num ticket de R$ 12 mil/mês dá R$ 1,8 mil | 4× a 7× |
| **Piso de contrato recorrente** | R$ 239 mil/ano, derivado de R$ 19,9 mil/mês com 10 clientes | **R$ 120 mil/ano**, derivado de um time que serviria 10 a 12 contratos | 2× |

A consequência é aritmética e não pode ser deixada para o leitor resolver: **com os números do documento 07, o plano Essencial de R$ 10.900/mês do documento 06 não paga a própria sustentação em nenhuma faixa de carteira.** Ele paga com folga no cenário do documento 11, que trata sustentação como 15% da receita.

**Qual dos dois é mais defensável.** O documento 07, porque é o único construído de baixo para cima: horas por chamado, chamados por cliente por ano, salário por função, multiplicador de encargos. O documento 11 usa um percentual derivado de benchmark de SaaS em nuvem, onde suporte não escala com instalação. Benchmark é ponto de partida, não medição.

**A decisão que fecha isso.** A causa raiz das três divergências é uma só: **a sustentação está embutida na assinatura ou é linha contratada à parte?** O documento 06 na especificação E1 diz que está embutida. O documento 07 prova que, embutida, ela consome de 50% a 100% da assinatura. As duas coisas não convivem.

- **Se embutida**, o preço do plano Essencial tem de subir para a ordem de R$ 20 mil/mês, e o documento 06 precisa de uma tabela nova, com o reposicionamento frente às âncoras de mercado refeito.
- **Se separada**, o cliente paga plataforma e sustentação em duas linhas, a margem de software volta para a faixa de 70%, a de serviço fica em 30% e o documento 11 precisa de uma linha a mais na tabela de margem por receita.

A recomendação é **separar**, por três razões. Primeiro, porque é o que o cliente on-premise já conhece: ele compra licença e compra manutenção, e compara as duas separadamente. Segundo, porque embutir esconde o custo real do suporte e transforma toda renovação numa negociação sobre um preço único, sem que o cliente saiba o que está discutindo. Terceiro, porque separar permite vender sustentação ampliada a quem precisa de plantão e sustentação básica a quem não precisa, o que é a única forma de servir cliente jurídico e cliente contábil com a mesma estrutura.

Enquanto a decisão não for tomada, os números dos documentos 06, 07, 08 e 11 devem ser lidos como faixa, não como compromisso. É exatamente o estatuto que o README já dá a todo o conjunto.

---

## 8. Como este documento envelhece

Quando os gaps de impacto alto estiverem fechados, esta análise perde a função e deve ser substituída por uma revisão curta a cada rodada de documentos. O que não deve acontecer é ela virar documento permanente: análise de gap que não é fechada vira desculpa para não avançar.

O critério de encerramento é simples: G1, G2, G3, G4, G15 e G16 fechados e os cinco de produto convertidos em especificação dentro dos requisitos existentes. Nesse momento, este arquivo pode ser arquivado com uma nota de uma linha dizendo onde cada gap foi resolvido.
