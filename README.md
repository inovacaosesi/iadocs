# iadocs

Documentação de requisitos para uma solução de IA local dedicada a documentos, com consulta externa auditada.

O repositório contém apenas especificação. Não há código de produto aqui.

## O problema

Escritórios de advocacia, áreas de compliance, departamentos contábeis e fiscais e a administração pública acumulam acervos que não podem sair do perímetro. Ao mesmo tempo, essas equipes já usam assistentes de IA no dia a dia, com frequência colando trechos de documentos sigilosos em ferramentas de consumo.

A conta é ruim nos dois sentidos. A proibição sem alternativa empurra o uso para fora do controle. A liberação sem controle expõe, de uma vez, sigilo profissional, segredo de justiça, sigilo fiscal, sigilo bancário e dados pessoais.

## A ideia

Processar o acervo inteiro dentro do ambiente do cliente. Quando o modelo local não der conta, e apenas quando o usuário pedir de forma expressa, permitir uma consulta a provedor externo homologado, com o conteúdo visível antes do envio, minimizado, autorizado e registrado de forma reconstruível.

Em uma frase: é possível trabalhar com o acervo sem expor o acervo, e quando algo sai, fica registrado.

## Como os documentos se organizam

| Documento | Conteúdo | Quando usar |
|---|---|---|
| [README.md](README.md) | Este arquivo | Ponto de entrada |
| [04-mvp-matriz.md](04-mvp-matriz.md) | Matriz do MVP: 17 requisitos e 90 especificações | Fase de discovery |
| [03-registro-decisoes.md](03-registro-decisoes.md) | Quatro decisões estruturantes, como hipóteses de trabalho | Insumo de discussão |
| [02-matriz-decisao-egresso.md](02-matriz-decisao-egresso.md) | Comportamento da consulta externa por classe de conteúdo | Ao desenhar o egresso |
| [01-catalogo-requisitos.md](01-catalogo-requisitos.md) | Catálogo completo: 40 requisitos e 349 especificações | Fases 2 e 3 |

O catálogo completo não é escopo. Ele existe para que nada importante seja esquecido quando o MVP crescer. Para o trabalho do dia a dia, use a matriz de MVP.

## Convenção de indexação

Requisitos são numerados como **R1, R2, ..., Rn**. As especificações de cada requisito são numeradas dentro dele como **E1, E2, ..., En**, então uma especificação só é identificável junto com o requisito que a contém.

Referências entre documentos diferentes são escritas por extenso, no formato: conforme especificação E4 do requisito R38.

Prioridade segue MoSCoW adaptado: Essencial, Importante, Desejável e Futuro. Na matriz de MVP há ainda três marcações: sem marca para o que está no escopo, **[a validar]** para o que depende de informação que ainda não existe, e **[Fase 2]** para o que está registrado e fora do escopo.

## Estado atual

Fase de discovery. Nenhum requisito aqui é compromisso contratual. As metas numéricas que aparecem nos documentos servem para dar concretude à conversa e serão recalibradas com dados reais durante o piloto.

O que já está definido como direção:

- Modo air-gapped integral como padrão de instalação e de contrato.
- Consulta externa como exceção governada, nunca como modo de operação.
- Citação obrigatória e validada contra o acervo em toda resposta.
- Nenhum envio automático para fora: sem fallback silencioso.
- Separação de acervo por cliente, verificada por teste.

## Escopo do MVP

Dezessete requisitos, agrupados em cinco frentes:

1. **Proteção do acervo**: confidencialidade por padrão, acesso e permissões, segurança e isolamento.
2. **Conhecimento**: ingestão, OCR, busca, resposta com citação.
3. **Controle da saída**: consulta externa auditada, registro e auditoria.
4. **Motor**: modelo local, qualidade mínima, infraestrutura.
5. **Operação**: interface, conformidade básica, modos de implantação, caso de uso piloto, atualização do corpus normativo.

Fora do MVP, e registrado no catálogo para as fases seguintes: classificação documental, extração estruturada, orquestração de agentes, integrações com sistemas processuais e com ERP, observabilidade, governança de IA e avaliação contínua.

## Corpus normativo

O requisito R17 prevê sincronização periódica com o repositório público [ctresb/leis](https://github.com/ctresb/leis), que mantém textos de normas brasileiras em markdown, com cabeçalho de metadados e recibos de integridade.

A automação é de sincronização e indexação, não de treinamento de modelo. O ganho vem da recuperação: a norma passa a ser encontrada e citada porque está no índice.

Antes de exibir citação de lei com confiança, é preciso verificar se o texto da fonte corresponde à redação vigente ou à redação original. Um corpus amplo com texto desatualizado é pior que nenhum corpus, porque produz resposta errada com aparência de correta.

## Verticais consideradas

Jurídico, compliance, administrativo e público, contábil e fiscal. Secundariamente: trabalhista e RH, saúde, seguros, engenharia e imobiliário.

## Licença

A definir.
