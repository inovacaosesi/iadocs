# Sustentação: com quantas pessoas se serve um cliente

**Fase:** discovery / brainstorming · **Versão:** 1.0

Este documento possui o requisito **R46**. Ele complementa [05-analise-de-gaps.md](05-analise-de-gaps.md), que apontou a lacuna G15, e depende de [01-catalogo-requisitos.md](01-catalogo-requisitos.md), de [06-precificacao-e-escala.md](06-precificacao-e-escala.md) e de [09-infraestrutura.md](09-infraestrutura.md).

---

## 1. Diagnóstico

### 1.1 O que mata empresa de software instalado

Não é o preço. É a conta de servir.

Em SaaS, o cliente número mil usa a mesma infraestrutura, o mesmo time de suporte e o mesmo pipeline de atualização do cliente número um. O custo marginal de servir tende a zero e a margem bruta mediana do setor é de **77%** (Fonte: Benchmarkit, 2025, dados de 2024, compilado na base de fatos deste conjunto). Em software instalado, cada cliente é uma instalação própria, em rede fechada, em hardware que não é nosso, com versão que pode divergir da de todos os outros. O custo de servir **não cai com escala de software**: cai apenas com automação, padronização e número de clientes por pessoa.

A margem bruta de serviços profissionais no mesmo benchmark é de **30%**. Essa é a margem que este negócio tem por natureza, não por incompetência. A pergunta não é como chegar a 77% — é como não cair abaixo de 30% quando o cliente número três entrar em crise na mesma semana que o cliente número dois.

Três fatos encarecem a sustentação deste produto em particular:

1. **Não há acesso remoto.** O Modo A é air-gapped integral, o modo de fábrica e o modo contratual, *conforme especificação E1 do requisito R38*. Todo diagnóstico é assíncrono e depende de alguém do cliente executar o que pedimos.
2. **O cliente não tem time de infraestrutura de IA.** O jurídico tem advogado e estagiário; o contábil tem contador e auxiliar. Ninguém do outro lado sabe ler log de GPU.
3. **O produto erra de forma cara.** Resposta errada com citação válida é pior que resposta ausente, e o cliente descobre isso no primeiro prazo processual perdido ou no primeiro fechamento mensal atrasado.

### 1.2 O que o mercado paga pelos cargos que faltam

A base de fatos deste conjunto traz engenheiro de IA (R$ 25.000 sênior, Fonte: Robert Half 2026 via Exame, 01/10/2026), engenheiro de dados (R$ 13.500 a R$ 18.000) e cientista de dados (R$ 19.100 de mediana), e registra explicitamente que **não localizou** salário de analista de suporte, consultor de implantação, pré-vendas técnico e SRE. A pesquisa complementar está abaixo, com a diferença entre média de mercado e o perfil que o produto exige declarada em cada linha.

| Função | Média de mercado | Fonte e data | Valor adotado aqui | Por quê |
|---|---|---|---|---|
| Analista de suporte técnico | R$ 4.109 (mediana R$ 3.000; teto R$ 7.487; 63.439 vínculos CLT) | salario.com.br, CAGED 12 meses até 05/11/2026 | N1: R$ 4.500 · N2: R$ 7.000 | N1 no meio da faixa; N2 no topo da faixa, porque atende air-gapped e domínio jurídico-fiscal |
| Consultor de implantação | R$ 3.947 (109 salários) | Indeed Brasil, atualizado em 30/10/2026 | R$ 9.000 | A média é de implantação de ERP genérico, presencial e roteirizada. Aqui a função exige infraestrutura, GPU, indexação e domínio do acervo — 2,3× a média é `[estimativa declarada]` |
| Pré-vendas técnico | R$ 6.396 (engenheiro de vendas, 83 salários) | Indeed Brasil, 2026 | R$ 11.000 fixo + variável `[estimativa declarada]` | Papel sênior, com demonstração em ambiente do cliente. Proxy por ausência de série específica para pré-vendas |
| DevOps / SRE | Mediana R$ 14.441 (47 salários) | salariotransparente.com.br, 2026 | R$ 14.500 | Amostra pequena e autoinformada; adotada por ser a única série pública localizada |
| Coordenação de sustentação | R$ 21.800 (gerente de TI júnior) | Robert Half 2026 via Exame, compilado na base de fatos | R$ 21.800 | Proxy declarado na base de fatos |

Sobre o multiplicador: o custo total de um CLT neste conjunto é **1,7 a 1,8× o salário bruto** (encargos de 68% a 82%, `[E]` na base de fatos). Este documento usa **1,75×** em todas as contas.

### 1.3 O erro de composição que a base de fatos já insinua

A base de fatos traz um time de exemplo com cinco cabeças — um engenheiro de IA, um engenheiro de dados, dois analistas de suporte e um consultor de implantação — a **R$ 60-70 mil brutos**, ou **R$ 105-125 mil de custo total por mês**. Esse time serve bem **dez clientes**. Com três clientes, ele custa R$ 35 mil por cliente por mês, o que nenhum contrato de sustentação paga.

O time não é o problema. O problema é contratar para dez clientes antes de ter três. A decisão abaixo é sobre *sequência*, não sobre tamanho.

---

## 2. Decisão proposta

**Começar com 2,7 FTE e contratar por gatilho de carteira, não por expectativa de carteira.**

A alternativa descartada: montar desde o mês 1 o time de cinco cabeças da base de fatos, apostando que a carteira chega em doze meses. Ela quebra porque R$ 105-125 mil por mês de custo fixo consome de 12 a 15 meses de receita antes do primeiro contrato relevante, e o produto é vendido em ciclo longo, com ticket alto — *conforme especificação E9 do requisito R38*, a produção departamental só começa depois de um piloto aprovado.

### 2.1 Estrutura mínima (mês 1 a 3, até 3 clientes)

| Função | FTE | Salário bruto | Custo total (×1,75) | O que faz |
|---|---|---|---|---|
| Consultor de implantação | 1,0 | R$ 9.000 | R$ 15.750 | Executa a implantação, treina o multiplicador, é o rosto da empresa no cliente |
| Analista de suporte N2 | 1,0 | R$ 7.000 | R$ 12.250 | Acumula N1 e N2, é o dono do runbook e do pacote de evidências |
| Engenheiro de IA | 0,5 | R$ 12.500 | R$ 21.875 | Referência técnica; não é dedicado a suporte, mas é o N3 |
| DevOps / SRE | 0,2 | R$ 2.900 | R$ 5.075 | Esteira de pacote offline, assinatura e rollback |
| **Total** | **2,7** | **R$ 31.400** | **R$ 54.950** | |

**R$ 55 mil por mês** de estrutura de sustentação. Com três clientes, isso é R$ 18,3 mil por cliente por mês — número que não fecha em contrato nenhum. A consequência é estrutural, e não é uma frase de efeito: **nos primeiros doze meses a sustentação é custo de aquisição de mercado, e precisa ser orçada como tal, não como linha de receita.** O que se cobra por cliente nessa fase é a implantação, à parte, mais uma taxa de sustentação que cobre apenas o variável.

### 2.2 Curva de contratação

Rácios usados, com origem declarada:

- **Clientes por analista de suporte N2:** 8 a 12 em regime estável; 4 a 6 no primeiro trimestre de cada cliente. Origem: `[hipótese]`, calibrada por analogia com suporte de sistemas instalados de missão crítica. Não há benchmark público de suporte air-gapped de IA documental.
- **Implantações simultâneas por consultor:** 2 (uma em curso e uma em estabilização), 3 no limite e só em implantação de escopo reduzido. Origem: `[hipótese]` de projeto.
- **Páginas indexadas por implantação por semana:** 10.000. Origem: `[hipótese]`, coerente com a faixa de piloto de 50 mil páginas, *conforme especificação E9 do requisito R38*, que assim fecha em cinco semanas de indexação.
- **Chamados por 100 usuários por mês:** 15 no primeiro trimestre, 5 em regime. Origem: `[hipótese]`; com produtividade de 80 a 120 chamados por N2/mês, uma base de 500 usuários exige um N2 em regime.

| Carteira | Quando | FTE | Composição | Custo mensal | Custo por cliente |
|---|---|---|---|---|---|
| 3 clientes | mês 1 | 2,7 | 1 implantação, 1 N2, 0,5 eng. IA, 0,2 SRE | R$ 55 mil | R$ 18,3 mil |
| 10 clientes | mês 12 | 6,0 | 2 implantação, 2 N2, 1 N1, 1 eng. IA, 0,5 SRE, 0,5 coord. | R$ 139 mil | R$ 13,9 mil |
| 25 clientes | mês 24 | 12,5 | 3 implantação, 4 N2, 2 N1, 1,5 eng. IA, 1 SRE, 1 coord. | R$ 241 mil | R$ 9,6 mil |
| 50 clientes | mês 36-48 | 20,0 | 4 implantação, 7 N2, 4 N1, 2 eng. IA, 1,5 SRE, 1,5 coord. | R$ 363 mil | R$ 7,3 mil |

Os números de 25 e 50 clientes incluem folga para férias, plantão e turnover — três analistas em carteira estável não cobrem 25 clientes, quatro cobrem com folga de uma pessoa em qualquer semana do ano. A coluna de FTE é derivada das frações acima e do custo bruto de cada função, multiplicado por 1,75.

**Gatilhos de contratação, não datas:** contratar o segundo N2 quando a carteira passar de 8 clientes ou quando o tempo médio de primeira resposta de severidade 1 estourar o SLA por três semanas seguidas. Contratar o primeiro N1 quando o volume mensal de chamados passar de 120. Contratar o segundo consultor de implantação quando houver dois contratos assinados sem implantação iniciada.

### 2.3 Cobertura e horário

| Janela | O que promete | O que custa | Para quem |
|---|---|---|---|
| **8x5** (padrão, inclusa) | Atendimento em dias úteis, 8 horas, canal assíncrono e sessão assistida agendada | Inclusa na estrutura mínima | Contábil-fiscal fora de fechamento |
| **12x5** (vendida à parte) | Das 7h às 19h em dias úteis, com primeira resposta em 2h úteis | +1,5 FTE por analista em escala; ordem de R$ 15 a 20 mil/mês por cliente `[estimativa declarada]` | Jurídico com prazo processual, contábil no fechamento |
| **Plantão** (vendido à parte) | Fora do horário comercial, com engenheiro de sobreaviso | +3 FTE por posição de escala para 24x7 real; abaixo disso é promessa que não se cumpre | Cliente com operação noturna — hoje, nenhum do perfil-alvo |

Dois fatos de negócio entram nessa escolha: cliente jurídico tem prazo processual que não respeita horário comercial, e cliente fiscal tem fechamento mensal com data fixa. Nos dois casos a janela crítica é previsível. **Plantão 24x7 permanente é a pior forma de cobrir isso**: custa 3 FTE o ano inteiro para resolver dois dias de pico por mês. O desenho certo é 8x5 com janela estendida contratada por evento nas semanas de fechamento e nos prazos declarados pelo cliente.

### 2.4 O item mais esquecido e o mais caro na prática

Suporte em ambiente air-gapped tem uma assimetria que nenhum outro item deste conjunto tem: **o fornecedor não vê a máquina do cliente.** Não há SSH, não há sessão remota, não há coleta automática de log. Cada incidente atravessa quatro fronteiras humanas — o cliente abre o chamado, nós devolvemos um procedimento, o cliente executa e devolve, nós analisamos.

Três consequências de custo, todas mensuráveis:

1. **Uma ida e volta custa de 4 a 24 horas de relógio**, não minutos. O tempo de restauração passa a depender da disponibilidade de uma pessoa do cliente, que tem outro emprego.
2. **A atualização assistida é o maior consumo oculto.** Estimar 12 atualizações por ano, 3 horas de especialista por cliente por atualização, dá 900 horas anuais em 25 clientes — **0,5 FTE só guiando alguém para rodar um comando que nós mesmos escrevemos**.
3. **Sem automação local, o custo cresce linearmente com a carteira.** É o único item deste documento em que investir em produto reduz headcount de forma direta.

Custo de mão de obra por evento, somando as duas pontas `[estimativa declarada]`, com base nas 1.700 horas úteis anuais de um FTE:

| Evento | Horas do fornecedor | Horas do cliente | Frequência por cliente/ano |
|---|---|---|---|
| Chamado de severidade 3 | 1 | 0,5 | 10 a 20 |
| Chamado de severidade 1 com sessão assistida | 4 | 3 | 2 a 4 |
| Atualização assistida de versão | 3 | 2 | 12 |
| Reindexação ou recuperação de acervo | 8 | 6 | 1 a 2 |

Some 12 atualizações, 3 chamados severos e 15 chamados leves por cliente: são cerca de **100 horas de fornecedor por cliente por ano**. Em 25 clientes, 2.500 horas — 1,5 FTE consumido apenas em atendimento reativo. É a razão pela qual a automação da E10 não é melhoria de produto: é o que decide se a curva de contratação da seção 2.2 vale alguma coisa.

### 2.5 O que a margem de 30% autoriza

Cruzando o custo por cliente da tabela de 2.2 com a margem bruta de serviços de 30% (Fonte: Benchmarkit, 2025), a linha de sustentação precisa de receita recorrente por cliente de:

| Carteira | Custo de sustentação por cliente | Receita necessária para 30% de margem bruta |
|---|---|---|
| 3 clientes | R$ 18,3 mil | R$ 26,2 mil/mês |
| 10 clientes | R$ 13,9 mil | R$ 19,9 mil/mês |
| 25 clientes | R$ 9,6 mil | R$ 13,7 mil/mês |
| 50 clientes | R$ 7,3 mil | R$ 10,4 mil/mês |

R$ 26 mil por mês de sustentação para um cliente de três é indefensável comercialmente. **A conclusão é que o contrato de sustentação não pode ser precificado por cliente nos dois primeiros anos** — precisa ser um valor de pacote com piso, e a implantação precisa carregar o custo real do período. O número exato de preço é do documento 06; o que este documento fixa é o piso de custo que o preço tem de cobrir. Se o documento 06 chegar a um preço recorrente abaixo da coluna da direita, o modelo não fecha e a decisão a revisitar é esta, não o preço.

---

## 3. Requisito

### R46. Sustentação com equipe enxuta

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** O requisito R39 define *o que* o suporte entrega: níveis de serviço, atualização isolada, tratamento de vulnerabilidade, runbooks. Ele não diz com quantas pessoas, com que cobertura e a que custo — e sustentação de produto instalado é o maior consumidor de margem nesse modelo. R46 responde a segunda pergunta. Ela é desconfortável nos dois sentidos: equipe enxuta demais perde o cliente na primeira crise, e o cliente perdido na primeira crise custa mais que a folga de um analista durante um ano. Equipe grande demais come a margem do contrato antes do segundo ano.

O ponto de equilíbrio não é um número de pessoas. É uma regra: **contratar por gatilho de carteira e por estouro de SLA, nunca por expectativa.** O produto é instalado, o ciclo de venda é longo e a receita recorrente depende do suporte — o que significa que errar para mais custa caixa hoje e errar para menos custa a conta inteira depois.

**Especificações**

- **E1. Catálogo de serviços de sustentação.** O contrato de sustentação descreve, item por item, o que está incluído e o que é cobrado à parte. Incluídos na assinatura: suporte N1 e N2 em janela 8x5, correção de defeito, atualização de corpus normativo *conforme especificação E3 do requisito R39*, atualização de versão *conforme especificação E2 do requisito R39*, acesso a runbooks e à base de conhecimento. Cobrados à parte: implantação, treinamento *conforme especificação E1 do requisito R36*, janela estendida e plantão, integração com sistema do cliente, recuperação de acervo corrompido por causa externa, e análise sob demanda acima de um limite declarado de horas. Todo item fora da lista é orçado antes de executado, sem exceção verbal.

- **E2. Estrutura mínima e fração de FTE por função.** A operação não começa sem, no mínimo: 1,0 FTE de consultor de implantação, 1,0 FTE de analista de suporte N2 acumulando N1, 0,5 FTE de engenheiro de IA como retaguarda técnica e 0,2 FTE de DevOps para a esteira de pacote offline. Custo total declarado: **R$ 55 mil por mês**, calculado sobre salário bruto vezes 1,75. A especificação é verificável por duas perguntas: quem atende o chamado de madrugada e quem responde quando essa pessoa não sabe. Se a segunda resposta for "o engenheiro de IA", a fração de 0,5 está correta; se for "ninguém", a estrutura não existe.

- **E3. Rácios operacionais declarados.** Clientes por analista N2: 8 a 12 em regime estável, 4 a 6 no primeiro trimestre de cada cliente. Implantações simultâneas por consultor: 2. Páginas indexadas por implantação por semana: 10.000. Chamados por 100 usuários por mês: 15 no primeiro trimestre e 5 em regime. Cada rácio declara no contrato interno se é mercado, norma ou hipótese — os quatro acima são `[hipótese]` — e cada um tem um indicador medido que o recalibra a cada trimestre. Rácio não medido vira folclore em seis meses.

- **E4. Curva de contratação por faixa de carteira.** A contratação segue gatilho, não calendário: segundo N2 ao passar de 8 clientes ou ao estourar SLA de severidade 1 por três semanas seguidas; primeiro N1 acima de 120 chamados por mês; segundo consultor de implantação com dois contratos assinados sem implantação iniciada. Para cada faixa — 3, 10, 25 e 50 clientes — existe planilha aberta com FTE por função, custo mensal total e custo por cliente, revisada a cada contratação.

- **E5. Cobertura e janela declaradas, sem promessa implícita.** A janela padrão é 8x5, em dias úteis, com canal assíncrono e sessão assistida agendada. Janela 12x5 e plantão existem apenas como serviço vendido à parte, com preço próprio e FTE adicional declarado — 1,5 FTE por analista em escala para 12x5 e 3 FTE por posição para 24x7 real. Nenhum contrato promete cobertura que a escala não sustenta. Para cliente jurídico, a janela crítica é o prazo processual; para o contábil-fiscal, o fechamento mensal — os dois são previsíveis e devem ser contratados por evento, não por plantão permanente.

- **E6. Escalonamento N1, N2 e N3 com critério de entrada e saída.** N1 resolve uso, acesso, configuração e dúvida de operação, com roteiro fechado. N2 resolve defeito reproduzível, indexação, qualidade de resposta e diagnóstico em ambiente isolado, e é o dono do pacote de evidências. N3 é o engenheiro de IA e só é acionado quando o problema é de modelo, de pipeline ou de integridade do índice. Cada nível tem critério objetivo de entrada e de devolução, e todo retorno de N3 para N2 gera item de runbook. A regra que sustenta a estrutura enxuta: **o N3 nunca atende chamado direto**; se atender, a empresa acabou de criar um gargalo de uma pessoa só.

- **E7. Matriz de responsabilidade com o cliente.** O contrato traz matriz RACI assinada. O cliente é **responsável** por: infraestrutura, energia, refrigeração, rede interna, backup e teste de restauração, janela de manutenção, liberação de mídia e de pacote de atualização, e designação nominal de um contato técnico com alçada para executar comando sob orientação. O fornecedor é **responsável** por: produto, correção de defeito, atualização de corpus e de versão, runbooks, treinamento e diagnóstico. É **consultado** em mudança de infraestrutura que afete desempenho. É **informado** de incidente de segurança e de fim de vida de versão *conforme especificação E5 do requisito R39*. Sem contato técnico designado, o SLA não começa a contar — essa cláusula é o que impede o fornecedor de pagar por uma indisponibilidade que não controla.

- **E8. Suporte em ambiente air-gapped, com procedimento próprio.** O fornecedor não acessa a máquina do cliente em nenhuma circunstância, nem com autorização. O atendimento segue quatro instrumentos: (a) **autodiagnóstico local**, que roda no cliente e produz laudo legível; (b) **pacote de evidências** assinado, gerado localmente, com versões, hashes, configuração redigida, logs e métricas, sem conteúdo de acervo, que o cliente inspeciona e envia pelo canal que ele escolher; (c) **sessão assistida** por vídeo, em que o cliente compartilha tela e executa o comando, com roteiro escrito antes da sessão e registro do que foi executado; (d) **atualização assistida**, com pacote assinado, procedimento de reversão e presença de um especialista durante a janela. O limite é declarado em contrato: prazo de primeira resposta e de contorno são comprometíveis, prazo de restauração não é, porque depende de execução do cliente. Este é o item mais esquecido do conjunto e o mais caro na prática.

- **E9. SLA interno e promessa contratual separados.** Existe tabela interna de metas, mais agressiva, usada para gestão; e tabela contratual, mais conservadora, usada para o cliente. Com dois analistas é possível prometer, em 8x5: severidade 1 (parada total ou risco de prazo), primeira resposta em 4 horas úteis e contorno em 1 dia útil; severidade 2, 8 horas úteis e 3 dias úteis; severidade 3, 2 dias úteis e próximo ciclo de versão. **Não é possível prometer**, com dois analistas: primeira resposta em 1 hora, disponibilidade 24x7, restauração em prazo fixo, atendimento presencial em menos de 48 horas, nem resolução garantida de defeito que dependa de fornecedor de terceiro. Cada uma dessas promessas só entra em contrato quando houver FTE dedicado e preço correspondente.

- **E10. Automação de sustentação como requisito de produto.** Runbook, autodiagnóstico, telemetria local e atualização com reversão são entregáveis de produto, e não documentos do time de suporte: runbooks versionados e distribuídos junto com a versão; autodiagnóstico executável localmente, sem rede; telemetria local, opt-in e desligável, agregada no próprio ambiente do cliente, nunca enviada; atualização assistida com verificação de integridade, aplicação e rollback em um comando. A meta declarada é reduzir o custo de atualização assistida de 3 horas para 1 hora de especialista por cliente até a carteira de 25. Sem isso, o custo de sustentação cresce linearmente com o número de clientes e a curva da seção 2.2 deixa de valer.

- **E11. Capacitação e retenção do próprio time.** Existe trilha interna de certificação por nível, com critério de promoção escrito, e a formação de um N2 em ambiente air-gapped leva de 3 a 6 meses `[estimativa declarada]`. Regra de ouro: **nenhum conhecimento crítico pode morar em uma pessoa só** — cada função da estrutura mínima tem pelo menos duas pessoas capazes de executá-la, incluindo o engenheiro de IA. A remuneração do time de suporte é posicionada acima da média de mercado (teto da faixa do CAGED, não a média), porque turnover em suporte é alto e a perda do único N2 custa mais que a diferença salarial de um ano. Indicador acompanhado: turnover voluntário do time de sustentação e tempo até autonomia de cada novo contratado.

- **E12. Custo de sustentação por cliente e efeito na margem.** O custo mensal de sustentação por cliente é calculado e publicado por faixa de carteira: R$ 18,3 mil com 3 clientes, R$ 13,9 mil com 10, R$ 9,6 mil com 25 e R$ 7,3 mil com 50. Sobre a margem bruta de serviços de 30% (Fonte: Benchmarkit, 2025), o custo é cruzado com o preço recorrente definido no documento 06, e a divergência é resolvida explicitamente. Enquanto a carteira estiver abaixo de 10 clientes, a sustentação é orçada como custo de aquisição de mercado e não como linha de receita, e o custo não absorvido é carregado pela implantação. A verificação é uma conta, feita a cada trimestre: receita recorrente da carteira menos custo de sustentação da carteira, dividida pela receita recorrente.

---

## 4. Como isso vira decisão de contratação

**Mês 1.** Contratar o consultor de implantação e o analista N2. Alocar 0,5 do engenheiro de IA e 0,2 do DevOps. Não contratar N1, não contratar pré-vendas técnico. Escrever o pacote de evidências e o autodiagnóstico antes do primeiro cliente entrar — depois do primeiro incidente é tarde. Custo: R$ 55 mil/mês.

**Mês 12, com 10 clientes.** Dois consultores, dois N2, um N1, um engenheiro de IA, meio SRE, meio coordenador. Contratar o segundo N2 pelo gatilho de oito clientes, não pelo décimo. Primeiro pré-vendas técnico entra aqui, junto com o segundo consultor, porque a demonstração em ambiente do cliente passou a ser o gargalo da venda. Custo: R$ 139 mil/mês, R$ 13,9 mil por cliente.

**Mês 24, com 25 clientes.** Quatro N2 e dois N1, com folga para férias e plantão; três consultores; 1,5 engenheiro de IA; um SRE inteiro. Neste ponto a automação da E10 precisa estar entregue: sem ela, o custo por cliente para de cair e o modelo não fecha. Custo: R$ 241 mil/mês, R$ 9,6 mil por cliente.

---

## Fontes

- salario.com.br — Analista de Suporte Técnico (CBO 2124-20), CAGED 12 meses até 05/11/2026: https://www.salario.com.br/profissao/analista-de-suporte-tecnico-cbo-212420/
- Indeed Brasil — Salário de Consultor de Implantação, atualizado em 30/10/2026: https://br.indeed.com/career/consultor-de-implanta%C3%A7%C3%A3o/salaries
- Indeed Brasil — Salário de Engenheiro de Vendas (proxy de pré-vendas técnico), 2026: https://br.indeed.com/career/engenheiro-de-vendas/salaries
- salariotransparente.com.br — DevOps Engineer, mediana 2026: https://salariotransparente.com.br/salarios/devops-engineer
- Base de fatos deste conjunto ([12-fontes-e-base-de-fatos.md](12-fontes-e-base-de-fatos.md)), pesquisa de 10/11/2026: salários de engenheiro de IA, engenheiro de dados e cientista de dados (Robert Half 2026 via Exame, 01/10/2026); proxy de Gerente de TI; multiplicador de encargos CLT de 1,7 a 1,8×; margem bruta de SaaS de 77% e de serviços profissionais de 30% (Benchmarkit, 2025).
- `docs/01-catalogo-requisitos.md` — R36, R38, R39.
- `docs/05-analise-de-gaps.md` — lacuna G15, que origina este documento.

## O que derruba esta recomendação

1. **O preço recorrente fechado no documento 06 ficar abaixo de R$ 10,4 mil por cliente por mês.** Se for, a estrutura de 50 clientes não paga a si mesma e a decisão a revisitar é o modelo de sustentação inteiro, não a folha.
2. **O piloto mostrar que o ambiente do cliente não tem quem execute comando.** A E7 assume um contato técnico com alçada. Se o cliente não tiver essa pessoa — e no jurídico de médio porte provavelmente não tem —, todo o procedimento da E8 colapsa e o custo de suporte por cliente sobe por um fator que este documento não estima.
3. **O tempo médio de primeira resposta passar de 8 horas úteis com três clientes.** Significa que a hipótese de 8 a 12 clientes por N2 está errada para este produto e a curva de contratação precisa ser refeita para baixo em clientes por analista.
4. **A automação da E10 não entregar a redução de 3 para 1 hora por atualização assistida.** Nesse caso o custo de sustentação deixa de ter economia de escala e a recomendação de crescer carteira perde sentido econômico.
5. **Turnover do time de suporte acima de dois N2 por ano.** Cada substituição custa de 3 a 6 meses de formação e derruba a capacidade da carteira num período em que a promessa contratual continua valendo.
