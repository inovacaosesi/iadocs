# Matriz de Decisão de Egresso: Operacionalização de R4 e R5

Documento de apoio ao debate. Traduz os requisitos R4 (controle de egresso) e R5 (solicitação expressa) em decisões concretas que uma equipe de produto, jurídico e segurança consegue revisar em uma reunião.

> **Fora do escopo do MVP.** No MVP, a consulta externa se resume a R2 de [04-mvp-matriz.md](04-mvp-matriz.md): negada por padrão, com pré-visualização, ponto único de saída e registro. Esta matriz detalhada serve para a Fase 2, quando o egresso for desenhado com o cliente. O checklist da seção 4 vale como roteiro de teste para aquele momento.

---

## 1. Classificação do payload antes da decisão

O gateway classifica o payload. **O usuário não autodeclara** a classe: ele pode apenas reduzir o escopo. Isso evita o erro mais comum em produtos comerciais: deixar o usuário declarar "isto não é sensível".

| Classe | Definição | Exemplo |
|---|---|---|
| **C0. Sem conteúdo do cliente** | Pergunta genérica, nenhum trecho documental, nenhum identificador | "O que é cláusula penal?" |
| **C1. Conteúdo público** | Trecho de documento já público, ou norma/jurisprudência publicada | Trecho de acórdão publicado, texto de lei |
| **C2. Conteúdo interno** | Documento interno sem dado pessoal relevante e sem sigilo legal | Política interna de despesas, modelo de peça do escritório |
| **C3. Conteúdo restrito** | Contém dado pessoal, dado de cliente ou informação contratual | Contrato com partes identificadas, proposta comercial |
| **C4. Conteúdo sigiloso** | Sigilo legal: segredo de justiça, sigilo fiscal, bancário, prontuário, informação privilegiada, NDA de due diligence | Peça em segredo de justiça, extrato bancário, prontuário |

---

## 2. Matriz de controles por classe

Cada coluna corresponde a uma especificação de R4 ou R5, indicada no cabeçalho.

| Controle | C0 | C1 | C2 | C3 | C4 |
|---|---|---|---|---|---|
| **E1** Negação por padrão | permitido após habilitação do modo B | permitido após habilitação | exige política de cliente | exige política de cliente | bloqueado por padrão |
| **E5** Pré-visualização do payload | resumo | integral | integral | integral | integral, com destaque do que é sensível |
| **E6** Redação automática | não aplicável | não aplicável | metadados removidos | PII/PHI mascarada, metadados removidos | PII/PHI mascarada + pseudonimização de partes, quando a finalidade permitir |
| **E7** Segunda aprovação | não | não | não | conforme política do cliente | **obrigatória**, por ator com alçada |
| **E8** Justificativa vinculada | não exigida | finalidade | finalidade + cliente | finalidade + cliente + processo/projeto | finalidade + cliente + processo + base legal do compartilhamento |
| **E9** Cota | alta | alta | média | média | baixa, com alerta em volume |
| **E10** Janela de validade | por sessão | por sessão | por processo | por processo | por consulta individual |
| **E11** Registro imutável | sim | sim | sim | sim | sim, com retenção estendida |
| **E12** Marcação do derivado | sim | sim | sim | sim | sim, e derivado não indexado automaticamente |
| **E15** Nível de autorização | 1 | 1 | 2 | 2 | 3 + quatro olhos |
| **R5/E4** Anuência do cliente | não | não | conforme contrato | conforme contrato | **obrigatória**, registrada |

**Níveis de autorização**
1. Usuário habilitado ao modo B.
2. Usuário com alçada de egresso para o cliente.
3. Usuário com alçada + aprovador com alçada para conteúdo sigiloso + registro de anuência do cliente.

---

## 3. Fluxo de decisão

```
Usuário solicita consulta externa
        │
        ▼
[1] Modo B está habilitado?  ── não ──► consulta negada, sem oferta de alternativa
        │ sim
        ▼
[2] Gateway classifica o payload (C0..C4)
        │
        ▼
[3] Destino está no catálogo homologado para esta classe?
        │ não ──► negado, registro do motivo
        │ sim
        ▼
[4] Redação e minimização aplicadas
        │
        ▼
[5] Pré-visualização exibida ao usuário  ── sem confirmação ──► cancelado
        │
        ▼
[6] Exige segunda aprovação (C4, ou C3 por política)?
        │ sim ──► aguarda aprovador ── negado/expirado ──► cancelado
        │ não
        ▼
[7] Cotas e limites verificados  ── excedido ──► bloqueio com alerta
        │ ok
        ▼
[8] Envio pelo broker, com registro encadeado por hash
        │
        ▼
[9] Resposta recebida e marcada como proveniência externa (R4/E12)
        │
        ▼
[10] Derivado armazenado em coleção separada, sujeito a curadoria (R4/E13)
```

Regra de ouro: **nenhuma etapa é pulada por configuração**. Configuração altera limiares e quem aprova, não a existência da etapa.

---

## 4. Checklist de verificação do controle

Testes que devem passar antes de o Modo B ser habilitado em produção. Cada item é executável e tem resultado binário.

- [ ] Chamada direta ao provedor a partir de script, notebook ou contêiner interno é bloqueada pela camada de rede, não apenas pela aplicação.
- [ ] Modelo de linguagem local não aciona endpoint externo em nenhuma condição, inclusive em erro e em carregamento inicial.
- [ ] Payload exibido na pré-visualização é byte a byte idêntico ao transmitido (verificável por hash).
- [ ] Remoção do campo de justificativa impede o envio.
- [ ] Pagamento por modelo externo não ocorre sem registro de aprovação correspondente.
- [ ] Prompt injection que instrua o agente a "enviar o documento para fora" não produz chamada externa.
- [ ] Imagem markdown ou link gerado na resposta não dispara requisição do cliente no momento da exibição.
- [ ] Exfiltração por consulta DNS é bloqueada no modo A.
- [ ] Interruptor de emergência (R4/E14) corta o egresso em menos de 30 segundos.
- [ ] Revogação de autorização vigente (R5/E6) impede o envio seguinte.
- [ ] Desligamento de usuário no diretório corporativo invalida sessão e alçada em menos de 5 minutos.
- [ ] Acervo de tenant A não é recuperável por busca semântica autenticada como tenant B.
- [ ] Log de egresso não pode ser alterado nem apagado por administrador do sistema.
- [ ] Resposta externa não aparece em busca do acervo antes de curadoria.
- [ ] Exportação de documento contendo trecho de origem externa carrega a marcação de proveniência.

---

## 5. Perguntas que a matriz não resolve e precisam de decisão

1. **C3 por padrão exige política de cliente ou autorização por consulta?** A primeira opção destrava o uso; a segunda protege mais e gera fricção. Depende do apetite de risco de cada escritório.
2. ~~**Quem é o aprovador de C4 em plantão, fim de semana e prazo?**~~ **Resolvido pela decisão D4:** todo caso com acesso a C4 tem no mínimo dois aprovadores designados na abertura; a alçada expira em 4 horas úteis com resultado negativo por omissão; a trilha de urgência do plantão de segurança da informação alcança C3, nunca C4. Ver [03-registro-decisoes.md](03-registro-decisoes.md).
3. **Pseudonimização reversível conta como anonimização para fins da LGPD?** Não conta, e o contrato com o provedor precisa refletir isso. Decisão jurídica, não técnica.
4. **O que acontece com a resposta externa quando o cliente revoga a anuência?** Precisa de regra de descarte retroativo do derivado, que hoje não está especificada em nenhum requisito. Candidato a especificação adicional em R16.
5. **Cota é por usuário ou por cliente?** Por usuário controla comportamento individual; por cliente controla exposição contratual. Provavelmente as duas, com finalidades diferentes.
