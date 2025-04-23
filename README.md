<div align="center">

<h1 style="color:#0d6efd">⚙️ render-keep-awake</h1>

[![Keep Awake](https://github.com/Cancha-FC/render-keep-awake/actions/workflows/keep-awake.yml/badge.svg)](https://github.com/Cancha-FC/render-keep-awake/actions/workflows/keep-awake.yml)
<img src="https://img.shields.io/badge/Auto--Ping-Every%2014%20min-6c757d?style=for-the-badge" />
<img src="https://img.shields.io/github/license/Cancha-FC/render-keep-awake?style=for-the-badge&color=000000" />

</div>

---

> Repositório **público** criado exclusivamente para manter dois serviços Render ativos 24 × 7, evitando que entrem em suspensão após 15 min de inatividade.

---

## 🌐 Serviços Pingados

| URL | Descrição |
|------|------------|
| [`/healthz`](https://canchacallback.onrender.com/healthz) | ⚡️ FastAPI Callback (Bling OAuth) |
| [`/swagger/`](https://cancha-back.onrender.com/swagger/) | 📘 Backend Cancha (Swagger UI) |

---

## 🛠️ Como funciona

* O GitHub Actions executa o workflow a cada **14 minutos**.
* Requisições `curl` são feitas para as URLs acima.
* Falhas não quebram o job (`|| true`).

```yaml
name: Keep Render Awake
on:
  schedule:
    - cron: "*/14 * * * *"
jobs:
  ping:
    runs-on: ubuntu-latest
    steps:
      - name: Ping Render services
        run: |
          curl -fsS https://canchacallback.onrender.com/healthz  || true
          curl -fsS https://cancha-back.onrender.com/swagger/    || true
```

---

## ✏️ Alterar ou adicionar URLs

1. Edite o arquivo `.github/workflows/keep-awake.yml`
2. Adicione/remova linhas `curl -fsS <URL> || true` no bloco `run:`
3. Commit → Push → o cron será atualizado automaticamente

---

## ⏱️ Frequência

* `*/14` mantém o serviço ativo antes do timeout da Render.
* Quer alterar?
  - `*/10 * * * *` → a cada 10 minutos
  - `*/20 * * * *` → a cada 20 minutos

---

## 📄 Licença

MIT © 2025 Leonardo Miranda / CtrlLabs

