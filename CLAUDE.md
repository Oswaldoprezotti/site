# CLAUDE.md — site cybercrimesprezotti.com.br

Documentação de manutenção para sessões do Claude. Leia antes de mexer em qualquer coisa.

## O que é

Site pessoal/portfólio de **Oswaldo Prezotti** (usuário desta máquina), estudante de Direito na Faculdade Aprendiz (Barbacena-MG). Publica artigos semanais educativos sobre Direito Penal e Direito Digital, gerados pela skill `artigo-semanal`. Não é o site do escritório Ayres Advocacia — é pessoal e o vínculo com o escritório é mencionado apenas genericamente ("um escritório de advocacia"), por decisão deliberada.

## Stack e infraestrutura

- **Jekyll no GitHub Pages** (build automático "legacy": branch `main`, pasta raiz). Sem servidor, sem CI própria, sem dependência local — o GitHub compila a cada push. Não há Ruby/Jekyll instalado nesta máquina e não precisa.
- **Repositório:** `Oswaldoprezotti/site` (conta GitHub `Oswaldoprezotti`, autenticada via `gh` CLI; credencial do git configurada com `gh auth setup-git`).
- **Pasta local:** `C:\Users\Oswal\OneDrive\Área de Trabalho\site-cybercrimesprezotti` (identidade git local: Oswaldo Prezotti / oswaldoprezotti01@gmail.com).
- **Domínio:** `cybercrimesprezotti.com.br` no Registro.br (usuário OSPRE4), zona hospedada no próprio Registro.br: 4 registros A na raiz (185.199.108.153 / .109 / .110 / .111) + CNAME `www` → `oswaldoprezotti.github.io`.
- **HTTPS:** certificado Let's Encrypt emitido pelo GitHub (renova sozinho), `https_enforced: true`.
- **Plugins Jekyll** (nativos do GitHub Pages): `jekyll-seo-tag` (title/meta/OG), `jekyll-feed` (/feed.xml), `jekyll-sitemap` (/sitemap.xml).

## Estrutura de arquivos

- `_config.yml` — título, descrição, plugins, exclusões. Posts recebem `layout: artigo` por default.
- `_layouts/default.html` — esqueleto único (head com {% raw %}`{% seo %}`{% endraw %}, topbar, rodapé).
- `_layouts/artigo.html` — masthead do artigo (usa `page.title_html` se existir, senão `page.title`; `page.lede`; `page.data_extenso`), depois o conteúdo, depois caixa de autor e aviso legal (automáticos — nunca duplicar no corpo do post).
- `_posts/AAAA-MM-DD-slug.md` — um arquivo por artigo. Front matter: `title`, `title_html` (opcional), `lede`, `data_extenso`, `description`, e `permalink` apenas quando preciso preservar URL antiga.
- `index.html` — capa; a lista de artigos é um loop `site.posts` (não editar manualmente a lista).
- `MODELO-ARTIGO.md` — modelo comentado para artigos novos (excluído do build).
- `CNAME` — arquivo de uma linha com o domínio. **Nunca apagar.**

## Rotina: publicar artigo novo

1. Gerar o texto com a skill `artigo-semanal` (ela já produz .md com referências ABNT e disclaimer).
2. Criar `_posts/AAAA-MM-DD-slug.md` conforme `MODELO-ARTIGO.md` (conteúdo em Markdown ou HTML; ambos funcionam).
3. `git add -A`, commit, `git push`. Capa, feed e sitemap atualizam sozinhos.
4. Conferir build: `gh api repos/Oswaldoprezotti/site/pages/builds/latest --jq .status` → esperar `built`. Se `errored`, o `.error.message` diz a causa (geralmente Liquid/YAML no front matter).

## Armadilhas conhecidas (aprendidas na prática)

1. **GitHub cria commits remotos sozinho** quando o domínio customizado é alterado via API/UI (commits "Delete CNAME"/"Create CNAME"). Sempre `git pull --rebase origin main` antes de push se houver rejeição.
2. **Não re-salvar o domínio customizado repetidamente** (PUT com cname na API do Pages): cada re-save pode reiniciar a emissão do certificado HTTPS. Se o certificado travar (cert: null por muito tempo), o gatilho correto é remover e re-adicionar o domínio UMA vez.
3. **Registro.br "Domínio em transição":** ao ativar o Modo Avançado da zona, há janela de ~2h em que edições são aceitas no painel mas não publicadas nos servidores autoritativos (a.auto.dns.br / b.auto.dns.br). O serial da zona sobe mesmo sem publicar os registros. Só esperar.
4. **PowerShell 5.1 desta máquina:** não aceita heredoc `<<`, nem `&&`. Para JSON no `gh api`, usar `-f "campo[sub]=valor"` ou `echo '{...}' | gh api --input -` no Git Bash.
5. **Datas por extenso:** Jekyll não formata mês em português — por isso o front matter tem `data_extenso` manual. A data do nome do arquivo só ordena.
6. **URL preservada:** o primeiro artigo mantém `permalink: /crimes-contra-honra-na-internet.html` porque essa URL foi publicada antes da migração para Jekyll. Artigos novos usam o permalink padrão do Jekyll — não precisam de `permalink`.

## Histórico do projeto (jul/2026)

1. **21/07** — Site criado do zero (os arquivos de uma conversa anterior nunca tinham sido salvos; design reaproveitado do Artifact "Direito Digital — Crimes contra a Honra e a Imagem" e conteúdo do artigo em `Área de Trabalho\Artigo Semanal - Crimes contra a honra digital\`). Versão 1: HTML estático (index + artigo + modelo + styles.css).
2. **21/07** — Repo `Oswaldoprezotti/site` criado via `gh`, Pages ativado, CNAME configurado. DNS no Registro.br preenchido por agente de IA no Chrome supervisionado pelo usuário (relatos na conversa). Espera da janela de transição; propagação confirmada por monitor.
3. **21/07** — Certificado HTTPS emitido após remover/re-adicionar domínio; Enforce HTTPS ativado automaticamente por monitor.
4. **21/07** — Contatos reais inseridos (e-mail oswaldoprezotti01@gmail.com, tel (32) 98809-4067, Instagram @Oswaldo_Prezotti; sem LinkedIn por opção). Masthead reescrito: nome como título, texto pessoal; depois reescrito em registro formal a pedido (sem travessões em série, sem metáforas, sem clichês de IA — preferência forte do usuário).
5. **21/07** — Migração para Jekyll: layouts centralizados, artigo movido para `_posts/`, lista automática, RSS/sitemap/SEO, 404, MODELO-ARTIGO.md, este CLAUDE.md.

## Preferências do usuário relevantes aqui

- Texto do site: registro formal, frases diretas, sem "vícios de IA" (travessões em série, metáforas de efeito, construções "não é X, é Y").
- O aviso legal educativo (não é consulta jurídica) deve existir em todo artigo — obrigatório, vem da skill `artigo-semanal`.
- Alterações de conteúdo podem ser publicadas direto (push); mudanças estruturais grandes merecem relato claro ao usuário.
