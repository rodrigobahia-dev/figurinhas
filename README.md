# Álbum Din Down Down

Álbum de figurinhas para acompanhar o andamento do projeto Din Down Down (Instituto Gingas). Cada figurinha é uma ação, oficina ou marco do projeto. Esta edição usa o Ano 1 ("Construindo laços com a família", Lei de Incentivo ICMS-RJ) como modelo de teste para o Ano 4.

O álbum é uma página só (`index.html`), sem instalação e sem etapa de build.

## Como rodar

- **No computador:** baixe o repositório e abra o `index.html` com dois cliques.
- **Na internet (GitHub Pages):** em *Settings > Pages*, escolha *Deploy from a branch*, branch `main`, pasta `/ (root)` e salve. Em um ou dois minutos o álbum fica em `https://rodrigobahia-dev.github.io/figurinhas/`.

## Onde o progresso fica salvo

| Onde o álbum é aberto | Progresso e responsáveis |
| --- | --- |
| Versão publicada no Claude | Compartilhados: toda a equipe vê o mesmo álbum |
| Este repositório (arquivo local ou GitHub Pages) | Só no navegador de cada pessoa (`localStorage`, chave `dindown-stickers-v1`) |

Nesta versão não há servidor. Se duas pessoas abrirem o site do GitHub Pages, cada uma terá o seu próprio álbum.

## Como usar

- Toque numa figurinha para ver os detalhes.
- Figurinha simples: **Colar figurinha** quando a ação estiver concluída.
- Figurinha progressiva (ex.: 4/11 rodas): informe quantas unidades já foram feitas. Ela é colada ao atingir a meta.
- Em cada figurinha dá para definir o **Responsável** pela ação. O nome aparece embaixo dela.

## Como adicionar ou editar uma figurinha

Abra o `index.html` e procure o bloco `<script type="application/json" id="config-album">`. É o único trecho a editar. Cada figurinha é uma linha como esta:

```json
{ "id": "of-07", "secao": "oficinas", "titulo": "Oficina de maculelê", "descricao": "Texto que aparece nos detalhes.", "etapa": 4, "meta": 1 }
```

- `id`: código único e fixo. O progresso salvo fica ligado a ele: mudar o título não apaga nada, mas mudar o `id` faz a figurinha voltar a ficar vazia.
- `secao`: o `id` de um dos capítulos listados em `secoes`.
- `meta`: `1` para figurinha simples. Um número maior cria uma figurinha progressiva. Nesse caso, informe também `unidade` (ex.: `"rodas"`).
- `rara`: `true` para marcos de destaque.
- `etapa`: número da etapa na matriz do projeto (use `0` se não houver).

A numeração e os contadores se ajustam sozinhos. Para criar um capítulo, acrescente um item em `secoes` com `id`, `titulo`, `sigla` (duas letras), `etapas`, `cor` e `tinta` (cor do texto sobre a cor do capítulo).

## Como zerar o progresso

Use o botão **Zerar álbum**, no fim da página. Ele descola todas as figurinhas e mantém os responsáveis. Para apagar tudo, inclusive os responsáveis, limpe os dados do site no navegador.

## Acessibilidade

- Navegação completa por teclado, com foco visível.
- Estado de cada figurinha descrito para leitores de tela, e avisos quando uma figurinha é colada.
- Figurinha rara identificada por texto ("★ Rara"), não só pela cor.
- Animações desligadas para quem ativa "reduzir movimento" no sistema.
- Temas claro e escuro, seguindo o sistema.

## Para ligar um servidor depois

A página fala com o armazenamento por uma interface pequena: `collection(nome).onSnapshot(...)` e `doc(id).set(...)` / `.delete()`. A função `criarBancoLocal()`, no fim do `index.html`, implementa isso com `localStorage`. Para ter progresso compartilhado fora do Claude, basta escrever outra função com a mesma forma apontando para um banco externo.
