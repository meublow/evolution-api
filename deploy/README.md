# Deploy self-hosted (bLOw)

Este `docker-compose.yml` builda a imagem a partir do código deste repositório (branch
`build-fix-463`, que já tem o bump do `baileys` que corrige a issue #463) em vez de depender de
uma imagem `:local` construída manualmente numa máquina só.

## Subir em uma máquina nova

```bash
git clone --branch build-fix-463 https://github.com/meublow/evolution-api.git
cd evolution-api/deploy
cp .env.example .env
# edite o .env: SERVER_URL e EVOLUTION_API_KEY
docker compose up -d --build
```

A API sobe em `http://localhost:8084`, com Postgres (`5434`) e Redis (`6380`) próprios.

## Atualizando a chave/URL depois

Edite `deploy/.env` e rode `docker compose up -d` novamente (não precisa `--build` se o código
não mudou).
