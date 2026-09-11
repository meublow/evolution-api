# Deploy self-hosted (bLOw)

A imagem é buildada e publicada automaticamente pelo GitHub Actions
(`.github/workflows/publish_ghcr.yml`) a cada push na branch `build-fix-463`, em
`ghcr.io/meublow/evolution-api`. Nenhuma máquina precisa buildar nada.

## Subir em uma máquina nova

```bash
git clone --branch build-fix-463 https://github.com/meublow/evolution-api.git
cd evolution-api/deploy
cp .env.example .env
# edite o .env: SERVER_URL e EVOLUTION_API_KEY
docker compose up -d
```

A API sobe em `http://localhost:8084`, com Postgres (`5434`) e Redis (`6380`) próprios.

### Se o pacote no GHCR estiver privado

O outro PC precisa autenticar uma vez antes do `docker compose up`:

```bash
echo $GHCR_TOKEN | docker login ghcr.io -u meublow --password-stdin
```

onde `GHCR_TOKEN` é um Personal Access Token (classic) com escopo `read:packages`.
Para dispensar o login, deixe o pacote público em
`https://github.com/users/meublow/packages/container/evolution-api/settings`.

## Atualizar para a última imagem

```bash
docker compose pull && docker compose up -d
```

## Buildar localmente (opcional)

```bash
docker compose -f docker-compose.yml -f docker-compose.build.yml up -d --build
```

## Tags publicadas

- `latest` e `build-fix-463` — sempre o último build da branch
- `sha-<commit>` — build de um commit específico
