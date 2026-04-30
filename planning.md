# Planning — Reorganização do Repositório

## Objetivo
Mover os arquivos de aula (`.md` com 3 dígitos no início do nome) para uma subpasta `aulas/` e atualizar os links do README.

## Etapas

1. **Identificar arquivos** — localizar todos os `.md` com nome iniciando em 3 dígitos na raiz do repositório.
2. **Criar pasta `aulas/`** — `mkdir -p aulas/`
3. **Mover arquivos** — `mv [0-9][0-9][0-9]*.md aulas/`
4. **Atualizar links no README** — substituir referências relativas `(xxx-arquivo.md)` por `(aulas/xxx-arquivo.md)` em toda a tabela de sumário.
5. **Commit e push** — stagear renomeações e alteração do README, commitar e enviar para `origin/main`.

## Resultado

- 35 arquivos movidos para `aulas/`
- 35 links corrigidos no `README.md`
- Commit `cd1658b` enviado para `main`
