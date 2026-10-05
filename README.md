# dojotame-status

Monitor simples da produção do **DojoTame** (`https://jiujitsu-saas-iota.vercel.app`), feito com GitHub Actions. O repositório é público só para ter minutos de Actions ilimitados; não contém segredo nem dado pessoal, apenas o endereço público do site.

- **A cada 15 min** (sujeito a atrasos do agendador do GitHub): `GET /login` deve responder 200.
- **De hora em hora:** também `GET /api/saude` deve responder 200 com `"status":"ok"` (consulta o banco; de hora em hora para economizar as horas de processamento do plano gratuito do Neon).
- **Falha** = 3 tentativas seguidas com 30 s de intervalo. Aí o workflow falha (o GitHub avisa por e-mail) e uma issue com a etiqueta `incidente` é aberta ou atualizada. Ao voltar ao normal, a issue é fechada com o horário da recuperação — o histórico de quedas fica nas issues fechadas.
- **Manter ativo:** um commit vazio mensal (`manter-ativo.yml`) evita que o GitHub desligue o agendamento após 60 dias sem atividade.

Checagem manual: aba **Actions** → **Saúde da produção** → **Run workflow**.

O que fazer quando cair: `docs/13-RESPOSTA-A-INCIDENTES.md` no repositório do sistema.

Ao trocar o endereço de produção (ex.: domínio próprio), atualize `URL_BASE` em `.github/workflows/saude.yml`.
