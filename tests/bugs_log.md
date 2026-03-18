# bugs_log.md - Log Centralizado de Bugs e Testes

## 1. Proposito

Centralizar o registro de bugs e testes por sprint com rastreabilidade suficiente para sustentar decisoes, correcoes e validacoes estruturais do projeto.

## 2. Regra de Uso

- Registrar bugs e testes por sprint
- Usar formato padronizado de identificacao
- Manter referencia cruzada com `Dev_Tracking_SX.md`
- Bugs: `BUG-SX-YY`
- Testes: `TEST-SX-YY`
- Registrar fatos observaveis, nao suposicoes
- Explicitar status e impacto de cada bug
- Registrar resultado real dos testes, sem citar validacoes inexistentes

---

## 3. Sprint S1

### 4. Bugs Registrados

Nenhum bug registrado nesta sprint.

### 5. Testes Registrados

Nenhum teste registrado nesta sprint.

---

## 6. Timestamp UTC

Usar formato DOC2.5 (ISO 8601, 24h): `YYYY-MM-DDTHH:MM:SS-ST` para inicio e `YYYY-MM-DDTHH:MM:SS-FN` para fim.

Event | Start | Finish | Status
---|---|---|---

## 7. Regras de Qualidade do Log

- Cada bug deve apontar para pelo menos uma evidencia observavel
- Cada teste deve descrever o escopo realmente validado
- O `Timestamp UTC` deve refletir eventos ja executados
- O log deve permanecer coerente com `README.md`, `Dev_Tracking.md` e `Dev_Tracking_SX.md`
- Itens historicos nao devem ser apagados sem justificativa formal

---

## 8. Sprints Futuras

Sprints subsequentes (`S2`, `S3`, etc.) devem ser adicionadas conforme a evolucao do projeto, preservando a ordem historica do log.
