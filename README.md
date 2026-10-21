# Estatística KBM & PLPR

Página estática que lê uma planilha de dados diários e calcula as estatísticas das operações:

- **KBM**: vender quando a ação sobe X% sobre o fechamento anterior e recomprar no fechamento do dia.
- **PLPR**: comprar quando a ação cai X% sobre o fechamento anterior e vender no fechamento do dia.

Tudo roda no navegador. A planilha não é enviada para nenhum servidor.

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub (por exemplo, `estatistica-kbm-plpr`).
2. Envie o arquivo `index.html` para a raiz do repositório (botão **Add file → Upload files**).
3. Vá em **Settings → Pages**, em *Source* escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e salve.
4. Em um ou dois minutos o site fica disponível em `https://SEU-USUARIO.github.io/estatistica-kbm-plpr/`.

Se o repositório for público, o código da página fica visível, mas suas planilhas não, porque elas nunca saem do seu computador.

## Formato da planilha

Arquivos `.csv`, `.xlsx` ou `.xls` com dados diários, **sem cabeçalho**, nesta ordem de colunas:

| A | B | C | D | E | F | G, H… |
|---|---|---|---|---|---|---|
| Nome | Data (dd/mm/aaaa) | Abertura | Máxima | Mínima | Fechamento | ignoradas |

Exemplo de linha: `BPAC11;20/10/2026;80,02;82,24;79,63;81,71;1134067992,00;13935800`

A ordem das datas não importa. Se o arquivo tiver mais de um ativo, a página mostra um seletor.

## Regras de cálculo

- Nível KBM = fechamento anterior × (1 + movimento). A operação ocorre se a máxima do dia atinge o nível.
- Nível PLPR = fechamento anterior × (1 − movimento). A operação ocorre se a mínima do dia atinge o nível.
- Se o dia abre além do nível (gap), a execução é no preço de abertura.
- Resultado KBM = venda − fechamento. Resultado PLPR = fechamento − compra. Ganho é resultado maior que zero.
- Taxa de assertividade = ganhos ÷ ocorrências. Volume médio = fechamento médio × quantidade.
- Custos de corretagem e taxas não são descontados.
