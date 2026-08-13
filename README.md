# Oblodai docs

Документация Oblodai — https://oblodai.mintlify.io

## Откуда берётся справка API

`api-reference/openapi.json` — **генерируется из кода ядра**, руками не редактируется:

- источник — `oblodai-backend/services/core/internal/app/docsapi` (список операций + рефлексия
  реальных DTO); тот же документ ядро отдаёт живьём на `GET https://api.oblodai.com/openapi.json`;
- локально перегенерить: `cd oblodai-backend/services/core && go run ./cmd/openapi-dump > <docs>/api-reference/openapi.json`;
- автоматически: workflow `openapi-sync` раз в сутки забирает спеку с прода и коммитит, если она
  изменилась (пуш в main передеплоивает Mintlify);
- полноту стережёт тест в ядре (`internal/app/openapi_coverage_test.go`): каждый роут mux обязан
  быть задокументирован (в публичной или внутренней доке) — и наоборот. Роут без доки роняет CI.

Таб «Плейграунд API» рисуется Mintlify прямо из этой спеки (эндпоинты, схемы, «try it»).
Рукописный «Справочник» — проза и примеры; при изменении API сверяйтесь со спекой.
