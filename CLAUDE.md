# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository stores custom AI skills (slash commands) developed for use with Claude Code. It is designed to be used as a **git submodule** in other projects.

## Directory Structure

```
xk-skills/
├── bin/cli.js              # CLI 入口 (npx xk-skills)
├── package.json            # npm 包配置
├── *.md                    # Root-level skills (slash commands)
├── frontend/
│   └── design-themes/      # Design theme system
│       ├── presets/         # Theme presets (fluent, glassmorphism, ...)
│       ├── compiler/        # design-spec.json → tokens.css + style.css + SKILL.md
│       ├── generated/       # Compiler output (gitignored)
│       └── schema.json      # JSON Schema for design-spec.json
├── ops/
│   └── git-commit/         # Git 提交规范 skill
└── CLAUDE.md
```

## Skill File Structure

Skills are `.md` files organized by domain. Each skill file typically contains:
- A frontmatter block with metadata (name, description, trigger conditions)
- The skill body with instructions, prompts, and any embedded logic

## Design Themes

Each theme preset lives in `frontend/design-themes/presets/<name>/` and contains:
- `design-spec.json` — Source of truth (hand-edited)
- `tokens.css` — Generated CSS variables
- `style.css` — Generated spatial metaphor styles
- `SKILL.md` — Generated skill documentation

To recompile a theme:
```sh
node frontend/design-themes/compiler/compile.cjs frontend/design-themes/presets/<name>/design-spec.json
```

## Working with Skills

- Skills are invoked in Claude Code via `/skill-name` syntax
- When creating new skills, follow the existing patterns in the repo
- Skill names should be lowercase, hyphenated (e.g., `my-skill.md`)

## npm 安装

```sh
# 安装全部 skill
npx xk-skills install

# 只安装指定 skill
npx xk-skills install git-commit

# 列出所有可用 skill
npx xk-skills list

# 卸载已安装的 skill
npx xk-skills uninstall
```

安装后重启 Claude Code 即可通过 `/skill-name` 使用。
