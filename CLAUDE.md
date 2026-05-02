# PlanosDeAula — Guia do Repositório

Repositório de planos de aula organizados por disciplina e turma. O mesmo conteúdo pode ser gerado em diferentes templates visuais, um por escola.

## Escolas e templates

| Escola | Template |
|--------|----------|
| **Fernandina** | `html_template/fernandina/template.html` |
| **Ozória** | `html_template/ozoria/template.html` *(placeholder — aguardando template)* |

Cada escola possui seu próprio layout visual de plano de aula. O conteúdo em Markdown é compartilhado; apenas o HTML gerado difere.

## Estrutura de diretórios

```
<disciplina>/
  <turma>/
    aulas/                — planos de aula em Markdown (fonte principal, compartilhada)
    aulas_html/
      fernandina/         — HTMLs gerados com o template Fernandina
      ozoria/             — HTMLs gerados com o template Ozória
html_template/
  fernandina/
    template.html         — template da Escola Fernandina
  ozoria/
    template.html         — template da Escola Ozória (placeholder)
template/                 — imagens e PDF do modelo visual de impressão
```

Exemplo atual:

```
astronomia/
  serie_01/
    aulas/                — 35 arquivos .md
    aulas_html/
      fernandina/         — 35 arquivos .html + aulas.css + index.html
```

Nomes de turma usam o padrão `serie_01`, `serie_02`, etc.

## Convenção de arquivos de aula

Os arquivos em `aulas/` seguem o padrão `NNN-slug.md`, onde `NNN` é um número sequencial de três dígitos com zero à esquerda:

```
001-o-que-e-astronomia.md
002-o-ceu-noturno.md
...
035-revisao-geral-e-celebracao.md
```

O arquivo HTML correspondente em `aulas_html/` tem o mesmo nome com extensão `.html`.

## Estrutura de um plano de aula (Markdown)

Cada arquivo `.md` segue este esqueleto:

```markdown
# Aula N: Título

**Semana:** N | **Data sugerida:** Mês/Ano | **Duração:** X horas
**Bloco temático:** Nome do bloco

---

## Objetivos de Aprendizagem
- ...

## Materiais Necessários
- ...

---

## Roteiro da Aula

### Parte 1 — Aquecimento (X min)
...

### Parte 2 — Conteúdo Principal (X min)
...

### Parte 3 — Dinâmica / Atividade Prática (X min)
...

### Parte 4 — Encerramento (X min)
...

---

## Avaliação / Observações para a Professora
...
```

## Templates HTML

Cada escola tem seu template em `html_template/<escola>/template.html`.

**Fernandina** (`html_template/fernandina/template.html`):
- Barra de ferramentas fixa com botão de impressão
- Layout paginado simulando folha A4
- CSS embutido (sem dependências externas)

**Ozória** (`html_template/ozoria/template.html`):
- Layout A4 retrato com brasão e logo Alagoas
- Tabela bimestral interativa (linhas adicionáveis/removíveis)
- Tema Integrador opcional (oculto por padrão)
- Campos editáveis: Professor(a), Disciplina, Bimestre, Ano

Para Ozória, gera-se **um único HTML por bimestre** (não um por aula), pré-preenchido com todas as aulas em linhas da tabela. Salvar em `aulas_html/ozoria/plano-<bimestre>-<ano>.html`.

Para Fernandina, gera-se **um HTML por aula**, salvo em `aulas_html/fernandina/NNN-slug.html`.

## README

O `README.md` na raiz lista todas as disciplinas e turmas. Cada seção corresponde a uma combinação `disciplina/turma` e contém a tabela de sumário de aulas com links para os arquivos `.md` em `<disciplina>/<turma>/aulas/`.

Ao adicionar uma nova aula ou disciplina, atualize o `README.md` para refletir a mudança.

## Fluxo de trabalho típico

1. Criar o arquivo `.md` em `<disciplina>/<turma>/aulas/NNN-slug.md`
2. Para Fernandina: gerar `aulas_html/fernandina/NNN-slug.html` usando o template
3. Para Ozória: gerar/atualizar `aulas_html/ozoria/plano-<bimestre>-<ano>.html` com os dados do bimestre
4. Atualizar o `README.md` na raiz com o novo link

---

## Geração de Planos de Aula

Use esta seção como receita ao criar um novo conjunto de planos a partir de parâmetros fornecidos.

### Parâmetros necessários

| Parâmetro | Exemplo |
|-----------|---------|
| `disciplina` | `quimica` (nome da pasta) |
| `turma` | `serie_01` |
| `escola(s)` | `ozoria`, `fernandina` ou ambas |
| `períodos letivos` | `04/05/2026–19/06/2026`, `07/07/2026–28/07/2026` |
| `recesso(s)` | `20/06/2026–06/07/2026` |
| `dia da semana` | `segunda-feira` |
| `duração por aula` | `1H` |
| `tópicos` | lista ordenada de conteúdos |

### Algoritmo de distribuição de datas

1. Para cada período letivo, listar todas as datas que caem no dia da semana especificado.
2. Remover as datas que caem dentro de algum recesso.
3. Resultado: lista ordenada de datas de aula.
4. Distribuir os tópicos em ordem pela lista de datas:
   - Se **tópicos > datas**: agrupar os tópicos mais simples ou relacionados na mesma aula.
   - Se **datas > tópicos**: a última data recebe uma aula de revisão geral.
5. A primeira aula pode incluir introdução ao tema geral antes do primeiro tópico específico.

### Estrutura de arquivos a criar

```
<disciplina>/<turma>/
  aulas/
    001-slug.md
    002-slug.md
    ...
  aulas_html/
    fernandina/   (um .html por aula, se escola Fernandina for alvo)
    ozoria/       (um .html por bimestre, se escola Ozória for alvo)
```

### HTML Ozória pré-preenchido

O arquivo HTML da Ozória deve ser baseado em `html_template/ozoria/template.html` e ter os dados populados via array JS no `<script>`:

```js
const AULAS = [
  {
    date: 'YYYY-MM-DD',   // para o date picker
    ch: 1,                // carga horária (inteiro)
    comp: 'Química',      // componente curricular
    tematica: '...',      // temática/objeto do conhecimento
    hab: '...',           // habilidades (códigos BNCC)
    recursos: '...'       // recursos/estratégias/atividades
  },
  // ...
];
```

Os campos de cabeçalho (Professor, Disciplina, Bimestre, Ano) devem ser pré-preenchidos com `textContent` ou `value` diretamente no HTML.

### O que atualizar após criar os arquivos

- `README.md`: adicionar seção para a nova disciplina/turma com tabela de sumário e links para os `.md`
- Se existir `index.html` dentro da pasta da escola: adicionar links para os novos HTMLs
