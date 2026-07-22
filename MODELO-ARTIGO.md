# Modelo de artigo novo

Para publicar um artigo, crie um arquivo em `_posts/` com o nome no formato:

```
_posts/AAAA-MM-DD-titulo-curto-do-artigo.md
```

Exemplo: `_posts/2026-07-26-stalking-e-perseguicao-digital.md`

Copie o conteúdo abaixo para dentro do arquivo e preencha. **Não é preciso mexer em mais nada**: a lista da página inicial, o feed RSS e o sitemap são atualizados automaticamente pelo site.

```markdown
---
title: "TÍTULO DO ARTIGO (texto puro, sem HTML)"
title_html: "TÍTULO DO ARTIGO com <span class=\"em\">palavra em destaque</span>"
lede: "Subtítulo do artigo. Uma ou duas frases que resumem a tese central — aparece na capa e no topo do artigo."
data_extenso: 26 de julho de 2026
description: "Resumo de 1-2 frases para o Google e redes sociais."
---

## Introdução

Primeiro parágrafo...

## Seção seguinte

Texto... Pode usar **negrito**, *itálico* e listas:

- item um;
- item dois.

## Conclusão

Fechamento...

<div class="refs">
  <h2>Referências</h2>
  <p>AUTOR. Título. Disponível em: URL. Acesso em: DATA.</p>
  <p>AUTOR. Título. Disponível em: URL. Acesso em: DATA.</p>
</div>
```

## Observações

- O conteúdo pode ser escrito em **Markdown puro** (`##` para seção, `**negrito**`, listas com `-`) ou em HTML — os dois funcionam.
- `title_html` é opcional: serve só para destacar uma palavra do título em itálico/cor. Se não quiser destaque, apague a linha.
- `data_extenso` é a data por extenso mostrada ao leitor. A data do nome do arquivo é a que ordena os artigos (o mais recente aparece primeiro na capa).
- A caixa de autor e o aviso legal são adicionados automaticamente no fim de todo artigo — não copie esses blocos para o texto.
- Depois de criar o arquivo, publique com:

```
git add -A
git commit -m "Artigo: TITULO"
git push
```

O site atualiza sozinho em 1-2 minutos.
