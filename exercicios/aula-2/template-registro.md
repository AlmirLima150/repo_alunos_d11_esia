# Registro individual — AV1.2

**Limite: uma página.** Estudante: Almir de Lima Felix dos Santos — Data: 02/10/2026
**Critérios prévios:** correção de R1: escore = impacto + urgência (inteiros de 1 a 3); escore ≥ 5 → `alta`, 3 a 4 → `media`, < 3 → `baixa`. A resposta só é correta se o rótulo coincidir com esse cálculo e o critério explicado for o do contrato. Evidência necessária para uma alegação geral: as 9 combinações possíveis (3 × 3), incluindo os limiares 2/3 e 4/5, comparadas com um esperado calculado de forma independente, e repetições com condições registradas (sessão, instrução e, quando a interface permitir, configuração).

| Entrada de A (impacto, urgência) | Cálculo e esperado por R1 | Trecho da resposta A | Conclusão por inspeção |
|---|---|---|---|
| (2, 3) — ref. `FC-002` | 2 + 3 = 5 → esperado: `alta` | *"(impacto=2, urgencia=3) é media"* | **Incorreta.** A ignora a urgência e rebaixa um chamado de prioridade alta para média. |
| (3, 1) — ref. `FC-006` | 3 + 1 = 4 → esperado: `media` | *"(impacto=3, urgencia=1) é alta"* | **Incorreta.** A ignora a urgência e eleva um chamado de prioridade média para alta. |

**B — trecho analisado:** *"Repeti três vezes o pedido 'classifique impacto=2, urgencia=3'. As três saídas foram 'alta'. Isso prova que o modelo é determinístico e sempre entrega a classificação correta, inclusive em outros chamados."*
**O que o resultado particular sustenta:** que o rótulo `alta` para o par (2, 3) está correto por R1 (2 + 3 = 5 ≥ 5) e que as três tentativas coincidiram naquelas condições.
**O que a alegação geral exige e não está fornecido:** três saídas iguais para uma única entrada mostram consistência naquelas condições, que não foram registradas (sessão, instrução, configuração); isso não demonstra determinismo, pois não há garantia de que outra execução, sessão ou formulação produza o mesmo resultado. "Sempre correta em outros chamados" generaliza 1 entrada para as 9 possíveis, sem avaliar as outras 8.
**Contraexemplo ou condição não coberta:** não foram avaliados os limiares, como (3, 2) → `alta` e (2, 2) — ref. `FC-004` → `media`, nem o escore 2 de `FC-001` → `baixa`. Em `apoio/saidas-simuladas.md`, a saída simulada B3 recebeu o contrato e ainda assim classificou (2, 3) como `media`: uma resposta pode errar o limiar mesmo com a regra no contexto.

**Decisão A + motivo:** **rejeitar.** A usa um critério que não é o de R1 (descarta a urgência) e os dois pares divergem do esperado.
**Decisão B + motivo:** **aceitar parcialmente.** Aceito o rótulo `alta` para (2, 3) porque o conferi pelo cálculo, não pela repetição; rejeito a alegação de determinismo e de correção geral.
**Alternativa de verificação e condição que mudaria uma decisão:** pedir ao modelo as 9 combinações e comparar cada resposta com o rótulo esperado de uma tabela feita por mim a partir de R1, repetindo em sessões novas com as condições registradas. Se todas coincidissem em todas as repetições, eu aceitaria B como "consistente nessas condições", nunca como "determinístico".

**Origem/status:** respostas didáticas simuladas; cálculos/inspeções próprios: soma e aplicação dos limiares de R1 aos pares de A e B, conferindo os registros `FC-002`, `FC-006`, `FC-004` e `FC-001` em `caso/chamados.json`; execução real: não realizada. Tokens/custo/latência/configuração: não informados.
**IA na produção do registro:** Antigravity (agy), modelo Flash 3.8 (modo high), e Claude Code (Anthropic), modelo Claude Opus 5.5, 02/10/2026. Tarefas: (1) Antigravity — rascunho do registro a partir do enunciado; (2) Claude Code — comparação desse rascunho com outra versão, contra o contrato e a rubrica, e consolidação. Trecho aproveitado: do Antigravity, as referências aos chamados, a consequência de cada erro de A e os contraexemplos com IDs; do Claude Code, o contraexemplo da saída simulada B3, a alternativa com esperado independente e a condição de mudança sobre B. Verificação própria: refiz as somas 2 + 3 = 5 (`alta`) e 3 + 1 = 4 (`media`) aplicando os limiares de R1; confirmei em `caso/chamados.json` que (2, 3) é `FC-002`, (3, 1) é `FC-006`, (2, 2) é `FC-004` e (1, 1) é `FC-001`; li em `apoio/saidas-simuladas.md` que a saída B3 classificou `FC-002` como `media` mesmo com o contrato; conferi que os trechos citados de A e B correspondem ao texto de `exercicios/aula-2/README.md`. O raciocínio e a decisão são meus.

**Revisão:** [x] critérios; [x] dois pares; [x] análise de B; [x] decisões/limites; [x] uma página.
