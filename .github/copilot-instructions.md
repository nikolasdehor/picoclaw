# Copilot Instructions — picoclaw

## Project Overview
picoclaw é uma aplicação Go (CLI / serviço).

## Architecture
- **Entry point:** `cmd/picoclaw/main.go`
- **Pacotes internos:** `internal/` — não exportados
- **Pacotes públicos:** `pkg/` — API estável (se aplicável)
- Build com `go build ./...`, testes com `go test ./...`

## Conventions
- Erros tratados explicitamente — sem `_ = err` silencioso
- `context.Context` propagado em todas as chamadas IO
- Sem `panic` em código de biblioteca; só em main durante init fatal
- Tabelinhas de teste (`tests := []struct{...}{...}`)
- Sem variáveis globais mutáveis; passar dependências por construtor
- `gofmt` + `go vet` antes de commit; preferir `golangci-lint` se config existir
- Goroutines com `context` e `sync.WaitGroup`/`errgroup` — sem leaks

## CLI (se aplicável)
- Flags via `flag` ou `cobra`
- `--help` documentado pra cada subcomando
- Signal handling (`SIGINT`, `SIGTERM`) com graceful shutdown

## Critical Files
- `go.mod` — deps
- `cmd/picoclaw/main.go` — entry
- `internal/` — lógica principal
