# Público-Alvo e Margem: Cinco Segmentos, Três Cenários e um Número Que Decide

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Papel:** segmentação de mercado, cenários de margem e potencial de receita · **Requisito:** R50

**Documentos irmãos:** [05-analise-de-gaps.md](05-analise-de-gaps.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [06-precificacao-e-escala.md](06-precificacao-e-escala.md) · [07-sustentacao.md](07-sustentacao.md) · [10-concorrentes.md](10-concorrentes.md)

**O que este documento é.** Um conjunto de cenários construídos sobre fatos declarados. Cada número do cenário aponta para a premissa que o sustenta, e cada premissa aponta para uma fonte com data ou para o rótulo `[estimativa declarada]` com a conta que a produziu. Onde não existe dado público, o documento diz que não existe em vez de preencher com chute — a lacuna é informação, não constrangimento.

**O que este documento não é.** Não é projeção financeira, não é plano de negócio e não serve para captação. A diferença é prática: projeção afirma o que vai acontecer; cenário mostra o que teria de ser verdade para acontecer. Uma planilha de projeção envelhece em três meses e vira mentira; um cenário com premissa rotulada continua útil quando a premissa cai, porque a queda estava prevista como possibilidade.

**Regra de leitura.** Nenhuma decisão de preço, desconto ou contratação deve ser tomada com o número agregado deste documento. As decisões se tomam com o número do cliente, medido. O que está aqui é a faixa em que o cliente precisa caber para o negócio fechar.

---

## 1. O universo, com fonte e data

| Universo | Número | Fonte | Data |
|---|---|---|---|
| Advogados inscritos na OAB | **1.514.918** (quadro geral 1.635.150, que inclui 12.206 estagiários e 108.026 suplementares) | CFOAB, quadro de advogados | consulta 10/11/2026 |
| Maiores seccionais | **SP 397.309 · RJ 164.149 · MG 152.153** | idem | idem |
| Profissionais da contabilidade | **550.864** | CFC, consulta por região | 10/11/2026 |
| Organizações contábeis ativas | **97.836** | CFC, matéria institucional | 25/04/2025 |
| Empresas ativas no Brasil | **~25,7 milhões** | Mapa de Empresas / Receita Federal | dados até 09/2026 |
| Municípios | **5.570** | IBGE, Divisão Territorial | Censo 2022 |
| Mercado brasileiro de software | **US$ 21,7 bi** em 2025, +21,4% | ABES/IDC, Mercado Brasileiro de Software 2026 | publicado 02/08/2026 |
| Sociedades de advogados registradas | **não publicado** | o painel do CFOAB conta inscrição individual, não pessoa jurídica | — |

A última linha é a mais importante da tabela. O universo de usuários é grande e conhecido; o universo de **compradores** não é. Um advogado inscrito não é um cliente — é um usuário potencial dentro de uma organização que pode ou não ter orçamento, acervo próprio e capacidade de comprar infraestrutura. Toda a análise abaixo depende dessa distinção, e é por isso que o SAM deste documento é construído por organização e não por profissional.

---

## 2. Segmentação por critério de qualificação econômica

Cinco segmentos, definidos por um critério que se verifica em cinco minutos de conversa e não por vertical de marketing. A qualificação responde a uma pergunta só: esta organização tem acervo próprio, exigência de sigilo e capacidade de comprar infraestrutura?

| Segmento | Critério de qualificação | Paga · decide | Usa · veta | Ciclo | On-premise: por que sim / por que não |
|---|---|---|---|---|---|
| **Grande banca** | 200+ advogados, área de TI própria, acervo na casa dos milhões de páginas, contrato de cliente com cláusula de confidencialidade | Sócio de administração e TI · comitê de sócios, com parecer de segurança da informação | Advogado, paralegal, equipe de contencioso de massa · **veta** segurança da informação e sócio que não quer mudar processo | 9 a 18 meses, com prova de conceito de 90 dias | **Sim:** já tem data center e exigência contratual de sigilo de cliente. **Não:** já paga Projuris ou Legal One, e prefere o selo internacional de CoCounsel ou Harvey |
| **Banca média** | 20 a 199 advogados, 5+ sócios, orçamento de software de R$ 3 mil a R$ 10 mil/mês, sem TI própria | Sócio administrativo · sócio majoritário | Advogado pleno e sênior · **veta** o sócio mais antigo (custo) e informalmente "quem mexe com TI" | 3 a 6 meses | **Sim:** sigilo do cliente e concorrente local já usando IA. **Não:** não tem GPU nem quem opere servidor — o preço tem de incluir hardware e implantação de terceiro |
| **Escritório de nicho** | 5 a 19 advogados, foco em uma tese ou setor, acervo de pareceres, ticket alto por caso | O sócio, do próprio bolso · o próprio sócio | 1 a 3 advogados · **veta** o preço por usuário que ele conhece do mercado | 30 a 90 dias | **Sim:** quer diferencial e confidencialidade. **Não:** a referência de preço dele é R$ 49–249/usuário/mês, e a instalação on-premise custa um múltiplo disso |
| **Departamento jurídico** | 10+ advogados internos ou grupo com compliance estruturado e DPO nomeado; compra por processo interno | Orçamento de jurídico/compliance · gerente jurídico com CIO, compras e segurança | Advogado interno e compliance · **veta** segurança da informação e compras (homologação de fornecedor) | 6 a 12 meses | **Sim:** residência do dado dispensa a análise de transferência internacional da LGPD e é argumento de venda pronto. **Não:** exige escrow de código, teste de intrusão e SLA que um time pequeno não entrega hoje |
| **Setor público** | Procuradoria ou consultoria jurídica própria, acervo de pareceres, compra pela Lei 14.133/2021 | Orçamento próprio · comissão de contratação e ordenador de despesa, com julgamento por técnica e preço | Procurador e assessor · **veta** o tribunal de contas, a área de TI e a própria lei, que veda pregão para serviço técnico intelectual | 12 a 24 meses | **Sim:** air-gap é requisito, não preferência, e a lei permite restringir a contratação a tecnologia nacional em TIC estratégico. **Não:** exige atestado, capital e qualificação técnica que um fornecedor novo não tem |

**Onde o veto realmente mora.** Em quatro dos cinco segmentos, quem veta não é quem paga. Na grande banca é o comitê; no departamento jurídico é a segurança da informação; no setor público é a comissão e o controle externo. Proposta enviada sem o mapa de veto preenchido é proposta que morre na terceira reunião, depois de consumir pré-vendas. Isso é custo de aquisição, e volta na seção 8.

**O segmento que parece fácil e não é.** O escritório de nicho tem o ciclo mais curto e o pior resultado econômico. O mercado já publicou preço para ele — R$ 55,92 a R$ 1.099,90/mês nos produtos de IA jurídica, R$ 49 a R$ 249/usuário/mês na gestão (Fonte: juridico.ai, Jusbrasil, Locus, asquadz.ai, leitura out–nov/2026). Vender on-premise nessa faixa é vender abaixo do custo de servir, e o cliente ainda precisa comprar a GPU, cujo piso de varejo é R$ 31.999,99 (Fonte: pcbuilder.com.br, 17/09/2026; servidor com GPU é vendido sob consulta, sem tabela pública em BRL).

---

## 3. Decisão: entrar pelo departamento jurídico e pela banca média, e recusar o nicho na fase 1

**Decisão proposta.** A fase 1 atende **departamento jurídico de empresa e banca média (20 a 199 advogados)**, nessa ordem de prioridade comercial. A grande banca entra depois, e apenas como projeto de implantação assistida, porque o ciclo de 9 a 18 meses consome o caixa do primeiro ano sem produzir receita. O escritório de nicho e o advogado individual ficam fora até existir produto empacotado com hardware e preço publicado — *conforme E2*.

A razão é aritmética, não preferência. O departamento jurídico reúne as três condições que o produto exige ao mesmo tempo: acervo próprio volumoso, exigência de sigilo com consequência jurídica e orçamento anual aprovado para software. A banca média reúne duas e resolve a terceira com o próprio fornecedor, o que é exatamente o papel da implantação assistida. O escritório de nicho não reúne nenhuma das três em escala suficiente.

**Alternativa descartada.** Começar pelo escritório de nicho e pelo advogado individual, atraídos pelo ciclo de 30 a 90 dias — descartada porque a referência de preço desse segmento já está publicada em R$ 49 a R$ 249/usuário/mês, o que estabelece um teto de receita por cliente abaixo do custo de servir de uma instalação on-premise.

**O que isso não muda.** A decisão não altera as faixas de implantação: piloto em nuvem privada na conta do cliente até ~50 mil páginas e 15 usuários, produção departamental on-premise entre 50 mil e 2 milhões de páginas, air-gap sempre on-premise (*conforme especificação E9 do requisito R38*, *conforme decisão D3*). O segmento escolhido aqui é o comprador; a faixa é técnica.

---

## 4. TAM, SAM e SOM

| Camada | Construção | Premissa em uma frase | Valor | Rótulo |
|---|---|---|---|---|
| **TAM** | 1.514.918 advogados × R$ 100 a R$ 250/mês | Todo inscrito na OAB vira assinante pagante ao preço de tabela do mercado de IA jurídica — premissa que nenhum produto realizou | **R$ 1,8 bi a R$ 4,5 bi/ano** | `[estimativa declarada]` — teto, não mercado |
| **SAM** | Soma de cinco componentes, cada um por unidade compradora × ticket anual (tabela abaixo) | Só entra a organização com acervo próprio, exigência de sigilo e capacidade de comprar servidor com GPU | **R$ 2,6 bi a R$ 2,8 bi/ano** | `[estimativa declarada]` |
| **SOM** | 39 clientes em 36 meses na curva base × ticket médio de R$ 145 mil | Conversão de 18% sobre 8 oportunidades qualificadas por mês a partir do mês 4 | **R$ 5,7 mi/ano, ~0,2% do SAM** | `[estimativa declarada]` |

| Componente do SAM | Unidades | Origem da contagem | Ticket anual | Receita |
|---|---|---|---|---|
| Banca grande (200+ advogados) | 250 | `[estimativa declarada]` — sociedades não publicadas pelo CFOAB | R$ 900 mil | R$ 225 mi |
| Banca média (20 a 199) | 3.000 | `[estimativa declarada]` sobre a base de 1.514.918 profissionais | R$ 180 mil | R$ 540 mi |
| Escritório de nicho com acervo relevante | 20.000 | `[estimativa declarada]` | R$ 48 mil | R$ 960 mi |
| Departamento jurídico de média e grande empresa | 2.500 | `[estimativa declarada]` sobre 25,7 mi de empresas ativas (RFB, 09/2026) | R$ 300 mil | R$ 750 mi |
| Setor público com procuradoria própria | 1.200 | `[estimativa declarada]` sobre 5.570 municípios (IBGE, Censo 2022) | R$ 180 mil | R$ 216 mi |

O TAM está aqui para ser desmontado, não usado. Ele diz que o teto teórico é de bilhões e não informa nada sobre o negócio, porque multiplica base de usuário por preço de tabela de um mercado adjacente. Um sócio cético derruba esse número em uma pergunta ("quantos desses já pagam por alguma coisa?"), e é bom que derrube rápido.

O SAM é o número que importa e o mais frágil dos três. Ele é a soma de cinco estimativas declaradas, e a maior delas — o escritório de nicho, R$ 960 milhões — é justamente o segmento que a seção 3 recomenda recusar na fase 1. Sem esse componente, o SAM endereçável cai para **R$ 1,7 bi** [estimativa declarada]. A diferença entre os dois números é a diferença entre o mercado que existe e o mercado que este fornecedor consegue atender. A lacuna mais cara desta seção é a ausência de número oficial de sociedades de advogados: é a primeira pesquisa a fazer antes da segunda rodada, porque é ela que sustenta ou derruba metade do SAM.

---

## 5. Cenários de margem

Custo de servir decomposto como percentual da receita contratual de um cliente típico. Todos os percentuais são `[estimativa declarada]` construída sobre os benchmarks da seção 6; a margem de 77% é mediana de SaaS, 81% em assinatura e 30% em serviços profissionais (Fonte: Benchmarkit 2025 SaaS Performance Metrics, dados de 2024).

| Linha de custo | Conservador | Base | Otimista | O que está dentro |
|---|---|---|---|---|
| Infraestrutura | 9% | 6% | 4% | Laboratório de homologação, GPU de teste, build do pacote offline, três perfis de hardware mantidos em paralelo |
| Sustentação | 20% | 15% | 11% | Suporte N1/N2, plantão, atualização offline trimestral, atualização normativa |
| Implantação | 20% | 13% | 8% | Horas de campo não cobertas pelo preço cobrado da implantação |
| Canal | 12% | 9% | 6% | Desconto de revenda, pré-vendas técnico e comissão |
| **Custo de servir** | **61%** | **43%** | **29%** | Soma das quatro linhas |
| **Margem bruta** | **39%** | **57%** | **71%** | Contra 77% de mediana SaaS e 81% em assinatura |

**Por que o on-premise fica abaixo da mediana de SaaS.** Quatro razões, todas estruturais. A primeira é o custo de suportar diversidade: um SaaS roda em um ambiente; este produto roda no de cada cliente, em três perfis e duas famílias de sistema operacional (*conforme especificação E1 do requisito R26*). A segunda é a atualização offline, que não é deploy contínuo e sim pacote assinado com janela acordada e procedimento de reversão (*conforme especificação E2 do requisito R39*) — trabalho humano por cliente por versão. A terceira é a implantação, que é projeto e não configuração. A quarta é que o cliente não compra infraestrutura do fornecedor, o que parece bom e esconde a conta: o fornecedor deixa de ganhar o markup de nuvem e continua pagando o custo de homologar o hardware alheio.

Mesmo o cenário otimista (71%) não alcança a mediana de assinatura pura (81%). Isso não é falha de execução; é a natureza do modelo. A consequência estratégica é que este negócio **não pode competir por preço** e precisa compensar em ticket e em canal, porque não compensa em margem.

---

## 6. Margem por linha de receita: proteger uma, diluir três

| Linha | Como se cobra | Custo de servir | Margem | Papel |
|---|---|---|---|---|
| **Licença e suporte** | Assinatura anual por instalação, com faixa por volume | 22% a 28% | **72% a 78%** | **Proteger.** É a única linha que paga o time e financia o produto |
| **Implantação** | Preço fechado por projeto, cobrado antes do início | 65% a 75% | **25% a 35%** | **Diluir.** Cobrir custo e margem de projeto, nunca descontar |
| **Hardware revendido** | Repasse do servidor ou da estação com GPU | 88% a 95% | **5% a 12%** | **Diluir a zero.** Cliente compra direto ou pelo integrador |
| **Customização** | Hora técnica ou escopo fechado | 75% a 90% | **10% a 25%** | **Diluir e limitar.** Só entra o que serve a outros clientes |

A linha de implantação tem uma armadilha específica: o mercado pratica onboarding de R$ 500 a R$ 5.000+ e treinamento de R$ 150 a R$ 500/hora (Fonte: asquadz.ai, 05/02/2026). Esses valores são de produto de autoatendimento e não cobrem a instalação de um servidor com GPU, a carga de um acervo histórico e o aceite de qualidade de indexação. Copiar a tabela de implantação do mercado é a forma mais rápida de transformar o primeiro contrato em prejuízo com nota fiscal.

Hardware revendido merece regra dura porque é a linha que o cliente pede com mais frequência e a que menos devolve: margem de 5% a 12% sobre um item de dezenas de milhares de reais consome capital de giro, prazo de entrega e garantia, e ainda transfere ao fornecedor um risco de fornecimento que não é o seu. Se o cliente não consegue comprar o servidor sozinho, o problema é de qualificação de segmento, não de linha de produto.

Customização entra com teto por contrato e critério de reuso, *conforme especificação E7 do requisito R23*: personalização por organização é recurso do produto; desenvolvimento sob encomenda é outra empresa. A confusão entre as duas é o item da seção 10.

---

## 7. Ponto de equilíbrio do time mínimo

O time enxuto custa **R$ 105 mil a R$ 125 mil por mês** — R$ 60 mil a R$ 70 mil de salário bruto com multiplicador de encargos de 1,7 a 1,8, sobre as medianas de mercado para engenheiro de IA (R$ 25 mil), engenheiro de dados (R$ 15 mil), dois analistas de suporte (R$ 5–7 mil cada) e um consultor de implantação (R$ 9–12 mil). Fonte das faixas salariais: Robert Half Guia Salarial 2026 via Exame, 01/10/2026; o multiplicador de encargos é `[estimativa declarada]` calculada sobre as alíquotas legais, sem fonte consolidada de pesquisa salarial.

| Cenário | Margem bruta | Custo anual do time | Receita necessária | Clientes a ticket de R$ 145 mil |
|---|---|---|---|---|
| Conservador | 39% | R$ 1,26 a R$ 1,50 mi | R$ 3,23 a R$ 3,85 mi | **22 a 27** |
| Base | 57% | R$ 1,26 a R$ 1,50 mi | R$ 2,21 a R$ 2,63 mi | **15 a 18** |
| Otimista | 71% | R$ 1,26 a R$ 1,50 mi | R$ 1,77 a R$ 2,11 mi | **12 a 15** |

Leia a tabela pela coluna dos clientes, não pela da receita. São **15 a 18 clientes** para pagar o time que entrega, no cenário base. A pergunta seguinte é quanto custa adquirir cada um deles, e a resposta disponível é desconfortável: a mediana de mercado é **US$ 2,00 de marketing e vendas por US$ 1,00 de nova receita anual** (Fonte: Benchmarkit, dados de 2024). Traduzido, cada real de ARR novo consome dois reais de S&M — e não existe dado público de CAC ou churn para o Brasil, o que torna esse número um proxy global, não um fato local `[a validar]`.

Duas consequências diretas. A primeira: o ponto de equilíbrio acima paga o time que entrega, não o time que vende. Com a relação de CAC da mediana, crescer R$ 1,45 milhão de ARR em um ano exige R$ 2,9 milhões de S&M — mais que a receita recorrente gerada no mesmo ano. A segunda: essa conta só fecha com canal, ou com ticket mais alto, ou com crescimento menor. Vender direto, cliente a cliente, com 15 a 18 clientes de base, é o caminho para o fornecedor financiar a própria estagnação.

---

## 8. Sensibilidade: quatro choques e o que cada um faz

| Choque | Conta | Efeito na margem | Efeito no ponto de equilíbrio |
|---|---|---|---|
| **Preço 20% menor** | Receita cai a R$ 96 mil; custos fixos (infraestrutura 6% + sustentação 15% = R$ 25,2 mil) e implantação em horas (R$ 15,6 mil) não caem; canal vira 9% de R$ 96 mil (R$ 8,6 mil) | 57% → **48,5%** (−8,5 p.p.) | R$ 2,21–2,63 mi → **R$ 2,60–3,09 mi** (+18%) |
| **Churn anual de 15% em vez de 5%** | Retenção em 36 meses: 61,4% contra 85,7% | Margem por cliente não muda | Payback de 3,5 anos contra vida média de 6,7 anos; **LTV/CAC de 1,9** |
| **Implantação levando o dobro do tempo** | 13% → 26% do contrato em horas | 57% → **44%** | O gargalo deixa de ser vendas: um consultor cobre metade das implantações por ano |
| **Metade dos clientes exigindo GPU dedicada** | Infraestrutura 6% → 9%, sustentação 15% → 17%; dois parques de hardware em vez de um | 57% → **52%** | Sobe ticket, alonga ciclo e aumenta objeção de preço no cliente |

O primeiro choque é o mais instrutivo. Descontar 20% não custa 20% de margem: custa 8,5 pontos percentuais de margem e 18% mais clientes para pagar a mesma conta. É por isso que a política comercial precisa da tabela de sensibilidade anexada a cada pedido de exceção — *conforme E9*.

O segundo choque é o que separa este negócio de um negócio viável. A margem bruta por cliente é indiferente ao churn; o que ele destrói é a recuperação do custo de aquisição. A 5% ao ano a vida média ultrapassa o horizonte contratual de cinco anos e o cliente paga o que custou trazê-lo; a 15% ela cai para 6,7 anos e o LTV/CAC fica em 1,9, abaixo de qualquer limite saudável. Churn, aqui, não é métrica de vaidade: é a variável que decide se a operação tem retorno. E é a mais difícil de estimar, porque não existe dado brasileiro publicado.

O terceiro choque é o mais provável de ocorrer, e o menos observado. Atraso de implantação não aparece no relatório financeiro como problema de margem; aparece como cliente insatisfeito e como consultor ocupado. As duas coisas são a mesma.

O quarto choque tem uma saída parcial: manter um perfil sem GPU para operação em CPU, com desempenho e limitações declarados (*conforme especificação E7 do requisito R26*), que reduz a barreira de entrada de quem não quer comprar acelerador — e reduz também a qualidade que o cliente percebe. É uma troca comercial, e precisa ser declarada como troca.

---

## 9. Receita em 24 e 36 meses

Três curvas, cada uma com a premissa de conversão que a produz. Ticket médio, conversão e churn são `[estimativa declarada]`; a aritmética está na coluna de premissa para que qualquer pessoa recombine a curva.

| Curva | Premissa de conversão | Clientes em 24 meses | ARR em 24 meses | Clientes em 36 meses | ARR em 36 meses |
|---|---|---|---|---|---|
| **Conservador** | 5 oportunidades qualificadas/mês a partir do mês 7; conversão de 15%; ciclo de 9 a 12 meses; ticket de R$ 120 mil; churn de 12% | 13 | R$ 1,56 mi | 20 | R$ 2,40 mi |
| **Base** | 8 oportunidades/mês a partir do mês 4; conversão de 18%; ciclo de 6 a 9 meses; ticket de R$ 145 mil; churn de 5% | 26 | R$ 3,77 mi | 39 | R$ 5,66 mi |
| **Otimista** | 10 oportunidades/mês a partir do mês 3, com 40% vindas de canal; conversão de 25%; ciclo de 4 a 6 meses; ticket de R$ 170 mil; churn de 4% | 45 | R$ 7,65 mi | 67 | R$ 11,39 mi |

A curva base paga o time mínimo por volta do mês 22 — 26 clientes contra os 15 a 18 necessários, com folga que existe justamente porque os primeiros contratos chegam depois de um ano de custo sem receita. A curva conservadora **não paga o time mínimo em 36 meses**: 20 clientes a ticket de R$ 120 mil produzem R$ 2,40 mi, abaixo dos R$ 3,23 a R$ 3,85 mi exigidos pela margem de 39% daquele cenário. Isso é o resultado mais importante desta seção e não deve ser suavizado: no cenário conservador, o produto não é um negócio, é uma linha de serviço subsidiada.

A diferença entre a curva base e a otimista não é esforço comercial, é canal. A otimista supõe 40% das oportunidades vindas de parceiro; a base supõe venda direta pura. Nenhum dos dois números tem lastro contratado, o que faz do documento [08-parcerias.md](08-parcerias.md) o mais determinante do conjunto para a viabilidade — e é o único dos sete que ainda não existe nesta rodada.

---

## 10. O risco que mais ameaça a margem: serviços engolindo o produto

Este é o risco que fecha empresas como esta, e ele não se anuncia. Nenhum fornecedor decide virar consultoria; ele aceita o primeiro pedido de customização para fechar a venda, o segundo porque o cliente é grande, o terceiro porque a receita de projeto tapa o buraco do mês. Em dezoito meses o roadmap é feito de tickets de cliente, o produto não evolui e a margem converge para os 30% de serviços profissionais (Fonte: Benchmarkit, dados de 2024).

**Como reconhecer cedo.** Quatro indicadores, medidos por trimestre, não por impressão:

| Indicador | Limite | O que significa quando estoura |
|---|---|---|
| Receita de serviços (implantação + customização) sobre receita total | acima de **35%** | O produto virou acessório do projeto |
| Horas de customização sobre o valor do contrato | acima de **20%** | O cliente comprou desenvolvimento, não licença |
| Receita recorrente sobre receita total | abaixo de **65%** | O que existe não é receita previsível |
| Reuso de customização em outro cliente | abaixo de **1 em 3** | Trabalho sob encomenda disfarçado de produto |

**O que fazer.** Três respostas, na ordem, e nenhuma delas é "aceitar e cobrar mais". Primeiro, precificar a customização com margem de projeto e recusar abaixo disso — recusar é a resposta, não negociar. Segundo, transformar o pedido recorrente em configuração do produto quando o mesmo pedido aparece em três clientes, o que é o caminho natural de *especificação E7 do requisito R23*. Terceiro, quando o cliente exigir desenvolvimento sob encomenda e ele for estratégico, isolá-lo em contrato de projeto separado, com escopo, prazo e equipe próprios, para que o resultado dele não contamine a margem da licença. O indicador que fecha o caso é o tempo médio de análise e a taxa de retrabalho do cliente (*conforme especificação E5 do requisito R22*): se o produto não move esses dois números, o que o cliente está comprando é serviço.

---

## 11. Requisito R50 — Segmentação de mercado e margem

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** O conjunto documenta com precisão como construir a plataforma e não responde para quem vendê-la, a que preço ela se paga e com que margem ela se sustenta. Sem isso, a decisão de aceitar um cliente passa a ser tomada por entusiasmo comercial, e a primeira conta que aparece no fim do ano é a que ninguém fez antes de assinar.

O que este requisito exige não é uma projeção, é rastreabilidade. Todo número de mercado usado em material comercial, proposta ou decisão de preço tem de apontar para a fonte que o sustenta ou para o rótulo de estimativa declarada com a conta à vista. Um cenário em que a premissa está escrita pode ser derrubado na reunião seguinte; um número sem origem não pode ser derrubado nem defendido, e vira folclore interno.

A escolha de segmento é a decisão comercial mais cara deste projeto, porque ela define preço, ciclo de venda e esforço de implantação ao mesmo tempo. Por isso ela é explicitada com o segmento escolhido e o segmento recusado, *conforme E2 e E3*, e não como lista de oportunidades. O requisito também trata a margem como grandeza a ser medida por cliente e por linha de receita, não deduzida do total — porque é no total que o serviço esconde o produto.

**Especificações**

- **E1. Universo declarado como fonte única.** Todo número de mercado usado em documento comercial, proposta ou modelo de margem deriva da lista da seção 1, com fonte e data; número novo entra por acréscimo à lista e não por citação avulsa. Verificação: auditoria trimestral de uma amostra de propostas, com rastreio de cada número de mercado até a lista. Nenhum número de mercado circula sem essa linha.
- **E2. Critério de qualificação econômica por segmento.** Cada oportunidade é classificada em um dos cinco segmentos por critério verificável — número de advogados, orçamento anual de software, existência de DPO e de TI própria, processo de compra —, registrado no CRM antes da proposta. Verificação: toda proposta emitida tem segmento e critério preenchidos; proposta sem classificação é rejeitada no fluxo comercial.
- **E3. Mapa de decisão e veto preenchido antes da proposta.** Para cada oportunidade, os papéis de quem paga, decide, usa e veta são nomeados por pessoa, e o caminho de aprovação de segurança da informação ou de compras é identificado. Verificação: proposta só é emitida com o mapa completo; a taxa de perda por veto não mapeado é medida por trimestre e tende a zero.
- **E4. SAM construído por unidade compradora, com TAM declarado como teto.** O SAM é a soma de componentes, cada um com contagem de unidades, origem da contagem, ticket anual e produto; o TAM é publicado apenas como teto e nunca usado em planejamento. Verificação: planilha de uma linha por componente que reproduz o número publicado no documento; componente sem origem declarada não entra na soma.
- **E5. SOM com premissa de conversão recomputável.** Cada curva de receita declara oportunidades por mês, taxa de conversão, ciclo de venda, ticket médio e churn, de modo que o número de clientes e o ARR resultem da aritmética. Verificação: recomputação independente da curva a partir das cinco premissas; desvio superior a 30% da curva por dois trimestres consecutivos reabre a premissa, não o orçamento.
- **E6. Custo de servir decomposto e medido por cliente.** Infraestrutura, sustentação, implantação e canal são apurados por cliente e por trimestre, com meta e teto por linha; a margem bruta reportada é a medida, não a do cenário. Verificação: relatório trimestral por cliente com as quatro linhas e a margem; cliente abaixo do teto entra em plano de reajuste ou de saída.
- **E7. Política de diluição por linha de receita.** Licença e suporte têm piso de margem; implantação é cobrada com margem de projeto e não pode ser vendida abaixo do custo; hardware revendido não é praticado; customização tem teto percentual do contrato e critério de reuso. Verificação: exceção a qualquer regra exige aprovação registrada e a tabela de sensibilidade de E9 anexada.
- **E8. Ponto de equilíbrio do time mínimo publicado e recalculado.** O número de clientes necessário para pagar o time de sustentação é publicado e recalculado a cada mudança de faixa salarial, de encargos ou de ticket. Verificação: tabela publicada com a conta aberta — custo mensal, multiplicador de encargos, margem bruta e ticket — e nota de versão a cada revisão.
- **E9. Teste de sensibilidade obrigatório antes de desconto ou exceção.** Queda de preço de 20%, churn de 15% ao ano, implantação em dobro do tempo e GPU dedicada em metade da base são calculados para o cliente concreto antes de qualquer aprovação comercial fora da tabela. Verificação: pedido de desconto sem a tabela de sensibilidade anexada é recusado pelo fluxo de aprovação.
- **E10. Indicador de contaminação por serviços com gatilho de ação.** Quatro indicadores trimestrais — serviços sobre receita total, horas de customização sobre o contrato, recorrente sobre receita total e reuso de customização — são medidos com limite declarado; estourado o limite, a resposta é recusar o escopo, reprecificar ou isolar o projeto em contrato separado, nunca aceitar por prazo indeterminado. Verificação: painel trimestral com os quatro indicadores e a decisão registrada quando o limite é atingido.
- **E11. Canal como condição de aquisição, não como alternativa.** A meta de aquisição declara qual percentual de oportunidades vem de parceiro e qual vem de venda direta, e o custo de aquisição é apurado por origem. Verificação: relatório trimestral de CAC por origem; se a venda direta responder por mais de 70% das oportunidades em dois trimestres, a estratégia de canal é reaberta como decisão, não como ajuste de meta.

---

## Fontes

- CFOAB, quadro de advogados — https://www.oab.org.br/institucionalconselhofederal/quadroadvogados (consulta 10/11/2026)
- CFC, consulta por região e matéria institucional — https://www3.cfc.org.br e https://cfc.org.br/noticias (10/11/2026 e 25/04/2025)
- Mapa de Empresas / Receita Federal — https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas (dados até 09/2026)
- IBGE, Divisão Territorial Brasileira — https://www.ibge.gov.br/geociencias/organizacao-do-territorio/divisao-territorial.html (Censo 2022)
- ABES/IDC, Mercado Brasileiro de Software 2026 (02/08/2026)
- Benchmarkit, 2025 SaaS Performance Metrics (dados de 2024)
- Robert Half, Guia Salarial 2026, via Exame (01/10/2026)
- Planalto, Lei 14.133/2021 — https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2021/lei/l14133.htm
- Tabelas de preço de IA jurídica: https://juridico.ai/planos · https://ia.jusbrasil.com.br/planos · https://ialocus.com.br · https://asquadz.ai/blog (leitura out–nov/2026)
- Preço de GPU de varejo — https://www.pcbuilder.com.br (17/09/2026)
- Base de fatos interna desta rodada — [12-fontes-e-base-de-fatos.md](12-fontes-e-base-de-fatos.md)

## O que derruba esta recomendação

- **Se o churn anual real for de 15% e não de 5%.** O LTV/CAC cai para 1,9 e a aquisição deixa de se pagar; a resposta não é vender mais, é mudar o modelo de contrato para prazo maior com renovação automática.
- **Se o número de sociedades de advogados com 20+ profissionais ficar muito abaixo de 3.000.** O componente de banca média do SAM cai junto, e com ele a curva base de 39 clientes em 36 meses.
- **Se a relação de CAC de 2,0 se confirmar no Brasil.** Ela é benchmark global e não dado local; se a realidade brasileira for pior, a venda direta fica inviável e o documento [08-parcerias.md](08-parcerias.md) passa de apoio a condição de sobrevivência.
- **Se o custo de servir medido no primeiro cliente ficar acima de 55% da receita.** Isso coloca o produto no cenário conservador por definição, e o cenário conservador não paga o time mínimo em 36 meses.
- **Se o preço de tabela tiver de acompanhar a âncora de R$ 1.099,90/mês do concorrente com air-gapped.** A receita por cliente cai abaixo do custo de implantação, e o segmento endereçável deixa de ser departamento jurídico para ser apenas grande banca.
- **Se a implantação não couber em 60 dias no cliente de referência.** O tempo até valor passa a consumir o patrocínio antes do primeiro resultado, e o ciclo de venda volta a crescer em todos os segmentos ao mesmo tempo.
