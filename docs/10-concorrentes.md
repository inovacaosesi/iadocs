# Concorrentes: Quem Cobra Quanto, o Que Atacar e o Que Copiar

**Fase:** discovery / brainstorming · **Versão:** 1.0 · **Papel:** mapa competitivo do mercado de IA documental no Brasil, com preço praticado, brecha atacável e vantagem a imitar.

**Requisito deste documento:** R49 — Inteligência competitiva.

**Documentos irmãos:** [05-analise-de-gaps.md](05-analise-de-gaps.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [06-precificacao-e-escala.md](06-precificacao-e-escala.md) · [08-parcerias.md](08-parcerias.md) · [11-publico-alvo-e-margem.md](11-publico-alvo-e-margem.md)

---

## 1. Diagnóstico: o concorrente que não aparece na planilha

Quem monta a planilha de concorrentes começa pelo Jurídico AI e pelo Jus IA. Começa errado. O concorrente que mais tira negócio deste produto não tem CNPJ de fornecedor de IA jurídica, não publica preço e não aparece em nenhuma análise de mercado: é o advogado ou o analista que copia o trecho do contrato, cola no ChatGPT e recebe uma resposta em oito segundos. Ele é gratuito na percepção de quem usa, já é familiar, não exige treinamento, não exige aprovação de TI e resolve o problema imediato. O piso de preço desse comportamento é conhecido e baixo: Claude Pro a US$ 20/mês e ChatGPT Business a US$ 25/assento/mês (Fonte: haqq.ai, 20/10/2026 [T]).

Isso não é uma observação sobre a qualidade da IA de consumo. É uma observação sobre a natureza da concorrência. Todo fornecedor pago deste mercado — inclusive este produto — é um aperfeiçoamento desse comportamento, e o comprador só migra quando a diferença entre os dois deixa de ser qualidade de resposta e passa a ser consequência. O usuário não troca o ChatGPT por ser pior; ele já sabe que é pior. Ele não troca porque ainda não pagou o preço de ter usado.

O preço que ele paga aparece em três momentos, e nenhum deles é técnico: quando o cliente do escritório pergunta de onde saiu aquele trecho e não existe resposta rastreável; quando o compliance pergunta o que exatamente foi enviado para fora na semana passada e não existe registro; quando o contrato de um cliente institucional proíbe expressamente o uso de ferramenta externa com dados do acervo e alguém descobre que a proibição é letra morta. Nesses três momentos, os cinco diferenciais do produto deixam de ser características e viram a única resposta possível — perímetro local, citação verificada contra o acervo, trilha de auditoria, air-gap e ausência de envio automático. Ver [01-catalogo-requisitos.md](01-catalogo-requisitos.md), requisitos R1, R4 e R19.

A consequência estratégica é contraintuitiva e precisa estar escrita: a mensagem de venda não é "respostas melhores que o ChatGPT". É "o mesmo hábito, dentro do perímetro, com rastro". Vender qualidade de modelo é entrar numa corrida que o fornecedor de modelo de fronteira vence todo trimestre. Vender governança do hábito é entrar numa corrida que ninguém está correndo com produto brasileiro, e é a única em que a instalação local é uma vantagem e não um custo.

O universo é grande o bastante para sustentar isso. São **1.514.918 advogados inscritos na OAB** (Fonte: oab.org.br, consulta 10/11/2026 [O]) e **550.864 profissionais da contabilidade ativos em 97.836 organizações contábeis** (Fonte: cfc.org.br, consulta 10/11/2026 [O]). Basta uma fração pequena desse universo ter um cliente institucional que exige confinamento para o produto ter mercado. Não é preciso converter o mercado; é preciso alcançar quem já é obrigado a se importar.

---

## 2. Mapa por categoria

Empresa não é categoria. O comprador não compara "Locus contra Jurídico AI"; ele compara "chat jurídico mensal" contra "sistema de gestão" contra "nada". O mapa abaixo usa as seis categorias que aparecem na mesa de compra.

**2.1 IA jurídica de autoatendimento.** Jurídico AI, Jus IA, Locus.IA, ChatADV, Forlex, MinutaIA, Legalcloud, Escavador. Compra no cartão, uso imediato, cobrança por usuário com cota de mensagens ou de análises. É a categoria mais barata e a mais comoditizada: o produto é o mesmo modelo de fronteira com um prompt de jurídico em cima, e a diferenciação real é o acervo que vem junto — Jus IA vende acesso ao Jusbrasil, Locus vende análise de documento. Satura entre R$ 50 e R$ 250 por usuário/mês.

**2.2 Gestão jurídica com IA embutida.** SAJ ADV, Astrea/Aurum, ADVBox, EasyJur, Juridiq, Projuris, Legal One, Themis, Looplex. Aqui o software já está dentro do escritório e a IA entra como módulo. É a categoria mais perigosa por distribuição, não por produto: o fornecedor não precisa convencer ninguém a adotar ferramenta nova, precisa só ligar um botão na base instalada. Looplex é o caso extremo — R$ 6.000/mês para 10 usuários no plano Básico (Fonte: looplex.com.br/pt-br/pricing, 10/11/2026 [O]), com créditos de IA e créditos de implantação embutidos, e o plano Ultimate declarando inferência de IA no ambiente do cliente. Quem já paga R$ 6.000/mês por software jurídico não compara preço com um chat de R$ 78,90.

**2.3 Pesquisa jurisprudencial.** Turivius, Jus IA na função de pesquisa, JUIT Rimor, CoCounsel no exterior. O ativo é o acervo, não o modelo. Nenhum deles publica preço; todos vendem por demonstração. A brecha é que acervo de terceiro não é acervo do cliente: a resposta cita o precedente público e não o documento que o cliente guarda.

**2.4 IA documental para contratos.** netLex, Looplex, Deep Legal, Kurier, Finch. ciclo de vida de contrato, geração e revisão. netLex é enterprise e não publica preço; a página de preços retornou 404 na consulta de 10/11/2026 [a validar]. Esta é a categoria que mais se parece com o produto em escopo funcional e menos se parece em postura: são plataformas de contrato em nuvem, não plataformas de acervo confinado.

**2.5 Plataforma soberana ou air-gapped.** Locus.IA no modo Local Air-Gapped e, no exterior, as ofertas de implantação dedicada de CoCounsel e Harvey. É a categoria em que este produto vive, e ela tem exatamente um preço público no Brasil: **R$ 1.099,90/mês** (Fonte: ialocus.com.br, 12/05/2026, rev. 15/10/2026 [I]). O resto é "sob consulta".

**2.6 Assistente genérico de uso pessoal.** ChatGPT, Claude, Gemini, Copilot. Não é concorrente de categoria, é o concorrente de comportamento descrito na seção 1. Aparece em toda negociação como a alternativa implícita e precisa ser tratado como tal no material de venda, não escondido.

---

## 3. Preço praticado, com fonte e data

Todos os valores em BRL salvo indicação. Onde a fonte é USD, o valor não foi convertido: a base de fatos usada por este conjunto não verificou câmbio (ver [Fontes](#fontes)), e converter agora produziria um número com duas camadas de incerteza.

| Concorrente | Categoria | Preço publicado | Fonte e data | Brecha que exploramos | Vantagem que imitamos |
|---|---|---|---|---|---|
| **Assistente genérico** (ChatGPT, Claude) | 6 — uso pessoal | US$ 20–25/mês por assento | haqq.ai, 20/10/2026 [T] | Dado sai do perímetro; sem citação verificável; sem trilha de auditoria; depende de internet por definição | Preço de entrada, onboarding em minutos e familiaridade |
| **Jurídico AI** | 1 — autoatendimento | R$ 55,92 (anual) a R$ 249,90/mês; grátis com 1 caso e 10 usos | juridico.ai/planos, out–nov/2026 [O] | Resposta sobre acervo de terceiro, não sobre o acervo do cliente; sem air-gap | Plano gratuito como porta de entrada e preço anual com desconto real |
| **Jus IA** (Jusbrasil) | 1 — autoatendimento | R$ 78,90 · R$ 108,90 · R$ 208,90/mês; 1º mês R$ 1,90 | ia.jusbrasil.com.br/planos, 2026 [O] | Acervo Jusbrasil não é o acervo do escritório; documento carregado sai do perímetro | Acervo próprio como argumento de venda; primeiro mês simbólico |
| **Locus.IA** | 1 e 5 — autoatendimento e air-gapped | R$ 149,90 / 249,90 / 499,90 / 699,90/mês por volume de análises; **Local Air-Gapped R$ 1.099,90/mês** | ialocus.com.br, 12/05/2026, rev. 15/10/2026 [I] | Cobrança por análise torna o custo imprevisível; air-gapped exige GPU do cliente e não inclui acervo, governança de egresso nem trilha de auditoria verificável | Ser o único concorrente que já provou que existe demanda por soberania — e usar o preço dele como âncora |
| **Judit** | adjacente — monitoramento | R$ 39,90 / 89,90 / 249,90/mês em créditos | ialocus.com.br, 15/10/2026 [I] | Produto de monitoramento processual, não de acervo; créditos de IA com custo variável | Modelo de crédito previsível para tarefa repetitiva |
| **SAJ ADV** (Softplan) | 2 — gestão | R$ 79–159/usuário/mês | asquadz.ai, 05/02/2026 [T] | IA como módulo acessório; sem operação air-gapped; dado no fornecedor | Base instalada e distribuição Softplan |
| **Astrea / Aurum** | 2 — gestão | R$ 89–179/usuário/mês | asquadz.ai, 05/02/2026 [T] | Foco em processo e financeiro, não em acervo documental; sem citação validada | UX de entrada e gratuidade inicial para captura de base |
| **ADVBox** | 2 — gestão | R$ 99–249/usuário/mês | asquadz.ai, 05/02/2026 [T] | Sem confinamento; sem auditoria de egresso | API aberta e integração com financeiro |
| **EasyJur** | 2 — gestão | R$ 69–149/usuário/mês | asquadz.ai, 05/02/2026 [T] | IA generativa como chamariz de plano, não como arquitetura | IA embutida no plano de entrada, sem cobrança adicional |
| **Juridiq** | 2 — gestão | R$ 49–99/usuário/mês | asquadz.ai, 05/02/2026 [T] | Preço baixo paga escopo baixo: sem soberania, sem auditoria | Preço de entrada mais agressivo do mercado |
| **Projuris** | 2 — gestão enterprise | a partir de ~R$ 200/usuário/mês; completo sob consulta | asquadz.ai, 05/02/2026 [T] | Departamento jurídico não aceita IA em nuvem para acervo sensível; nada air-gapped | Venda consultiva para departamento jurídico e integração com gestão |
| **Legal One** (Thomson Reuters) | 2 — gestão enterprise | não publicado / sob consulta | asquadz.ai, 05/02/2026 [T] | Preço opaco e dependência de nuvem estrangeira | Marca e conteúdo jurídico internacional |
| **Themis** | 2 — gestão enterprise | não publicado | asquadz.ai, 05/02/2026 [T] | Ausência de air-gap e de trilha de auditoria própria | Foco em departamento jurídico de grande porte |
| **Turivius** | 3 — jurisprudência | não publicado (venda consultiva) | turivius.com; ialocus.com.br, 15/10/2026 [I] | Acervo jurisprudencial próprio não cobre o acervo do cliente | Acervo de jurisprudência como ativo comercial |
| **Looplex** | 2 e 4 — gestão e contratos | R$ 6.000/mês (10 usuários, anual) · R$ 18.000 (30) · R$ 48.000 (100); Ultimate sob medida | looplex.com.br/pt-br/pricing, 10/11/2026 [O] | Cobrança por faixa de usuários e créditos que expiram; inferência no cliente só no plano Ultimate | Empacotamento por valor entregue e créditos de implantação inclusos |
| **netLex** | 4 — contratos | não publicado (enterprise, proposta) | netlex.io/precos → 404, 10/11/2026 [a validar] | CLM em nuvem; acervo contratual no fornecedor | Fluxo de aprovação contratual e integração com assinatura |
| **D4Sign** | adjacente — assinatura | página de planos retornou 404 na consulta de 10/11/2026; **não publicado** | d4sign.com.br/planos, 10/11/2026 [a validar] | Assinatura sem camada de conhecimento sobre o conteúdo assinado | Distribuição e preço de entrada baixo |
| **Deep Legal, Kurier, Finch, Sync, Toogle** | 4 — documental | **não localizado** preço publicado em 10/11/2026 | — [a validar] | Tratar como "sob consulta" até checagem direta | A confirmar — nenhuma afirmação sem fonte |
| **CoCounsel** (Thomson Reuters) | 5 — soberana, no exterior | US$ 340,85 · US$ 882,30 · US$ 1.694,90/mês | haqq.ai, 20/10/2026 [T] | Preço em dólar, dado fora do Brasil, contrato de direito estrangeiro | Marca, acervo Westlaw e configurador de preço transparente |
| **Paxton AI** | 5 — no exterior | US$ 499/usuário/mês ou US$ 2.999/usuário/ano | haqq.ai, 20/10/2026 [T] | Sem operação no Brasil, sem acervo brasileiro, sem air-gap declarado | Preço publicado sem "fale com vendas" |
| **Genie AI** | 1 — no exterior | US$ 75/mês (1 usuário) · US$ 320 (5) · enterprise a partir de US$ 600 | haqq.ai, 20/10/2026 [T] | Fora da jurisdição brasileira; sem português jurídico nativo | Degrau de preço por número de usuários, sem cotas de mensagem |
| **Harvey** | 5 — no exterior | **não publicado** (harvey.ai/pricing → 404); terceiros relatam de US$ 1.200/assento/ano a US$ 1.200–2.000/assento/mês, com divergência de 12× entre fontes e contestação da empresa | bindlegal.com, rev. 06/11/2026 [T] | Inacessível ao mercado brasileiro médio e sem instalação local | Posicionamento de categoria: vende resultado, não modelo |

Duas leituras de preço divergem da base de fatos em unidade, e ficam registradas como **[a validar]**: uma leitura de 14/10/2026 publica Astrea com planos de R$ 209 a R$ 1.249/mês (por escritório, não por usuário) e ADVBox de R$ 220 a R$ 1.800/mês, valores que não são comparáveis à faixa por usuário acima e não a substituem (Fonte: juridicoagil.com, 14/10/2026 [T]).

O padrão que a tabela revela é único e vale mais que qualquer linha: **todo fornecedor enterprise esconde o preço, e o único que publica preço de air-gapped é o que tem menos a perder ao publicá-lo.** Preço publicado é ferramenta de aquisição; preço escondido é ferramenta de negociação. Este produto, por ser instalado e de ticket alto, tem incentivo para o segundo modelo — e isso é uma desvantagem competitiva que precisa ser compensada com transparência em outro lugar: na decomposição do custo total, que já é requisito em R37 do catálogo.

---

## 4. O que atacar

Cada brecha abaixo está escrita como o cliente a enuncia, não como o analista a classifica. É a diferença entre uma objeção que o vendedor responde e uma frase de folheto.

- **"Isso pode ir para fora?"** Nenhum concorrente de autoatendimento responde com arquitetura; responde com política de privacidade. Nós respondemos com air-gap verificável por auditor terceiro, *conforme especificação E4 do requisito R1*, e com a especificação E10 do mesmo requisito, que deixa o cliente executar a suíte de confinamento sem depender da nossa palavra.
- **"De onde saiu essa frase?"** A resposta padrão do mercado é o link para o documento na nuvem do fornecedor. A nossa é citação validada contra o índice do acervo, com bloqueio de citação inexistente, *conforme especificação E2 do requisito R19*.
- **"O que foi enviado para fora semana passada?"** Nenhum concorrente de autoatendimento consegue responder por cliente, por usuário e por processo. Nós respondemos com registro encadeado por hash por envio, *conforme especificação E11 do requisito R4*, e com o caminho único do broker, *conforme especificação E3 do requisito R4*.
- **"Quanto vai custar no mês cheio?"** Modelos por análise e por crédito (Locus.IA, Judit, Looplex) transferem ao cliente o risco de volume. O cliente reconhece isso como imprevisibilidade orçamentária, e departamento jurídico de banco não assina orçamento variável.
- **"Funciona se a internet cair?"** Nenhum SaaS funciona. Instalação local funciona por construção, incluindo atualização de software e de base normativa em ambiente isolado, *conforme especificação E5 do requisito R38* e *conforme especificação E3 do requisito R39*.
- **"E se eu quiser conferir sozinho?"** A verificação independente é especificação nossa, não cortesia comercial. É o único argumento que sobrevive à mesa de segurança da informação.

## 5. O que imitar

Imitar não é elogiar. É reconhecer o que o concorrente faz melhor e decidir, item por item, se copiamos.

- **Preço de entrada baixo, do Jurídico AI e do Juridiq.** Copiar em forma, não em valor: um ambiente de demonstração com acervo sintético que roda antes da compra, *conforme especificação E9 do requisito R1*. O cliente experimenta em minutos sem que ninguém instale nada. Não copiamos o preço; copiamos a ausência de atrito até o primeiro resultado.
- **Acervo próprio como argumento, do Jus IA e do Turivius.** Copiar o conceito e inverter o sujeito: o nosso acervo próprio é o corpus normativo versionado e com estado de vigência (README, seção Corpus normativo). O argumento passa a ser "a lei que citamos está vigente e sabemos desde quando", que é verificável e que nenhum concorrente de autoatendimento entrega.
- **Créditos de implantação inclusos, do Looplex.** Copiar. O plano anual do Looplex embute 36 a 480 créditos de serviço profissional, o que remove a objeção de "quanto custa a mais para começar". Nós temos custo de implantação real (R$ 500–5.000+ é a faixa praticada no mercado, Fonte: asquadz.ai, 05/02/2026 [T]) e precisamos apresentá-lo dentro do pacote, não como fatura separada — ver [06-precificacao-e-escala.md](06-precificacao-e-escala.md).
- **Integração com o sistema de gestão, da categoria 2 inteira.** Copiar por parceria, não por construção: a integração vale mais como canal do que como feature, e é o que transforma o produto de ferramenta paralela em camada dentro do fluxo — ver [08-parcerias.md](08-parcerias.md).
- **UX de primeiro uso, do Astrea e do Jus IA.** Copiar o padrão de primeira sessão com valor visível em menos de cinco minutos. É a vantagem que mais subestimamos, porque instalação local tende a produzir primeira sessão longa.
- **Configurador de preço público, do CoCounsel.** Copiar o hábito, não o número: publicar a lógica de composição do preço, mesmo sem publicar o valor final.

## 6. A âncora de preço do nicho: R$ 1.099,90

Este é o dado mais importante do documento e precisa ser lido duas vezes, porque sustenta duas conclusões opostas e ambas são verdadeiras.

**Como validação.** Existe, hoje, no Brasil, um fornecedor cobrando **R$ 1.099,90 por mês** para rodar IA jurídica no hardware do cliente, exigindo GPU do comprador (Fonte: ialocus.com.br, 12/05/2026, rev. 15/10/2026 [I]). Isso responde à pergunta que todo projeto on-premise enfrenta na primeira reunião — "alguém paga por isso?" — e responde com preço publicado, não com intenção declarada. A demanda por soberania existe e paga aproximadamente **14 vezes** o plano de entrada do Jus IA (R$ 1.099,90 contra R$ 78,90, ambos de 2026) e quase **20 vezes** o plano mais barato do mercado de autoatendimento (R$ 55,92 do Jurídico AI, no anual). Esse múltiplo é o número que a área comercial deve usar; é defensável e tem fonte.

**Como teto.** A mesma oferta estabelece o limite superior do que o mercado aceita pagar por soberania isolada. Nenhum comprador informado paga dez vezes a âncora por uma diferença que ele não consegue ver. Portanto o produto não pode se posicionar como "air-gap"; tem de se posicionar como "air-gap mais acervo governado, citação validada e auditoria". A diferença de preço tem de ser justificada por escopo, nunca por confinamento — porque confinamento o concorrente já vende por R$ 1.099,90.

**O número que falta na comparação.** A âncora é mensalidade de software sobre hardware do cliente, e o hardware não é gratuito: uma RTX 5090 de 32 GB custava **R$ 31.999,99 no Pix** em oferta de 17/09/2026 (Fonte: pcbuilder.com.br [I]). Um cliente que entra nessa oferta gasta, no primeiro ano, R$ 31.999,99 de hardware mais R$ 13.198,80 de assinatura — **R$ 45.198,79** [cálculo próprio, a partir das duas fontes acima]. Toda proposta deste produto deve ser comparada contra esse total e não contra a mensalidade. É a única comparação honesta, e é também a que nos favorece quando o hardware entra no pacote de implantação.

---

## 7. Decisão proposta

**Entramos acima da âncora, com preço por implantação e por assento nomeado, e nunca por consulta ou por análise.** A lógica é a do comprador institucional: ele não compra volume de perguntas, compra a substituição de um risco. Cobrança por consumo reintroduz exatamente a imprevisibilidade que o produto promete eliminar, e alinha o nosso incentivo ao contrário do interesse do cliente — quanto mais ele usa, mais paga, num produto cujo valor cresce com o uso.

Três consequências fecham a decisão. Primeira: não lançamos plano de entrada abaixo de R$ 250/mês. Segunda: a comparação comercial é sempre contra o custo total do primeiro ano, hardware incluído, jamais contra a mensalidade do concorrente. Terceira: a faixa em que entramos fica acima de R$ 1.099,90 e abaixo do piso internacional de IA jurídica enterprise, que é o CoCounsel Essentials a US$ 340,85/mês (Fonte: haqq.ai, 20/10/2026 [T]) — sem conversão, porque a taxa não foi verificada, e com a conversão a ser fixada em [06-precificacao-e-escala.md](06-precificacao-e-escala.md). O valor exato é decisão daquele documento; o que se decide aqui é a posição relativa.

**Alternativa descartada:** lançar um plano de entrada em R$ 49–99/usuário/mês para capturar base e converter depois. Descartada porque, com implantação cobrada a R$ 500–5.000 por cliente no mercado e ciclo de venda on-premise, essa faixa não paga nem o custo de aquisição nem o de suporte — e um cliente que entra pelo preço sai pelo preço.

---

## 8. R49. Inteligência competitiva

**Prioridade:** Importante · **Verticais:** todas

**Racional.** Concorrência, neste mercado, não se acompanha por lista de empresas: acompanha-se por categoria de compra, porque é assim que o cliente decide. O risco real não é perder para um concorrente melhor; é perder para o comportamento gratuito que ninguém colocou na planilha, ou ser surpreendido por um fornecedor de gestão jurídica que liga um botão de IA na base instalada. Sem registro de preço com fonte e data, o posicionamento de preço vira opinião, e a âncora de R$ 1.099,90 — que é simultaneamente teto e prova de demanda — deixa de ser usada como instrumento.

Este requisito não produz análise de mercado bonita. Produz três coisas verificáveis: uma tabela que qualquer sócio pode conferir linha por linha, uma brecha declarada por concorrente em linguagem de cliente, e um número de negócios perdidos que transforma "achismo competitivo" em dado de produto.

**Especificações**

- **E1. Mapa por categoria, não por empresa.** O mapa competitivo é mantido nas seis categorias da seção 2 — autoatendimento, gestão com IA, jurisprudência, documental para contratos, soberana/air-gapped e assistente genérico — e cada concorrente conhecido está classificado em uma delas com data de última revisão. Verificação: nenhum concorrente aparece sem categoria ou em duas categorias simultâneas sem justificativa registrada.
- **E2. Ficha de preço com fonte, data e unidade.** Toda linha de preço registra valor, moeda, unidade de cobrança (usuário, análise, crédito, faixa de usuários), data da leitura e URL da fonte. Preço não publicado é registrado literalmente como "não publicado", com a data da tentativa de verificação. Verificação: auditoria amostral de dez linhas reconstrói cada valor a partir da fonte citada.
- **E3. O concorrente de comportamento é linha de primeira classe.** O assistente genérico de uso pessoal aparece em toda tabela e em todo material de venda como alternativa explícita, com o preço do piso de assinatura e data. Verificação: o roteiro de demonstração nomeia o hábito de copiar e colar e explica o que muda, em até dois minutos.
- **E4. Brecha declarada em linguagem de cliente.** Cada concorrente relevante tem uma desvantagem registrada em uma frase que o cliente reconhece — dado que sai do perímetro, resposta sem citação verificável, ausência de trilha de auditoria, ausência de air-gap, dependência de internet, custo por consulta imprevisível — e cada frase tem a evidência que a sustenta. Verificação: nenhuma brecha é registrada sem evidência; afirmação sobre funcionalidade de concorrente sem fonte é removida.
- **E5. Vantagem a imitar com decisão de cópia.** Cada vantagem competitiva identificada recebe uma de três decisões — copiar, copiar em forma, não copiar — com justificativa e destino. Vantagem sem decisão é vantagem que será redescoberta na próxima reunião. Verificação: nenhuma vantagem listada fica sem uma das três marcações.
- **E6. Âncora de preço monitorada com gatilho de revisão.** A oferta de IA jurídica em hardware do cliente a R$ 1.099,90/mês é monitorada mensalmente, e movimento de preço dessa oferta acima ou abaixo de 20% dispara revisão formal do posicionamento. Verificação: histórico da âncora registrado com data, e revisão disparada dentro de 15 dias do gatilho.
- **E7. Critério objetivo de concorrente relevante.** Concorrente relevante é o que aparece em ao menos uma fração dos negócios perdidos, com a fração definida no encerramento do piloto e registrada aqui antes do primeiro ciclo comercial completo. O critério substitui a intuição de "quem é grande". Verificação: relatório por motivo de perda, com concorrente nomeado, alimentado pelo registro comercial — ver [11-publico-alvo-e-margem.md](11-publico-alvo-e-margem.md).
- **E8. Monitoramento com fonte, cadência e dono.** Cada fonte monitorada tem URL, cadência e responsável nomeado: páginas de preço dos concorrentes mensalmente, publicações setoriais que comparam preços mensalmente, movimentos internacionais trimestralmente, e mudança regulatória que afete a proposta de soberania a cada publicação. Verificação: calendário publicado e registro datado de cada rodada.
- **E9. Da brecha ao backlog.** Toda brecha atacável e toda vantagem marcada como "copiar" tem destino declarado em um de três lugares: item de backlog de produto, item de roteiro de venda ou decisão de não fazer com motivo. Verificação: nenhum item do mapa competitivo termina o trimestre sem destino.
- **E10. Resposta preparada para movimento previsível.** Existem respostas escritas para os quatro movimentos com probabilidade material: guerra de preço do air-gapped, fornecedor de gestão embutindo IA na base instalada, concorrente passando a vender por crédito de forma agressiva, e provedor de nuvem lançando região soberana no Brasil. Cada resposta nomeia o gatilho de reconhecimento, a resposta comercial e o que não faremos. Verificação: simulada uma vez por semestre, com a resposta revisada em ata.

---

## 9. Como os concorrentes devem reagir, e o que temos preparado

**O concorrente de autoatendimento reage com preço.** É a única alavanca que ele tem, porque o produto dele é o mesmo modelo com prompt diferente. Esperado: corte de preço e aumento de cota em poucas semanas. Resposta preparada: não acompanhar. A comparação muda de eixo para custo total do primeiro ano, hardware incluído — a mesma conta da seção 6 — e para o que o produto barato não faz. Concorrente que entra em guerra de preço conosco está saindo do mercado em que é forte.

**O fornecedor de gestão reage com bundling.** É o movimento mais provável e o mais perigoso: Projuris, Legal One, SAJ ADV e Looplex ligam um módulo de IA na base instalada e o cliente percebe que "já tem". Resposta preparada: não competir por feature contra a base instalada; competir por confinamento e por auditoria, que são requisitos de contrato do cliente final e não módulo de software. E antecipar o movimento por parceria — ver [08-parcerias.md](08-parcerias.md).

**O concorrente de air-gapped reage descendo de faixa.** Locus.IA pode reduzir a mensalidade local ou incluir o hardware. Resposta preparada: o gatilho está na especificação E6 do requisito R49; se a âncora cair abaixo de R$ 500, o posicionamento de preço precisa ser refeito e a justificativa migra de soberania para governança de acervo e auditoria — que é onde o escopo é maior e a comparação nos favorece.

**A nuvem reage com região soberana.** AWS, Azure e Google podem anunciar processamento no Brasil com garantia contratual de residência. Isso não é air-gap e a diferença precisa ser explícita em toda proposta: residência de dado é onde o disco está; air-gap é a ausência da rota. A especificação E4 do requisito R1 torna a diferença verificável, e a especificação E2 do mesmo requisito impede a dependência de serviço externo por desenho.

---

## 10. Monitoramento contínuo

O monitoramento é barato e precisa ser mecânico, porque time enxuto — ver [07-sustentacao.md](07-sustentacao.md) — não sustenta análise competitiva artesanal.

| Fonte | O que acompanha | Cadência | Dono |
|---|---|---|---|
| Páginas de preço dos concorrentes brasileiros (juridico.ai, ia.jusbrasil.com.br, ialocus.com.br, looplex.com.br) | preço, cota, empacotamento | mensal | pré-vendas |
| Páginas de preço internacionais (CoCounsel, Paxton, Genie, Harvey) | piso internacional, conversão, movimento de categoria | trimestral | responsável de produto |
| Publicações que comparam preços do setor (haqq.ai, asquadz.ai, jurídico ágil) | leitura de terceiro, inclusive divergência entre fontes | mensal | pré-vendas |
| ialocus.com.br/blog | concorrente que publica comparação de preços de terceiros — fonte hostil e útil | mensal | pré-vendas |
| Registro comercial de negócios perdidos | concorrente nomeado, motivo, estágio | contínuo, revisão mensal | direção comercial |
| Câmara dos Deputados, PL 2338/2023; CNJ | mudança regulatória que altere a proposta de soberania | a cada publicação | responsável de produto |
| OAB/CFOAB e CFC | tamanho e composição do universo | semestral | responsável de produto |

O produto do monitoramento não é relatório. É uma linha no registro de mudanças, com data, e um destino na especificação E9 do requisito R49. Relatório competitivo trimestral que ninguém lê é o modo mais comum de gastar dinheiro fingindo que se acompanha o mercado.

---

## Fontes

- Base de fatos comum deste conjunto: [12-fontes-e-base-de-fatos.md](12-fontes-e-base-de-fatos.md), pesquisa de 10/11/2026 (tabelas de concorrentes brasileiros, internacionais, hardware e câmbio não verificado).
- Looplex — https://www.looplex.com.br/pt-br/pricing — leitura 10/11/2026.
- Looplex e netLex — https://juridicoagil.com/blog/ias-juridicas-brasileiras — leitura 14/10/2026 (também: divergência de unidade em Astrea e ADVBox, registrada como [a validar]).
- Locus.IA, Judit, Turivius, ChatADV — https://ialocus.com.br — 12/05/2026, rev. 15/10/2026.
- Preços de gestão jurídica (SAJ ADV, Astrea, ADVBox, EasyJur, Juridiq, Projuris, Legal One, Themis) e custo de implantação — https://asquadz.ai/blog — 05/02/2026.
- Preços internacionais (CoCounsel, Paxton, Genie, Harvey) e piso de assinatura de uso pessoal — https://haqq.ai — 20/10/2026.
- Harvey, estimativas de terceiros e contestação — https://bindlegal.com — rev. 06/11/2026.
- Jurídico AI — https://juridico.ai/planos — out–nov/2026.
- Jus IA — https://ia.jusbrasil.com.br/planos — 2026.
- Turivius — https://turivius.com — sem página de preços na consulta.
- netLex e D4Sign — páginas de preço retornaram 404 em 10/11/2026.
- RTX 5090 a R$ 31.999,99 — https://pcbuilder.com.br — oferta de 17/09/2026.
- OAB — https://www.oab.org.br/institucionalconselhofederal/quadroadvogados — consulta 10/11/2026.
- CFC — https://www3.cfc.org.br e https://cfc.org.br/noticias — consulta 10/11/2026.

## O que derruba esta recomendação

1. **Se a âncora cair abaixo de R$ 500/mês.** O argumento inteiro repousa em existir demanda disposta a pagar ~14× o autoatendimento por soberania. Preço local abaixo da metade destrói o teto e obriga a competir por escopo, não por confinamento — o que muda o produto, não só a proposta.
2. **Se o piloto mostrar que o cliente não paga por auditoria e citação.** Se, em negócios reais, o motivo de perda for sempre preço e nunca risco, a tese de governança está errada e o produto precisa de um plano de entrada que hoje está descartado na seção 7.
3. **Se o critério da especificação E7 do requisito R49 não fechar.** Sem uma fração de negócios perdidos apurada no piloto, toda a priorização competitiva volta a ser opinião, e o documento perde a função que justifica existir.
4. **Se um fornecedor de gestão embutir IA air-gapped na base instalada sem cobrar por isso.** O bundling com distribuição instalada é o cenário que anula a diferenciação de canal e nos empurra para a venda direta contra incumbente.
5. **Se o preço de hardware com GPU despencar.** A comparação de custo total do primeiro ano, que é o eixo de nossa defesa comercial, depende de o hardware ser um custo material. Hardware barato reduz o custo de entrada do concorrente de air-gapped e derruba a âncora junto.
