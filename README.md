render-keep-awake

Este repositório público existe exclusivamente para manter dois serviços hospedados na Render ativos 24 × 7, evitando que entrem em suspensão automática após 15 min sem tráfego.

Serviços pingados

URL	Descrição
https://canchacallback.onrender.com/healthz	FastAPI Callback (Bling OAuth)
https://cancha-back.onrender.com/swagger/	Backend Cancha (Swagger UI)



Como funciona
	•	O workflow GitHub Actions (.github/workflows/keep-awake.yml) é executado a cada 14 min usando runners da própria plataforma (minutos ilimitados para repositórios públicos).
	•	Faz simples requisições curl às URLs acima.
	•	Qualquer falha (curl ≠ 0) é ignorada (|| true) para não quebrar o job.

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

Alterando ou adicionando URLs
	1.	Edite o bloco run: do arquivo keep-awake.yml.
Adicione/remove linhas curl -fsS <URL> || true conforme necessário.
	2.	Commit e envia (push) para main — o cron usará a nova lista automaticamente.

Frequência
	•	14 min foi escolhido para ficar logo abaixo do limite de 15 min da Render e, ao mesmo tempo, consumir ≈ 3 000 min/mês (a cota do plano Pro, caso algum dia o repo seja tornado privado).
	•	Para mudar, ajuste a expressão cron:. Ex.:
	•	*/10 * * * * → a cada 10 min
	•	*/20 * * * * → a cada 20 min

Segurança

Nenhum segredo é necessário — todas as URLs são públicas.

Licença

MIT © 2025 Leonardo Miranda / CtrlLabs
