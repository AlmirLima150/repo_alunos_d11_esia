# Registro individual — AV1.3

**Limite: uma página.** Estudante: Almir de Lima Felix dos Santos — Data: 02/10/2026
**Critério de aceite derivado de R2/R4:** `listar_ativos` deve retornar exclusivamente os chamados em estado `"aberto"` ou `"em_andamento"`, excluir `"fechado"` e manter exatamente a ordem da entrada, conferida por igualdade de lista (não por conjunto ou pertencimento). A documentação (R4) deve registrar unicamente essas 4 condições, sem acrescentar ordenações.

| Caso / estado focal | Entrada (IDs e ordem) | IDs esperados na ordem | Obrigação de R2 e como verificar |
|---|---|---|---|
| 1 / aberto | `[TR-33]` | `["TR-33"]` | Inclusão de `aberto`: comparar o retorno com `["TR-33"]`. |
| 2 / em_andamento | `[TR-31]` | `["TR-31"]` | Inclusão de `em_andamento`: comparar com `["TR-31"]`. É o caso que detecta o defeito do `caso/fila_clara.py` original, que só aceita `aberto`. |
| 3 / fechado | `[TR-32]` | `[]` | Exclusão de `fechado`: `assertEqual(resultado, [])`. TR-32 tem escore 6 (alta) e mesmo assim sai: a prioridade não interfere. |

**Entrada combinada TR-31, TR-32, TR-33 → IDs esperados:** `["TR-31", "TR-33"]`
**Trecho essencial de evidência da ordem e modo de conferir:** na sequência `[TR-31 (em_andamento, escore 2), TR-32 (fechado, escore 6), TR-33 (aberto, escore 5)]`, o esperado é `["TR-31", "TR-33"]`. Uma implementação que ordenasse por prioridade devolveria `["TR-33", "TR-31"]` e seria detectada pela asserção de lista: `self.assertEqual([c["id"] for c in resultado], ["TR-31", "TR-33"])`. Um teste com `set` ou `in` passaria com a ordem errada (falso positivo). Esta entrada não distingue "ordenar por id", pois a ordem crescente de id coincide com a de entrada; por isso confiro também a entrada invertida `[TR-33, TR-32, TR-31]` → `["TR-33", "TR-31"]`.
**Documentação proposta (até três frases):** A função `listar_ativos` retorna apenas os chamados com estado "aberto" ou "em_andamento", descartando os de estado "fechado". O resultado preserva a ordem em que os chamados foram fornecidos na entrada. Nenhuma reordenação por impacto, urgência, departamento ou id é aplicada.

**Etapa delegável / tarefa de assistência / responsável:** rascunho do código dos casos de teste e da docstring a partir do texto de R2 / pessoa da manutenção responsável pela listagem.
**Verificação para o aceite humano:** calcular os IDs esperados por R2 antes de ler o rascunho; conferir que a docstring não promete ordenação inexistente; auditar o teste para garantir comparação de lista na ordem, sem `set` ou testes de pertencimento que mascaram erros de ordem.
**Alternativa sem IA e comparação:** redação manual do teste e da documentação: exige mais esforço de redação, mas elimina o risco de regra inventada no rascunho. Com assistência, a conferência contra as 4 obrigações de R2 continua obrigatória, e a responsabilidade pelo aceite é a mesma.
**Limite da cobertura e condição para rever o aceite:** os casos cobrem os três estados e a ordem, mas não lista vazia nem dois chamados ativos seguidos; entradas com campos ausentes estão fora do escopo (`caso/regras.md`). Reveria o aceite se R2 mudasse (por exemplo, exigindo ordenação por prioridade) ou se surgisse um estado novo.

**Procedência/status:** entrada fictícia do enunciado (`TR-31`, `TR-32`, `TR-33`); esperado por contrato: todos os IDs acima, derivados de R2; inspeção própria: conferência dos estados, escores e ordem de entrada; execução opcional: não realizada (os IDs são esperados, não observados).
**IA:** Antigravity (agy), modelo Flash 3.8 (modo high), e Claude Code (Anthropic), modelo Claude Opus 5.5, 02/10/2026. Tarefas: (1) Antigravity — rascunho do registro a partir do enunciado; (2) Claude Code — comparação desse rascunho com outra versão, contra o contrato e a rubrica, e consolidação. Trecho aproveitado: do Antigravity, a asserção de lista, o alerta sobre `set`/`in` e a documentação; do Claude Code, a entrada invertida, a ligação do caso 2 ao defeito do kit, a observação sobre o escore de TR-32 e a remoção de estimativas de tempo sem medição. Minha verificação: conferi no enunciado os estados de TR-31 (`em_andamento`), TR-32 (`fechado`) e TR-33 (`aberto`); refiz os escores 2, 6 e 5; derivei de R2 os IDs esperados dos três casos, da entrada combinada e da invertida; confrontei cada frase da documentação com as quatro obrigações de R2. O raciocínio e a decisão são meus.

**Revisão:** [x] três estados; [x] ordem; [x] texto; [x] aceite/limite; [x] uma página.
