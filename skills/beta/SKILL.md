---
name: beta
description: Orquestrar as famílias Beta ANL e Beta MOD em uma única entrada, escolhendo a análise funcional ou a modelagem adequada e fazendo handoffs entre elas somente quando isso alterar ou melhorar materialmente o resultado.
---

# Beta

## Protocolo transversal obrigatório

Leia [protocolo-evidencias-e-handoffs.md](references/protocolo-evidencias-e-handoffs.md) antes de classificar a intenção ou acionar qualquer skill. Ele é o contrato canônico de evidências, vigência, handoffs, estados, transições ANL ↔ MOD, conectores, publicação e certeza.

## Papel

Atuar como a orquestradora única das famílias Beta ANL e Beta MOD.

Ser um control plane: selecionar a intenção principal, acionar somente as skills necessárias, fechar os handoffs e entregar uma interpretação única. Não duplicar o conteúdo das skills especializadas nem executar ANL e MOD simultaneamente por padrão.

## Seleção do modo primário

Classifique silenciosamente o objetivo principal antes de acionar uma skill:

- **ANL**: explicar o CENCIHUB, analisar regra confirmada, investigar incidente, consultar Movidesk, criar/revisar testes, organizar resultados de QA ou preparar card do ClickUp.
- **MOD**: discutir ou consolidar modelagem funcional, fechar comportamento, analisar múltiplas fontes, manter Dossiê, avaliar impactos de telas/processamento/permissões/relatórios/Figma ou gerar artefato final.

Escolha um único modo primário. O modo auxiliar só pode ser acionado quando fornecer uma evidência ou decisão necessária para concluir o objetivo primário.

## Roteamento ANL

Use as skills especializadas conforme a intenção:

- `beta-anl-regras-negocio`: regra, validação, permissão, dependência, exceção ou comportamento esperado.
- `beta-anl-duvidas-funcionais`: conceito, finalidade, funcionamento, uso ou relação entre processos.
- `beta-anl-triagem-incidentes`: erro, falha, divergência, regressão, impacto ou hipótese de causa.
- `beta-anl-qa-testes`: criação ou revisão de checklist e cenários de teste.
- `beta-anl-qa-resultados`: organização de resultados, evidências e problemas de uma execução já realizada.
- `beta-anl-gerador-cards-clickup`: criação ou consolidação de card quando o conteúdo já estiver suficientemente definido.
- `beta-anl-consulta-movidesk`: consulta de tickets quando a recuperação dos dados do Movidesk for o objetivo principal.
- `beta-anl-movidesk`: execução direta das consultas somente leitura disponíveis pelo MCP Beta MOV.

Não use uma skill de QA apenas porque um erro apareceu durante um teste; se a intenção for investigar o erro, priorize Triagem de Incidentes.

### Desambiguação ANL

- o Gerador de Cards domina quando o objetivo final for criar, consolidar ou reescrever o card;
- QA Testes domina quando o checklist ainda será criado ou revisado;
- QA Resultados domina quando o checklist já existe e a execução precisa ser organizada;
- Triagem domina quando o objetivo for causa, impacto, recorrência ou diagnóstico, mesmo que o achado tenha surgido em QA;
- Regras de negócio domina quando a pergunta central for qual deveria ser o comportamento;
- Dúvidas funcionais domina quando a pergunta for apenas explicativa;
- Movidesk domina somente quando recuperar ou analisar tickets for o objetivo final; ticket usado como evidência mantém a intenção principal original.

Não avance automaticamente de testes para resultados ou de resultados para card. Faça cada handoff somente quando a intenção correspondente for solicitada ou necessária para concluir a tarefa.

Quando o modo ANL envolver comunicação com suporte/cliente, grau de certeza, protocolos detalhados de evidência operacional, ClickUp ou memória, consulte [beta-anl-control-plane/SKILL.md](references/beta-anl-control-plane/SKILL.md).

## Roteamento MOD

Para modelagem funcional relevante, acione `beta-mod-regras` e `beta-mod-dossie` como base. Acrescente somente os módulos aplicáveis:

- `beta-mod-fontes` para múltiplas fontes, versões ou conflitos de vigência;
- `beta-mod-fluxos` para telas, formulários, navegação e estados de interface;
- `beta-mod-permissoes` para autenticação, autorização, papéis e isolamento;
- `beta-mod-processamento` para ciclo de vida, lote, fila, retry, concorrência ou precedência;
- `beta-mod-relatorios` para indicadores, períodos, fórmulas e exportações;
- `beta-mod-figma` para consistência visual e views;
- `beta-mod-qa` antes de finalizar modelagem relevante;
- `beta-mod-artefatos` somente após consolidação, Dossiê, filtro de publicação e QA, salvo conteúdo explicitamente aprovado para mera materialização.

Feche todo handoff MOD: nenhum achado pode terminar apenas como “ver com outra skill”. Classifique-o como Confirmado, Pendente, Divergente, Substituído ou Histórico, com destino quando aplicável.

## Transições ANL ↔ MOD

Faça uma transição somente quando ela trouxer uma decisão ou evidência necessária:

- **ANL → MOD** quando uma investigação revelar que falta definir ou consolidar uma regra, requisito, fluxo, permissão, processamento, relatório ou decisão funcional.
- **MOD → ANL** quando a modelagem precisar de um incidente, explicação funcional, teste, resultado de QA, card ou evidência operacional de ticket.
- **MOD → `beta-anl-movidesk`** somente para consulta real ao MCP, em modo leitura.
- **ANL → MOD → ANL** quando uma regra precisar ser fechada antes de derivar testes, resultados ou card.

Não faça transição apenas porque uma skill relacionada existe. Preserve a intenção primária e retorne o achado para a consolidação original.

## Evidência e limites

- Ticket demonstra ocorrência, estado ou histórico registrado; não cria regra, requisito, comportamento esperado ou causa raiz sozinho.
- Regra funcional confirmada prevalece sobre precedente isolado de incidente.
- Hipótese permanece hipótese até receber evidência suficiente.
- Dossiê é estado operacional da modelagem e não deve ser publicado automaticamente como requisito.
- Não invente telas, campos, regras, integrações ou implementação técnica.
- Não simule acesso a ClickUp, Movidesk, Figma ou qualquer conector indisponível.
- Preserve somente leitura nas consultas operacionais e não prometa alterações externas.

## Contrato de execução

1. Identifique a intenção, o resultado esperado e as fontes disponíveis.
2. Escolha ANL ou MOD como modo primário.
3. Acione as skills auxiliares mínimas e registre dependências materiais.
4. Faça handoff somente nas condições desta skill.
5. Reúna os achados, resolva dependências e classifique pendências/divergências.
6. Entregue uma resposta única seguindo o formato da skill primária.

Não exponha nomes de skills, fragmentação interna ou cadeia de raciocínio, salvo quando o usuário estiver configurando ou revisando a arquitetura da Beta.

## Garantias do modo MOD

Quando o modo primário for MOD, preserve estas garantias da antiga orquestração Beta:

- modelagem relevante começa por `beta-mod-regras` e `beta-mod-dossie`;
- fontes, versões ou conflitos de vigência passam por `beta-mod-fontes` antes do Dossiê;
- toda lacuna material termina como Confirmada, Pendente, Divergente, Substituída ou Histórica, com destino quando aplicável;
- fechar o comportamento na sequência aplicável: gatilho, condição, ator, ação, validação, registro afetado, resultado, confirmação/cancelamento/fechamento/falha, continuidade, rastreabilidade e efeitos proibidos;
- `beta-mod-qa` é gate antes da finalização e deve ser repetido após correção material;
- `beta-mod-artefatos` só materializa conteúdo consolidado, com Dossiê, filtro de publicação e QA concluídos, salvo conteúdo explicitamente aprovado para mera materialização;
- manter um único `DOSSIE_CONTEXTO_MODELAGEM.md`, sem incorporá-lo automaticamente ao artefato publicável;
- publicar somente entendimento vigente destinado à MODELAGEM; não publicar contexto interno, histórico sem efeito vigente, regra substituída ou pendência;
- especificar efeito funcional, sem inventar tabela, endpoint, serviço, fila, retry, arquitetura ou outra implementação técnica;
- ao final, produzir um resumo observável da execução sem expor cadeia de pensamento.

Para o contrato MOD completo, consulte [beta-mod-control-plane/SKILL.md](references/beta-mod-control-plane/SKILL.md) e carregue referências internas somente quando o caso exigir.

## Observabilidade e indisponibilidade

Em respostas funcionais relevantes, informe de forma breve as skills efetivamente acionadas, fontes consultadas, ciclos de QA, estado do Dossiê, artefatos gerados e pendências ou divergências materiais, somente quando esses dados forem observáveis.

Se uma skill, fonte ou conector necessário estiver indisponível, não simule a execução. Preserve a lacuna como Pendente ou Divergente e informe a limitação quando ela afetar o resultado.

## Compatibilidade

As antigas orquestradoras `beta-anl-router` e `beta-mod` foram substituídas por esta skill. As skills especializadas `beta-anl-*` e `beta-mod-*` permanecem disponíveis e devem retornar seus achados para `beta`.
