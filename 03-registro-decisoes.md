# Registro de Decisões: D1 a D4

**Versão:** 1.1 · **Status:** hipóteses de trabalho, não política fechada.

> Estamos em discovery. As decisões abaixo servem para dar concretude à conversa e evitar que o debate fique no abstrato. Os números (90 dias, 30 consultas, dois provedores) são pontos de partida plausíveis, não compromissos: serão recalibrados com dado real no piloto. Leia como "esta é a direção, sujeita a ajuste".

**Referência:** [04-mvp-matriz.md](04-mvp-matriz.md) · [01-catalogo-requisitos.md](01-catalogo-requisitos.md) · [02-matriz-decisao-egresso.md](02-matriz-decisao-egresso.md)

Cada decisão abaixo tem o mesmo formato: a pergunta, as opções que estavam na mesa, a decisão, por que ela venceu, o que muda no catálogo e qual evidência faria revertê-la. Uma decisão sem critério de reversão não é decisão, é inércia.

---

## D1: O egresso é exceção governada ou modo de operação?

**Status:** Decidida.

### Opções consideradas

| Opção | O que significa | Risco |
|---|---|---|
| **A. Exceção governada** | Egresso desligado por padrão; habilitado por cliente, com escopo mínimo, prazo e cota baixa | Fricção; risco de contorno informal |
| **B. Modo de operação** | Egresso habilitado por política para perfis e tarefas definidos | Controle vira formalidade; exposição cresce sem percepção |
| **C. Vedado** | Nunca | Perde o ganho de qualidade onde ele é decisivo |

### Decisão

**Opção A: exceção governada, com prazo e revisão obrigatória.**

Parâmetros que passam a valer como padrão de fábrica e de contrato:

- **Modo padrão:** Modo A (air-gapped integral) é o modo contratual e de instalação, *conforme especificação E1 do requisito R38*.
- **Escopo da habilitação:** por cliente. Nunca global, nunca por vertical inteira, nunca por padrão de instalação.
- **Prazo:** habilitação inicial de **90 dias**, renovável por decisão registrada, com revisão contratual obrigatória em **12 meses**.
- **Catálogo de destinos:** no máximo **dois provedores homologados** no primeiro ciclo, *conforme especificação E2 do requisito R4*. Dois é o teto por razão prática: cada destino exige DPA próprio, avaliação de retenção, revisão de subprocessadores e teste de contrato. Catálogo grande é catálogo mal auditado.
- **Cotas iniciais por classe de payload**, *conforme matriz de decisão de egresso*:

| Classe | Cota por usuário/mês | Aprovação |
|---|---|---|
| C0: sem conteúdo do cliente | sem cota de governança; só limite de custo | nenhuma |
| C1: conteúdo público | sem cota de governança; só limite de custo | nenhuma |
| C2: conteúdo interno | 100 consultas | política prévia por cliente |
| C3: conteúdo restrito | 30 consultas e 150 mil caracteres | política prévia + alçada |
| C4: conteúdo sigiloso | 5 consultas | individual, quatro olhos |

- **Gatilho de revisão:** ao final de dois ciclos trimestrais, decidir com dado, não com impressão, se o regime muda. O dado é o de *especificação E8 do requisito R22*: ganho real medido no conjunto dourado do cliente, comparando execução com e sem egresso.

### Por que esta opção

Modo de operação (opção B) parece mais amigável e é o erro clássico de projetos assim: o egresso começa como exceção, ganha um atalho por conveniência, e em doze meses ninguém sabe mais qual percentual do acervo saiu. A exceção governada mantém a decisão no nível de quem responde pelo risco e força a conversa trimestral sobre custo e benefício.

A opção C perde porque o ganho de qualidade em raciocínio jurídico e fiscal complexo é real e mensurável. Renunciar a ele por princípio, sem medir, é tão irracional quanto expor tudo por conveniência.

### Consequência prática

Todo cliente começa em Modo A. Habilitar egresso é um projeto com data de início, data de fim e dono nomeado, não uma caixa de seleção em tela de configuração. Ao término do prazo sem renovação, o broker volta ao estado negado automaticamente, sem depender de alguém lembrar.

### Critério de reversão

Se, ao final dos dois ciclos, o ganho medido no conjunto dourado for **inferior a 3 pontos percentuais** em todas as tarefas avaliadas, o egresso não se paga e deve ser descontinuado como recurso, mantendo-se apenas o desenho técnico documentado. Se o ganho for **superior a 15 pontos percentuais** em tarefas de alto valor e a exposição média ficar abaixo de 20% do acervo consultado, reabrir a discussão sobre modo de operação com controles reforçados.

---

## D2: Qual o teto de qualidade aceitável para justificar não usar a nuvem?

**Status:** Decidida.

### O problema da pergunta

"Qual a perda de qualidade aceitável" medida de forma global é uma pergunta mal formulada, e respondê-la assim produz um número que ninguém consegue defender. O custo do erro não é uniforme: errar um CNPJ numa nota fiscal é catástrofe silenciosa; errar o tom de um resumo é irrelevante. A decisão precisa ser **por tipo de tarefa**, com portões separados.

### Decisão

Adotar cinco portões de qualidade, *conforme especificação E1 do requisito R19*. Portão não atingido significa que **a tarefa não é oferecida em Modo A.** o produto declara a limitação em vez de entregar resultado ruim com aparência de bom.

| Portão | Tarefa | Meta | Consequência da falha |
|---|---|---|---|
| **Q1. Integridade de citação** | Toda citação produzida | **100%** das citações resolvem para trecho existente no acervo | Resposta bloqueada |
| **Q2. Extração validável** | CNPJ, CPF, valores, datas, número de processo | **≥ 99,5%**; **100%** em campos com validação algorítmica | Campo vai para revisão humana obrigatória |
| **Q3. Classificação documental** | Tipo e sensibilidade | **≥ 95%** top-1 e **≥ 99%** top-3 | Fila de revisão; não aplica política automática |
| **Q4. Fidelidade ao documento** | Afirmação factual sobre o acervo | **≥ 95%**; afirmação sem âncora = **0** | Aviso de baixa confiança e revisão integral |
| **Q5. Abstenção correta** | Pergunta fora da cobertura da base | **≥ 85%** de abstenção correta; **≤ 2%** de erro confiante | Recalibração antes de liberar a vertical |

A distinção entre Q1/Q2 e Q4/Q5 é o núcleo da decisão: **erro silencioso e confiante é o único erro intolerável**. Erro com aviso é custo operacional; erro sem aviso é passivo jurídico.

### Defasagem tolerada em relação à referência em nuvem

Medida no acervo do próprio cliente, com o mesmo conjunto dourado e o mesmo modelo de referência, nunca em benchmark genérico.

| Tipo de tarefa | Defasagem máxima | Condição |
|---|---|---|
| Extração e classificação | **≤ 5 pontos percentuais** | Sem condição adicional |
| Recuperação e resumo | **≤ 10 pontos percentuais** | Citação obrigatória |
| Raciocínio e redação | **≤ 20 pontos percentuais** | Revisão humana obrigatória e rotulagem de origem |

O limite de 20 pontos na redação não é complacência: é o reconhecimento de que, nessa tarefa, o ato com efeito jurídico já exige revisão humana por *especificação E4 do requisito R8*. Se o texto gerado for ponto de partida e não peça final, a defasagem tem custo menor.

**Meta de convergência:** reduzir a defasagem de raciocínio e redação para **≤ 10 pontos percentuais em 18 meses**, por meio de R23 (adaptação ao domínio) e R22 (avaliação contínua). Defasagem que não converge é defasagem que cresce, porque os modelos de referência continuam evoluindo.

### Regra de medição

O modelo de referência precisa ser **declarado e versionado** no relatório. Comparar com "o melhor modelo disponível" é comparar com um alvo móvel e produzir número que não se reproduz no trimestre seguinte. O relatório registra: versão do modelo local, versão do modelo de referência, data, conjunto dourado utilizado e tamanho da amostra.

### Critério de reversão

Se um portão não for atingido em duas avaliações consecutivas da mesma vertical, a tarefa correspondente sai do escopo de Modo A e passa a exigir egresso autorizado ou execução puramente humana. Não existe terceira via: tarefa que não passa no portão e continua disponível é dívida de risco acumulada.

---

## D3: Hardware próprio, nuvem privada ou híbrido?

**Status:** Decidida, com o valor de corte a confirmar por cotação real.

### Decisão

**Arquitetura em três faixas, com regra de passagem objetiva entre elas.**

| Faixa | Volume de referência | Implantação | Razão |
|---|---|---|---|
| **Piloto** | até ~50 mil páginas; até 15 usuários | Nuvem privada dedicada na conta do cliente, região Brasil, chave gerenciada pelo cliente | Tempo até valor de 4 a 6 semanas; sem capex; valida com acervo real |
| **Produção departamental** | ~50 mil a 2 milhões de páginas; 15 a 100 usuários | Servidor com GPU on-premise | A partir desta faixa, a depreciação do servidor fica abaixo do custo mensal de GPU em nuvem |
| **Produção com requisito de air-gap** | qualquer volume | Cluster on-premise obrigatório | Air-gap integral não é verificável em nuvem de terceiro, ainda que privada |

**Regra de passagem, sem arbítrio:** a migração de nuvem privada para on-premise é disparada quando o custo mensal de GPU e armazenamento em nuvem projetado para 24 meses exceder o custo total de aquisição do servidor equivalente. O cálculo usa cotação real, não estimativa de tabela.

### Ponto cego que a decisão precisa encarar

Hardware de GPU **não tem ciclo de depreciação de cinco anos** como servidor tradicional. O ciclo útil para acompanhar modelos abertos competitivos é de **três anos**, porque a cada geração de modelo as exigências de memória e de capacidade computacional sobem. Isso encurta o payback e muda a conta: comparar capex de GPU com opex de API usando depreciação de cinco anos superestima a vantagem do on-premise em quase 40%. A planilha de *especificação E1 do requisito R37* deve usar três anos.

### Por que nuvem privada não contradiz a premissa

Contradiz se for a nuvem do fornecedor. Não contradiz quando é a conta do cliente, na jurisdição do cliente, com chave do cliente e cláusula de não acesso pelo provedor de infraestrutura. O que a premissa proíbe é o dado sair do controle do cliente, não é o formato do hardware. Ainda assim, o Modo C fica como exceção comercial, não como padrão, *conforme especificação E3 do requisito R38*.

### Consequência contratual

Independentemente da faixa, o contrato precisa garantir a saída: exportação integral do acervo, do índice e do histórico em formato aberto, *conforme especificação E4 do requisito R16*, e *conforme especificação E8 do requisito R38*. Cliente que não consegue sair não tem soberania, tem refém.

### Critério de reversão

Se a cotação real mostrar que o servidor on-premise equivalente custa mais que 36 meses de nuvem privada no volume de referência da faixa departamental, a faixa colapsa: piloto e departamento passam a ser ambos em nuvem privada, e on-premise fica restrito ao requisito de air-gap.

---

## D4: Quem aprova o egresso?

**Status:** Decidida.

### Opções consideradas

| Modelo | Vantagem | Problema |
|---|---|---|
| DPO aprova tudo | Concentra o olhar de privacidade | Vira gargalo; DPO não responde pelo cliente |
| Sócio responsável aprova tudo | Alinhado ao dever de sigilo | Fricção alta em volume |
| Aprovação automática por política | Fluidez | Controle formal, sem julgamento no caso concreto |
| Compliance central aprova | Padronização | Distância do caso; incentivo errado |

### Decisão

**Aprovação em camadas por classe, com papéis separados por natureza da decisão.**

| Classe | Quem decide | Momento |
|---|---|---|
| C0, C1 | ninguém; usuário habilitado ao Modo B | não se aplica |
| C2 | política prévia por cliente, aprovada pelo **responsável da área** | uma vez, na abertura do cliente |
| C3 | política prévia por cliente aprovada pelo **sócio responsável**, com alçada nominal | uma vez, na abertura do cliente |
| C4 | **sócio responsável pelo caso**, com quatro olhos por consulta | a cada consulta |

**Papéis que não se confundem:**

- **Sócio responsável** decide sobre o caso concreto. É quem carrega o dever de sigilo e responde disciplinarmente por ele. A decisão de expor conteúdo de cliente fica com quem responde pelo cliente.
- **DPO** define a política, detém **poder de veto** sobre qualquer habilitação ou consulta, revoga autorização a qualquer tempo e audita. Ele **não aprova caso a caso.** se aprovasse, seria gargalo e perderia a distância necessária para auditar.
- **Segurança da informação** opera o broker e o interruptor de emergência, mas não concede alçada de negócio.
- **Aprovador nunca aprova a própria solicitação**, *conforme especificação E4 do requisito R7*.

### O problema real: prazo, plantão e fim de semana

O controle que só funciona em horário comercial será contornado na primeira urgência real. A decisão incorpora três mecanismos que existem precisamente para isso:

- **Substituto nomeado na abertura do caso.** Todo caso com acesso a C4 tem no mínimo **dois aprovadores** designados. Ausência de um não paralisa.
- **Prazo de resposta de 4 horas úteis, com expiração negativa.** Silêncio não aprova. Consulta não respondida expira como negada, com registro de que houve solicitação e não houve decisão, o que é diferente de ter sido negada.
- **Trilha de urgência limitada a C3.** Em situação de prazo processual iminente, o plantão de segurança da informação pode aprovar C3 temporariamente, com justificativa e revisão posterior obrigatória pelo DPO em até 24 horas. **C4 nunca tem trilha de urgência.** Se o caso exige expor conteúdo sigiloso em prazo de horas, a resposta correta é revisão humana, não egresso.

### Consequência sobre a matriz de egresso

A linha de aprovação da [matriz de decisão](02-matriz-decisao-egresso.md) passa a ter dono nomeado em cada classe. O item em aberto daquela matriz sobre aprovador de plantão fica resolvido por esta decisão: existe, mas só alcança C3.

### Critério de reversão

Se, em dois trimestres, a taxa de expiração negativa de C4 ultrapassar **10%** das solicitações, o desenho está gerando paralisia e não proteção. A resposta então não é afrouxar o quatro olhos, e sim revisar a lista de aprovadores substitutos e o desenho de política prévia do cliente.

---

## Resumo das decisões

| ID | Decisão em uma linha |
|---|---|
| **D1** | Egresso é exceção governada por cliente, com prazo de 90 dias, no máximo dois provedores e cotas por classe |
| **D2** | Qualidade medida por cinco portões por tarefa; tarefa que não passa no portão não é oferecida em Modo A |
| **D3** | Nuvem privada para piloto, on-premise para departamento, on-premise obrigatório para air-gap; depreciação em três anos |
| **D4** | Sócio decide o caso, DPO define política e veta, aprovador nunca aprova a própria solicitação, C4 sem trilha de urgência |

## O que permanece aberto

D5 a D10 seguem na seção 12 do catálogo. Os dois que bloqueiam trabalho concreto:

- **D5** (uso de acervo de cliente para ajuste de modelo) trava a implementação de *especificação E3 do requisito R23*.
- **D7** (quem é controlador no egresso) trava a redação de *especificação E17 do requisito R4* e precisa de decisão jurídica antes do primeiro contrato com provedor.
