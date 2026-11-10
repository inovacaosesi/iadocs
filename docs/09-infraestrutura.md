# Infraestrutura Local: Enxuta, Modular e Elástica

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Requisito:** R48 · **Papel:** definir a menor configuração que entrega valor, como ela cresce sem recompra e quanto custa cada degrau.

Este documento não substitui R26 nem R38 do [catálogo](01-catalogo-requisitos.md). R26 diz o que compõe a infraestrutura e R38 define os modos de implantação. R48 responde outra pergunta, e ela é comercial antes de ser técnica: **qual é a menor máquina que justifica a compra, quanto custa o próximo degrau e em que ponto o ferro próprio passa a ganhar da nuvem.** Sem essa resposta, "infraestrutura enxuta e elástica" é adjetivo.

**Documentos irmãos:** [05-analise-de-gaps.md](05-analise-de-gaps.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [04-mvp-matriz.md](04-mvp-matriz.md) · [06-precificacao-e-escala.md](06-precificacao-e-escala.md) · [07-sustentacao.md](07-sustentacao.md) · [12-fontes-e-base-de-fatos.md](12-fontes-e-base-de-fatos.md)

---

## 1. Diagnóstico

### 1.1 "Elástico" é uma palavra emprestada da nuvem, e aqui ela não vale

Em nuvem, elasticidade é acrescentar capacidade em minutos e devolver no dia seguinte. No ambiente do cliente não existe elasticidade: existe **granularidade de compra**. Ninguém compra meia GPU, e ninguém devolve a que comprou. O que o produto pode prometer é outra coisa, mais modesta e mais honesta:

- **modularidade** — o cliente começa com o módulo que resolve o problema dele e acrescenta os demais sem reinstalar nada;
- **crescimento por nó** — a segunda GPU entra ao lado da primeira, não no lugar dela;
- **separação de carga** — o lote de indexação roda em horário distinto da consulta interativa, o que permite hardware menor do que a soma dos picos sugeriria;
- **reversibilidade** — o cliente que comprou demais consegue reaproveitar a máquina em outro uso, porque o produto não exige hardware exótico.

Prometer elasticidade real em air-gapped é a primeira forma de perder a confiança do arquiteto do cliente. A especificação E1 abaixo proíbe essa promessa por escrito.

### 1.2 O único preço de hardware publicado é o do degrau de entrada

A pesquisa desta rodada encontrou **um** preço público em real: **RTX 5090 de 32 GB a R$ 31.999,99 no Pix** (pcbuilder.com.br, 17/09/2026). Todo o resto — servidor com L40S, RTX 6000 Ada, A6000, estações de quatro GPUs — é vendido por revenda Dell, HPE, Lenovo e Supermicro **sob consulta**, sem tabela pública em BRL. E o DGX Spark, que seria a alternativa de baixo consumo, aparece na página da NVIDIA com especificação completa e sem preço: **fonte de 240 W, TDP de 140 W, 64 ou 128 GB de memória unificada a 273 GB/s, até 4 TB de NVMe, 1 petaFLOP em FP4**.

Isso não é falha da pesquisa, é informação de mercado: **hardware corporativo com GPU não tem preço de tabela no Brasil.** Quem monta proposta com "servidor a partir de X" está inventando X. O documento trabalha com faixas estimadas declaradas e diz o que precisa de cotação real antes de virar proposta.

### 1.3 Energia não é o driver. A placa é

A conta de energia é pequena e vale ser dita em voz alta para tirar o assunto da mesa: um servidor de uma GPU a 600 W médios, em 730 horas, consome 438 kWh; a **R$ 0,4525/kWh fora ponta na Enel SP** (REH ANEEL 3.596/2026, vigência 04/07/2026, grupo A4 azul), dá **R$ 198 por mês**. Um rack de quatro GPUs a 2,5 kW dá **R$ 826 por mês**.

O que pesa é o CAPEX da placa e a depreciação dela. E aqui vale a regra já fixada na *decisão D3*: GPU se deprecia em **três anos**, não em cinco, porque a cada geração de modelo a exigência de memória sobe. Toda conta deste documento usa 36 meses.

### 1.4 A nuvem de São Paulo é 1,7 vez mais cara, e é a régua honesta

Preço on-demand na AWS sa-east-1, tabela oficial (vigência 01–07/11/2026): **g6.xlarge com 1× L4 a US$ 1,368/hora**, o que dá **US$ 999 por mês** em 730 horas; **g5.xlarge com 1× A10G a US$ 1,710/hora**; **g5.48xlarge com 8× A10G a US$ 27,686/hora**, ou **US$ 20.211 por mês**; **p5.48xlarge com 8× H100 a US$ 92,467/hora**, ou **US$ 67.501 por mês**. A mesma g6.xlarge custa US$ 0,8048/hora em us-east-1: **São Paulo é cerca de 1,7 vez mais caro que a Virgínia**.

Azure Brazil South confirma a ordem de grandeza: T4 a US$ 0,894/hora, 2× A100 a US$ 14,692/hora, 8× H200 a US$ 169,60/hora.

O câmbio não foi verificado nesta rodada, e por isso a comparação abaixo é feita **sem converter moeda** — o que, aliás, produz um resultado mais forte do que a conversão produziria.

---

## 2. Decisão proposta

**Quatro degraus de hardware, quatro módulos de software, e uma regra de crescimento que o cliente consegue verificar sozinho.**

A alternativa descartada é o caminho inverso, comum em produto de infraestrutura: um único perfil "corporativo" dimensionado para o maior cliente, vendido a todos. Ela quebra em duas frentes. Na entrada, porque o cliente de 20 mil páginas paga por capacidade que não usa e desiste no preço. No topo, porque o perfil único vira gargalo no primeiro acervo de dois milhões de páginas, e a resposta passa a ser uma recompra em vez de um acréscimo.

### 2.1 Quatro módulos, e o que é obrigatório no dia um

| Módulo | Função | Obrigatório no dia 1? | Pode operar separado? |
|---|---|---|---|
| **Ingestão e OCR** | Recebe arquivo, sanitiza, converte, reconhece texto e gera derivados | Sim | Sim, em máquina sem GPU |
| **Índice e busca** | Índice lexical e vetorial, filtros de governança, recuperação | Sim | Sim, escala por nó próprio |
| **Inferência** | Modelo de linguagem, embeddings, reranking, classificação | Sim | Sim, é o único que exige GPU |
| **Interface e API** | Navegador, API, integrações, trilha de auditoria | Sim | Sim, é o mais leve |

A modularidade tem uma consequência comercial que vale mais que a técnica: **só um dos quatro módulos exige GPU.** Um cliente que já tem servidor pode começar apenas com o módulo de inferência em uma única placa, mantendo indexação e interface na máquina que já possui. Isso reduz o degrau de entrada de uma compra de servidor para uma compra de placa.

Módulos opcionais, que entram depois sem reinstalação: observabilidade local, réplica de leitura do índice, e segundo nó de inferência para alta disponibilidade.

### 2.2 Os quatro degraus, com o preço que existe e o que falta cotar

| Degrau | Hardware | Capacidade de referência | CAPEX | Status do preço |
|---|---|---|---|---|
| **D1. Entrada** | Estação ou servidor de 1 GPU: RTX 5090 32 GB; alternativa DGX Spark de 128 GB unificados para quem precisa de baixo consumo | até 50 mil páginas indexadas, 5 a 10 usuários simultâneos, modelo de 8 a 14 bilhões de parâmetros em 4 bits | **R$ 32 mil** (só a placa, no varejo) a **R$ 45 mil** (máquina completa) | Placa confirmada; máquina completa `[estimativa declarada]` |
| **D2. Departamento** | Servidor 1U ou 2U com 1 GPU de 48 GB (L40S ou RTX 6000 Ada) | até 500 mil páginas, 25 usuários, modelo de 30 a 70 bilhões quantizado | **R$ 120 mil a R$ 180 mil** | `[a validar]` — revenda não publica tabela em BRL |
| **D3. Corporativo** | Servidor de 4 GPUs de 48 GB, 2 a 4 TB de NVMe | até 2 milhões de páginas, 60 a 100 usuários, modelo maior com folga de contexto | **R$ 400 mil a R$ 600 mil** | `[a validar]` — cotação com Dell, HPE, Lenovo ou Supermicro |
| **D4. Institucional air-gap** | Dois nós de 4 GPUs, com separação de cargas e réplica | acima de 2 milhões de páginas, 100+ usuários, multiunidade | **R$ 900 mil a R$ 1,2 milhão** | `[a validar]` — inclui redundância e sítio secundário |

Os degraus conversam com as faixas da *decisão D3* e da especificação E9 do requisito R38: D1 e D2 atendem o piloto e a produção departamental, D3 e D4 atendem a produção com requisito de air-gap.

**O que precisa acontecer antes de qualquer proposta:** cotação real com dois fornecedores por degrau, com prazo de entrega e garantia. Enquanto isso não existe, a proposta usa faixa e diz que é faixa. Cliente corporativo prefere uma faixa honesta a um número inventado que muda no dia seguinte.

### 2.3 Quanto custa servir, por degrau

Custo mensal de infraestrutura = CAPEX dividido por 36 meses, mais energia, mais operação interna estimada. Sem margem, sem imposto.

| Degrau | CAPEX/36 | Energia | Operação interna | Total/mês | Por mil páginas/mês | Por usuário/mês |
|---|---|---|---|---|---|---|
| D1 | R$ 1.250 | R$ 198 | R$ 500 | **R$ 1.948** | R$ 39 (a 50 mil páginas) | R$ 195 (10 usuários) |
| D2 | R$ 4.167 | R$ 198 | R$ 1.500 | **R$ 5.865** | R$ 12 (a 500 mil páginas) | R$ 235 (25 usuários) |
| D3 | R$ 13.889 | R$ 826 | R$ 4.000 | **R$ 18.715** | R$ 9 (a 2 milhões de páginas) | R$ 187 (100 usuários) |
| D4 | R$ 29.167 | R$ 1.652 | R$ 8.000 | **R$ 38.819** | R$ 19 (a 2 milhões de páginas) | R$ 259 (150 usuários) |

A leitura que importa está na terceira coluna da direita: **o custo por usuário é praticamente constante entre R$ 190 e R$ 260, e o custo por página cai com o volume.** Isso tem duas consequências comerciais diretas. A primeira: cobrar por página premia o cliente grande e pune o pequeno, que é o inverso do que a estrutura de custo sugere. A segunda: o cliente de D1 paga R$ 195 por usuário em infraestrutura e o preço de tabela precisa cobrir isso mais sustentação, mais margem — o que confirma, pelo lado do hardware, a conclusão do [documento 11](11-publico-alvo-e-margem.md) de que o escritório de nicho não fecha.

A operação interna de R$ 500 a R$ 8.000 é o custo de alguém do cliente ou do parceiro cuidando de backup, atualização e monitoração. Ela não aparece na fatura e aparece no orçamento de todo projeto on-premise que dá errado por falta dela.

### 2.4 A regra de crescimento, em uma tabela

| Sinal observado | O que fazer | O que **não** fazer |
|---|---|---|
| Fila de indexação acima de 24 horas | Acrescentar nó de ingestão (sem GPU) | Comprar GPU nova |
| Tempo até o primeiro token acima de 5 segundos no p95 | Revisar quantização e limite de contexto | Trocar a máquina por reflexo |
| Memória de GPU acima de 90% em uso normal | Subir de degrau ou quantizar mais | Rodar modelo maior "porque cabe" |
| Latência de busca degradando | Partição do índice e réplica de leitura | Índice maior na mesma máquina |
| Mais de 25 usuários simultâneos no D1 | Subir para D2 | Empilhar usuários e prometer fila |
| Volume de acervo acima de 70% da faixa | Subir de degrau com 90 dias de antecedência | Esperar o limite para trocar |

A regra de ouro é a penúltima linha da primeira coluna: **o sinal de que precisa de mais máquina não é lentidão, é ocupação de faixa.** Lentidão é sintoma; faixa é previsão.

### 2.5 Em que ponto o ferro ganha da nuvem

A *decisão D3* fixou a regra: migrar quando o custo projetado de 24 meses em nuvem exceder o custo total de aquisição do servidor equivalente. Com os preços desta rodada, a regra ganha número:

| Comparação | Nuvem (24 meses) | Ferro próprio (CAPEX) | Câmbio de indiferença |
|---|---|---|---|
| 1 GPU de entrada (g6.xlarge, 1× L4) | US$ 23.976 | R$ 120 mil a R$ 180 mil (D2) | **R$ 5,00 a R$ 7,50 por dólar** |
| 8 GPUs (g5.48xlarge, 8× A10G) | US$ 485.064 | R$ 400 mil a R$ 600 mil (D3) | **R$ 0,82 a R$ 1,24 por dólar** |
| 8 GPUs topo (p5.48xlarge, 8× H100) | US$ 1.620.024 | R$ 900 mil a R$ 1,2 milhão (D4) | **R$ 0,56 a R$ 0,74 por dólar** |

Câmbio de indiferença é a cotação em que nuvem e ferro custam o mesmo em 24 meses. Qualquer cotação acima do número da direita faz o ferro ganhar. **No degrau de entrada a decisão é sensível ao câmbio e merece conta caso a caso. Do terceiro degrau em diante, a nuvem de São Paulo perde por um fator de quatro a oito, e a discussão acaba.**

Isso não significa que nuvem privada seja erro no piloto. Ela compra tempo até valor, dispensa capex e valida o acervo real — que é exatamente o papel que a *decisão D3* lhe deu. O erro seria manter em nuvem o cliente de 8 GPUs por conforto.

### 2.6 O que o arquiteto do cliente vai perguntar

Três perguntas aparecem em toda homologação, e as três têm resposta curta.

**Rede.** O produto não precisa de destino externo em Modo A. Precisa de portas internas documentadas, resolução de nome interna, e uma lista assinada do que ele é capaz de acionar — a especificação E4 do requisito R26 já exige essa lista, e a E6 do requisito R1 exige o teste que falha o build se houver conexão não declarada.

**Atualização.** Pacote assinado, com verificação de integridade, procedimento de reversão e janela acordada. Em air-gapped, o pacote viaja em mídia física trazida por alguém do cliente; o fornecedor não entra na rede.

**Capacidade de armazenamento.** De 0,5 a 1 GB por mil páginas, contando original, derivados, texto extraído, índice vetorial e uma cópia de backup. Acervo digitalizado ocupa o topo da faixa; PDF nativo com camada de texto, o piso.

---

## 3. Requisito

### R48. Infraestrutura local modular e elástica

**Prioridade:** Essencial · **Verticais:** todas

**Racional.** R26 e R38 definem o que compõe a infraestrutura e quais são os modos de implantação. Falta a camada que decide a compra: qual é a menor configuração defensável, quanto custa cada degrau seguinte, como o cliente cresce sem recompra e em que ponto o equipamento próprio passa a ganhar da nuvem. Em produto que se instala no cliente, essa é a diferença entre uma proposta que avança e uma conversa que morre na área de compras.

A exigência de "elástico" precisa ser traduzida. Em ambiente sem internet não existe escala automática; existe granularidade, modularidade e previsibilidade de crescimento. O requisito é que essas três coisas sejam demonstráveis antes da venda, e não descobertas na primeira expansão.

**Especificações**

- **E1. Promessa de elasticidade limitada ao que se pode cumprir.** Toda proposta descreve crescimento por acréscimo de nó e por mudança de degrau, e declara explicitamente que não há escala automática em ambiente isolado. Nenhum material comercial usa a expressão "elástico" sem essa qualificação. Verificação: revisão do material de proposta contra a tabela de degraus e a regra de crescimento de E4.
- **E2. Decomposição em quatro módulos implantáveis de forma independente.** Ingestão e OCR, índice e busca, inferência, e interface e API operam como unidades separadas, comunicando-se por contrato versionado, e apenas o módulo de inferência exige acelerador. Um cliente que já possui servidor pode adquirir somente o módulo de inferência. Verificação: instalação de homologação com os módulos em máquinas distintas e com um deles ausente, sem falha dos demais.
- **E3. Degraus de hardware com faixa de preço publicada e capacidade declarada.** Quatro degraus publicados, com hardware de referência, capacidade em páginas e usuários simultâneos, consumo elétrico e faixa de CAPEX; preço sem cotação vigente é publicado como faixa e identificado como tal, nunca como valor fechado. Verificação: tabela versionada de degraus e cotação de dois fornecedores anexada a cada proposta.
- **E4. Regra de crescimento verificável pelo cliente.** Para cada sinal de saturação — fila de indexação, memória de acelerador, latência no p95, ocupação de faixa de acervo e usuários simultâneos — existe limiar declarado e ação correspondente, com antecedência mínima de 90 dias para mudança de degrau. Verificação: painel de ocupação por degrau, visível ao cliente, com o limiar e a ação sugerida.
- **E5. Custo unitário de infraestrutura por degrau.** Custo mensal de infraestrutura por mil páginas indexadas e por usuário ativo é calculado para cada degrau, com premissa de depreciação em **36 meses**, energia ao preço da distribuidora local e operação interna declarada. O número alimenta a política de preço de *especificação E11 do requisito R44*. Verificação: planilha publicada com as três parcelas e a memória de cálculo.
- **E6. Comparação com nuvem privada em câmbio de indiferença.** A decisão entre nuvem privada e equipamento próprio é apresentada como câmbio de indiferença em 24 meses, comparando o custo do serviço equivalente na região do cliente com o CAPEX do degrau, *conforme especificação E9 do requisito R38* e *conforme decisão D3*. Moeda estrangeira não é convertida sem taxa declarada e datada. Verificação: uma linha por degrau na planilha de proposta, com a cotação usada.
- **E7. Instalação física especificada com número.** Cada degrau declara consumo médio em watts, consumo mensal em kWh, custo de energia ao preço vigente da distribuidora, dissipação térmica em BTU, espaço em rack, peso e nível de ruído. O cliente decide onde instalar com esse número, e não com "precisa de sala refrigerada". Verificação: ficha de instalação por degrau revisada a cada cotação de hardware.
- **E8. Requisitos de rede em lista fechada.** Lista publicada de portas, protocolos e resolução de nome necessários, com a declaração de que não há destino externo no Modo A, *conforme especificação E4 do requisito R26*. A lista é assinada pela segurança do cliente antes da instalação. Verificação: documento de rede por degrau, comparado com a captura de tráfego do teste de confinamento.
- **E9. Crescimento de armazenamento dimensionado.** O dimensionamento declara gigabytes por mil páginas para original, derivados, índice vetorial e backup, com a diferença entre acervo digitalizado e documento nativo, e reserva de 30% de folga. Verificação: calculadora de armazenamento entregue ao cliente e conferida contra o acervo do piloto ao final da carga.
- **E10. Atualização de hardware e de modelo sem parada da operação.** Troca de modelo, ampliação de memória e entrada de novo nó ocorrem com a busca disponível, aproveitando a separação entre carga interativa e carga de lote de *especificação E3 do requisito R27*, com janela acordada e procedimento de reversão. Verificação: ensaio documentado de upgrade em ambiente de homologação, com tempo de indisponibilidade medido.
- **E11. Isolamento de memória de acelerador verificável.** A escolha entre processo de inferência dedicado por tenant, limpeza explícita de memória entre requisições e acelerador exclusivo para cliente de alto sigilo é declarada, configurável por cliente e comprovada por teste, *conforme especificação E4 do requisito R25*. A escolha de acelerador exclusivo é apresentada com o seu custo em degrau, para que seja decisão comercial informada. Verificação: teste que executa requisição de um tenant e inspeciona a memória liberada antes da seguinte.
- **E12. Mínimo observável para operação sem acesso remoto.** Todo degrau entrega monitoração local de CPU, memória, acelerador, disco, fila de ingestão, latência e integridade de backup, com alerta local e relatório exportável, sem depender de serviço externo, *conforme especificação E1 do requisito R29*. É o insumo do pacote de evidências de *especificação E8 do requisito R46*. Verificação: painel local funcionando com a rede externa bloqueada.
- **E13. Perfil sem acelerador declarado como troca, não como equivalente.** O modo somente CPU existe com desempenho, latência e limitação de qualidade declarados, para viabilizar avaliação de baixo custo, e nunca é apresentado como substituto de um degrau com GPU. Verificação: ficha de desempenho em CPU publicada ao lado da ficha com GPU, com a mesma carga de teste.

---

## 4. O que derruba esta recomendação

1. **A cotação real do D2 ficar acima de R$ 220 mil.** O custo por usuário sobe de R$ 235 para cerca de R$ 350 por mês e o degrau departamental deixa de caber no preço de tabela do [documento 06](06-precificacao-e-escala.md). A resposta seria reduzir o D2 para uma placa de 32 GB e reservar 48 GB para o D3.
2. **O acervo real ocupar mais de 2 GB por mil páginas.** Toda a coluna de armazenamento e metade da coluna de custo por página mudam, e o cálculo de backup passa a dominar o CAPEX.
3. **O modelo local passar a exigir 70 bilhões de parâmetros como piso de qualidade.** O D1 deixa de existir comercialmente, o degrau de entrada vira D2 e o preço de entrada dobra.
4. **A nuvem soberana brasileira passar a oferecer GPU a preço competitivo e com jurisdição aceita pelo cliente.** O argumento do ferro próprio cai de "quatro a oito vezes mais barato" para "pouco mais barato", e a venda passa a depender só do requisito de air-gap.
5. **O cliente não tiver quem opere backup e monitoração.** A operação interna estimada em R$ 500 a R$ 8.000 por mês deixa de ser premissa e vira custo do fornecedor, o que reabre a curva do [documento 07](07-sustentacao.md).
6. **O teste de isolamento de memória de acelerador da E11 falhar em multi-tenant.** A instância dedicada passa a ser obrigatória, e com ela o degrau mínimo sobe para D2 em todo cliente.

## 5. Fontes

- **Hardware:** pcbuilder.com.br (oferta RTX 5090, 17/09/2026); nvidia.com/en-us/products/workstations/dgx-spark (especificação e consumo, consulta 10/11/2026).
- **Energia:** Enel SP, grupo A4 azul, e REH ANEEL 3.596/2026, vigência 04/07/2026.
- **GPU em nuvem:** AWS sa-east-1, tabela oficial de preços `AmazonEC2/current/sa-east-1/index.csv` (vigência 01–07/11/2026); Azure Retail Prices API, região `brazilsouth` (consulta 10/11/2026).
- **Interno:** [01-catalogo-requisitos.md](01-catalogo-requisitos.md) (R25, R26, R27, R29, R38) · [03-registro-decisoes.md](03-registro-decisoes.md) (D3) · [12-fontes-e-base-de-fatos.md](12-fontes-e-base-de-fatos.md) (seções 5 e 6).
- Preço de servidor com GPU em real **não é publicado** por Dell, HPE, Lenovo e Supermicro no Brasil. Toda faixa marcada `[a validar]` depende de cotação direta.
