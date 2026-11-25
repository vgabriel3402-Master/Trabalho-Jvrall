# ATUALIZACAO.md

Registro de progresso para troca entre os dois integrantes e seus Claudes. A entrada mais recente fica no topo.

---

## 25/11/2026 — Site do GitHub Pages (Termos, Privacidade, callback) e arquivos de controle

### Resumo
Primeira entrega da parte do Vitor/João Pedro: criado o site estático que o TikTok for Developers exige no cadastro do app (página inicial, Termos de Uso, Política de Privacidade e página de callback para o OAuth). Também foram criados os arquivos de controle do projeto. O repositório no GitHub estava vazio na última checagem.

### Arquivos criados
| Arquivo | Para que serve |
|---|---|
| `docs/index.html` | Página inicial do app (URL do site no cadastro do TikTok) |
| `docs/termos.html` | Termos de Uso (URL dos Termos no cadastro) |
| `docs/privacidade.html` | Política de Privacidade (URL da Privacidade no cadastro) |
| `docs/callback.html` | Redirect URI do OAuth: recebe `?code=...` do TikTok e mostra o código para copiar |
| `docs/style.css` | Estilo compartilhado (sem dependências externas, claro/escuro) |
| `CLAUDE.md` | Contexto do projeto, divisão de tarefas, regras e status |
| `ATUALIZACAO.md` | Este arquivo |
| `.gitignore` | Impede que segredos, estado, vídeos e cache entrem no Git |

Nenhum arquivo do parceiro foi criado ou alterado.

### O que funciona / o que está incompleto
- **Pronto (não publicado ainda):** as quatro páginas HTML e o CSS. Conteúdo em português, responsivas, com tema claro/escuro. Não foram testadas em um navegador real neste ambiente.
- **Incompleto:** o site ainda não está no ar (falta subir ao GitHub e ativar o Pages). O app no TikTok for Developers ainda não foi criado. Nenhum envio real ao TikTok foi testado.
- **Texto legal:** os Termos e a Privacidade foram redigidos como modelo para o projeto. Não substituem revisão jurídica.

### Como publicar e testar (sem segredos)
1. Suba o conteúdo deste pacote para o repositório `Trabalho-Jvrall` (branch `main`).
2. No GitHub: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / pasta `/docs`**.
3. Aguarde o deploy. A URL deve ser `https://vgabriel3402-master.github.io/Trabalho-Jvrall/` (conferir a URL exata em Settings → Pages).
4. Abra no navegador: `/`, `/termos.html`, `/privacidade.html` e `/callback.html`.
5. Teste do callback: abra `/callback.html?code=teste123` e confira se mostra o código; abra `/callback.html?error=access_denied` e confira a mensagem de erro.

URLs para o cadastro do app (ajustar para a URL real do Pages):
- Site / Termos / Privacidade: `.../`, `.../termos.html`, `.../privacidade.html`
- Redirect URI: `.../callback.html`

### Decisões e motivos
- **Site em `docs/`**: o GitHub Pages publica essa pasta sem misturar com o código Python do parceiro.
- **HTML puro, sem scripts ou fontes de terceiros**: a política de privacidade afirma que o site não coleta dados; carregar recursos externos poderia contradizer isso.
- **`callback.html` mostra o código para copiar**: o Redirect URI precisa ser HTTPS e público, mas o programa roda no PC do responsável. A página só lê a URL no navegador (sem enviar nem gravar) e o código sozinho não dá acesso sem a Client Secret.
- **Redigido em português**: a revisão do TikTok pode preferir inglês. Se pedirem, adiciono versões em inglês.
- **`.gitignore` incluído**: proteção contra vazamento de `config.yaml`, tokens e `estado.json`. É um arquivo novo; o parceiro pode ajustá-lo.

### ⚠️ Impacto na parte do parceiro (ler com atenção)
1. **Fluxo do comando `login`.** O Redirect URI cadastrado no TikTok será a página `callback.html` no GitHub Pages (HTTPS), não um endereço local. Se o `login` atual espera o retorno em `http://localhost`, ele precisa mudar para um destes modelos:
   - **(A) Colar o código:** o programa abre a URL de autorização, o usuário autoriza, a página mostra o código, e o usuário cola no terminal (`input()`). O programa troca o código por token. *Foi o fluxo que a `callback.html` foi desenhada para atender.*
   - **(B) Redirecionar para localhost:** exigiria outro Redirect URI e alteração na página. Não recomendo sem confirmar se o TikTok aceita.
2. **`config.yaml` / `config.exemplo.yaml`:** o campo da Redirect URI deve apontar para a URL do `callback.html`. Nenhum formato foi alterado por mim; só preciso que o parceiro confirme o nome do campo.
3. **Pasta `docs/` e `.gitignore`** são novos na raiz. Não alteram `conteudos/`, `estado.json` nem os comandos.

### Pendências e próximos passos
1. Subir o pacote ao GitHub e ativar o Pages.
2. Criar a conta de desenvolvedor e o app (tipo Web) no TikTok for Developers, com Login Kit e Content Posting API (Direct Post), escopos `user.info.basic` e `video.publish`.
3. Cadastrar as URLs do site, Termos, Privacidade e Redirect URI.
4. Fazer a verificação da URL/domínio. O TikTok fornece um arquivo ou método de verificação; se for arquivo, ele vai em `docs/`.
5. Testar no Sandbox, gravar o vídeo de demonstração e enviar para auditoria.
6. Guardar Client Key e Client Secret só no `config.yaml` local do parceiro/operador.

### Riscos e dúvidas
- Não confirmei que o TikTok aceita um domínio `github.io` na verificação de URL. Se recusar, será preciso um domínio próprio ou outro host. Vale checar cedo.
- A auditoria pode exigir contas e conteúdo de demonstração que sigam as regras do TikTok. Até a aprovação, os posts ficam privados (`SELF_ONLY`).
- Os vídeos são cortes de streamers: confirmar a autorização dos streamers, pois isso pode pesar na aprovação e nas regras de direitos autorais.

### Perguntas para o parceiro
1. O `login` atual usa localhost ou pede para colar o código? Aceita mudar para o modelo (A)?
2. Qual o nome do campo da Redirect URI no `config.yaml`?
3. Ele já subiu o código no GitHub ou prefere me enviar o zip dele para eu integrar a documentação?
4. O nome do responsável na documentação é João Pedro Carvalho ou Vitor?
