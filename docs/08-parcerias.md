# Parcerias e Canal: Quem Implanta, Quem Vende e Quem Pode Virar Concorrente

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Requisito:** R47 · **Papel:** definir por onde o produto chega ao cliente quando o fornecedor é pequeno e o produto exige presença física.

**Documentos irmãos:** [05-analise-de-gaps.md](05-analise-de-gaps.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [06-precificacao-e-escala.md](06-precificacao-e-escala.md) · [10-concorrentes.md](10-concorrentes.md)

---

## 1. Diagnóstico

### 1.1. O produto vende para um universo que um fornecedor pequeno não alcança sozinho

O universo endereçável, em números oficiais: 1.514.918 advogados inscritos na OAB (quadro geral de 1.635.150, com SP em 397.309), 550.864 profissionais da contabilidade ativos e 97.836 organizações contábeis (Fonte: oab.org.br e cfc.org.br, consulta 10/11/2026), 5.570 municípios (Fonte: IBGE, Censo 2022) e ~25,7 milhões de empresas ativas (Fonte: Mapa de Empresas / Receita Federal, dados até set/2026).

O mercado comprador não é a restrição: software e serviços somam US$ 35,4 bi com crescimento de 16,7% em 2025 (Fonte: ABES/IDC, Mercado Brasileiro de Software 2026, publicado em 02/08/2026). A restrição é distribuição — e ela é estrutural, não comercial. O Modo A é air-gapped integral, sem nenhuma rota externa, e é o modo de fábrica e o modo contratual *conforme especificação E1 do requisito R38*. Sem rota, não existe acesso remoto de suporte. O primeiro atendimento tem de ser de alguém que esteja no prédio.

### 1.2. Hardware é o gargalo mais concreto da proposta

Nenhum servidor com GPU tem preço público em BRL. L40S, RTX 6000 Ada e servidores de 4 GPUs são vendidos sob consulta por Dell, HPE, Lenovo e Supermicro, e o próprio DGX Spark não publica preço na página do fabricante. O único número verificável é o de varejo: RTX 5090 a R$ 31.999,99 no Pix (Fonte: pcbuilder.com.br, oferta de 17/09/2026).

Isso é uma frase de venda ruim e uma frase de compra pior: toda proposta começa com "depende de cotação". Um fabricante que publica preço de lista, homologa configuração e financia a compra vale mais para este negócio do que qualquer desconto de canal.

### 1.3. A margem de canal no Brasil não é pública, e isso muda a decisão

Consultei os programas de parceiros de Dell, HPE, Lenovo, NVIDIA e Microsoft e os distribuidores de valor Allnations, Officer, Pauta, Teltec e SND. Os programas existem e são públicos na estrutura; **o percentual de desconto não é**. A política de registro de oportunidade da Dell que circula publicamente está marcada como uso interno e confidencial.

O padrão internacional de 20–35% de desconto de revenda em software é **[estimativa declarada]**, sem fonte brasileira localizada. A premissa que a sustenta: mercado de canal maduro, distribuidor de valor com duas camadas (distribuidor e revenda) e produto de ticket médio com ciclo de venda consultivo.

A consequência é dura: sem saber quanto o canal custa, a única forma de decidir é fixar o desconto de dentro para fora, a partir da margem que o produto suporta. A margem bruta mediana de SaaS é 77%, e a de serviços profissionais é 30% (Fonte: Benchmarkit, SaaS Performance Metrics 2025, dados de 2024). Desconto de canal sai dos 77%, nunca dos 30%.

### 1.4. Existe âncora de preço baixa no nicho

A oferta air-gapped já publicada no Brasil é de R$ 1.099,90/mês rodando no hardware do cliente (Fonte: ialocus.com.br, 15/10/2026, autopublicidade). Com esse teto de percepção, um desconto de revenda de 30% sobre a licença consome quase um terço da receita recorrente de um produto cujo custo real inclui suporte de campo. Não há folga para pagar canal e sustentar o time descrito em [07-sustentacao.md](07-sustentacao.md).

O mesmo dado tem uma leitura favorável. Um concorrente que já cobra R$ 1.099,90/mês para rodar no hardware do cliente está dizendo, com preço publicado, que existe disposição a pagar por residência local. O canal não precisa criar essa disposição; precisa alcançar quem já a tem.

### 1.5. Implantação é custo que o fornecedor pagaria de qualquer forma

A referência de mercado para onboarding de software jurídico é de R$ 500 a R$ 5.000 ou mais por cliente, com treinamento ao vivo a R$ 150–500/hora e migração de dados cobrada à parte (Fonte: asquadz.ai, 05/02/2026). Esse número é de produto em nuvem, onde o dado já está no servidor do fornecedor e ninguém precisa subir um rack.

Instalação on-premise é outro serviço: servidor, rede, energia, migração de acervo com fila de exceções e treinamento presencial. Um time enxuto de sustentação com um consultor de implantação custa, no total, algo entre R$ 105 mil e R$ 125 mil por mês **[estimativa declarada, a partir do custo de pessoal da base de fatos e do multiplicador de encargos de ~1,7–1,8×]**. Esse custo existe com ou sem parceiro. Pagar repasse ao integrador não cria despesa nova; converte despesa fixa em variável e libera o time para o que só ele pode fazer.

### 1.6. Compras públicas são o canal onde a capilaridade importa mais

São 5.570 municípios, e a Lei 14.133/2021 permite julgamento por técnica e preço para bens e serviços especiais de TIC, com peso técnico de até 70% (art. 36, §1º, III). Um produto cuja diferença é técnica tem vantagem em técnica e preço e desvantagem em pregão de menor preço. Isso define com quem se faz canal: parceiro que sabe montar processo licitatório, não parceiro que sabe dar lance.

O ciclo mínimo de divulgação do edital é de 35 dias úteis em técnica e preço (art. 55), e o prazo real de ponta a ponta não está publicado. Cada certame é um projeto, e projeto em 5.570 municípios não se faz de um escritório só.

### 1.7. A economia do parceiro empurra ele para o lado do concorrente

Serviços profissionais têm margem mediana de 30%; assinatura de software tem 81% (Fonte: Benchmarkit, 2025). Um integrador que implanta ganha a margem de serviços; um integrador que vira fornecedor de produto ganha a margem de software. A tentação não é deslealdade, é aritmética.

O que ele aprende no caminho é justamente o ativo: método de implantação, critério de acervo pronto, forma de calibrar avaliação e o jeito de provar valor nas duas primeiras semanas. Código-fonte ele não leva; método ele leva na cabeça. Por isso a governança da parceria não protege o software — protege o método, e protege o cliente.

---

## 2. Decisão proposta

**Recomendação: o canal é de indicação e de implantação credenciada. A licença continua sendo contratada entre o fornecedor e o cliente.**

O parceiro vende o serviço de campo que o fornecedor não consegue entregar — instalar servidor, preparar rede, migrar acervo, treinar usuário na sala — e recebe por isso com margem alta e verificável. O fornecedor mantém o contrato de licença, o preço de tabela e a relação com o cliente. O parceiro é remunerado por indicação e por implantação, não por revenda de licença com desconto estrutural.

**Alternativa descartada:** revenda plena de licença com desconto de linha de tabela e opção de marca branca desde o primeiro ciclo. Descartada porque transfere ao parceiro o preço-âncora e a titularidade da relação justamente no momento em que o produto ainda precisa provar a tese e não tem base instalada para defender margem.

Duas parcerias entram primeiro, nesta ordem: **integrador regional de implantação** — porque sem ele não existe primeiro atendimento em ambiente sem rota — e **fabricante de GPU e servidor** — porque sem preço de hardware publicado não existe proposta que o cliente consiga aprovar.

### 2.1. Tipologia de parceria

| Tipo | O que resolve | O que custa |
|---|---|---|
| **Revenda de licença** | alcance comercial e capilaridade onde o fornecedor não tem vendedor | 20–30% da margem recorrente; o parceiro passa a conhecer o produto e o cliente |
| **Integrador de implantação** | presença física, hardware, rede, migração de acervo, primeira linha em ambiente sem acesso remoto | certificação e treinamento, risco de qualidade, disputa sobre quem responde pelo SLA |
| **Fabricante de GPU e servidor** | homologação, preço de lista publicado, financiamento, unidade de demonstração, co-marketing | dependência de roadmap alheio; o fornecedor pequeno é conta de baixa prioridade |
| **Nuvem e colocation** | capacidade elástica para os modos C e D, energia, refrigeração e Link dedicado | contrato de nuvem, jurisdição, risco de o cliente confundir o produto com SaaS |
| **Associação profissional** | legitimidade e alcance a 1,5 milhão de advogados e 550 mil contadores | regra de publicidade, risco de captação indevida, ciclo político longo |
| **Produtor de conteúdo** | demanda qualificada e educação de um mercado que ainda não sabe o que pedir | atribuição, controle editorial, CAC difuso e difícil de atribuir |
| **Validação técnica** (laboratório, universidade, auditoria) | evidência independente para venda institucional e para o questionário de segurança | tempo, custo, e o risco de o resultado ser negativo e público |

### 2.2. Aritmética da remuneração

Desconto de canal se confunde com margem, e a confusão custa caro na negociação. A tabela abaixo fixa o vocabulário.

| Instrumento | Número | O que significa na prática | Margem que sobra no fornecedor |
|---|---|---|---|
| Desconto de revenda de licença | 20% da tabela (faixa 15–25%) | parceiro compra a 80 e revende a 100: margem de 20% sobre a receita, markup de 25% sobre o custo | 0,80 × 77% = **62%** da receita cheia |
| Desconto de renovação | 10% da tabela | renovação não tem custo de aquisição; desconto menor é defensável | 0,90 × 77% = **69%** |
| Comissão de indicação | 10% do primeiro ano (faixa 8–12%) | parceiro só indica, não implanta nem fatura; pago após recebimento | **62%** no primeiro ano, 77% depois |
| Repasse de implantação | 60–70% do valor cobrado | parceiro executa o campo; o fornecedor fica com 30–40% e sem o custo variável | margem de serviços, próxima dos **30%** do benchmark |

Todos os percentuais de desconto e comissão são **[estimativa declarada]**: não há fonte pública brasileira de margem de canal, e o padrão internacional de 20–35% não foi localizado em publicação que o sustente. A premissa que ancora os números é a margem bruta de 77% do benchmark de SaaS (Benchmarkit 2025), que é o teto de qualquer conversa de desconto.

A coluna da direita é o argumento que fecha a decisão: desconto de revenda de licença custa 15 pontos de margem por cliente e por ano, para sempre, enquanto repasse de implantação custa uma vez e substitui um custo que já existiria.

### 2.3. O que esta decisão recusa, explicitamente

- **Recusa desconto de canal sobre suporte recorrente.** O suporte é o maior consumidor de margem do modelo e o parceiro não o executa — quem responde pelo nível de serviço *conforme especificação E1 do requisito R39* é o fornecedor.
- **Recusa exclusividade territorial no primeiro ciclo.** Exclusividade sem histórico de entrega é monopólio pago adiantado a quem ainda não provou nada.
- **Recusa parceria com quem revende concorrente direto**, mesmo que o concorrente seja de categoria adjacente. A exceção, se houver, é registrada e justificada por escrito.
- **Recusa qualquer arranjo que dê ao parceiro acesso ao acervo do cliente.** Ele instala no ambiente do cliente e sai. Não recebe cópia, não recebe amostra, não recebe índice.
- **Recusa convênio com associação profissional que envolva pagamento por indicação de associado**, mesmo disfarçado de patrocínio ou de repasse a fundo institucional. É captação de clientela com outro nome e contamina o produto inteiro.

---

## 3. R47. Ecossistema de parcerias e canal

**Prioridade:** Importante · **Verticais:** todas

**Racional.** A tese do produto — trabalhar com o acervo sem expor o acervo — só chega ao cliente por alguém que entre no prédio. O fornecedor é pequeno por desenho, e o produto exige hardware, rede e relacionamento local. Isso cria uma dependência real de terceiros e um risco simétrico: quem implanta aprende o produto, ganha a confiança do cliente e pode virar concorrente ou refém da relação.

O erro comum é tratar canal como desconto. Desconto é o preço da dependência; a pergunta que decide é quem fica com o cliente e com o preço. Por isso a recomendação separa a remuneração do serviço de campo da titularidade da licença, e trata revenda de licença como um passo que se paga com volume comprovado, não como ponto de partida.

O segundo risco é de qualidade, não de dinheiro. Um integrador que implanta mal em um cliente de referência custa mais caro do que dez propostas perdidas, porque o acervo é sensível e o erro vira notícia no setor.

Há uma restrição que nenhuma parceria resolve e que precisa estar escrita: o padrão air-gapped e a vedação de egresso automático valem para o parceiro também. Nenhum acordo autoriza rota de suporte, telemetria, atualização em nuvem ou conector com internet fora do Modo B. Parceiro que não aceita isso não é parceiro — é o primeiro incidente.

**Especificações**

- **E1. Tipologia obrigatória com contrapartida declarada.** Nenhum acordo é assinado sem que se declare em qual das sete categorias da tabela da seção 2.1 ele se enquadra, qual problema resolve e qual contrapartida recebe. Verificação: registro de parceria ativo com categoria, contrapartida, território e prazo, revisado a cada renovação.

- **E2. Critério de seleção e critério de exclusão.** Seleção exige presença física na praça, capacidade de primeira linha em ambiente sem acesso remoto, aceite escrito do modo air-gapped como padrão e situação financeira verificável. Exclusão automática por: revenda ativa de concorrente direto mapeado em [10-concorrentes.md](10-concorrentes.md); recusa de treinamento ou de auditoria de qualidade; histórico de incidente de dados; insistência em habilitar egresso. Verificação: ficha de qualificação com declaração de conflito de interesse assinada, renovada anualmente e conferida contra a carteira pública do parceiro.

- **E3. Modelo de remuneração com números.** Três instrumentos, e nenhum deles é desconto aberto: revenda de licença a **20% sobre o preço de tabela** (faixa 15–25%), caindo para 10% na renovação, porque renovação não tem custo de aquisição; comissão de indicação de **10% do valor do primeiro ano** (faixa 8–12%), paga somente após recebimento; repasse de implantação de **60 a 70% do valor cobrado do cliente**, com referência de R$ 12 mil a R$ 20 mil por instalação departamental. Todos os três são **[estimativa declarada]**, com duas premissas: a margem bruta de 77% do benchmark de SaaS (Benchmarkit 2025) como teto, e 10 a 15 dias de campo por instalação, ao custo total de R$ 15–22 mil/mês de um consultor. O valor absoluto da implantação é fixado em [06-precificacao-e-escala.md](06-precificacao-e-escala.md); aqui se fixa a proporção. Verificação: tabela de remuneração versionada e simulação de margem por combinação de tipo e volume.

- **E4. Fabricante de GPU e servidor: o que se pede além do desconto.** O acordo com fabricante tem de entregar seis coisas, e desconto é a menos importante: homologação do servidor nos perfis de implantação *conforme especificação E1 do requisito R26*; preço de lista em BRL publicado e válido para cotação do cliente; financiamento ou leasing; unidade de demonstração para prova de conceito; co-marketing com o produto nomeado; e engenharia de segunda linha para problema de driver, firmware e memória de acelerador. Verificação: acordo com anexo de homologação assinado e cláusula de preço de lista público com prazo de validade.

- **E5. Implantação por integrador regional: certificação, qualidade e SLA.** Certificação por exame e implantação supervisionada, com selo válido por 12 meses e no mínimo duas pessoas certificadas por parceiro. Auditoria de qualidade em uma a cada cinco implantações, com checklist e nota. O fornecedor responde ao cliente pelo nível de serviço *conforme especificação E1 do requisito R39*, e o integrador responde ao fornecedor por contrato de subcontratação com prazo interno mais curto que o prazo externo prometido. Verificação: painel por parceiro com chamados, prazo de primeira resposta, reincidência e nota de auditoria.

- **E6. Associações profissionais: o que é legítimo e o que colide.** Legítimo: convênio de benefício ao associado, conteúdo técnico, curso com certificação, participação em evento institucional e pesquisa de mercado com associados que consentirem. Vedado: comissão por indicação de associado, acesso a lista de inscritos para abordagem, uso de brasão ou selo como endosso, e qualquer arranjo que caracterize captação de clientela — vedada pelo Estatuto da Advocacia e pelo Código de Ética e Disciplina da OAB, com vedação equivalente a propaganda imoderada no código do CFC. O sigilo profissional impõe que nenhum dado de associado, de escritório ou de acervo transite pela associação. Verificação: parecer jurídico arquivado antes da assinatura de cada convênio.

- **E7. Ecossistema de complemento.** Integrações com GED e assinatura eletrônica, ERP, sistemas de processo eletrônico e mercado de integração, apoiadas nos conectores e na API de R33, *conforme especificação E3 do requisito R33* e *conforme especificação E6 do requisito R33*, e homologadas pelo processo de *especificação E3 do requisito R40*. Nenhum conector de parceiro abre rota de egresso: integração que dependa de internet só existe no Modo B, com destino no catálogo fechado *conforme especificação E2 do requisito R38*. Verificação: homologação com teste de egresso anexado ao processo do conector.

- **E8. Compras públicas como canal.** Três frentes, com tratamento distinto. Primeira: julgamento por técnica e preço para bens e serviços especiais de TIC, com peso técnico de até 70% (Lei 14.133/2021, art. 36, §1º, III) — favorável, porque a diferenciação do produto é técnica. Segunda: restrição a tecnologia desenvolvida no País em TIC estratégico (art. 26, §7º), que só se aplica se o produto atender ao processo produtivo básico **[a validar]**. Terceira: registro de preços, cuja ata vale um ano e é prorrogável por igual período (art. 84), permitindo que um certame sirva vários órgãos. Pregão por menor preço é ameaça, não canal: comoditiza o objeto e é vedado para serviço técnico intelectual (art. 29, parágrafo único). O ciclo mínimo de divulgação em técnica e preço é de 35 dias úteis (art. 55). Exceção declarada à regra de titularidade: em compra pública o parceiro pode ser o contratado do hardware e da implantação, com a licença contratada diretamente pelo órgão ou sublicenciada com cláusula de auditoria e de reversão. Verificação: pipeline público com órgão, categoria, prazo e parceiro responsável.

- **E9. Governança da parceria.** Contrato padrão com: metas anuais em número de implantações e de usuários ativos, não em receita de licença; território definido; exclusividade apenas após 24 meses e dez implantações com nota de auditoria aprovada; treinamento mínimo; renovação anual; término com aviso de 90 dias. Na transição, acervo, credencial, índice e histórico de chamados passam ao fornecedor em até 30 dias, e o parceiro não retém cópia. Verificação: contrato padrão vigente e checklist de transição testado em um caso simulado antes do primeiro acordo.

- **E10. Risco de o parceiro virar concorrente, e a hipótese de marca branca.** O risco é real e não se mitiga por telemetria: no Modo A não há rota para o fornecedor observar a base instalada. As mitigações são contratuais e de produto — licença vinculada a CNPJ com renovação offline *conforme especificação E6 do requisito R38*, relatório de uso assinado pelo cliente, auditoria anual com direito de acesso, e cláusula de não concorrência de 24 meses sobre produto equivalente. Marca branca se aceita somente com as três condições juntas: volume mínimo que pague uma linha de produto separada, auditoria e não concorrência aceitas, e nome do fornecedor visível na documentação técnica e no contrato do cliente final. Fora disso, recusa. Verificação: decisão registrada por proposta de marca branca, com as três condições checadas.

- **E11. Métrica de sucesso do canal.** Quatro números, medidos por trimestre: participação do canal na receita nova de 25% no ano 2 e 40% no ano 3; nenhum parceiro acima de 20% da receita de canal; desconto total pago no ano inferior ao custo de aquisição direta equivalente, usando a referência de US$ 2,00 de vendas e marketing por US$ 1,00 de receita nova (Benchmarkit 2025); e retorno do investimento em canal em 18 meses. Com desconto de 20% e margem bruta de 77%, cada R$ 1,00 de receita de canal entrega R$ 0,62 de margem de contribuição no primeiro ano. As quatro metas são **[estimativa declarada]**, com premissa de dois parceiros certificados e dez implantações por parceiro no primeiro ciclo. Verificação: painel trimestral com os quatro números e decisão registrada quando dois deles falharem por dois trimestres.

- **E12. Origem e licença do que o parceiro agrega.** Todo conector, extrator, adaptador ou corpus trazido por parceiro passa pela homologação de *especificação E3 do requisito R40*, com licença declarada e parecer arquivado antes da primeira entrega; componente com licença copyleft em produto distribuído é bloqueado. Parceiro não embute pesos de modelo sem licença compatível com o processo de *especificação E4 do requisito R40*. Verificação: SBOM por integração de parceiro e parecer arquivado, revalidados a cada versão maior.

**Ordem de execução.** Primeiros 90 dias: contrato padrão da E9 escrito, ficha de qualificação da E2 em uso e tabela de remuneração da E3 publicada internamente, antes de qualquer conversa com parceiro. Depois disso: dois integradores certificados na E5, em duas praças distintas, e um acordo de homologação com fabricante na E4. O primeiro acordo de revenda de licença só entra depois de dez implantações com nota de auditoria aprovada — é o que a exclusividade condicional da E9 já pressupõe.

---

## Fontes

- OAB — Quadro de Advogados: https://www.oab.org.br/institucionalconselhofederal/quadroadvogados (consulta 10/11/2026)
- CFC — consulta por região e matéria institucional sobre organizações contábeis: https://www3.cfc.org.br e https://cfc.org.br/noticias (25/04/2025)
- IBGE — Divisão Territorial, Censo 2022 (municípios)
- gov.br — Mapa de Empresas / Receita Federal (empresas ativas, dados até set/2026)
- ABES/IDC — Mercado Brasileiro de Software 2026, publicado em 02/08/2026: https://www.abes.org.br
- asquadz.ai — referência de custo de onboarding e serviços atrelados, 05/02/2026
- Benchmarkit — SaaS Performance Metrics 2025 (dados de 2024)
- ialocus.com.br — página de planos, revisão de 15/10/2026 (âncora de preço air-gapped)
- pcbuilder.com.br — oferta RTX 5090, 17/09/2026
- nvidia.com — DGX Spark: https://www.nvidia.com/en-us/products/workstations/dgx-spark/ (preço não publicado)
- Planalto — Lei 14.133/2021, arts. 26, 29, 36, 55 e 84: https://www.planalto.gov.br/ccivil_03/_ato2019-2022/2021/lei/l14133.htm
- Programas de parceiros consultados sem percentual público: Dell, HPE, Lenovo, NVIDIA NPN, Microsoft; distribuidores Allnations, Officer, Pauta, Teltec e SND

---

## O que derruba esta recomendação

- **Se o fabricante de GPU publicar preço de lista em BRL e aceitar venda direta ao cliente final**, a parceria de hardware perde a função e o integrador volta a ser o único canal necessário.
- **Se o desconto de revenda praticado no mercado brasileiro for de 35% ou mais**, a regra de 20% da E3 fica fora do mercado e a remuneração de licença precisa ser refeita — e, nesse caso, a licença deixa de financiar o canal.
- **Se o parceiro aceitar implantar sem certificação porque o cliente exigiu prazo**, a E5 perde efeito e o controle de qualidade vira ficção. Um caso desses autoriza revisar a política de credenciamento, não relativizá-la.
- **Se o processo produtivo básico não for atendido**, a frente de compras públicas por tecnologia nacional (art. 26, §7º) desaparece e sobra apenas técnica e preço.
- **Se um único parceiro passar de 20% da receita de canal por dois trimestres**, a dependência que a E11 tenta evitar já aconteceu e a decisão de exclusividade precisa ser revista antes da renovação.
- **Se o integrador não conseguir cumprir primeira linha presencial em 48 horas na praça dele**, a premissa do diagnóstico 1.1 cai e o credenciamento não se sustenta: nesse caso a conversa volta a ser sobre cobertura própria, não sobre canal.
