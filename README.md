# cybercrimesprezotti.com.br

Site pessoal de Oswaldo Prezotti — artigos semanais educativos sobre Direito Penal e Direito Digital (crimes cibernéticos).

Hospedado no **GitHub Pages** (gratuito, sem servidor) com **Jekyll** e domínio registrado no **Registro.br**.

## Como publicar um artigo novo

1. Crie um arquivo `_posts/AAAA-MM-DD-titulo-curto.md` seguindo o [MODELO-ARTIGO.md](MODELO-ARTIGO.md).
2. `git add -A && git commit -m "Artigo: título" && git push`
3. Pronto. A capa, o feed RSS e o sitemap atualizam sozinhos em 1-2 minutos.

## Estrutura

| Caminho | Função |
|---|---|
| `_config.yml` | Configuração do site (título, descrição, plugins) |
| `_layouts/default.html` | Esqueleto de toda página: head, barra superior, rodapé |
| `_layouts/artigo.html` | Layout de artigo: cabeçalho, caixa de autor, aviso legal |
| `_posts/*.md` | Os artigos — um arquivo por artigo, nada mais a editar |
| `index.html` | Capa: apresentação + lista automática de artigos + contato |
| `styles.css` | Folha de estilo única (com modo claro/escuro automático) |
| `404.html` | Página de erro para endereços inexistentes |
| `MODELO-ARTIGO.md` | Modelo comentado para criar artigos (não publicado no site) |
| `CLAUDE.md` | Documentação técnica para manutenção via Claude (não publicada) |
| `CNAME` | Domínio customizado do GitHub Pages — **não apagar** |

## URLs geradas automaticamente

- `https://cybercrimesprezotti.com.br/feed.xml` — feed RSS
- `https://cybercrimesprezotti.com.br/sitemap.xml` — sitemap para buscadores

## Infraestrutura

- Repositório: `Oswaldoprezotti/site` · GitHub Pages servindo o branch `main` (raiz)
- DNS no Registro.br: 4 registros A na raiz (IPs do GitHub Pages) + CNAME `www` → `oswaldoprezotti.github.io`
- HTTPS: certificado emitido e renovado automaticamente pelo GitHub; Enforce HTTPS ativado
