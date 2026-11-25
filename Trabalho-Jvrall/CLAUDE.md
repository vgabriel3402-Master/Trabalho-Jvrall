# CLAUDE.md — Trabalho-Jvrall

Contexto para qualquer Claude (ou pessoa) que continuar este projeto. Leia este arquivo e o `ATUALIZACAO.md` antes de mexer em qualquer coisa.

## O que é o projeto

Automação em Python que posta cortes de vídeo de streamers no TikTok, de forma automática e em rodízio, usando a API oficial do TikTok (Content Posting API, Direct Post).

Resumo do funcionamento (definido pelo parceiro):

- `conteudos/DD MM AAAA/<streamer>/NN_nome.mp4`: uma pasta por dia, uma por streamer. Os números (01_, 02_...) definem a ordem de postagem.
- `fila.py`: começa pelo dia mais antigo com cortes não postados, ignora datas futuras, faz rodízio entre streamers (A → B → C → A) e tira da vez quem não tem cortes.
- Legenda: usa o `.txt` com o mesmo nome do vídeo, se existir. Senão, usa o modelo do `config.yaml` (título do arquivo + nome do streamer + hashtags do streamer).
- `estado.json`: registra o que já foi postado.
- `config.yaml`: horários, modelo de legenda, hashtags, privacidade e credenciais (local, fora do Git).
- `tiktok_api.py`: OAuth via Login Kit (`user.info.basic`, `video.publish`), renovação de token, upload em chunks.
- Até a auditoria do TikTok, posts saem como `SELF_ONLY`. Depois, `PUBLIC_TO_EVERYONE` no config. Limite aproximado: 15 posts/dia por conta.
- Comandos (`autopost.py`): `plano`, `rodar`, `login`, `postar [--seco]`, `status`.

## Quem faz o quê

| Pessoa | Parte |
|---|---|
| **Parceiro** (Claude dele) | Código da automação: `fila.py`, `tiktok_api.py`, `autopost.py`, `config.yaml`/`config.exemplo.yaml`, README, rodar como serviço, integrações opcionais |
| **João Pedro / Vitor** (este Claude) | Páginas públicas no GitHub Pages (`docs/`: início, Termos, Privacidade, callback) e cadastro/aprovação do app no TikTok for Developers |

> Observação: o briefing original citava "Vitor" no campo da parte; o responsável informado para as páginas é João Pedro Carvalho. Confirmar qual nome vale na documentação.

## Regras de trabalho (valem para todos)

1. Não alterar a estrutura de pastas, o formato do `config.yaml`, o `estado.json` nem a interface dos comandos sem avisar o parceiro.
2. Nunca colocar Client Key, Client Secret, tokens ou senhas no código, nos `.md` ou no zip. Usar `config.yaml` local (fora do Git/zip) ou variáveis de ambiente; manter `config.exemplo.yaml` sem segredos.
3. Código organizado e comentado onde não for óbvio.
4. A cada avanço: atualizar `ATUALIZACAO.md` e a seção de status abaixo; commit + push (ou zip limpo, se não houver acesso ao GitHub).
5. Zip sem: `venv`, `node_modules`, `__pycache__`, `config.yaml` com segredos, `estado.json`, tokens, vídeos.

## Status / tarefas (atualizado em 25/11/2026)

### Parte do parceiro (código)
- [x] `fila.py`, `tiktok_api.py`, `autopost.py`, `config.yaml`, README — **existem no computador do parceiro; ainda não estão neste repositório**
- [x] Fila e rodízio testados com vídeos falsos
- [ ] Envio real ao TikTok (aguarda o app existir em developers.tiktok.com)
- [ ] Ajustar o fluxo de `login` ao Redirect URI HTTPS (ver "Impacto no parceiro" no `ATUALIZACAO.md`)
- [ ] Rodar como serviço (iniciar sozinho)
- [ ] Opcionais: integração com ferramenta de cortes, várias contas, agendador de terceiros

### Parte do Vitor/João Pedro (este Claude)
- [x] Páginas `docs/`: `index.html`, `termos.html`, `privacidade.html`, `callback.html`, `style.css`
- [x] `CLAUDE.md`, `ATUALIZACAO.md`, `.gitignore` iniciais
- [ ] Subir o repositório e ativar o GitHub Pages (Settings → Pages → branch `main`, pasta `/docs`)
- [ ] Criar conta e app (tipo Web) no TikTok for Developers: Login Kit + Content Posting API (Direct Post)
- [ ] Verificar a URL/domínio no TikTok
- [ ] Testar no Sandbox, gravar o vídeo de demonstração, enviar para auditoria
- [ ] Após aprovação: avisar o parceiro para trocar a privacidade para `PUBLIC_TO_EVERYONE`

## Estado do repositório

Na última checagem (25/11/2026) o repositório no GitHub estava **vazio**. O primeiro conteúdo a entrar é este pacote (`docs/`, `CLAUDE.md`, `ATUALIZACAO.md`, `.gitignore`).
