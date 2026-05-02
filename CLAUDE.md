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
- Placeholder — template será fornecido em breve

Ao gerar HTMLs de uma aula, aplique o template da escola alvo e salve o resultado em `aulas_html/<escola>/NNN-slug.html`.

## README

O `README.md` na raiz lista todas as disciplinas e turmas. Cada seção corresponde a uma combinação `disciplina/turma` e contém a tabela de sumário de aulas com links para os arquivos `.md` em `<disciplina>/<turma>/aulas/`.

Ao adicionar uma nova aula ou disciplina, atualize o `README.md` para refletir a mudança.

## Fluxo de trabalho típico

1. Criar o arquivo `.md` em `<disciplina>/<turma>/aulas/NNN-slug.md`
2. Para cada escola alvo, gerar o HTML em `<disciplina>/<turma>/aulas_html/<escola>/NNN-slug.html` usando o template correspondente
3. Atualizar o `index.html` dentro da pasta da escola, se existir
4. Atualizar o `README.md` na raiz com o novo link
