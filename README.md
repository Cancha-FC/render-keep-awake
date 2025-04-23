Claro! Aqui está uma versão estilizada, moderna e totalmente compatível com o GitHub para seu README.md do projeto render-keep-awake — com visual limpo, ícones, tabelas organizadas, links funcionais e cores baseadas na sua identidade (azul, cinza, branco, preto):

⸻



<div align="center">

# ⚙️ render-keep-awake

[![Keep Awake](https://github.com/Cancha-FC/render-keep-awake/actions/workflows/keep-awake.yml/badge.svg)](https://github.com/Cancha-FC/render-keep-awake/actions/workflows/keep-awake.yml)
![Auto Ping](https://img.shields.io/badge/Auto--Ping-Every%2014%20min-6c757d?style=flat-square)
![License](https://img.shields.io/github/license/Cancha-FC/render-keep-awake?style=flat-square)

<p align="center">
Repositório <strong>público</strong> criado para manter serviços <a href="https://render.com">Render</a> ativos 24 × 7, evitando que entrem em modo “sleep” por inatividade.
</p>

</div>

---

## 🌐 URLs Pingadas

| Endereço | Descrição |
|----------|-----------|
| [`/healthz`](https://canchacallback.onrender.com/healthz) | ⚡ FastAPI Callback (Bling OAuth) |
| [`/swagger`](https://cancha-back.onrender.com/swagger/)  | 📘 Backend Cancha – Documentação Swagger |

---

## 🛠️ Como funciona

> Este repositório usa **GitHub Actions** para rodar um workflow a cada 14 minutos:

- Faz **pings com `curl`** para manter os serviços ativos
- Falhas são ignoradas (`|| true`) para não quebrar o job
- Utiliza **runners gratuitos** (minutos ilimitados para repositórios públicos)

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



⸻

✏️ Como editar ou adicionar novas URLs
	1.	Acesse o arquivo: .github/workflows/keep-awake.yml
	2.	Adicione/remova linhas curl -fsS <URL> || true
	3.	Salve, commit e dê push — o cron será atualizado automaticamente

⸻

⏱️ Frequência

A expressão */14 * * * * define execução a cada 14 minutos, abaixo do limite de suspensão da Render (15 min).

Exemplos de outros intervalos:

Intervalo desejado	Cron equivalente
A cada 10 minutos	*/10 * * * *
A cada 20 minutos	*/20 * * * *



⸻

🧠 Autor

Leonardo Miranda – CtrlLabs
📧 leonardo@ctrllabs.com.br
🌐 ctrlabs.com.br

⸻

📄 Licença

MIT © 2025 CtrlLabs

⸻



---

Se quiser, posso criar esse `README.md` direto no repositório ou gerar como arquivo `.md` aqui para colar no projeto. Deseja isso?
