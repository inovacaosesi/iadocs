# Precificação e Escala: Preço Defensável e o Caminho para Virar Referência

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Requisitos:** R44 e R45 · **Papel:** preço, empacotamento comercial, métrica de cobrança e posicionamento de mercado do produto instalado no cliente.

Produto instalado no ambiente do cliente não se precifica com a tabela do concorrente. Precifica-se com a conta que
o cliente faz e com o custo que nós temos: hardware que ele compra, implantação que consome horas para receber,
suporte que não existe em autoatendimento e ciclo de venda que dura meses. Cada uma dessas quatro coisas aparece na
margem de um jeito diferente, e tratá-las como um número só é o erro que transforma plataforma em boutique de
projeto. Preço aqui é requisito técnico: verificável, reproduzível por quem vende e falseável por dado.

**Documentos irmãos:** [05-analise-de-gaps.md](05-analise-de-gaps.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [04-mvp-matriz.md](04-mvp-matriz.md) · [07-sustentacao.md](07-sustentacao.md) · [10-concorrentes.md](10-concorrentes.md)

---

## R44. Precificação e empacotamento comercial

**Prioridade:** Essencial · **Verticais:** todas

### Diagnóstico

O mercado brasileiro já precificou o que parece ser este produto, e o número não é generoso. Há oferta de IA jurídica
em modo air-gapped a **R$ 1.099,90/mês** — roda no hardware do cliente, exige GPU e é vendida por assinante
(ialocus.com.br, out/2026). O autoatendimento jurídico satura entre **R$ 49 e R$ 249 por usuário/mês** (asquadz.ai,
fev/2026), e o enterprise é sempre "sob consulta": a Projuris é a única com faixa visível, **~R$ 200+/usuário/mês**
(asquadz.ai, fev/2026). O padrão é claro: o mercado cobra por usuário, e a âncora on-premise existente é o preço de
uma ferramenta de um assento, não de uma plataforma instalada.

| Âncora | Preço publicado | O que está incluído | O que não está |
|---|---|---|---|
| Autoatendimento jurídico | R$ 49–249/usuário/mês | uso do produto, em nuvem | instalação, acervo próprio, suporte |
| Concorrente air-gapped | R$ 1.099,90/mês por assinante | software no hardware do cliente | implantação, curadoria, integração |
| Enterprise jurídico | ~R$ 200+/usuário/mês, sob consulta | gestão, venda consultiva | preço público, previsibilidade |
| **Este produto** | **R$ 10.900 a R$ 48.000/mês por instituição** | plataforma, instalação, suporte, atualização | hardware, egresso |

O teto da faixa também tem referência publicada, ainda que em outra moeda: CoCounsel a **US$ 340,85/mês** na versão de
entrada e **US$ 1.694,90/mês** na completa, e Paxton a **US$ 499/usuário/mês** (haqq.ai, leitura em 20/10/2026, sobre
páginas oficiais). Não há câmbio verificado nesta rodada, então a comparação fica com o leitor — mas ela diz que o
plano Institucional está abaixo do preço internacional de uma ferramenta equivalente, e isso é margem não capturada,
não bondade.

A estrutura de custo do que vendemos é outra. Implantação no cliente é serviço executado por gente: onboarding no
mercado custa de **R$ 500 a R$ 5.000+** (asquadz.ai, fev/2026), e isso é para produto de autoatendimento em nuvem,
sem GPU, sem migração de acervo e sem curadoria. A referência de margem é conhecida: **77% mediana em software por
assinatura, 81% só em assinaturas e 30% em serviços profissionais** (Benchmarkit 2025, dados de 2024). Precificar
instalação como SaaS de autoatendimento garante que a margem de 30% vença, porque é ela que define o negócio quando
o volume de projeto cresce.

A métrica errada destrói a proposta on-premise por três motivos concretos. Primeiro, o cliente já pagou o hardware:
uma RTX 5090 sai por **R$ 31.999,99 no Pix** (pcbuilder.com.br, 17/09/2026), e a energia de um servidor de uma GPU é
de **~R$ 198/mês** sobre R$ 0,4525/kWh da Enel SP (REH ANEEL 3.596/2026, vigência 04/07/2026) — energia não é o
driver de custo, o CAPEX da placa é. Segundo, cobrar por token em Modo A é cobrar do cliente um custo que ele já
pagou, e a primeira pergunta da renovação vira "por que pago por token na minha própria máquina?". Terceiro, o
medidor convida à auditoria: cada renovação passa a discutir contagem em vez de resultado. Token é unidade de custo
de egresso, não de plataforma.

### Decisão proposta

A cobrança é por instituição, com duas dimensões de volume — acervo indexado e usuários ativos — e o preço fica
ancorado dos dois lados. Para cima: **~75% acima do teto do autoatendimento**, comparando R$ 249 × 25 assentos
(R$ 6.225/mês) com os R$ 10.900/mês do plano Essencial. Para baixo: **~60% abaixo do concorrente air-gapped no mesmo
número de assentos**, comparando R$ 1.099,90 × 25 (R$ 27.497,50/mês) com os mesmos R$ 10.900. A diferença para cima
é instalação, suporte e acervo que não sai; a diferença para baixo é que não vendemos assento, vendemos plataforma
com serviço embutido. Alternativa descartada: cobrar por token ou por consulta, porque no Modo A isso transfere ao
cliente um custo que é nosso CAPEX e transforma toda renovação em discussão de medidor.

| Plano | Faixa de implantação | Usuários | Acervo indexado | Receita recorrente |
|---|---|---|---|---|
| Piloto pago | nuvem privada do cliente | até 15 | até 50 mil páginas | R$ 60–90 mil, escopo fechado |
| Essencial | on-premise departamental | até 25 | até 250 mil páginas | R$ 10.900/mês |
| Corporativo | on-premise departamental | até 60 | até 1,5 milhão de páginas | R$ 24.000/mês |
| Institucional | air-gap integral, multiunidade | 100+ | 2 milhões+ | a partir de R$ 48.000/mês |

A conta do Essencial mostra por que o desenho fecha: R$ 130.800/ano de recorrência e R$ 45 mil de implantação dão
R$ 175.800 no primeiro ano, com projeto em 26% da receita — dentro do limite de E4. A recorrente, a 72% de margem,
deixa R$ 94 mil de margem bruta no ano; o projeto, a 30%, deixa R$ 13,5 mil. Quem olha só o segundo número escolhe
o negócio errado.

### Especificações

- **E1. Métrica de cobrança.** A assinatura é por instituição, medida em duas dimensões declaradas em contrato: acervo indexado, em faixas de páginas, e usuários ativos, com franquia e excedente por assento. Nenhuma linha de fatura em Modo A menciona token, consulta ou requisição de modelo. O relatório de uso é entregue todo mês com as duas dimensões medidas e não autodeclaradas, *conforme especificação E2 do requisito R37*. Verificação: contrato-modelo e extrato mensal revisados contra esta regra antes da primeira proposta.
- **E2. Arquitetura de planos.** Quatro planos conforme a tabela acima, cada um amarrado a uma faixa de implantação de *especificação E9 do requisito R38*, sem plano gratuito permanente e sem "sob consulta" para faixa já tabelada. Toda proposta usa o mesmo livro de preços, versionado; variação fora do livro é exceção registrada, *conforme E6*. Verificação: nenhuma proposta enviada no trimestre com valor fora do livro vigente.
- **E3. Piso de contrato.** Nenhum contrato de receita recorrente abaixo de **R$ 120.000/ano** (R$ 10.000/mês). O piso é derivado e não escolhido: o time de sustentação custa **R$ 105–125 mil/mês** de custo total (Base de fatos, seção 7) e um time sustenta de 10 a 12 contratos, o que dá R$ 105–150 mil/ano por contrato. Verificação: relatório de carteira lista todo contrato ativo abaixo do piso; existir um sem renúncia registrada da direção é falha de processo, não desconto.
- **E4. Separação entre recorrente e projeto.** Receita recorrente — licença, suporte de *especificação E1 do requisito R39*, atualização normativa e de software — persegue margem bruta de **70% ou mais**, contra os 77–81% do benchmark de assinatura. Receita de projeto — implantação, integração, migração de acervo, treinamento e hardware — persegue **25% a 35%**, contra os 30% do benchmark de serviços. Nenhum contrato pode ter, no segundo ano, receita de projeto maior que a recorrente. Verificação: DRE por contrato com as duas linhas separadas e razão entre elas apurada no fechamento trimestral.
- **E5. Política de reajuste.** Reajuste anual pelo IPCA (IBGE) na data de aniversário do contrato, comunicado com 60 dias de antecedência, com piso de 0% e sem repasse retroativo. Contrato plurianual fixa a tabela de reajuste na assinatura. Reajuste extraordinário só existe por mudança de escopo comprovada — nova vertical, novo modo de implantação, ampliação de faixa — e nunca por variação de custo interno. Verificação: cláusula-padrão no contrato-modelo e nenhum aditivo de reajuste fora dessas duas hipóteses.
- **E6. Política de desconto com alçada e teto.** O desconto incide sobre a recorrência, nunca sobre a taxa de implantação, nunca sobre o excedente de faixa, e nunca leva o contrato abaixo do piso de E3. **30% é teto absoluto.** Cada exceção exige contrapartida registrada — prazo maior, pagamento anual antecipado, caso de referência publicável ou ampliação de escopo — e entra em relatório trimestral por motivo. Verificação: toda proposta com desconto carrega a alçada, o nome de quem aprovou e a contrapartida.

| Alçada | Desconto máximo | Contrapartida exigida |
|---|---|---|
| Vendedor | 10% | nenhuma além do registro |
| Gestão comercial | 20% | prazo de 24 meses ou pagamento anual |
| Direção | 30% (teto) | caso de referência publicável ou ampliação de escopo |

- **E7. Egresso repassado, nunca embutido.** Consumo externo é linha separada da assinatura, repassado ao preço público vigente do provedor homologado com **30% de administração**, sob teto mensal por cliente configurado no gateway, *conforme especificação E5 do requisito R20* e *conforme especificação E9 do requisito R4*. O cliente pode usar a própria chave: contrata direto o provedor, mantém os mesmos controles e a mesma trilha de auditoria, e paga taxa fixa de **R$ 2.500/mês** pelo broker. Ordem de grandeza: um documento de 30 páginas custa **~US$ 0,06** em modelo de fronteira intermediário e **~US$ 0,20** no topo (Base de fatos, seção 4; câmbio não verificado nesta rodada — [a validar]). Em Modo A a linha é zero, e a proposta diz isso em uma frase.
- **E8. Licenciamento offline.** A licença funciona sem consulta a servidor externo, *conforme especificação E6 do requisito R38*: arquivo assinado, vinculado à impressão digital do servidor, com prazo igual ao do contrato e tolerância de **90 dias** de operação plena após o vencimento antes de entrar em modo somente-leitura. Nenhuma funcionalidade central degrada por falta de conectividade, e a renovação ocorre por arquivo ou mídia física. Verificação: teste de instalação em rede isolada e teste de licença vencida, ambos com resultado arquivado.
- **E9. Prova de conceito paga e regra de conversão.** Piloto custa **R$ 60–90 mil** por 8 a 12 semanas, com escopo fechado — uma vertical, um caso de uso, até 50 mil páginas e 15 usuários, *conforme especificação E9 do requisito R38*. O valor é creditado integralmente no primeiro ano se o contrato for assinado em até 30 dias após o aceite. A conversão é objetiva: quatro dos cinco portões de *especificação E1 do requisito R19* atingidos e dois casos de uso em uso real por duas semanas, alinhado aos critérios de "MVP pronto" do documento 04. Se não atingir, o valor do piloto é retido e o processo termina sem desconto de consolação.
- **E10. Critério objetivo de recusa.** Não se vende quando qualquer uma destas quatro condições aparecer: margem bruta recorrente projetada abaixo de **60%** no segundo ano; payback do custo de implantação acima de **12 meses**; desconto acima do teto de E6; ou cliente que exige preço de autoatendimento, isto é, dentro da faixa de R$ 49–249 por usuário/mês. Verificação: planilha de aprovação de proposta com os quatro números preenchidos e assinados antes do envio.
- **E11. Recalibração com custo medido.** A tabela é revisada a cada seis meses contra o custo unitário medido de *especificação E2 do requisito R37* — custo por página indexada, por consulta e por usuário ativo. Nenhuma tabela fica vigente mais de 12 meses sem essa revisão. Se o custo por página cair, o que se move é o limite de faixa, não o preço-base: preço que cai sozinho ensina o cliente a esperar.

---

## R45. Escala de mercado e posicionamento de referência

**Prioridade:** Importante · **Verticais:** todas

### Diagnóstico

O universo é grande e mensurável: **1.514.918 advogados inscritos** na OAB (CFOAB, consulta 10/11/2026), **550.864
profissionais da contabilidade** ativos e **97.836 organizações contábeis** (CFC, 2025/2026), sobre **~25,7 milhões
de empresas ativas** (Mapa de Empresas, dados até set/2026). O mercado comprador de software e serviços é de
**US$ 35,4 bilhões em 2025**, com software em **US$ 21,7 bilhões (+21,4%)** e gasto com IA generativa projetado em
**US$ 1,9 bilhão em 2026 (+36,1%)** (ABES/IDC, publicado 02/08/2026). Mercado grande, porém, não é plano: nenhuma
dessas linhas diz quantos clientes compram o que vendemos.

Os benchmarks de modelo de negócio dão o resto do diagnóstico, e são menos confortáveis: **margem bruta mediana de
77%**, **NRR de 101%**, **GRR de 88%**, **CAC ratio de 2,0** — US$ 2 de vendas e marketing por US$ 1 de ARR novo — e
**crescimento mediano de 26%** (Benchmarkit 2025, dados de 2024). Com CAC ratio 2,0 e margem de 77%, o payback
implícito é de **~31 meses** [estimativa declarada: 24 meses de ARR de CAC divididos por 0,77 de margem]. Num negócio
on-premise com 40% da receita do primeiro ano em projeto a 30% de margem, o mesmo CAC leva o payback a **~40 meses**
e a margem consolidada a **~60%** [estimativa declarada: 0,6 × 77 + 0,4 × 30]. Isso não é preferência sobre canal: é
aritmética dizendo que venda direta com CAC de SaaS em nuvem não fecha nesse modelo, e que a venda conduzida pelo
fundador nos primeiros contratos é a única forma de o CAC existir.

"Virar referência" hoje é uma frase sem unidade. Não há dado público de participação nesse nicho, e a única métrica
que importa — ser lembrado sem ter sido convidado — não está em painel nenhum. Ela precisa ser construída por
medição própria, com questionário de win/loss, ou continuará sendo adjetivo.

O risco de posicionamento é conhecido e tem prazo: enquanto o produto for tecnicamente distinto, concorrente de bolso
cobrando um décimo não compete na mesma conversa. Quando a distinção virar lista de recursos copiáveis, a defesa passa
a ser a prova publicada e a base instalada, não o discurso — e nenhuma das duas existe no ano um.

| Vertical | Universo medido | Fonte do universo | Por que nesta ordem |
|---|---|---|---|
| Jurídico | 1.514.918 advogados | CFOAB, 10/11/2026 | maior valor por caso e maior exigência de citação |
| Contábil-fiscal | 550.864 profissionais · 97.836 organizações | CFC, 2025/2026 | resultado mensurável, ciclo mais curto |
| Terceira vertical | — | — | só com dado de win/loss, não por intuição |

### Decisão proposta

Crescer por vertical, uma por vez, com prova técnica publicada e venda conduzida pelo fundador até o gatilho de
contratação; a referência é definida por quatro números verificáveis com prazo, não por percepção. Alternativa
descartada: expansão por funcionalidade — entregar mais recursos a todos os segmentos ao mesmo tempo —, porque dilui
o conjunto de avaliação de *especificação E1 do requisito R22* e transforma cada venda numa demonstração diferente,
que é exatamente o que impede medir qualidade e comparar trimestres.

| Indicador | Benchmark (Benchmarkit 2025) | Meta desta operação |
|---|---|---|
| Margem bruta recorrente | 77% (assinaturas: 81%) | ≥ 70% |
| Margem bruta de projeto | 30% | ≥ 30% |
| NRR | 101% | ≥ 101% |
| GRR | 88% | ≥ 88% |
| CAC ratio | US$ 2,00 por US$ 1,00 de ARR novo | ≤ 2,0 |
| Crescimento de ARR | 26% ao ano | ≥ 26% |

### Especificações

- **E1. Definição operacional de referência.** Ser referência significa, cumulativamente, até **31/12/2028**: **30 contratos ativos** em produção em pelo menos **3 verticais**; **ARR de R$ 8 milhões**; **GRR ≥ 88% e NRR ≥ 101%** medidos em janela de 12 meses, contra os benchmarks da tabela acima; e menção espontânea em **50% ou mais** das listas curtas de concorrências em que a empresa participa, medida por questionário trimestral de win/loss. Abaixo disso, a palavra "referência" não aparece em material comercial. Verificação: painel trimestral com os quatro números e a data de apuração.
- **E2. Expansão por vertical, com ordem de ataque.** Jurídico primeiro: maior concentração de valor por caso e maior exigência de citação verificável, que é onde os portões de *especificação E1 do requisito R19* valem mais como diferencial. Contábil-fiscal segundo: **550.864 profissionais** e **97.836 organizações** (CFC), resultado mais mensurável e ciclo mais curto. A terceira vertical só é escolhida com dado de win/loss. Nenhuma vertical nova entra antes de a anterior passar dois trimestres em produção nos portões de R19, *conforme especificação E5 do requisito R40* e *conforme especificação E10 do requisito R22*.
- **E3. Prova técnica pública como ativo comercial.** Publicar, por vertical, o resultado no conjunto de avaliação de *especificação E1 do requisito R22* contra os cinco portões de *especificação E1 do requisito R19*, com versão de modelo, perfil de hardware e data de apuração declarados, *conforme especificação E9 do requisito R22*. O corpus publicado é sintético ou público, ou de cliente que autorizou por escrito: o conjunto dourado é acervo sensível e não vira peça de marketing sem consentimento. O benchmark publicado é o único material comercial que não envelhece mal, porque é datado e reproduzível por quem quiser repetir o teste.
- **E4. Escada comercial e gatilho de contratação.** O fundador conduz os **8 primeiros contratos**, aproximadamente o primeiro ano. O primeiro vendedor é contratado quando três condições ocorrem juntas: **8 contratos ativos**, **ARR de R$ 1,5 milhão** e pipeline com cobertura de **3× a meta trimestral** por dois trimestres consecutivos. O segundo vendedor só entra depois de o primeiro bater meta por dois trimestres. Verificação: registro em CRM com a data de cada condição atingida e a decisão de contratação assinada.
- **E5. Indicadores de escala e meta.** Os seis indicadores da tabela acima são medidos trimestralmente com definição escrita de cada um. Margem consolidada do primeiro ano não é indicador de saúde — com projeto em 40% da receita, ela cai para ~60% por construção, e olhar esse número isolado faz a empresa cortar preço para melhorá-lo, que é o caminho mais curto para virar boutique. Verificação: uma página por trimestre, com as seis linhas e a memória de cálculo.
- **E6. Produtividade por vendedor.** Com ciclo de venda de **6 a 9 meses** [estimativa declarada; premissa: três a cinco reuniões até proposta e duas aprovações internas no cliente — a validar com os 10 primeiros processos], cada vendedor precisa fechar **4 a 6 contratos novos por ano**, o que no piso de R$ 120 mil/ano dá R$ 480–720 mil de ARR novo por vendedor. O custo total do vendedor, com encargos de ~1,7 a 1,8× o salário bruto (Base de fatos, seção 7), precisa caber em metade do ARR novo que ele gera; se não couber, a venda continua com o fundador e não se contrata.
- **E7. Gatilhos de internacionalização.** Não agora, e a regra é explícita: só se abre operação fora do Brasil com **ARR doméstico ≥ R$ 25 milhões**, **NRR ≥ 110% por quatro trimestres**, **três verticais maduras** e um sócio com mandato exclusivo para isso. A ordem, se acontecer, é América Latina antes de Europa e Estados Unidos, porque parte do argumento — residência local do dado e enquadramento na LGPD — não viaja, e cada país exige corpus normativo, idioma e suporte próprios, sustentados pelo mesmo time enxuto descrito no documento 07. **[Fase 2]**
- **E8. O que recusar para não virar boutique.** Recusa registrada, com motivo, para: desenvolvimento sob medida fora do modelo de extensão de *especificação E2 do requisito R40*; exclusividade por vertical ou por região; operação do acervo do cliente pelo nosso time, que é BPO e não produto; e qualquer contrato que exija preço de autoatendimento. Três recusas iguais no mesmo trimestre não são três perdas: são uma decisão de produto mal tomada, e viram item de roadmap com dono e prazo.
- **E9. Medição de win/loss e disposição a pagar.** Todo processo perdido tem entrevista em até 30 dias, com três perguntas fixas: preço, confiança técnica e qual alternativa foi escolhida. O livro de preços de R44 é revisado com esse dado a cada seis meses. Sem essa rotina, o preço praticado é a opinião do vendedor mais convincente da equipe, e isso não é política comercial.

---

## Fontes

- **Preço e posicionamento de concorrentes:** juridico.ai/planos; ia.jusbrasil.com.br/planos; ialocus.com.br (12/05/2026, rev. 15/10/2026 — autopublicidade do fornecedor, tratar como indício); turivius.com; asquadz.ai/blog (05/02/2026); haqq.ai/blog (20/10/2026).
- **Benchmarks de modelo de negócio:** Benchmarkit, *2025 SaaS Performance Metrics* (dados de 2024).
- **Mercado e universo:** ABES/IDC, *Mercado Brasileiro de Software 2026* (02/08/2026); OAB/CFOAB, oab.org.br/institucionalconselhofederal/quadroadvogados (consulta 10/11/2026); cfc.org.br (2025/2026); gov.br — Mapa de Empresas (dados até set/2026).
- **Custo de egresso:** platform.claude.com/docs/en/about-claude/pricing; developers.openai.com/api/docs/pricing; aistudio.google.com/docs/pricing; together.ai/pricing (leitura 10/11/2026).
- **Hardware e energia:** pcbuilder.com.br (17/09/2026); Enel SP e REH ANEEL 3.596/2026 (vigência 04/07/2026); AWS sa-east-1 e Azure Retail Prices API para Brazil South (consulta 10/11/2026).
- **Pessoal:** Robert Half, *Guia Salarial 2026*, via Exame (01/10/2026).
- **Interno:** [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [03-registro-decisoes.md](03-registro-decisoes.md) · [04-mvp-matriz.md](04-mvp-matriz.md) · [05-analise-de-gaps.md](05-analise-de-gaps.md).

Nenhum valor em dólar foi convertido para real: o câmbio não foi verificado nesta rodada. **[a validar]**

---

## O que derruba esta recomendação

1. **O acervo real é maior que a faixa.** Se, nos dez primeiros clientes, mais da metade passar de 1,5 milhão de páginas indexadas, a tabela de R44/E2 está errada na dimensão que mais importa e precisa ser refeita por página, não por usuário.
2. **A disposição a pagar fica abaixo do piso.** Se dez propostas no segmento de 25 usuários fecharem abaixo de R$ 10.000/mês, o piso de R$ 120 mil/ano não se sustenta — e a resposta correta é reduzir escopo de produto, não reduzir preço.
3. **O concorrente air-gapped vira plataforma.** Se a oferta de R$ 1.099,90/mês passar a incluir implantação, curadoria e suporte, a âncora sobe de patamar e a diferença de 60% descrita em R44 deixa de ser argumento.
4. **O GRR medido fica abaixo de 88%.** Renovação abaixo do benchmark significa que o preço está acima do valor entregue e que o problema é o produto, não a tabela.
5. **O preço de API cai e muda a conversa.** Modelo aberto hospedado já custa **US$ 0,15/US$ 0,60** por milhão de tokens, contra **US$ 2–10/US$ 10–50** do modelo de fronteira. Se o comprador passar a comparar com o piso aberto, o argumento de economia de R37/E1 perde força. O argumento de soberania não perde, e é por isso que o preço nunca deve ser justificado por economia de token.
6. **O time não sustenta a carteira.** Se a sustentação de 12 contratos exigir mais do que o time enxuto projetado no documento 07, o piso de contrato sobe e o plano Essencial deixa de existir na faixa em que está tabelado.

O critério de reversão é o mesmo das decisões D1 a D4: um número observável, um prazo e uma decisão. Sem isso, esta recomendação é preferência.
