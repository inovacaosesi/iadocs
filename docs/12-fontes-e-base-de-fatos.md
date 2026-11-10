# Fontes e Base de Fatos Verificados

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Papel:** anexo de evidência. Reúne, com fonte e data, os números de mercado usados nos documentos [05-analise-de-gaps.md](05-analise-de-gaps.md) a [11-publico-alvo-e-margem.md](11-publico-alvo-e-margem.md).

Este anexo existe por um motivo prático. Os documentos de negócio citam preço de concorrente, salário, tarifa de energia, preço de GPU em nuvem e tamanho de mercado. Cada um desses números precisa de uma casa. Espalhados por seis documentos, eles divergem na primeira revisão; reunidos aqui, envelhecem juntos e se corrigem uma vez só. Nenhum número deste anexo deve ser usado sem a linha de fonte que o acompanha, e os documentos que o citam apontam para a seção correspondente.

**Data da pesquisa:** 10/11/2026. **Moeda:** BRL salvo indicação. **Câmbio USD→BRL não verificado nesta pesquisa** — não converti valores.
**Legenda de confiança da fonte:** `[O]` oficial (órgão/empresa dona do dado) · `[I]` imprensa · `[T]` terceiro/consultoria · `[E]` estimativa minha (cálculo explícito) · `[sem fonte]`

---

## 1. Tamanho de mercado — Brasil

| Item | Número | Fonte | Data do dado | Tipo |
|---|---|---|---|---|
| Advogados inscritos na OAB | **1.514.918** (quadro geral 1.635.150, inclui 12.206 estagiários, 108.026 suplementares) | oab.org.br/institucionalconselhofederal/quadroadvogados | consulta 10/11/2026 (atualiza diariamente) | [O] |
| Maior seccional | SP 397.309 · RJ 164.149 · MG 152.153 | idem | idem | [O] |
| Sociedades de advogados registradas | **não publicado** no painel do CFOAB; não localizei número oficial consolidado | — | — | [sem fonte] |
| Profissionais da contabilidade ativos | **550.864** | www3.cfc.org.br (consulta por região) | 10/11/2026 | [O] |
| Organizações contábeis ativas | **97.836** | cfc.org.br/noticias (materia institucional) | 25/04/2025 | [O] |
| Empresas ativas no Brasil | **~25,7 milhões** | gov.br — Mapa de Empresas / Receita Federal | dados até set/2026 | [O] (não reconferido na fonte primária) |
| Municípios | **5.570** | IBGE — Divisão Territorial | Censo 2022 | [O] (página bloqueou acesso; valor de conhecimento consolidado) |
| Mercado brasileiro de TI (2025) | **US$ 67,8 bi** (+18,5%); 10º mundial; 38,4% da América Latina | ABES/IDC — Mercado Brasileiro de Software 2026 | publicado 02/08/2026 | [T] |
| Mercado de **software** (2025) | **US$ 21,7 bi** (+21,4%) | idem | idem | [T] |
| Software + serviços (mercado comprador, 2025) | **US$ 35,4 bi** (+16,7%); ~1,5% do mercado mundial | idem | idem | [T] |
| Gastos com **IA/IA generativa** (projeção 2026) | **US$ 1,9 bi** (+36,1% — maior crescimento do estudo) | idem | projeção p/ 2026 | [T] |
| Verticais que mais gastam | Financeiro US$ 8,99 bi (25,4%) · Serviços/telecom US$ 8,61 bi (24,3%) · Indústria US$ 6,92 bi (19,5%) | idem | 2025 | [T] |
| Gasto com serviços jurídicos no Brasil | **não localizado** número agregado público | — | — | [sem fonte] |

**Leitura para discovery:** ~1,5 mi de advogados + ~0,55 mi de profissionais contábeis + ~98 mil escritórios contábeis formam o universo de usuários individuais; o orçamento de software do país é US$ 21,7 bi e cresce 21%/ano.

---

## 2. Concorrentes diretos e indiretos no Brasil

| Produto | O que faz / público | Cobrança | **Preço publicado** | Fonte / data |
|---|---|---|---|---|
| **Jurídico AI** | IA jurídica (chat, jurisprudência, análise de caso/documento); advogado individual | por assinatura, por usuário; mensal ou anual; PIX sob contato | **a partir de R$ 55,92/mês** (anual); **Crescimento R$ 129,90/mês** (anual R$ 77,94); **Escala R$ 249,90/mês** (anual R$ 149,94); grátis = 1 caso/1 documento/1 processo/10 usos | juridico.ai + /planos, leitura out–nov/2026 | [O] |
| **Jus IA** (Jusbrasil) | IA sobre acervo Jusbrasil + documentos | por usuário; mensal/anual (−33%); corporativo sem preço | **Essencial R$ 78,90** (30 msg + 10 uploads) · **Profissional R$ 108,90** (150 msg) · **Premium R$ 208,90** (ilimitado); 1º mês R$ 1,90 | ia.jusbrasil.com.br/planos, 2026 | [O] |
| **Locus.IA** | IA jurídica, inclui modo air-gapped local | por assinante; tiers por volume de análises | **R$ 149,90 / 249,90 / 499,90 / 699,90** (50/100/200/300 análises; custo por análise R$ 3,00→R$ 2,33); **Local Air-Gapped R$ 1.099,90/mês** (roda no hardware do cliente, exige GPU); Enterprise sob consulta ("modo Soberania") | ialocus.com.br (blog do próprio fornecedor), 12/05/2026, rev. 15/10/2026 | [I] (autopublicidade) |
| **Turivius** | Pesquisa e análise jurisprudencial com IA | demonstração | **não publicado** (venda consultiva) | turivius.com (sem /planos; 404); confirmado em ialocus.com.br | [I] |
| **Projuris** | Gestão jurídica enterprise (departamentos, grandes bancas) | por usuário, venda consultiva | **~R$ 200+/usuário/mês**, "completo sob consulta" | asquadz.ai/blog, 05/02/2026 | [T] |
| **Legal One** (Thomson Reuters) | Gestão jurídica enterprise | por usuário, demo | **não publicado / sob consulta** | asquadz.ai, 05/02/2026 | [T] |
| **Themis** | Gestão jurídica enterprise | demo | **não publicado** | idem | [T] |
| **SAJ ADV** (Softplan) | Gestão para escritórios | por usuário | **R$ 79–159/usuário/mês** | idem | [T] |
| **Astrea** | Gestão para escritórios | por usuário | **R$ 89–179/usuário/mês** | idem | [T] |
| **ADVBox** | Gestão + financeiro + API | por usuário | **R$ 99–249/usuário/mês** | idem | [T] |
| **EasyJur** | Gestão com IA generativa em planos de entrada | por usuário | **R$ 69–149/usuário/mês** | idem | [T] |
| **Juridiq** | Gestão jurídica de entrada | por usuário | **R$ 49–99/usuário/mês** | idem | [T] |
| **Judit** | Monitoramento processual + créditos de IA (categoria adjacente) | créditos | **R$ 39,90 / 89,90 / 249,90** | ialocus.com.br, 15/10/2026 | [I] |
| **ChatADV** | Chat jurídico | assinatura | citado como "faixa de entrada do mercado"; valor não conferido | idem | [I] |
| **Looplex, Deep Legal, Kurier, Aurum, Finch, Sync, Toogle, Netlex, D4Sign** | documentação/contratos, GED, assinatura, IA documental | por usuário ou contrato | **não verificado individualmente nesta pesquisa** — tratar como "sob consulta" até checagem | — | [sem fonte] |

**Serviços atrelados (referência de custo de implantação no mercado):** onboarding R$ 500–5.000+; treinamento ao vivo R$ 150–500/h; migração de dados e armazenamento acima de 5–20 GB cobrados à parte — `asquadz.ai/blog`, 05/02/2026 [T].

**Padrões observados:** (a) autoatendimento jurídico satura em **R$ 50–250/usuário/mês**; (b) enterprise (Projuris, Legal One, Themis) é **sempre "sob consulta"**; (c) já existe oferta **air-gapped a R$ 1.099,90/mês** — âncora de preço do nicho on-premise.

---

## 3. Concorrentes internacionais — preço conhecido

| Fornecedor | Preço publicado | Observação | Fonte / data |
|---|---|---|---|
| **CoCounsel** (Thomson Reuters) | **US$ 340,85/mês** (Essentials, equipes internas) · **US$ 882,30/mês** (com Practical Law) · **US$ 1.694,90/mês** (CoCounsel Legal) | escritórios via configurador; desconto 12% (2 anos) / 18% (3 anos) em Westlaw Advantage | haqq.ai/blog (leitura das páginas oficiais em 20/10/2026) | [T] |
| **Paxton AI** | **US$ 499/usuário/mês** ou US$ 2.999/usuário/ano | preço publicado | idem | [T] |
| **Genie AI** | US$ 75/mês (1 usuário) · US$ 320/mês (5 usuários) · enterprise a partir de US$ 600/mês | idem | idem | [T] |
| **Harvey** | **não publicado** (harvey.ai/pricing = 404) | estimativas de terceiros: **US$ 1.200/assento/ano** (Artificial Lawyer, abr/2024 e jun/2025) e, em outro roundup, **US$ 1.200–2.000+/assento/mês com mínimo de 20–25 assentos/12 meses**; a Harvey contestou as premissas ("wildly off") | bindlegal.com (rev. 06/11/2026) | [T]/[I] — divergência de 12x entre fontes; tratar como relato |
| **Legora, Spellbook, Luminance, Alexi, Ivo, Eve, Robin AI, Lexis+ Protégé, Everlaw** | **não publicado** (11 de 20 fornecedores checados) | Spellbook: teste de 7 dias sem valor; Alexi: trial guiado | haqq.ai, 20/10/2026 | [T] |
| **Robin AI** | não vende mais como produto independente | braço de serviços vendido à Scissero (dez/2025); ≥18 funcionários contratados pela Microsoft (Bloomberg Law, 14/01/2026) | haqq.ai | [I] |
| **vLex/Vincent, Hebbia, Glean** | **não cobertos** pela checagem acima; sem preço verificado | — | — | [sem fonte] |

**Referência de custo de stack barata:** Claude Pro US$ 20/mês e ChatGPT Business US$ 25/assento/mês são o piso do "advogado solo usando IA" — `haqq.ai`, 20/10/2026 [T].

---

## 4. Preço de API de modelo de fronteira (custo de egresso) — USD por 1M tokens

**Tabelas lidas em 10/11/2026 nas páginas oficiais dos provedores.**

| Provedor / modelo | Input | Output | Cache hit | Fonte |
|---|---|---|---|---|
| Anthropic **Claude Fable 5.2** (topo) | 8,00 | 40,00 | 0,20 | platform.claude.com/docs/en/about-claude/pricing [O] |
| Anthropic **Claude Opus 5.5** | 4,00 | 20,00 | 0,20 | idem [O] |
| Anthropic **Claude Sonnet 5.5** (intermediário) | 2,00 | 10,00 | 0,10 | idem [O] |
| Anthropic **Claude Haiku 5.5** (≤100k tokens) | 0,10 | 0,50 | 0,05 | idem [O] |
| OpenAI **gpt-6-astra** (topo) | 10,00 | 50,00 | 1,00 | developers.openai.com/api/docs/pricing [O] — >272k input: 20/75 |
| OpenAI **gpt-6.1-sol** | 2,00 | 10,00 | 0,10 | idem [O] |
| OpenAI **gpt-5-mini** | 0,25 | 2,00 | 0,025 | idem [O] |
| OpenAI **embedding 3-small / 3-large** | 0,02 / 0,13 | — | — | idem [O] |
| Google **Gemini 4 Carbon** | 2,00 (até 30/11/2026) → 4,00 | 10,00 → 20,00 | — | aistudio.google.com/docs/pricing [O] — cobra tokens de raciocínio |
| Google **Gemini 3.1 Pro** | 2,00 (≤200k) / 4,00 | 12,00 / 18,00 | — | idem [O] |
| Google **Gemini 3.5 Flash-Lite** | 0,30 | 2,50 | — | idem [O] |
| Google **Gemini Embedding** | 0,15 (texto) | — | — | idem [O] |

**Modelos abertos hospedados (referência de "modelo aberto servido por terceiro"):**

| Modelo | Input | Output | Fonte |
|---|---|---|---|
| **gpt-oss-120B** (Together) | 0,15 | 0,60 | together.ai/pricing [O], 10/11/2026 |
| **Qwen3.7-Plus** | 0,32 | 1,28 | idem |
| **Qwen3.7-Max** | 2,50 (0,50 cache) | 7,50 | idem |
| **DeepSeek V4.1 Flash** | 0,30 (0,006 cache) | 1,20 | idem |
| **DeepSeek API direto** — v4-pro off-peak | 0,66 | 1,98 | api-docs.deepseek.com [O] (peak = 2x) |
| **DeepSeek API direto** — flash off-peak | 0,15 | 0,60 | idem |
| **GPU alugada por hora** H100 / H200 / B200 (Together) | 3,99 / 5,99 / 8,19 US$/GPU·h (preemptible: 1,99 / 2,99 / 4,09) | — | idem |

**Faixa útil para o business case de egresso:** modelo de fronteira ≈ **US$ 2–10 entrada / US$ 10–50 saída** por 1M tokens; modelo aberto hospedado ≈ **US$ 0,15 / 0,60**. Um documento de 30 páginas (~20k tokens in, ~2k out) custa ~US$ 0,06 no Sonnet 5.5 e ~US$ 0,20 no Fable 5.2 `[E]`.

---

## 5. Hardware com GPU no Brasil

| Item | Preço | Consumo | Fonte / data |
|---|---|---|---|
| **NVIDIA RTX 5090** (consumidor, 32 GB) | **R$ 31.999,99 no Pix** (Gigabyte Gaming OC, Pichau); artigo fala em "modelos perto de R$ 32 mil"; EUA: US$ 6.395–6.449 (set/2026), sugerido US$ 1.999 | TDP 575 W `[sem fonte nesta pesquisa]` | pcbuilder.com.br, oferta de 17/09/2026 [I] |
| **NVIDIA DGX Spark / GB10** | preço **não publicado** na página do produto (só "Where to Buy") | **PSU 240 W, TDP do GB10 140 W** | nvidia.com/en-us/products/workstations/dgx-spark/ [O], 10/11/2026 |
| …especificação DGX Spark | 64 GB ou 128 GB LPDDR5X unificada (273 GB/s), até 4 TB NVMe, 1 petaFLOP FP4, ConnectX-7 200 Gbps | — | idem |
| **L40S / RTX 6000 Ada / A6000 — servidor ou estação de 1 a 4 GPUs** | **não publicado** — vendido por revenda Dell/HPE/Lenovo/Supermicro sob consulta; não localizei tabela pública em BRL | — | [sem fonte] |
| **Energia — Enel SP, grupo A4 (2,3–25 kV), azul** | **R$ 0,4525/kWh fora ponta** · R$ 0,633/kWh na ponta · demanda R$ 19,04/kW (fora ponta) / R$ 31,75/kW (ponta) | — | Enel SP + **REH ANEEL 3.596/2026**, vigência 04/07/2026 (reajuste médio +15%) [O] |
| **Energia — A2 (88–138 kV)** | R$ 0,3968/kWh fora ponta · R$ 0,5773/kWh ponta | — | idem [O] |
| Baixa tensão comercial (B3) | não publicada na página da distribuidora; consultar ANEEL | — | [sem fonte] |

**Conta de energia de um servidor de inferência `[E]`:** 1 GPU classe L40S em servidor de ~600 W, 730 h/mês = 438 kWh × R$ 0,4525 ≈ **R$ 198/mês** de energia por servidor. Um rack de 4 GPUs a ~2,5 kW ≈ **R$ 826/mês**. Energia **não** é o driver de custo do on-premise — o CAPEX da GPU é.

---

## 6. GPU em nuvem na região São Paulo

**AWS sa-east-1 — preço on-demand Linux, tabela oficial de preços (arquivo `AmazonEC2/current/sa-east-1/index.csv`, vigência 01–07/11/2026)** `[O]`:

| Instância | GPU | US$/hora | US$/mês (730h) `[E]` |
|---|---|---|---|
| g4dn.xlarge | 1× T4 | 0,894 | 653 |
| **g6.xlarge** | 1× L4 | **1,368** | 999 |
| g5.xlarge | 1× A10G | 1,710 | 1.248 |
| g6.48xlarge | 8× L4 | 22,693 | 16.566 |
| g5.48xlarge | 8× A10G | 27,686 | 20.211 |
| p4d.24xlarge | 8× A100 40 GB | 35,557 | 25.957 |
| **p5.48xlarge** | 8× H100 | **92,467** | 67.501 |

*Comparação:* a mesma g6.xlarge custa US$ 0,8048/h em us-east-1 (vantage.sh) — **São Paulo é ~1,7× mais caro**.

**Azure Brazil South — Azure Retail Prices API (`armRegionName eq 'brazilsouth'`), consulta 10/11/2026** `[O]`:

| SKU | GPU | US$/hora |
|---|---|---|
| Standard_NC4as_T4_v3 | 1× T4 | 0,894 |
| Standard_NV6ads_A10_v5 | 1/6× A10 | 0,908 |
| Standard_NC16as_T4_v3 | 1× T4 (16 vCPU) | 2,046 |
| Standard_NC48ads_A100_v4 | 2× A100 | 14,692 |
| Standard_ND96amsr_A100_v4 | 8× A100 80 GB | 65,540 |
| Standard_ND96isr_MI300X_v5 | 8× MI300X | 96,00 |
| Standard_ND96isr_H200_v5 | 8× H200 | 169,60 |
| Standard_ND128isr_NDR_GB200_v6 | 4× GB200 (NVL72) | 216,32 |

**Google Cloud southamerica-east1:** preço **não obtido** — a página de GPUs não renderiza tabela e a Cloud Billing Catalog API exige chave; disponibilidade de GPU na região não confirmada. **Magalu Cloud:** a página de preços anuncia apenas Compute/Storage/Database/Network e **não menciona GPU**; calculadora não carrega `[sem fonte]`. Oracle/outros provedores BR: não verificados.

---

## 7. Custo de pessoal no Brasil (mensal, BRL, bruto)

| Cargo | Faixa | Fonte / data |
|---|---|---|
| **Engenheiro de IA** | 25º p R$ 19.500 · **50º p R$ 25.000** · 75º p R$ 27.100 | Robert Half Guia Salarial 2026, via Exame, 01/10/2026 [T] |
| Especialista IA/ML · Engenheiro de prompt | R$ 17.950–23.550 · R$ 19.050–26.100 | idem |
| **Cientista de dados** | R$ 14.700–24.600, mediana **R$ 19.100** (Robert Half); ~R$ 11.000 média CAGED | idem |
| **Engenheiro de dados** | R$ 13.500 (pleno) · R$ 18.000 (sênior) — tabela de referência do governo federal para TI | idem |
| **DevOps/SRE** | **não localizado** em fonte com data 2026 | — [sem fonte] |
| **Analista de suporte N1/N2** | **não localizado** em fonte com data 2026 | — [sem fonte] |
| **Consultor de implantação** | **não localizado** | — [sem fonte] |
| **Pré-vendas técnico** | **não localizado** | — [sem fonte] |
| **Gerente de projetos** | **não localizado**; proxies: Gerente de TI R$ 21.800 / 28.300 / 36.500 (25/50/75) · Gerente de Infraestrutura R$ 17.400 / 22.600 / 29.100 · Gerente de Dados R$ 22.700–37.950 | Robert Half 2027 (site), e 2026 via Exame [T] |
| Cibersegurança (referência de mercado adjacente) | analista pleno R$ 8.500–14.300 · sênior R$ 11.300–19.000 · coordenador R$ 18.000–24.650 · gerente R$ 22.250–37.250 | Exame/Robert Half, 01/10/2026 [T] |
| **Encargos trabalhistas CLT** | **~68–82% sobre o salário** `[E]` — composição legal: INSS patronal 20%, FGTS 8%, 13º 8,33%, férias + 1/3 11,11%, aviso prévio e provisões de rescisão. **Multiplicador de custo total: ~1,7–1,8× o salário bruto** | cálculo meu a partir das alíquotas legais; **sem fonte de pesquisa salarial que consolide o percentual** |

**Uso no modelo:** um time enxuto de sustentação com 1 engenheiro de IA (R$ 25 mil), 1 engenheiro de dados (R$ 15 mil), 2 analistas de suporte (R$ 5–7 mil cada) e 1 consultor de implantação (R$ 9–12 mil) ≈ **R$ 60–70 mil/mês brutos → R$ 105–125 mil/mês de custo total** `[E]`.

---

## 8. Benchmarks de modelo de negócio SaaS B2B

| Métrica | Valor | Fonte / data |
|---|---|---|
| **Ticket de software jurídico no Brasil** — autoatendimento | R$ 49–249/usuário/mês (solo: R$ 49–249; 10 usuários: R$ 490–2.490) | asquadz.ai, 05/02/2026 [T] |
| Ticket — enterprise jurídico | R$ 200+/usuário/mês, sob consulta | idem |
| Ticket — IA jurídica publicada | R$ 55,92 a R$ 1.099,90/mês | seção 2 [O] |
| Implantação cobrada à parte | R$ 500–5.000+ por cliente | asquadz.ai [T] |
| **Margem bruta mediana SaaS** (receita total) | **77%** (assinaturas: 81%; serviços profissionais: 30%) | Benchmarkit 2025 SaaS Performance Metrics (dados 2024) [T] |
| NRR / GRR medianos | 101% / 88% (GRR era 90% três anos antes) | idem |
| New CAC ratio | US$ 2,00 de S&M por US$ 1,00 de novo ARR (+14% desde 2022) | idem |
| OPEX como % da receita | S&M 37% · P&D 34% · G&A 24% | idem |
| Crescimento mediano | 26% realizado em 2024 | idem |
| **CAC e churn específicos do Brasil** | **não localizados** dados públicos consolidados | — [sem fonte] |

**Implicação para o produto:** hardware e serviços de implantação corroem a margem de 77% — o modelo on-premise tende a se parecer com "software + serviços" (30% de margem em serviços), o que exige separar receita recorrente (licença/suporte) de receita de projeto.

---

## 9. Regulação e compras públicas

| Tema | O que a norma diz | Fonte |
|---|---|---|
| **Lei 14.133/2021 — escopo** | cobre expressamente "contratações de tecnologia da informação e de comunicação" (art. 2º, VII) | Planalto, texto compilado [O] |
| **Soberania / tecnologia nacional (art. 26, §7º)** | para implantação, manutenção e aprimoramento de **sistemas de TIC estratégicos** definidos por ato do Executivo federal, a licitação **"poderá ser restrita a bens e serviços com tecnologia desenvolvida no País"**, produzidos sob o processo produtivo básico (Lei 10.176/2001) | idem [O] |
| **Julgamento por técnica e preço (art. 36, §1º, III)** | permitido para "bens e serviços especiais de TIC", com peso técnico de até 70% | idem [O] |
| **Pregão (art. 29, § único)** | aplicável a objeto com especificação usual de mercado; vedado para serviços técnicos intelectuais | idem [O] |
| **Prazos mínimos de edital (art. 55)** | bens: **8 dias úteis** (menor preço/maior desconto), 15 nos demais · serviços comuns: **10 dias úteis** · serviços especiais: **25 dias úteis** · técnica e preço: **35 dias úteis** | idem [O] |
| **Software de uso difundido (art. 43, §2º)** | contratação de soluções baseadas em software de uso difundido deve seguir regulamento com processo de gestão estratégica | idem [O] |
| **Prazo típico de contratação** | mínimo legal 10–35 dias úteis de divulgação; **prazo real de ponta a ponta não localizado** (fase interna + homologação + recursos) | — [sem fonte] |
| **LGPD (Lei 13.709/2018)** | transferência internacional de dados só para países/organismos com grau adequado ou mediante garantias (art. 33) — **residência local dispensa essa análise** e é argumento de venda | conhecimento consolidado — não reconferido no Planalto nesta pesquisa |
| **CNJ — IA no Judiciário** | **Resolução CNJ 332/2020** disciplina uso de IA no Poder Judiciário (supervisão humana, transparência, não discriminação, proteção de dados). **Não confirmei** se foi substituída por norma posterior em 2025/2026 — verificar antes de citar em proposta | [O] para a 332/2020; **status atual não verificado** |
| **Marco legal da IA — PL 2338/2023** | **aprovado no Senado** (parecer 207/2024-PLEN) e remetido à Câmara em **17/03/2025**. Na Câmara: Comissão Especial criada em 04/04/2025, instalada 29/04/2025, relator **Dep. Aguinaldo Ribeiro (PP-PB)** designado em 20/05/2025; situação em nov/2026 = **"aguardando parecer do relator"**, sem aprovação em nenhuma etapa, com **40 proposições apensadas** (última apensação relevante: 01/09/2026) | senado.leg.br/materia/157233 e camara.leg.br/proposicoesLegislativas/2487262 [O], consulta 10/11/2026 |
| **Implicação** | **não há marco legal de IA vigente no Brasil em 10/11/2026** — o produto convive com LGPD + regulação setorial (CNJ, BACEN) + o que vier do PL 2338 | — |

---

## 10. Parcerias e canais

| Categoria | Quem | Status da verificação |
|---|---|---|
| Distribuidores de TI de valor | Allnations, Officer, Pauta, Teltec, SND, MPS, Akiyama | **não verificados** — nenhum programa/margem consultado `[sem fonte]` |
| Integradores / revendas de hardware | Dell, HPE, Lenovo, Supermicro via revenda; integradores regionais | vendas de servidor com GPU só sob consulta; **margem de canal não publicada** `[sem fonte]` |
| Nuvem soberana / local | Magalu Cloud (sem GPU anunciada), Embratel/Claro, Scala, Ascenty (colocation) | não verificados `[sem fonte]` |
| Associações | OAB/CFOAB (1,5 mi de inscritos), CFC/CRCs (550 mil profissionais, 98 mil organizações) | números oficiais na seção 1; **modelo de parceria/credenciamento não verificado** |
| GED/DMS jurídico e assinatura | D4Sign, Clicksign, Netlex, Looplex | não verificados `[sem fonte]` |
| Fabricantes de GPU | NVIDIA (NPN), Dell/HPE/Lenovo (programas de parceiro) | existência do programa é fato notório; **margem/tier não verificados** `[sem fonte]` |
| **Margem típica de canal em software no Brasil** | **não localizada** fonte pública com faixa de desconto de revenda (o padrão internacional de 20–35% é `[E]`, sem fonte brasileira) | [sem fonte] |

---

## Lacunas de pesquisa

1. **Número de sociedades de advogados registradas** — o painel do CFOAB só publica inscrições individuais; não há número oficial consolidado localizado.
2. **Preço de hardware de servidor com GPU em BRL** (L40S, RTX 6000 Ada, estações e servidores de 4 GPUs, DGX Spark no Brasil) — todos vendidos sob consulta por Dell/HPE/Lenovo/Supermicro e revendas; nenhuma tabela pública encontrada. Só consegui preço de varejo da RTX 5090.
3. **GPU em nuvem em São Paulo no Google Cloud e em provedores brasileiros** — a página de preços do GCP não renderiza tabela sem JS e a API de billing exige chave; Magalu Cloud não anuncia GPU. Só AWS e Azure foram obtidos (e por API oficial de preços).
4. **CAC e churn de SaaS B2B no Brasil** — nenhum dado público consolidado; usei benchmarks globais (Benchmarkit) como proxy, o que não é o mesmo mercado.
5. **Faixas salariais de analista de suporte N1/N2, consultor de implantação, pré-vendas técnico, DevOps/SRE e gerente de projetos** — Glassdoor (403), Catho, Vagas.com e salario.com.br não retornaram conteúdo utilizável; o Guia Salarial Robert Half só expôs a aba de Liderança Executiva. **Percentual consolidado de encargos trabalhistas** também não foi obtido de fonte primária — usei cálculo próprio a partir das alíquotas legais.
6. **Margem de canal / desconto de revenda de software no Brasil** e programas de parceiros de distribuidores e fabricantes de GPU — não localizados.
7. **Status atual da norma de IA do CNJ** (se a Resolução 332/2020 foi substituída em 2025/2026) — site do CNJ retornou 403; **verificar antes de usar em proposta comercial**.
8. **Concorrentes brasileiros não verificados individualmente:** Looplex, Deep Legal, Kurier, Aurum, Finch, Sync, Toogle, Netlex, D4Sign — presumir "sob consulta" até checagem direta.
9. **Número de órgãos públicos federais/estaduais compradores** e **gasto agregado com serviços jurídicos no Brasil** — não localizados.
10. **Câmbio USD/BRL de referência** — não verificado nesta pesquisa; nenhuma conversão foi feita.
