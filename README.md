# cybercrimesprezotti.com.br

Site pessoal de Oswaldo Prezotti — artigos semanais educativos sobre Direito Penal e Direito Digital (crimes cibernéticos).

Hospedado no GitHub Pages com domínio registrado no Registro.br.

## Estrutura

| Arquivo | Função |
|---|---|
| `index.html` | Página inicial: lista de artigos, sobre, contato |
| `styles.css` | Folha de estilo única de todo o site |
| `artigo-modelo.html` | Modelo para criar artigos novos |
| `crimes-contra-honra-na-internet.html` | Artigo publicado em 19/07/2026 |
| `CNAME` | Domínio customizado do GitHub Pages (não apagar) |

## Publicar um artigo novo (rotina semanal)

1. Duplique `artigo-modelo.html` com um nome descritivo, ex.: `crimes-contra-honra-stf.html`.
2. Cole o conteúdo gerado pela skill `artigo-semanal` na área marcada com `COLE AQUI O CONTEÚDO DO ARTIGO` e preencha título, data, subtítulo e referências (procure os marcadores `EDITAR`).
3. No `index.html`, copie o bloco `<li>` da lista de artigos e ajuste data, título, resumo e link (o mais recente fica no topo).
4. Suba os arquivos alterados no GitHub (upload pelo navegador ou `git push`) — o site atualiza sozinho em 1–2 minutos.

## DNS (Registro.br)

Zona do domínio `cybercrimesprezotti.com.br`:

- 4 registros **A** na raiz (nome em branco): `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- 1 registro **CNAME** com nome `www` apontando para `SEUUSUARIO.github.io`

Depois da propagação, marcar **Enforce HTTPS** em Settings → Pages.
